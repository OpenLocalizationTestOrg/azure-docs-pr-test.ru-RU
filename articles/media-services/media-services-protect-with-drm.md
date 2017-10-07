---
title: "aaaUsing PlayReady и/или Widevine динамического общее шифрование | Документы Microsoft"
description: "Службы мультимедиа Microsoft Azure позволяет вам toodeliver MPEG-DASH, Smooth Streaming и Http-Live-Streaming (HLS) потоки защищены с помощью Microsoft PlayReady DRM. Он также позволяет toodelivery зашифрован Widevine DRM ТИРЕ. В этом разделе показано, как зашифровать toodynamically с помощью PlayReady и Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a>Использование общего динамического шифрования PlayReady и (или) Widevine DRM

> [!div class="op_single_selector"]
> * [.NET](media-services-protect-with-drm.md)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

Службы мультимедиа Microsoft Azure позволяет toodeliver MPEG-DASH, Smooth Streaming и HTTP-Live-Streaming (HLS) потоки, защищенные с помощью [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). Он также позволяет потоки ТИРЕ toodeliver зашифрованы с лицензии Widevine DRM. PlayReady и Widevine шифруются на hello спецификации общее шифрование (CENC ISO/IEC 23001-7). Можно использовать [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (начиная с версии hello 3.5.1) или REST API tooconfigure вашей AssetDeliveryConfiguration toouse Widevine.

Службы мультимедиа обеспечивают доставку лицензий PlayReady и DRM Widevine. Службы мультимедиа также предоставляют интерфейсы API, позволяющие настроить hello права и ограничения, которые hello PlayReady или Widevine DRM среды выполнения tooenforce, в когда пользователь воспроизводит защищенное содержимое. Когда пользователь запрашивает содержимое защищенного DRM, приложение hello-проигрыватель будет запрашивать лицензию из службы лицензий hello AMS. Служба лицензий AMS Hello будет выдавать лицензии проигрыватель toohello ли он авторизован. Лицензии PlayReady или Widevine содержит ключ расшифровки hello, который может использоваться hello клиента toodecrypt и поток hello содержимое проигрывателя.

Можно также использовать следующие toohelp партнеров AMS доставки лицензии Widevine hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Дополнительные сведения см. в статьях, посвященных интеграции с [Axinom](media-services-axinom-integration.md) и [castLabs](media-services-castlabs-integration.md).

Службы мультимедиа поддерживают несколько способов авторизации пользователей, которые запрашивают ключи. Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: открыть или маркер ограниченного использования программ. политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS). Службы мультимедиа поддерживают только токены в hello [токенов SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) формат (SWT) и [веб-маркера JSON](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) формате. Дополнительные сведения см. в разделе Настройка hello содержимого политики авторизации ключа.

преимущества tootake динамического шифрования требуется актив, содержащий набор MP4-файлов с разными скоростями или файлы источника Smooth Streaming с разными скоростями toohave. Необходимо также tooconfigure hello доставки политик для средства hello (описывается далее в этом разделе). Затем на основании hello формат, указанный в URL-адрес потоковой передачи hello, hello сервера потоковой передачи по требованию проверит доставку потока hello в протоколе hello, которую вы выбрали. В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать hello соответствующие HTTP-ответа на основе каждого запроса от клиента.

В этом разделе будет полезно toodevelopers, работы с приложениями, доставки мультимедиа, защищенные с помощью нескольких DRMs, например, PlayReady и Widevine. Hello разделе показано, как tooconfigure hello службы доставки лицензий PlayReady с политиками авторизации, чтобы только авторизованные клиенты могли получать лицензии PlayReady или Widevine. Здесь также показано, как шифрование toouse динамического шифрования с помощью PlayReady или DRM Widevine через дефис.

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. 

