---
title: "aaaConnecting tooMedia службы записи с помощью .NET"
description: "В этом разделе показано, как подписку служб tooMedia tooconnect .NET."
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="478cd-103">Подключение tooMedia учетной записи службы, с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="478cd-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="478cd-104">REST</span><span class="sxs-lookup"><span data-stu-id="478cd-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="478cd-105">.NET</span><span class="sxs-lookup"><span data-stu-id="478cd-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="478cd-106">В этом разделе описывается, как tooobtain tooMicrosoft программное подключение при программировании с использованием служб мультимедиа Azure hello пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="478cd-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="478cd-107">Соединение tooMedia служб</span><span class="sxs-lookup"><span data-stu-id="478cd-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="478cd-108">tooconnect tooMedia службы программными средствами, необходимо заранее настроить учетную запись Azure, настроенными службами мультимедиа в этой учетной записи и затем настроить проект Visual Studio для разработки с hello пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="478cd-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="478cd-109">Дополнительные сведения см. в разделе Настройка для разработки с hello пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="478cd-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="478cd-110">В конце процесса настройки учетной записи службы мультимедиа hello hello, полученный hello следующие необходимые значения подключения.</span><span class="sxs-lookup"><span data-stu-id="478cd-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="478cd-111">Используйте эти подключения программный toomake tooMedia служб.</span><span class="sxs-lookup"><span data-stu-id="478cd-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="478cd-112">Имя учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="478cd-112">Your Media Services account name.</span></span>
* <span data-ttu-id="478cd-113">Ключ учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="478cd-113">Your Media Services account key.</span></span>

