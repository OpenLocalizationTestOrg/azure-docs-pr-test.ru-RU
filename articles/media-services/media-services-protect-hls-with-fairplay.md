---
title: "aaaProtect HLS содержимого с помощью Microsoft PlayReady или Apple FairPlay - Azure | Документы Microsoft"
description: "В этом разделе приводится обзор и показано, как службы мультимедиа Azure toodynamically toouse шифрования контента с Apple FairPlay HTTP Live Streaming (HLS). Здесь также показано, как toouse hello Media Services лицензии toodeliver службы доставки лицензий tooclients FairPlay."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a>Защита содержимого HLS с помощью Apple FairPlay или Microsoft PlayReady
Службы мультимедиа позволяют Azure, вы toodynamically шифрования контента HTTP Live Streaming (HLS) с помощью hello следующие форматы:  

* **Незащищенный ключ конверта AES-128**

    Hello весь блок шифруется с помощью hello **CBC AES-128** режим. Расшифровка Hello hello потока имеет собственной поддержки iOS и OS X проигрывателя. Дополнительные сведения см. в статье [Использование динамического шифрования AES-128 и службы доставки ключей](media-services-protect-with-aes128.md).
* **Apple FairPlay**

    Здравствуйте, отдельные видео и аудио образцы, шифруются с помощью hello **CBC AES-128** режим. **Потоковая передача FairPlay** интегрируется в hello операционных систем устройств со встроенной поддержкой в iOS и Apple TV (кадров/с). Safari в OS X позволяет кадров в Секунду, используя поддержку интерфейса hello зашифрованные мультимедиа расширения (EME).
* **Microsoft PlayReady**

Hello на рисунке показаны hello **HLS + FairPlay или PlayReady динамического шифрования** рабочего процесса.

