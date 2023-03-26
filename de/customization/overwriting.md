# Überschreiben von application.rb

Wenn Sie die Datei `config/application.rb` erweitern oder modifizieren müssen, tun Sie dies einfach in der Datei `config/application_custom.rb`. Wenn Sie zum Beispiel die Standardsprache auf Englisch ändern wollen, fügen Sie einfach hinzu:

```ruby
module Consul
  class Application < Rails::Application
    config.i18n.default_locale = :en
    config.i18n.available_locales = [:en, :es]
  end
end
```

Denken Sie daran, dass Sie den Server neu starten müssen, um diese Änderungen zu sehen.
