# Usando AWS S3 como almacenamiento de archivos

Mientras CONSUL mantiene la mayoría de sus datos en una base de datos PostgreSQL, todos los archivos como documentos o imágenes tienen que ser almacenados en otro lugar.

Para couparse de ellos, CONSUL utiliza la [gema Paperclip](https://github.com/thoughtbot/paperclip) (Advertencia: esta gema está ahora obsoleta y CONSUL probablemente migrará a ActiveStorage en el futuro. Comprueba que esto no sea así antes de utilizar esta guía).

Por defecto, los archivos adjuntos se almacenan en el sistema de archivos. Sin embargo, con servicios como Heroku, no hay almacenamiento persistente, lo que significa que estos archivos se borran periódicamente.

Este tutorial explica cómo configurar Paperclip para que utilice[AWS S3](https://aws.amazon.com/fr/s3/). No recomienda S3 ni el uso de los servicios de Amazon y se espera que se amplíe para incluir la configuración de [almacenamiento en la nube](http://fog.io/storage/).

## Añadir la gema *aws-sdk-s3*

Primero, añade la siguiente línea en tu *Gemfile_custom*

```
gem 'aws-sdk-s3', '~> 1'
```

Asegúrate de tener una versión reciente de Paperclip (CONSUL está usando actualmente la versión 5.2.1, que no reconoce *aws-sdk-s3*). En tu Gemfile, la línea debería ser:

```
gem 'paperclip', '~> 6.1.0'
```

Ejecuta `bundle install` para aplicar los cambios.

## Añadir tus credenciales en *secrets.yml*

Esta guía asumirá que tienes una cuenta de Amazon configurada para usar S3 y que has creado un bucket para tu instancia de CONSUL. Es muy recomendable utilizar un bucket diferente para cada caso (producción, preproducción, desarollo).

Necesitarás la siguiente información:
- el **nombre** del S3 bucket
- la **región** del S3 bucket (`eu-central-1` para UE-Frankfurt por ejemplo)
- el **hostname** del S3 bucket (`s3.eu-central-1.amazonaws.com` para Frankfurt, por ejemplo)
- un **id de la clave de acceso** y una **clave de acceso secreta** con permiso de lectura/escritura de ese bucket

**ADVERTENCIA:** se recomienda crear usuarios IAM (Identity and Access Management) que sólo tengan permiso de lectura/escritura para el bucket que desea utilizar para esa instancia específica de CONSUL.

Una vez que tengas estas piezas de información, puedes guardarlas como variables de entorno de la instancia que ejecuta CONSUL. En este tutorial, los guardamos respectivamente como *AWS_S3_BUCKET*, *AWS_S3_REGION*, *AWS_S3_HOSTNAME*, *AWS_ACCESS_KEY_ID* y *AWS_SECRET_ACCESS_KEY*.

Añade el siguiente bloque en tu archivo *secrets.yml*:

```
aws: &aws
  aws_s3_region: <%= ENV["AWS_S3_REGION"] %>
  aws_access_key_id: <%= ENV["AWS_ACCESS_KEY_ID"] %>
  aws_secret_access_key: <%= ENV["AWS_SECRET_ACCESS_KEY"] %>
  aws_s3_bucket: <%= ENV["AWS_S3_BUCKET"] %>
  aws_s3_host_name: <%= ENV["AWS_S3_HOST_NAME"] %>
```

y `<<: *aws` debajo de los entornoes donde quieres usar S3, por ejemplo:

```
production:
[...]
  <<: *aws
```

## Configuración de Paperclip
Primero, activa el adaptador URI de Paperclip creando el archivo *config/initializers/paperclip.rb* con el siguiente contenido:

```
Paperclip::UriAdapter.register
```

Por último, añade las siguientes líneas en el fichero de entorno de la instancia con la que deseas utilizar S3. En producción, por ejemplo, deberías editar *config/environments/production.rb*.

```
# Paperclip settings to store images and documents on S3
config.paperclip_defaults = {
  storage: :s3,
  preserve_files: true,
  s3_host_name: Rails.application.secrets.aws_s3_host_name,
  s3_protocol: :https,
  s3_credentials: {
    bucket: Rails.application.secrets.aws_s3_bucket,
    access_key_id: Rails.application.secrets.aws_access_key_id,
    secret_access_key: Rails.application.secrets.aws_secret_access_key,
    s3_region: Rails.application.secrets.aws_s3_region,
  }
}
```

Tendrás que reiniciar para aplicar los cambios.