## <a name="download-sample"></a>Скачивание образца
Вы можете загрузить пример hello, описанных в этой статье из [здесь](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a>Настройка общего динамического шифрования и службы доставки лицензий DRM

Hello ниже приведены общие шаги, что tooperform понадобятся вам при защите ресурсов с помощью PlayReady, использовании службы доставки лицензий Media Services hello и использовании динамического шифрования.

1. Создание актива и отправка файлов в актив hello.
2. Кодирование hello активов содержащего hello файл toohello с адаптивной скоростью набор MP4.
3. Создание ключа контента и связать его с активом hello кодировке. В службах мультимедиа ключ контента hello содержит ключ шифрования актива hello.
4. Настройка политики авторизации hello ключа содержимого. Политика авторизации ключей содержимого Hello должно быть настроена вами и клиент hello, чтобы клиент доставленный toohello содержимого ключа toobe hello.

    При создании политики авторизации ключа контента hello, необходимо следующее hello toospecify: метод (PlayReady или Widevine) ограничения доставки (open или маркер) и сведения о конкретных toohello доставки ключей тип, который определяет способ доставки ключа hello Клиент toohello ([PlayReady](media-services-playready-license-template-overview.md) или [Widevine](media-services-widevine-license-template-overview.md) шаблон лицензии).

5. Настройте политику hello доставки для актива. Hello конфигурация политики доставки включает: тип динамического шифрования (например, общее шифрование), PlayReady или URL-адрес приобретения лицензии Widevine hello протокол доставки (например, MPEG DASH, HLS, Smooth Streaming или все).

    Можно применить другой политике tooeach протокола на hello одного средства. Например можно применить шифрование PlayReady tooSmooth/DASH и AES Envelope tooHLS. Все протоколы, которые не определены в политике доставки (например, добавить отдельную политику, которая указывает в качестве протокола hello только HLS) будут заблокированы для потоковой передачи. Hello toothis исключение — когда нет определенных политик доставки активов. Затем все протоколы будут разрешены в hello снимите флажок.

6. Создание указателя OnDemand в порядке tooget URL-адрес потоковой передачи.

Можно найти полный пример, в конце hello раздела hello .NET.

Следующие изображения Hello демонстрирует hello рабочего процесса, описанного выше. Здесь hello маркер используется для проверки подлинности.

![Защита с помощью PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

Hello остальной части этого раздела содержатся подробные объяснения, примеры кода и tootopics ссылки, которые показывают, как tooachieve hello задач, описанных выше.

## <a name="current-limitations"></a>Текущие ограничения
При добавлении или обновлении политики доставки активов необходимо удалить hello связанные указатель (если есть) и создать новый указатель.

Ограничение при шифровании с помощью Widevine в службах мультимедиа Azure: в настоящее время использование нескольких ключей содержимого не поддерживается.

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a>Создание актива и отправка файлов в актив hello
В порядке toomanage, кодирования и потоковой передачи видео необходимо сначала передать содержимое в службы мультимедиа Microsoft Azure. После отправки контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.

Дополнительные сведения см. в статье [Передача файлов в учетную запись служб мультимедиа с помощью .NET](media-services-dotnet-upload-files.md).

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a>Кодирование hello активов содержащего hello файл toohello с адаптивной скоростью набор MP4
При использовании динамического шифрования требуется всего лишь toocreate актив, содержащий набор MP4-файлов с разными скоростями или файлы источника Smooth Streaming с разными скоростями. Затем на основе заданного формата hello в манифесте hello и фрагмент запроса, hello server проверит Получение потока hello в протоколе hello, которую вы выбрали потоковой передачи по требованию. В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента. Дополнительные сведения см. в разделе hello [Общие сведения о динамической упаковке](media-services-dynamic-packaging-overview.md) раздела.

Инструкции о том, как tooencode, в разделе [как tooencode ресурс с помощью Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).

## <a id="create_contentkey"></a>Создание ключа контента и связать его с активом hello кодировке
В службах мультимедиа ключ контента hello содержит ключ hello, что требуется tooencrypt актива с.

Дополнительные сведения см. в статье [Создание ContentKey с использованием .NET](media-services-dotnet-create-contentkey.md).

## <a id="configure_key_auth_policy"></a>Настройка политики авторизации hello ключ содержимого
Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи. Политика авторизации ключей содержимого Hello должно быть настроена вами и hello клиент (проигрыватель) в порядке для ключа toobe hello доставить toohello клиента. Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: открыть или маркер ограниченного использования программ.

Дополнительные сведения см. в разделе [Настройка политики авторизации ключа содержимого](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).

## <a id="configure_asset_delivery_policy"></a>Настройка политики доставки для ресурса-контейнера
Настройте политику hello доставки для актива. Некоторые элементы, которые hello конфигурация политики доставки актива включает в себя:

* Hello DRM приобретения URL-адрес лицензии.
* Hello протокол доставки актива (например, MPEG DASH, HLS, Smooth Streaming или все).
* Hello тип динамического шифрования (в данном случае общее шифрование).

Дополнительные сведения см. в разделе [Настройка политик доставки ресурсов](media-services-rest-configure-asset-delivery-policy.md).

## <a id="create_locator"></a>Создание OnDemand потоковой передачи указателя в порядке tooget URL-адрес потоковой передачи
Вам потребуется tooprovide пользователей с hello потоковой передачи URL-адрес для Smooth, DASH или HLS.

> [!NOTE]
> При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.
>
>

Инструкции по статье toopublish актива и построения URL-АДРЕСЕ потоковой передачи, [построения URL-адрес потоковой передачи](media-services-deliver-streaming-content.md).

## <a name="get-a-test-token"></a>Получение маркера тестирования
Получение тестового токена, на основе ограничения токенов hello, которое использовалось для политики авторизации ключа hello.

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


Можно использовать hello [AMS проигрывателя](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest потока.

## <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

1. Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 
2. Добавьте следующие элементы слишком hello**appSettings** определенной в файле app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Пример

Hello следующий пример демонстрирует функциональных возможностей, появившихся в Azure Media Services SDK для .net-версии 3.5.2 (в частности, toodefine возможность hello Widevine лицензии шаблона и запрос лицензии Widevine из службы мультимедиа Azure).

Перезаписать hello код в файле Program.cs кодом hello, приведенные в этом разделе.

>[!NOTE]
>Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy). Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики). Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.

Сделайте том tooupdate переменных toopoint toofolders где расположены входные файлы.

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Дополнительные материалы
[CENC with Multi-DRM and Access Control (CENC с несколькими подсистемами DRM и контролем доступа)](media-services-cenc-with-multidrm-access-control.md)

[Настройка упаковки Widevine с использованием AMS](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[Анонс служб доставки лицензий Google Widevine в службах мультимедиа Azure](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
