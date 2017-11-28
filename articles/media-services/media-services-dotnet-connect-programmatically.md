---
title: "Подключение к учетной записи служб мультимедиа с помощью .NET"
description: "В этом разделе показано, как подключиться к службам мультимедиа с помощью .NET."
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
ms.openlocfilehash: 892932116934952265a21ab17aac3434b5760136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="df0b3-103">Подключение к учетной записи служб мультимедиа с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="df0b3-103">Connecting to Media Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="df0b3-104">REST</span><span class="sxs-lookup"><span data-stu-id="df0b3-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="df0b3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="df0b3-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="df0b3-106">В этом разделе описывается установка программного подключения к службам мультимедиа Microsoft Azure при программировании с помощью пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="df0b3-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span></span>

## <a name="connecting-to-media-services"></a><span data-ttu-id="df0b3-107">Подключение к службам мультимедиа</span><span class="sxs-lookup"><span data-stu-id="df0b3-107">Connecting to Media Services</span></span>
<span data-ttu-id="df0b3-108">Для программного подключения к службам мультимедиа необходимо предварительно настроить учетную запись Azure, настроить службы мультимедиа для этой учетной записи, а затем настроить проект Visual Studio для разработки с помощью пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="df0b3-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span></span> <span data-ttu-id="df0b3-109">Дополнительную информацию см. в разделе "Настройка для разработки с помощью пакета SDK служб мультимедиа для .NET".</span><span class="sxs-lookup"><span data-stu-id="df0b3-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span></span>

<span data-ttu-id="df0b3-110">В конце процесса настройки учетной записи служб мультимедиа вы получите следующие значения, необходимые для подключения.</span><span class="sxs-lookup"><span data-stu-id="df0b3-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span></span> <span data-ttu-id="df0b3-111">Используйте их для программного подключения к службам мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="df0b3-111">Use these to make programmatic connections to Media Services.</span></span>

* <span data-ttu-id="df0b3-112">Имя учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="df0b3-112">Your Media Services account name.</span></span>
* <span data-ttu-id="df0b3-113">Ключ учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="df0b3-113">Your Media Services account key.</span></span>

<span data-ttu-id="df0b3-114">Чтобы найти эти значения, перейдите на портал управления Azure, выберите свою учетную запись служб мультимедиа и щелкните значок**УПРАВЛЕНИЕ КЛЮЧАМИ**в нижней части окна портала.</span><span class="sxs-lookup"><span data-stu-id="df0b3-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span></span> <span data-ttu-id="df0b3-115">Щелкните значок рядом с каждым текстовым полем, чтобы скопировать значения в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="df0b3-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="df0b3-116">Создание экземпляра CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="df0b3-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="df0b3-117">Чтобы начать программирование для служб мультимедиа, необходимо создать экземпляр **CloudMediaContext** , представляющий контекст сервера.</span><span class="sxs-lookup"><span data-stu-id="df0b3-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="df0b3-118">**CloudMediaContext** содержит ссылки на важные коллекции, в том числе на задания, ресурсы, файлы, политики доступа и указатели.</span><span class="sxs-lookup"><span data-stu-id="df0b3-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="df0b3-119">Класс **CloudMediaContext** не является потокобезопасным.</span><span class="sxs-lookup"><span data-stu-id="df0b3-119">The **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="df0b3-120">Для каждого потока или набора операций необходимо создать новый CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="df0b3-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="df0b3-121">В CloudMediaContext предусмотрено пять перегрузок конструктора.</span><span class="sxs-lookup"><span data-stu-id="df0b3-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="df0b3-122">Рекомендуется использовать конструкторы, принимающие **MediaServicesCredentials** в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="df0b3-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="df0b3-123">Дополнительную информацию см. ниже в разделе **Повторное использование маркеров службы управления доступом**.</span><span class="sxs-lookup"><span data-stu-id="df0b3-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="df0b3-124">В следующем примере используется открытый конструктор CloudMediaContext(учетные данные MediaServicesCredentials):</span><span class="sxs-lookup"><span data-stu-id="df0b3-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="df0b3-125">Повторное использование маркеров службы управления доступом</span><span class="sxs-lookup"><span data-stu-id="df0b3-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="df0b3-126">В этом разделе показано, как повторно использовать маркеры службы управления доступом с помощью конструкторов CloudMediaContext, принимающих MediaServicesCredentials в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="df0b3-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="df0b3-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (Access Control Service или ACS) — это облачная служба, с помощью которой можно легко провести аутентификацию и авторизацию пользователей для предоставления им доступа к их веб-приложениям.</span><span class="sxs-lookup"><span data-stu-id="df0b3-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span></span> <span data-ttu-id="df0b3-128">Службы мультимедиа Microsoft Azure управляют доступом к своим службам по протоколу OAuth, для которого требуется маркер ACS.</span><span class="sxs-lookup"><span data-stu-id="df0b3-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="df0b3-129">Службы мультимедиа получают маркеры ACS с сервера авторизации.</span><span class="sxs-lookup"><span data-stu-id="df0b3-129">Media Services receives the ACS tokens from an authorization server.</span></span>

