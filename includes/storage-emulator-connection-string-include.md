<span data-ttu-id="179f4-101">Эмулятор хранения поддерживает одну предопределенную учетную запись и известный ключ аутентификации для аутентификации с помощью общего ключа.</span><span class="sxs-lookup"><span data-stu-id="179f4-101">The storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="179f4-102">Эти учетная запись и ключ — единственные разрешенные учетные данные общего ключа для использования с эмулятором хранения.</span><span class="sxs-lookup"><span data-stu-id="179f4-102">This account and key are the only Shared Key credentials permitted for use with the storage emulator.</span></span> <span data-ttu-id="179f4-103">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="179f4-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="179f4-104">Ключ аутентификации, поддерживаемый эмулятором хранения, предназначен только для тестирования работы клиентского кода.</span><span class="sxs-lookup"><span data-stu-id="179f4-104">The authentication key supported by the storage emulator is intended only for testing the functionality of your client authentication code.</span></span> <span data-ttu-id="179f4-105">Его использование не гарантирует защиту.</span><span class="sxs-lookup"><span data-stu-id="179f4-105">It does not serve any security purpose.</span></span> <span data-ttu-id="179f4-106">Нельзя использовать рабочую учетную запись хранения и ключ для эмулятора хранения.</span><span class="sxs-lookup"><span data-stu-id="179f4-106">You cannot use your production storage account and key with the storage emulator.</span></span> <span data-ttu-id="179f4-107">Не следует использовать учетную запись для разработки с рабочими данными.</span><span class="sxs-lookup"><span data-stu-id="179f4-107">You should not use the development account with production data.</span></span>
> 
> <span data-ttu-id="179f4-108">Эмулятор хранения поддерживает подключения только по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="179f4-108">The storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="179f4-109">Тем не менее для доступа к ресурсам в рабочей учетной записи хранения Azure рекомендуется использовать протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="179f4-109">However, HTTPS is the recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-to-the-emulator-account-using-a-shortcut"></a><span data-ttu-id="179f4-110">Подключение к учетной записи эмулятора с помощью ярлыка</span><span class="sxs-lookup"><span data-stu-id="179f4-110">Connect to the emulator account using a shortcut</span></span>
<span data-ttu-id="179f4-111">Самый простой способ подключиться к эмулятору хранения из приложения — настроить строку подключения в файле конфигурации приложения, на которое ссылается ярлык: `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="179f4-111">The easiest way to connect to the storage emulator from your application is to configure a connection string in your application's configuration file that references the shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="179f4-112">Ниже приведен пример строки подключения к эмулятору хранения в файле *app.config*:</span><span class="sxs-lookup"><span data-stu-id="179f4-112">Here's an example of a connection string to the storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-to-the-emulator-account-using-the-well-known-account-name-and-key"></a><span data-ttu-id="179f4-113">Подключение к учетной записи эмулятора с помощью известного имени и ключа учетной записи</span><span class="sxs-lookup"><span data-stu-id="179f4-113">Connect to the emulator account using the well-known account name and key</span></span>
<span data-ttu-id="179f4-114">Для создания строки подключения, которая содержит ссылку на имя учетной записи и ключ эмулятора, в строке подключения следует указать конечные точки для каждой службы, которую нужно использовать из эмулятора.</span><span class="sxs-lookup"><span data-stu-id="179f4-114">To create a connection string that references the emulator account name and key, you must specify the endpoints for each of the services you wish to use from the emulator in the connection string.</span></span> <span data-ttu-id="179f4-115">Это необходимо, чтобы строка подключения содержала ссылки на конечные точки эмулятора, которые отличаются от конечных точек рабочей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="179f4-115">This is necessary so that the connection string will reference the emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="179f4-116">Например, значение строки подключения будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="179f4-116">For example, the value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="179f4-117">Это значение идентично показанному выше ярлыку ( `UseDevelopmentStorage=true`).</span><span class="sxs-lookup"><span data-stu-id="179f4-117">This value is identical to the shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="179f4-118">Указание прокси-сервера HTTP</span><span class="sxs-lookup"><span data-stu-id="179f4-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="179f4-119">Если вы тестируете службу на эмуляторе хранения, можно также указать прокси-сервер HTTP.</span><span class="sxs-lookup"><span data-stu-id="179f4-119">You can also specify an HTTP proxy to use when you're testing your service against the storage emulator.</span></span> <span data-ttu-id="179f4-120">Это может быть полезно для отслеживания HTTP-запросов и ответов при отладке операций со службами хранилища.</span><span class="sxs-lookup"><span data-stu-id="179f4-120">This can be useful for observing HTTP requests and responses while you're debugging operations against the storage services.</span></span> <span data-ttu-id="179f4-121">Чтобы указать прокси-сервер, добавьте параметр `DevelopmentStorageProxyUri` в строку подключения и присвойте ему значение URI прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="179f4-121">To specify a proxy, add the `DevelopmentStorageProxyUri` option to the connection string, and set its value to the proxy URI.</span></span> <span data-ttu-id="179f4-122">В качестве примера приведена строка подключения, которая указывает эмулятор хранения и задает прокси-сервер HTTP:</span><span class="sxs-lookup"><span data-stu-id="179f4-122">For example, here is a connection string that points to the storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

