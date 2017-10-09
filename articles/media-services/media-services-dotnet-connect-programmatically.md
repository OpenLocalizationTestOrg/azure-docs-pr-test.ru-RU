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
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>Подключение tooMedia учетной записи службы, с помощью пакета SDK служб мультимедиа для .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

В этом разделе описывается, как tooobtain tooMicrosoft программное подключение при программировании с использованием служб мультимедиа Azure hello пакета SDK служб мультимедиа для .NET.

## <a name="connecting-toomedia-services"></a>Соединение tooMedia служб
tooconnect tooMedia службы программными средствами, необходимо заранее настроить учетную запись Azure, настроенными службами мультимедиа в этой учетной записи и затем настроить проект Visual Studio для разработки с hello пакета SDK служб мультимедиа для .NET. Дополнительные сведения см. в разделе Настройка для разработки с hello пакета SDK служб мультимедиа для .NET.

В конце процесса настройки учетной записи службы мультимедиа hello hello, полученный hello следующие необходимые значения подключения. Используйте эти подключения программный toomake tooMedia служб.

* Имя учетной записи служб мультимедиа.
* Ключ учетной записи служб мультимедиа.

Эти значения, toofind go toohello портала управления Azure, выберите свою учетную запись службы мультимедиа и щелкните hello»**УПРАВЛЕНИЕ КЛЮЧАМИ**» значок hello нижней части окна портала hello. Щелкнув hello значок Далее tooeach текстовое поле копии hello значение toohello системный буфер обмена.

## <a name="creating-a-cloudmediacontext-instance"></a>Создание экземпляра CloudMediaContext
Программирование реакции на Media Services необходима toocreate toostart **CloudMediaContext** экземпляр, представляющий контекст сервера hello. Hello **CloudMediaContext** содержит ссылки на коллекции tooimportant, включая задания, активы, файлы, политики доступа и указатели.

> [!NOTE]
> Hello **CloudMediaContext** класс не является потокобезопасным. Для каждого потока или набора операций необходимо создать новый CloudMediaContext.
> 
> 

В CloudMediaContext предусмотрено пять перегрузок конструктора. Это рекомендуемый toouse конструкторов, принимающих **MediaServicesCredentials** как параметр. Дополнительные сведения см. в разделе hello **повторное использование токенов службы контроля доступа** ниже. 

Hello следующий пример использует открытый конструктор CloudMediaContext(MediaServicesCredentials credentials) hello.

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Повторное использование маркеров службы управления доступом
В этом разделе показано, как маркеры tooreuse службы контроля доступа с помощью CloudMediaContext конструкторов, принимающих MediaServicesCredentials в качестве параметра.

