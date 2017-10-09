<span data-ttu-id="76a1e-101">Эмулятор хранилища Hello поддерживает фиксированной учетной записи и хорошо известных проверки подлинности с ключом для проверки подлинности Shared Key.</span><span class="sxs-lookup"><span data-stu-id="76a1e-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="76a1e-102">Этой учетной записи и ключ, hello единственные Shared Key учетные данные для использования с эмулятором хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="76a1e-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="76a1e-103">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="76a1e-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="76a1e-104">Hello ключ проверки подлинности, поддерживаемых эмулятором хранилища hello предназначена только для тестирования функции hello кода проверки подлинности клиента.</span><span class="sxs-lookup"><span data-stu-id="76a1e-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="76a1e-105">Его использование не гарантирует защиту.</span><span class="sxs-lookup"><span data-stu-id="76a1e-105">It does not serve any security purpose.</span></span> <span data-ttu-id="76a1e-106">Нельзя использовать рабочую учетную запись хранилища и ключ с помощью эмулятора хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="76a1e-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="76a1e-107">Не следует использовать учетную запись hello разработки с рабочими данными.</span><span class="sxs-lookup"><span data-stu-id="76a1e-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="76a1e-108">Эмулятор хранилища Hello поддерживает только подключения по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="76a1e-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="76a1e-109">Однако HTTPS — hello, рекомендуется использовать протокол для доступа к ресурсам в рабочей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="76a1e-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="76a1e-110">Подключить эмулятор toohello учетную запись, с помощью ярлыка</span><span class="sxs-lookup"><span data-stu-id="76a1e-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="76a1e-111">Hello простым способом tooconnect toohello эмулятор хранилища из своего приложения — tooconfigure строку подключения в файле конфигурации приложения, ссылающийся на ярлык hello `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="76a1e-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="76a1e-112">Ниже приведен пример эмулятора хранения toohello строку подключения в *app.config* файла:</span><span class="sxs-lookup"><span data-stu-id="76a1e-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="76a1e-113">Подключиться с помощью hello хорошо известная учетная запись имени и ключа учетной записи эмулятора toohello</span><span class="sxs-lookup"><span data-stu-id="76a1e-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="76a1e-114">toocreate строку подключения, что ссылки hello эмулятор имя учетной записи и ключа, необходимо указать hello конечных точек для каждого из hello служб, которые следует toouse из эмулятора hello в строке подключения hello.</span><span class="sxs-lookup"><span data-stu-id="76a1e-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="76a1e-115">Это необходимо, чтобы строка подключения hello будет ссылаться эмулятор hello конечных точек, которые отличаются от тех, для рабочую учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="76a1e-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="76a1e-116">Например значение hello в строке подключения будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="76a1e-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="76a1e-117">Это значение является показанный выше, контекстное идентичные toohello `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="76a1e-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="76a1e-118">Указание прокси-сервера HTTP</span><span class="sxs-lookup"><span data-stu-id="76a1e-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="76a1e-119">Можно также указать toouse прокси-сервер HTTP при тестировании службы со hello эмулятор хранилища.</span><span class="sxs-lookup"><span data-stu-id="76a1e-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="76a1e-120">Это может быть полезна для отслеживания запросов и ответов HTTP, при отладке операций со службами хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="76a1e-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="76a1e-121">toospecify прокси-сервера, добавить hello `DevelopmentStorageProxyUri` toohello строку соединения и задайте его значение toohello URI прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="76a1e-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="76a1e-122">Например вот строка подключения указывает toohello эмулятора хранилища и настраивает прокси-сервер HTTP.</span><span class="sxs-lookup"><span data-stu-id="76a1e-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

