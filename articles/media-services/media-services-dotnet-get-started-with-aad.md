---
title: "aaaUse tooaccess проверки подлинности Azure AD API служб мультимедиа Azure с помощью .NET | Документы Microsoft"
description: "В этом разделе показано, как toouse tooaccess проверки подлинности Azure Active Directory (Azure AD) служб мультимедиа Azure (AMS) API в .NET Framework."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>Использование проверки подлинности Azure AD tooaccess API служб мультимедиа Azure в .NET Framework

Начиная с windowsazure.mediaservices 4.0.0.4, службы мультимедиа Azure поддерживают аутентификацию на основе Azure Active Directory (Azure AD). В этом разделе показано, как toouse tooaccess проверки подлинности Azure AD API служб мультимедиа Azure с помощью Microsoft .NET.

## <a name="prerequisites"></a>Предварительные требования

- Учетная запись Azure. Дополнительные сведения см. на странице с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Учетная запись служб мультимедиа. Дополнительные сведения см. в разделе [создать учетную запись служб мультимедиа Azure с помощью портала Azure hello](media-services-portal-create-account.md).
- Здравствуйте, последняя версия [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) пакета.
- Знакомство с разделом hello [доступ к Azure API служб мультимедиа с обзор проверки подлинности AAD](media-services-use-aad-auth-to-access-ams-api.md). 

Процесс аутентификации Azure AD в службах мультимедиа Azure можно выполнить двумя способами.

- **Проверка подлинности пользователя** проверяет подлинность пользователя, работающего с toointeract приложения hello с ресурсами Azure Media Services. интерактивные приложения Hello должен сначала запросить учетные данные пользователя hello. Например, управления консольное приложение, которое используется заданий кодирования toomonitor авторизованных пользователей или динамической потоковой передачи. 
- **Аутентификация субъекта-службы** позволяет проверить подлинность службы. Этот метод аутентификации обычно используют приложения, которые выполняют службы управляющей программы, службы среднего уровня или запланированные задания, например веб-приложения, приложения-функции, приложения логики, интерфейсы API или микрослужбы.

>[!IMPORTANT]
>Службы мультимедиа Azure в настоящее время поддерживают модель аутентификации с помощью службы контроля доступа Azure. Тем не менее управление доступом авторизации будет toobe в 1 июня 2018 устаревшей. Рекомендуется как можно быстрее перейти tooan модель проверки подлинности Azure Active Directory.

## <a name="get-an-azure-ad-access-token"></a>Получение маркера доступа Azure AD

tooconnect toohello API служб мультимедиа Azure с проверкой подлинности Azure AD, клиентское приложение hello должен toorequest маркера доступа Azure AD. При использовании клиента hello Media Services .NET SDK, многие детали hello о оболочку tooacquire маркера доступа Azure AD и упрощены для вас в hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) и [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) классы. 

Например, нет необходимости использовать центр tooprovide hello Azure AD, URI ресурса служб мультимедиа или собственный подробные сведения о приложении Azure AD. Это хорошо известного значения, которые уже настроены hello класс поставщика маркера доступа Azure AD. 

Если вы не используете пакет SDK .NET служб мультимедиа Azure, мы рекомендуем использовать hello [библиотеки аутентификации Azure AD](../active-directory/develop/active-directory-authentication-libraries.md). tooget значения для параметров hello, необходимость toouse с библиотеки аутентификации Azure AD, в разделе [использовать параметры проверки подлинности Azure tooaccess портала Azure AD hello](media-services-portal-get-started-with-aad.md).

Также имеется возможность замены реализация по умолчанию hello hello hello **AzureAdTokenProvider** собственной реализацией.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Установка и настройка пакета SDK служб мультимедиа для .NET.

>[!NOTE] 
>проверки подлинности toouse Azure AD с hello Media Services .NET SDK, необходимо toohave hello последней [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) пакета. Кроме того, добавьте toohello ссылки **Microsoft.IdentityModel.Clients.ActiveDirectory** сборки. При использовании существующего приложения включают hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** сборки. 

1. Создайте в Visual Studio новое консольное приложение C#.
2. Используйте hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall пакета NuGet **Azure Media Services .NET SDK**. 

    tooadd ссылки с помощью NuGet, иметь hello следующие шаги: в **обозревателе решений**, щелкните правой кнопкой мыши имя проекта hello и выберите **управление пакетами NuGet**. Затем найдите **windowsazure.mediaservices** и щелкните **Установить**.
    
    -или-

    Выполнения hello следующую команду в **консоль диспетчера пакетов** в Visual Studio.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. Добавить **с помощью** tooyour исходного кода.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>Использование аутентификации пользователя