<span data-ttu-id="df0b3-130">При разработке с помощью пакета SDK служб мультимедиа при желании можно отказаться от использования маркеров, так как код пакета SDK обрабатывает их автоматически.</span><span class="sxs-lookup"><span data-stu-id="df0b3-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span></span> <span data-ttu-id="df0b3-131">Тем не менее, когда пакет SDK полностью управляет маркерами ACS, это приводит к созданию лишних запросов маркеров.</span><span class="sxs-lookup"><span data-stu-id="df0b3-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span></span> <span data-ttu-id="df0b3-132">На обработку запросов маркеров тратится время и ресурсы клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="df0b3-132">Requesting tokens takes time and consumes the client and server resources.</span></span> <span data-ttu-id="df0b3-133">Кроме того, если их слишком много сервер ACS регулирует поток запросов.</span><span class="sxs-lookup"><span data-stu-id="df0b3-133">Also, the ACS server throttles the requests if the rate is too high.</span></span> <span data-ttu-id="df0b3-134">Предельное значение — 30 запросов в секунду. Дополнительную информацию см. в статье [Ограничения службы ACS](https://msdn.microsoft.com/library/gg185909.aspx).</span><span class="sxs-lookup"><span data-stu-id="df0b3-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="df0b3-135">Начиная с пакета SDK служб мультимедиа версии 3.0.0.0, маркеры ACS можно использовать повторно.</span><span class="sxs-lookup"><span data-stu-id="df0b3-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span></span> <span data-ttu-id="df0b3-136">Конструкторы **CloudMediaContext**, принимающие **MediaServicesCredentials** в качестве параметра, обеспечивают возможность совместного использования токенов службы ACS в нескольких контекстах.</span><span class="sxs-lookup"><span data-stu-id="df0b3-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span></span> <span data-ttu-id="df0b3-137">Класс MediaServicesCredentials инкапсулирует учетные данные служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="df0b3-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span></span> <span data-ttu-id="df0b3-138">Если маркер ACS доступен и известен срок его действия, можно создать новый экземпляр MediaServicesCredentials с маркером и передать его в конструктор CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="df0b3-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span></span> <span data-ttu-id="df0b3-139">Обратите внимание, что пакет SDK служб мультимедиа позволяет автоматически обновлять маркеры при истечении срока их действия.</span><span class="sxs-lookup"><span data-stu-id="df0b3-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="df0b3-140">Как показано в примерах ниже, маркеры ACS можно использовать повторно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="df0b3-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span></span>

* <span data-ttu-id="df0b3-141">Объект **MediaServicesCredentials** можно кэшировать в памяти (например, в переменной статического класса).</span><span class="sxs-lookup"><span data-stu-id="df0b3-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="df0b3-142">Затем кэшированный объект передается конструктору CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="df0b3-142">Then, pass the cached object to the CloudMediaContext constructor.</span></span> <span data-ttu-id="df0b3-143">Объект MediaServicesCredentials содержит маркер ACS, который можно использовать, если он все еще действителен.</span><span class="sxs-lookup"><span data-stu-id="df0b3-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="df0b3-144">Если маркер недействителен, он будет обновлен пакетом SDK для служб мультимедиа с использованием учетных данных, предоставленных конструктору MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="df0b3-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="df0b3-145">Обратите внимание, что объект **MediaServicesCredentials** получает действительный токен после вызова RefreshToken.</span><span class="sxs-lookup"><span data-stu-id="df0b3-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span></span> <span data-ttu-id="df0b3-146">**CloudMediaContext** вызывает метод **RefreshToken** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="df0b3-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span></span> <span data-ttu-id="df0b3-147">Если вы планируете сохранить значения маркера во внешнем хранилище, перед сохранением данных маркера обязательно убедитесь, что значение TokenExpiration действительно.</span><span class="sxs-lookup"><span data-stu-id="df0b3-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span></span> <span data-ttu-id="df0b3-148">Если оно недействительно, вызовите RefreshToken перед кэшированием.</span><span class="sxs-lookup"><span data-stu-id="df0b3-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="df0b3-149">Кроме того, можно кэшировать строку AccessToken и значения TokenExpiration.</span><span class="sxs-lookup"><span data-stu-id="df0b3-149">You can also cache the AccessToken string and the TokenExpiration values.</span></span> <span data-ttu-id="df0b3-150">Значения можно будет использовать позже для создания нового объекта MediaServicesCredentials с кэшированными данными маркера.</span><span class="sxs-lookup"><span data-stu-id="df0b3-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span></span>  <span data-ttu-id="df0b3-151">Это особенно удобно в сценариях, в которых маркер может безопасно использоваться несколькими процессами или компьютерами.</span><span class="sxs-lookup"><span data-stu-id="df0b3-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="df0b3-152">В следующих фрагментах кода вызываются методы SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage и UpdateTokenDataInExternalStorageIfNeeded, которые не определены в этом примере.</span><span class="sxs-lookup"><span data-stu-id="df0b3-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="df0b3-153">Эти методы можно определить для хранения, извлечения и обновления маркеров данных во внешнем хранилище.</span><span class="sxs-lookup"><span data-stu-id="df0b3-153">You could define these methods to store, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="df0b3-154">Используйте сохраненные значения токена для создания MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="df0b3-154">Use the saved token values to create MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="df0b3-155">Обновите копию в случае, если токен был обновлен пакетом SDK служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="df0b3-155">Update the token copy in case the token was updated by the Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="df0b3-156">При наличии несколько учетных записей служб мультимедиа (например, для распределения нагрузки или географического распределения) объекты MediaServicesCredentials можно кэшировать с помощью коллекции System.Collections.Concurrent.ConcurrentDictionary (ConcurrentDictionary — это потокобезопасная коллекция пар "ключ-значение", к которой могут обращаться несколько потоков одновременно).</span><span class="sxs-lookup"><span data-stu-id="df0b3-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="df0b3-157">Затем можно использовать метод GetOrAdd для получения кэшированных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="df0b3-157">You can then use the GetOrAdd method to get the cached credentials.</span></span> 
  
        // Declare a static class variable of the ConcurrentDictionary type in which the Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials to create a new CloudMediaContext object.
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

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a><span data-ttu-id="df0b3-158">Подключение к учетной записи служб мультимедиа, расположенной в северном регионе Китая</span><span class="sxs-lookup"><span data-stu-id="df0b3-158">Connecting to a Media Services account located in the North China region</span></span>
<span data-ttu-id="df0b3-159">Если ваша учетная запись находится в северном регионе Китая, используйте следующий конструктор:</span><span class="sxs-lookup"><span data-stu-id="df0b3-159">If your account is located in the North China region, use the following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="df0b3-160">Например:</span><span class="sxs-lookup"><span data-stu-id="df0b3-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="df0b3-161">Хранение в конфигурации значений для подключения</span><span class="sxs-lookup"><span data-stu-id="df0b3-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="df0b3-162">Настоятельно рекомендуем хранить значения для подключения, особенно конфиденциальные, например имя учетной записи и пароль, в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df0b3-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="df0b3-163">Кроме того, рекомендуется шифровать конфиденциальные данные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df0b3-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span></span> <span data-ttu-id="df0b3-164">С помощью шифрованной файловой системы (EFS) Windows можно зашифровать весь файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df0b3-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="df0b3-165">Чтобы включить файловую систему EFS для файла, щелкните правой кнопкой мыши файл, выберите **Свойства** и включите шифрование на вкладке параметров **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="df0b3-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab.</span></span> <span data-ttu-id="df0b3-166">Кроме того, с помощью защищенной конфигурации можно создать пользовательское решение для шифрования выбранных частей файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df0b3-166">Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="df0b3-167">См. статью [Шифрование сведений о конфигурации с помощью функции защищенной конфигурации](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="df0b3-167">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="df0b3-168">Следующий файл App.config содержит необходимые значения для подключения.</span><span class="sxs-lookup"><span data-stu-id="df0b3-168">The following App.config file contains the required connection values.</span></span> <span data-ttu-id="df0b3-169">Значения в элементе <appSettings> — это обязательные значения, получаемые в процессе настройки учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="df0b3-169">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="df0b3-170">Чтобы получить значения для подключения из конфигурации, можно использовать класс **ConfigurationManager** , а затем присвоить значения полям в коде:</span><span class="sxs-lookup"><span data-stu-id="df0b3-170">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="df0b3-171">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="df0b3-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="df0b3-172">Отзывы</span><span class="sxs-lookup"><span data-stu-id="df0b3-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