<span data-ttu-id="478cd-114">Эти значения, toofind go toohello портала управления Azure, выберите свою учетную запись службы мультимедиа и щелкните hello»**УПРАВЛЕНИЕ КЛЮЧАМИ**» значок hello нижней части окна портала hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="478cd-115">Щелкнув hello значок Далее tooeach текстовое поле копии hello значение toohello системный буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="478cd-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="478cd-116">Создание экземпляра CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="478cd-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="478cd-117">Программирование реакции на Media Services необходима toocreate toostart **CloudMediaContext** экземпляр, представляющий контекст сервера hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="478cd-118">Hello **CloudMediaContext** содержит ссылки на коллекции tooimportant, включая задания, активы, файлы, политики доступа и указатели.</span><span class="sxs-lookup"><span data-stu-id="478cd-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="478cd-119">Hello **CloudMediaContext** класс не является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="478cd-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="478cd-120">Для каждого потока или набора операций необходимо создать новый CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="478cd-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="478cd-121">В CloudMediaContext предусмотрено пять перегрузок конструктора.</span><span class="sxs-lookup"><span data-stu-id="478cd-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="478cd-122">Это рекомендуемый toouse конструкторов, принимающих **MediaServicesCredentials** как параметр.</span><span class="sxs-lookup"><span data-stu-id="478cd-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="478cd-123">Дополнительные сведения см. в разделе hello **повторное использование токенов службы контроля доступа** ниже.</span><span class="sxs-lookup"><span data-stu-id="478cd-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="478cd-124">Hello следующий пример использует открытый конструктор CloudMediaContext(MediaServicesCredentials credentials) hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="478cd-125">Повторное использование маркеров службы управления доступом</span><span class="sxs-lookup"><span data-stu-id="478cd-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="478cd-126">В этом разделе показано, как маркеры tooreuse службы контроля доступа с помощью CloudMediaContext конструкторов, принимающих MediaServicesCredentials в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="478cd-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="478cd-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (также называется Access Control Service или ACS) является облачная служба, предоставляющая простой способ проверки подлинности и авторизацию доступа пользователей toogain tootheir веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="478cd-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="478cd-128">Службы мультимедиа Microsoft Azure управляет доступом службы tooits Хотя протокол OAuth, который требуется токен ACS.</span><span class="sxs-lookup"><span data-stu-id="478cd-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="478cd-129">Службы мультимедиа получает hello токены ACS из сервера авторизации.</span><span class="sxs-lookup"><span data-stu-id="478cd-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="478cd-130">При разработке с помощью пакета SDK служб мультимедиа hello, вы можете toonot приходится иметь дело с hello токены, так как hello диспетчеры кода SDK ими.</span><span class="sxs-lookup"><span data-stu-id="478cd-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="478cd-131">Тем не менее позволяя hello SDK полностью управлять запросы маркеров toounnecessary интересы токены hello ACS.</span><span class="sxs-lookup"><span data-stu-id="478cd-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="478cd-132">Запрашиваемые токены времени и потребляет ресурсы hello клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="478cd-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="478cd-133">Кроме того сервер ACS hello регулирует hello запросов, если hello значение слишком велико.</span><span class="sxs-lookup"><span data-stu-id="478cd-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="478cd-134">Hello ограничение составляет 30 запросов в секунду см. в разделе [ограничения службы ACS](https://msdn.microsoft.com/library/gg185909.aspx) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="478cd-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="478cd-135">Начиная с пакета SDK служб мультимедиа версии 3.0.0.0 hello, можно повторно использовать токены ACS hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="478cd-136">Hello **CloudMediaContext** конструкторов, принимающих **MediaServicesCredentials** как параметр включения совместного использования токенов hello ACS между несколькими контекстами.</span><span class="sxs-lookup"><span data-stu-id="478cd-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="478cd-137">Hello MediaServicesCredentials класс инкапсулирует учетные данные службы мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="478cd-138">Если токен ACS доступен и известен ее срок, можно создать новый экземпляр MediaServicesCredentials с маркером hello и передать его конструктору toohello CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="478cd-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="478cd-139">Обратите внимание, что hello пакета SDK служб мультимедиа автоматически обновляет токены по истечении их срока действия.</span><span class="sxs-lookup"><span data-stu-id="478cd-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="478cd-140">Существует два способа tooreuse токены ACS, как показано в следующих примерах hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="478cd-141">Можно кэшировать hello **MediaServicesCredentials** объект в памяти (например, в переменной статического класса).</span><span class="sxs-lookup"><span data-stu-id="478cd-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="478cd-142">Затем передайте конструктор CloudMediaContext toohello кэширования hello объекта.</span><span class="sxs-lookup"><span data-stu-id="478cd-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="478cd-143">Hello объект MediaServicesCredentials содержит токен ACS, которую можно использовать повторно, если он по-прежнему допустим.</span><span class="sxs-lookup"><span data-stu-id="478cd-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="478cd-144">Если токен hello не является допустимым, он будет обновлен с hello пакета SDK служб мультимедиа с использованием учетных данных hello получает toohello MediaServicesCredentials конструктор.</span><span class="sxs-lookup"><span data-stu-id="478cd-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="478cd-145">Обратите внимание, что hello **MediaServicesCredentials** объект получает допустимый токен после RefreshToken вызывается hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="478cd-146">Hello **CloudMediaContext** hello вызовов **RefreshToken** метод в конструкторе hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="478cd-147">При планировании внешнего хранилища значения маркера hello tooan toosave принять убедиться, что toocheck hello TokenExpiration значение является допустимым, прежде чем сохранять данные токена hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="478cd-148">Если оно недействительно, вызовите RefreshToken перед кэшированием.</span><span class="sxs-lookup"><span data-stu-id="478cd-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="478cd-149">Также можно кэшировать строку hello AccessToken и hello TokenExpiration значения.</span><span class="sxs-lookup"><span data-stu-id="478cd-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="478cd-150">значения Hello позже может быть используется toocreate новый MediaServicesCredentials объекта с hello кэшированные данные токена.</span><span class="sxs-lookup"><span data-stu-id="478cd-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="478cd-151">Это особенно полезно для сценариев, где маркер hello, могут безопасно использоваться нескольких процессах или компьютеров.</span><span class="sxs-lookup"><span data-stu-id="478cd-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="478cd-152">Hello следующие фрагменты кода вызывают hello методы SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage и UpdateTokenDataInExternalStorageIfNeeded методы, которые не определены в этом примере.</span><span class="sxs-lookup"><span data-stu-id="478cd-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="478cd-153">Вы можете определить эти toostore методы, получение и обновление данных токена во внешнем хранилище.</span><span class="sxs-lookup"><span data-stu-id="478cd-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="478cd-154">Используйте сохраненные значения токена toocreate MediaServicesCredentials hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    <span data-ttu-id="478cd-155">Обновите копию токена hello в случае, если токен hello был обновлен пакетом hello пакета SDK служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="478cd-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="478cd-156">Если у вас несколько учетных записей служб мультимедиа (например, для управления доступом целей или географического распределения нагрузки) можно кэшировать MediaServicesCredentials объектов с помощью коллекции System.Collections.Concurrent.ConcurrentDictionary hello (hello Коллекция ConcurrentDictionary представляет потокобезопасную коллекцию пар "ключ значение", может осуществляться несколькими потоками одновременно).</span><span class="sxs-lookup"><span data-stu-id="478cd-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="478cd-157">Затем можно использовать учетные данные в кэше hello tooget метод GetOrAdd hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="478cd-158">Подключение tooa учетная запись служб мультимедиа в hello северном регионе Китая</span><span class="sxs-lookup"><span data-stu-id="478cd-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="478cd-159">Если ваша учетная запись находится в hello северном регионе Китая, используйте hello следующий конструктор:</span><span class="sxs-lookup"><span data-stu-id="478cd-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="478cd-160">Например:</span><span class="sxs-lookup"><span data-stu-id="478cd-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="478cd-161">Хранение в конфигурации значений для подключения</span><span class="sxs-lookup"><span data-stu-id="478cd-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="478cd-162">Это значения подключения toostore настоятельно рекомендуется, особенно конфиденциальные значения, такие как имя учетной записи и пароля в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="478cd-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="478cd-163">Кроме того это рекомендуемый подход tooencrypt конфиденциальные данные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="478cd-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="478cd-164">Hello весь файл конфигурации можно зашифровать с помощью hello Windows шифрованной файловой системы (EFS).</span><span class="sxs-lookup"><span data-stu-id="478cd-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="478cd-165">Выберите tooenable EFS с файлом, щелкните правой кнопкой мыши файл hello, **свойства**и включите шифрование в hello **Дополнительно** вкладка "Параметры". Кроме того, с помощью защищенной конфигурации можно создать пользовательское решение для шифрования выбранных частей файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="478cd-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="478cd-166">См. статью [Шифрование сведений о конфигурации с помощью функции защищенной конфигурации](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="478cd-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="478cd-167">Привет, следующий файл App.config содержит hello необходимые значения подключения.</span><span class="sxs-lookup"><span data-stu-id="478cd-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="478cd-168">Здравствуйте, значения в hello <appSettings> являются hello необходимых значений, полученных из процесса настройки учетной записи службы мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="478cd-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="478cd-169">tooretrieve значения подключения из конфигурации, можно использовать hello **ConfigurationManager** класса, а затем назначьте hello toofields значения в коде:</span><span class="sxs-lookup"><span data-stu-id="478cd-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="478cd-170">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="478cd-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="478cd-171">Отзывы</span><span class="sxs-lookup"><span data-stu-id="478cd-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

