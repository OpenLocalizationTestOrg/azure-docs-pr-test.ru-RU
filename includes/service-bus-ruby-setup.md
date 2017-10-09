## <a name="create-a-ruby-application"></a>Создание приложения Ruby
Инструкции см. в разделе [Создание приложения Ruby в Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Настройка вашего приложения tooUse Service Bus
toouse Service Bus, загрузите и используйте hello Azure Ruby пакет, который включает в себя набор библиотек удобства, взаимодействующих со службами REST hello хранилища.

### <a name="use-rubygems-tooobtain-hello-package"></a>Используйте RubyGems tooobtain hello пакет
1. Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).
2. Введите команду «gem Установка azure» в hello команда окна tooinstall hello gem и зависимости.

### <a name="import-hello-package"></a>Импорт пакета hello
С помощью предпочитаемого текстового редактора, добавьте следующие toohello вверху hello Ruby hello файла, в котором предполагается toouse хранилища:

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Настройка подключения к Service Bus
Используйте hello следующий код tooset hello значения пространства имен, имя hello ключ, ключ, подписавшего и узла:

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

Задайте значение toohello значение пространства имен hello, созданный вместо hello весь URL-адрес. Например, используйте **yourexamplenamespace**, а не yourexamplenamespace.servicebus.windows.net.
