## <a name="create-a-ruby-application"></a><span data-ttu-id="2f46c-101">Создание приложения Ruby</span><span class="sxs-lookup"><span data-stu-id="2f46c-101">Create a Ruby application</span></span>
<span data-ttu-id="2f46c-102">Инструкции см. в разделе [Создание приложения Ruby в Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="2f46c-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="2f46c-103">Настройка вашего приложения tooUse Service Bus</span><span class="sxs-lookup"><span data-stu-id="2f46c-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="2f46c-104">toouse Service Bus, загрузите и используйте hello Azure Ruby пакет, который включает в себя набор библиотек удобства, взаимодействующих со службами REST hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="2f46c-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="2f46c-105">Используйте RubyGems tooobtain hello пакет</span><span class="sxs-lookup"><span data-stu-id="2f46c-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="2f46c-106">Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="2f46c-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="2f46c-107">Введите команду «gem Установка azure» в hello команда окна tooinstall hello gem и зависимости.</span><span class="sxs-lookup"><span data-stu-id="2f46c-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="2f46c-108">Импорт пакета hello</span><span class="sxs-lookup"><span data-stu-id="2f46c-108">Import hello package</span></span>
<span data-ttu-id="2f46c-109">С помощью предпочитаемого текстового редактора, добавьте следующие toohello вверху hello Ruby hello файла, в котором предполагается toouse хранилища:</span><span class="sxs-lookup"><span data-stu-id="2f46c-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="2f46c-110">Настройка подключения к Service Bus</span><span class="sxs-lookup"><span data-stu-id="2f46c-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="2f46c-111">Используйте hello следующий код tooset hello значения пространства имен, имя hello ключ, ключ, подписавшего и узла:</span><span class="sxs-lookup"><span data-stu-id="2f46c-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="2f46c-112">Задайте значение toohello значение пространства имен hello, созданный вместо hello весь URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="2f46c-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="2f46c-113">Например, используйте **yourexamplenamespace**, а не yourexamplenamespace.servicebus.windows.net.</span><span class="sxs-lookup"><span data-stu-id="2f46c-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
