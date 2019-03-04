# Desplegando en Heroku

## Despliegue manual

Este tutorial asume que ya has clonado CONSUL en tu máquina y está funcionando.

1. Primero, crea una cuenta en [Heroku](https://www.heroku.com) si todavía no lo has hecho.
2. Instala [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli) e inicia sesión usando

   ```
   heroku login
   ```

3. Ve a tu repositorio de CONSUL y ejecuta

   ```
   cd consul
   heroku create nombre-de-tu-app
   ```

   Puedes añadir `--region eu` si deseeas utilizar sus servidores europeos en lugar de los estadounidenses.

   Si _nombre-de-tu-app_ no está cogido, Heroku debería crear tu aplicación.

4. Crea una base de datos usando

   ```
   heroku addons:create heroku-postgresql
   ```

   Ahora deberías tener acceso a una base de datos Postgres vacía cuya dirección se guardó automáticamente como una variable de entorno llamada _DATABASE\_URL_. CONSUL se conectará automáticamente cuando se despliegue.

5. Añade un archivo _heroku.yml_ en la raíz de tu proyecto y pega lo siguiente en él

    ```
    build:
      languages:
        - ruby
      packages:
        - imagemagick
    run:
      web: bundle exec rails server -e ${RAILS_ENV:-production}
    ```
6. Ahora, genera una clave secreta y guárdala en una variable llamada SECRET\_KEY\_BASE usando

    ```
    heroku config:set SECRET_KEY_BASE=`ruby -rsecurerandom -e "puts SecureRandom.hex(64)"
    ```

    Es necesario que la aplicación sepa dónde está almacenada la clave secreta añadiendo un enlace a la variable en _config/secrets.yml_

    ```
    production:
      secret_key_base: <%= ENV["SECRET_KEY_BASE"] %>
    ```
    haz commit de este archivo en el repositorio comentando la línea correspondiente en _.gitignore_.

    ```
    #/config/secrets.yml
    ```
    **¡Recuerda no hacer commit del archivo si tiene información confidencial en él!**

7. Ahora puedes desplegar tu aplicación usando

    ```
    git push heroku your-branch:master
    ```

8. No funcionará inmediatamente porque la base de datos no contiene las tablas necesarias. Para crearlas, ejecuta

    ```
    heroku run rake db:migrate
    heroku run rake db:seed
    ```

    Si deseas añadir los datos de prueba a la base de datos, mueve `gem `faker', ` ~> 1.8.7'` fuera de `group :development` y ejecuta

    ```
    heroku config:set DATABASE_CLEANER_ALLOW_REMOTE_DATABASE_URL=true
    heroku config:set DATABASE_CLEANER_ALLOW_PRODUCTION=true
    heroku run rake db:dev_seed
    ```

9. Tu aplicación debería estar lista para usar. Puedes abrirla con

    ```
    heroku open
    ```

    También puedes ejecutar la consola en heroku usando

    ```
    heroku console --app your-app-name
    ```

10. Heroku no permite guardar imágenes o documentos en sus servidores, por lo que es necesario realizar los siguientes cambios

    En `app/models/image.rb:47` y `app/models/document.rb:39`

    Cambia `URI.parse(cached_attachment)` por `URI.parse("http:" + cached_attachment)`

    Crea un nuevo archivo en `config/initializers/paperclip.rb` con el siguiente contenido

    ```
    Paperclip::UriAdapter.register
    ```

    Consulta nuestra [guía de AWS S3](../getting_started/using-aws-s3-as-storage.md) para más detalles sobre configurar Paperclip con S3.

### Opcional pero recomendado:

**Instalar rails\_12factor y especificar la versión de Ruby**

Como recomienda Heroku, puedes añadir la gema rails\_12factor y especificar la versión de Ruby que quieres usar. Puedes hacerlo añadiendo

```
gem 'rails_12factor'

ruby '2.3.2'
```

en el archivo _Gemfile\_custom_. No olvides ejecutar

```
bundle install
```

para generar el archivo _Gemfile.lock_ antes de hacer commit y desplegar al servidor.

### Opcional pero recomendado:

**Usar Puma como servidor web**

Heroku recomienda utilizar Puma en lugar del servidor web predeterminado para mejorar la capacidad de respuesta de su aplicación en [varios niveles](http://blog.scoutapp.com/articles/2017/02/10/which-ruby-app-server-is-right-for-you). Primero, agrega la gema en tu archivo _Gemfile_custom_:

  ```
  gem 'puma'
  ```

Luego necesitas crear un nuevo archivo llamado _puma.rb_ \(tu carpeta _config_ es un buen lugar para almacenarlo\). Aquí hay un contenido estándar para este archivo:

  ```
  workers Integer(ENV['WEB_CONCURRENCY'] || 1)
  threads_count = Integer(ENV['RAILS_MAX_THREADS'] || 5)
  threads threads_count, threads_count

  preload_app!

  rackup      DefaultRackup
  port        ENV['PORT']     || 3000
  environment ENV['RACK_ENV'] || 'production'

  on_worker_boot do
    # Worker specific setup for Rails 4.1+
    # See: https://devcenter.heroku.com/articles/deploying-rails-applications-with-the-puma-web-server#on-worker-boot
    ActiveRecord::Base.establish_connection
  end
  ```

Puedes encontrar una explicación para cada uno de estos ajustes en el [tutorial de Heroku](https://devcenter.heroku.com/articles/deploying-rails-applications-with-the-puma-web-server).

La última parte es cambiar la tarea _web_ para usar Puma cambiándola en tu archivo _heroku.yml_:

  ```
  web: bundle exec puma -C config/puma.rb
  ```