[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (также называется Access Control Service или ACS) является облачная служба, предоставляющая простой способ проверки подлинности и авторизацию доступа пользователей toogain tootheir веб-приложений. Службы мультимедиа Microsoft Azure управляет доступом службы tooits Хотя протокол OAuth, который требуется токен ACS. Службы мультимедиа получает hello токены ACS из сервера авторизации.

При разработке с помощью пакета SDK служб мультимедиа hello, вы можете toonot приходится иметь дело с hello токены, так как hello диспетчеры кода SDK ими. Тем не менее позволяя hello SDK полностью управлять запросы маркеров toounnecessary интересы токены hello ACS. Запрашиваемые токены времени и потребляет ресурсы hello клиента и сервера. Кроме того сервер ACS hello регулирует hello запросов, если hello значение слишком велико. Hello ограничение составляет 30 запросов в секунду см. в разделе [ограничения службы ACS](https://msdn.microsoft.com/library/gg185909.aspx) для получения дополнительных сведений.

Начиная с пакета SDK служб мультимедиа версии 3.0.0.0 hello, можно повторно использовать токены ACS hello. Hello **CloudMediaContext** конструкторов, принимающих **MediaServicesCredentials** как параметр включения совместного использования токенов hello ACS между несколькими контекстами. Hello MediaServicesCredentials класс инкапсулирует учетные данные службы мультимедиа hello. Если токен ACS доступен и известен ее срок, можно создать новый экземпляр MediaServicesCredentials с маркером hello и передать его конструктору toohello CloudMediaContext. Обратите внимание, что hello пакета SDK служб мультимедиа автоматически обновляет токены по истечении их срока действия. Существует два способа tooreuse токены ACS, как показано в следующих примерах hello.

* Можно кэшировать hello **MediaServicesCredentials** объект в памяти (например, в переменной статического класса). Затем передайте конструктор CloudMediaContext toohello кэширования hello объекта. Hello объект MediaServicesCredentials содержит токен ACS, которую можно использовать повторно, если он по-прежнему допустим. Если токен hello не является допустимым, он будет обновлен с hello пакета SDK служб мультимедиа с использованием учетных данных hello получает toohello MediaServicesCredentials конструктор.
  
    Обратите внимание, что hello **MediaServicesCredentials** объект получает допустимый токен после RefreshToken вызывается hello. Hello **CloudMediaContext** hello вызовов **RefreshToken** метод в конструкторе hello. При планировании внешнего хранилища значения маркера hello tooan toosave принять убедиться, что toocheck hello TokenExpiration значение является допустимым, прежде чем сохранять данные токена hello. Если оно недействительно, вызовите RefreshToken перед кэшированием.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* Также можно кэшировать строку hello AccessToken и hello TokenExpiration значения. значения Hello позже может быть используется toocreate новый MediaServicesCredentials объекта с hello кэшированные данные токена.  Это особенно полезно для сценариев, где маркер hello, могут безопасно использоваться нескольких процессах или компьютеров.
  
    Hello следующие фрагменты кода вызывают hello методы SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage и UpdateTokenDataInExternalStorageIfNeeded методы, которые не определены в этом примере. Вы можете определить эти toostore методы, получение и обновление данных токена во внешнем хранилище. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Используйте сохраненные значения токена toocreate MediaServicesCredentials hello.

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

    Обновите копию токена hello в случае, если токен hello был обновлен пакетом hello пакета SDK служб мультимедиа. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Если у вас несколько учетных записей служб мультимедиа (например, для управления доступом целей или географического распределения нагрузки) можно кэшировать MediaServicesCredentials объектов с помощью коллекции System.Collections.Concurrent.ConcurrentDictionary hello (hello Коллекция ConcurrentDictionary представляет потокобезопасную коллекцию пар "ключ значение", может осуществляться несколькими потоками одновременно). Затем можно использовать учетные данные в кэше hello tooget метод GetOrAdd hello. 
  
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>Подключение tooa учетная запись служб мультимедиа в hello северном регионе Китая
Если ваша учетная запись находится в hello северном регионе Китая, используйте hello следующий конструктор:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Например:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Хранение в конфигурации значений для подключения
Это значения подключения toostore настоятельно рекомендуется, особенно конфиденциальные значения, такие как имя учетной записи и пароля в конфигурации. Кроме того это рекомендуемый подход tooencrypt конфиденциальные данные конфигурации. Hello весь файл конфигурации можно зашифровать с помощью hello Windows шифрованной файловой системы (EFS). Выберите tooenable EFS с файлом, щелкните правой кнопкой мыши файл hello, **свойства**и включите шифрование в hello **Дополнительно** вкладка "Параметры". Кроме того, с помощью защищенной конфигурации можно создать пользовательское решение для шифрования выбранных частей файла конфигурации. См. статью [Шифрование сведений о конфигурации с помощью функции защищенной конфигурации](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Привет, следующий файл App.config содержит hello необходимые значения подключения. Здравствуйте, значения в hello <appSettings> являются hello необходимых значений, полученных из процесса настройки учетной записи службы мультимедиа hello.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


tooretrieve значения подключения из конфигурации, можно использовать hello **ConfigurationManager** класса, а затем назначьте hello toofields значения в коде:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