![Схема рабочего процесса динамического шифрования](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

В этом разделе показано, как toodynamically toouse Media Services зашифровать содержимое HLS с Apple FairPlay. Здесь также показано, как toouse hello Media Services лицензии toodeliver службы доставки лицензий tooclients FairPlay.

> [!NOTE]
> Если также требуется tooencrypt контента HLS содержимого с помощью PlayReady, требуется toocreate общим ключом содержимого и связать его с ресурсом. Необходимо также tooconfigure hello содержимого политики авторизации ключа, как описано в [динамического общее шифрование с помощью PlayReady](media-services-protect-with-drm.md).
>
>

## <a name="requirements-and-considerations"></a>Требования и рекомендации

При использовании служб мультимедиа toodeliver шифрования HLS с FairPlay и лицензии FairPlay toodeliver, не требуется Hello следующие:

  * Учетная запись Azure. Дополнительные сведения см. на странице с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
  * Учетная запись служб мультимедиа. разделе toocreate, [создать учетную запись служб мультимедиа Azure с помощью портала Azure hello](media-services-portal-create-account.md).
  * Регистрация в [программе разработки Apple](https://developer.apple.com/).
  * Apple требует hello владельца содержимого tooobtain hello [пакет развертывания](https://developer.apple.com/contact/fps/). Состояние уже реализован модуль безопасности ключ (KSM) с помощью служб мультимедиа и запрашивается hello конечного пакета число кадров в Секунду. Существуют инструкциям hello окончательного кадров в Секунду пакета toogenerate сертификации и получить hello секретный ключ приложения (ASK). Используется, чтобы ЗАДАТЬ tooconfigure FairPlay.
  * Пакет SDK служб мультимедиа Azure для .NET **3.6.0** или более поздней версии.

Привет, выполнив действия должно быть задано на стороне доставки ключей служб мультимедиа:

  * **Приложение Cert (AC)**: это PFX-файл, который содержит закрытый ключ hello. Создайте этот файл и зашифруйте его с помощью пароля.

       При настройке политики доставки ключей, необходимо указать этот пароль и hello PFX-файл в формате Base64.

      Привет, следующие шаги описывают, как toogenerate сертификата PFX-файла для FairPlay:

    1. Установите OpenSSL со страницы https://slproweb.com/products/Win32OpenSSL.html.

        Go toohello папку, где сертификат FairPlay hello и другие файлы, доставленные Apple.
    2. Выполните следующую команду из командной строки hello hello. Это преобразует hello .cer файл tooa PEM-файл.

        "C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem
    3. Выполните следующую команду из командной строки hello hello. Это преобразует hello .pem файл tooa PFX-файл с закрытым ключом hello. затем Hello пароль для PFX-файл hello запрашивается с помощью OpenSSL.

        "C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt
  * **Пароль сертификата приложения**: hello пароль для создания hello PFX-файл.
  * **Идентификатор пароля приложения Cert**: hello пароля, аналогично toohow, они отправляют других ключей служб мультимедиа, необходимо передать. Используйте hello **ContentKeyType.FairPlayPfxPassword** hello tooget значение enum, службы мультимедиа по идентификатору. Это происходит, они должны toouse внутри hello параметр политики доставки ключей.
  * **iv** — случайное 16-байтовое значение. Он должен соответствовать hello iv в hello политики доставки активов. При создании hello вектора инициализации и поместить его в обоих местах: hello политики доставки активов и параметр политики доставки ключей hello.
  * **ПОПРОСИТЕ**: при создании hello сертификации с помощью портала разработчиков Apple hello получения этого ключа. Каждая группа разработчиков получает свой, уникальный ASK. Сохранить копию hello ПОПРОСИТЕ и сохраните ее в надежном месте. Понадобится tooconfigure ПОПРОСИТЕ как FairPlayAsk tooMedia службы позже.
  * **Идентификатор ASK** — этот идентификатор будет получен при отправке ASK в службы мультимедиа. ПОПРОСИТЕ необходимо передать с помощью hello **ContentKeyType.FairPlayAsk** значение перечисления. Результат hello возвращается hello идентификатор служб мультимедиа, а это, следует использовать при задании параметра политики доставки ключей hello.

Hello следующее должно быть задано при hello кадров в Секунду на стороне клиента:

  * **Приложение Cert (AC)**: это.cer/.der файл, содержащий открытый ключ hello, какая операционная система hello использует tooencrypt некоторые полезные данные. Службы мультимедиа должно tooknow о нем, так как она затребована проигрывателя hello. Служба доставки ключей Hello расшифровывает его с помощью соответствующего закрытого ключа hello.

tooplay резервное зашифрованный поток FairPlay, получать реальные ОБРАТИТЕСЬ в первую очередь, а затем создать реальный сертификат. В результате этого процесса создаются три элемента:

  * DER-файл;
  * PFX-файл;
  * пароль для PFX-файл hello

Hello следующие клиенты поддерживают HLS с **CBC AES-128** шифрования: Safari на iOS, OS X, Apple TV.

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a>Настройка общего динамического шифрования FairPlay и службы доставки лицензий
Hello ниже приведены общие шаги для защиты активов с FairPlay с помощью службы доставки лицензий Media Services hello, а также с помощью динамического шифрования.

1. Создание актива и отправка файлов в актив hello.
2. Кодирование активов hello, содержащий hello файл toohello с адаптивной скоростью набор MP4.
3. Создание ключа контента и связать его с активом hello в кодировке.  
4. Настройка политики авторизации hello ключа содержимого. Укажите hello ниже:

   * способ доставки Hello (в данном случае FairPlay).
   * Конфигурация параметров политики FairPlay. Дополнительные сведения о том, как tooconfigure FairPlay, в разделе hello **ConfigureFairPlayPolicyOptions()** метод в следующем примере hello.

     > [!NOTE]
     > Как правило вам бы хотелось tooconfigure FairPlay политики параметры только один раз, у вас будет только один набор сертификации и ASK.
     >
     >
   * Ограничения (открытая авторизация или с помощью маркера).
   * Тип доставки ключей сведения о конкретных toohello, определяющий способ доставки ключа hello toohello клиента.
5. Настройка политики доставки активов hello. Конфигурация политики доставки Hello включает:

   * протокол доставки Hello (HLS).
   * тип динамического шифрования (общее шифрование CBC) Hello.
   * Hello приобретения URL-адрес лицензии.

     > [!NOTE]
     > Если вы хотите toodeliver поток, который зашифрован FairPlay и другой системой управления цифровыми правами (DRM), у вас есть tooconfigure доставки отдельные политики:
     >
     > * Один tooconfigure IAssetDeliveryPolicy динамической адаптивной потоковой передачи по HTTP (дефис) с помощью Common Encryption (CENC) (PlayReady + Widevine), а также Smooth с помощью PlayReady
     > * Другой IAssetDeliveryPolicy tooconfigure FairPlay для HLS
     >
     >
6. Создание указателя OnDemand tooget URL-адрес потоковой передачи.

## <a name="use-fairplay-key-delivery-by-player-apps"></a>Использование доставки ключей FairPlay приложениями проигрывателей
Можно разрабатывать приложения проигрывателя с помощью hello iOS SDK. toobe может tooplay FairPlay содержимое, у вас есть лицензии exchange tooimplement hello протокола. Этот протокол не указывается компанией Apple. Он работает приложение tooeach способ доставки ключей toosend запросов. Служба доставки ключей Media Services FairPlay Hello ожидает hello SPC toocome в сообщении кодировке post www-form-url, hello следующие формы:

    spc=<Base64 encoded SPC>

> [!NOTE]
> Azure Media Player не поддерживает воспроизведение FairPlay стандартной hello. Воспроизведение FairPlay tooget на MAC OS X, получить образец hello проигрывателя hello учетную запись разработчика Apple.
>
>

## <a name="streaming-urls"></a>URL-адреса потоковой передачи
Если актива был зашифрован с более чем одной DRM, следует использовать тег шифрования в URL-адрес потоковой передачи hello: (format = «m3u8-aapl» шифрования = 'xxx').

применить Hello следующие вопросы:

* Можно указать только один тип шифрования или ни одного.
* Тип шифрования Hello не toobe, указанный в URL-адрес hello, если только один шифрования был применен toohello активов.
* Тип шифрования Hello без учета регистра.
* можно указать следующие типы шифрования Hello.  
  * **cenc** — общее шифрование (Playready или Widevine);
  * **cbcs-aapl** — Fairplay;
  * **cbc** — шифрование конверта AES.

## <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

1. Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 
2. Добавьте следующие элементы слишком hello**appSettings** определенной в файле app.config:

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a>Пример

Следующий образец Hello демонстрирует возможности hello toouse toodeliver служб мультимедиа зашифрован FairPlay содержимого. Эта возможность появилась в hello Azure Media Services SDK для .NET версии 3.6.0. 

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
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a>Дальнейшие действия: схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