tooconnect toohello API служб мультимедиа Azure с проверкой подлинности пользователя hello, клиентское приложение hello должен toorequest hello маркера Azure AD с помощью следующих параметров:  

- Конечная точка клиента Azure AD. сведения о клиенте Hello можно получить из hello портал Azure. Наведите указатель мыши hello пользователя, выполнившего вход в правом верхнем углу hello.
- Универсальный код ресурса (URI) для ресурса служб мультимедиа.
- Идентификатор клиента (собственного) приложения служб мультимедиа. 
- Универсальный код ресурса (URI) перенаправления (собственного) приложения служб мультимедиа. 

Hello значения для этих параметров можно найти в **AzureEnvironments.AzureCloudEnvironment**. Hello **AzureEnvironments.AzureCloudEnvironment** константы — это помощник в tooget .NET SDK hello hello параметров переменных среды вправо для открытого центр обработки данных Azure. 

Он содержит предопределенные переменные окружения для доступа к службам мультимедиа в hello открытые данные только для центров обработки. Для независимых облачных регионов или облачных регионов для государственных организаций можно использовать **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** или **AzureGermanCloudEnvironment** соответственно.

Следующий пример кода Hello создает токен:
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart программировании служб мультимедиа, необходимо toocreate **CloudMediaContext** экземпляр, представляющий контекст сервера hello. Hello **CloudMediaContext** содержит ссылки на коллекции tooimportant, включая задания, активы, файлы, политики доступа и указатели. 

Необходимо также toopass hello **ресурса (URI) для REST служб мультимедиа** toohello **CloudMediaContext** конструктор. tooget hello ресурса (URI) REST служб мультимедиа, вход toohello портал Azure, выберите учетную запись служб мультимедиа Azure, рекомендуется выбрать **доступ к API**и выберите **подключения служб мультимедиа tooAzure с пользователем Проверка подлинности**. 

Hello следующий пример кода создает **CloudMediaContext** экземпляр:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

Hello в следующем примере показано, как toocreate hello Azure AD токен и hello контекст.

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>Если возникнет исключение, сообщающее «hello удаленный сервер вернул ошибку: проверки подлинности (401), «hello. в разделе [управления доступом к](media-services-use-aad-auth-to-access-ams-api.md#access-control) часть доступа к API служб мультимедиа Azure с обзор проверки подлинности Azure AD.

## <a name="use-service-principal-authentication"></a>Использование аутентификации субъекта-службы
    
tooconnect toohello API служб мультимедиа Azure с основной параметр hello службы, приложения среднего уровня (веб-API или веб-приложение) должен toorequests маркера Azure AD hello следующие параметры:  

- Конечная точка клиента Azure AD. сведения о клиенте Hello можно получить из hello портал Azure. Наведите указатель мыши hello пользователя, выполнившего вход в правом верхнем углу hello.
- Универсальный код ресурса (URI) для ресурса служб мультимедиа.
- Значения приложения Azure AD: hello **идентификатор клиента** и **секрет клиента**.

Здравствуйте, значения для hello **идентификатор клиента** и **секрет клиента** параметры можно найти в hello портал Azure. Дополнительные сведения см. в разделе [Приступая к работе с Azure AD с помощью проверки подлинности hello портал Azure](media-services-portal-get-started-with-aad.md).

Hello следующий пример кода создает токен с помощью hello **AzureAdTokenCredentials** конструктор, принимающий **AzureAdClientSymmetricKey** как параметр: 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

Можно также указать hello **AzureAdTokenCredentials** конструктор, принимающий **AzureAdClientCertificate** как параметр. 

Инструкции о том, как toocreate и настроить сертификат в форме, которая может использоваться с Azure AD см. в разделе [tooAzure AD в приложениях управляющей программы с сертификатами - ручную настройку проверки подлинности](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart программировании служб мультимедиа, необходимо toocreate **CloudMediaContext** экземпляр, представляющий контекст сервера hello. Необходимо также toopass hello **ресурса (URI) для REST служб мультимедиа** toohello **CloudMediaContext** конструктор. Вы можете получить hello **ресурса (URI) для REST служб мультимедиа** значение из hello также портал Azure.

Hello следующий пример кода создает **CloudMediaContext** экземпляр:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
Hello в следующем примере показано, как toocreate hello Azure AD токен и hello контекст.

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>Дальнейшие действия

Приступая к работе с [передача файлов учетная запись tooyour](media-services-dotnet-upload-files.md).
