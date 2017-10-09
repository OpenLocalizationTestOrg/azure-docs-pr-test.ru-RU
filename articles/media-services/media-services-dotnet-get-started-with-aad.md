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
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="8d4d0-103">Использование проверки подлинности Azure AD tooaccess API служб мультимедиа Azure в .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8d4d0-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="8d4d0-104">Начиная с windowsazure.mediaservices 4.0.0.4, службы мультимедиа Azure поддерживают аутентификацию на основе Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8d4d0-105">В этом разделе показано, как toouse tooaccess проверки подлинности Azure AD API служб мультимедиа Azure с помощью Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d4d0-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8d4d0-106">Prerequisites</span></span>

- <span data-ttu-id="8d4d0-107">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-107">An Azure account.</span></span> <span data-ttu-id="8d4d0-108">Дополнительные сведения см. на странице с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="8d4d0-109">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-109">A Media Services account.</span></span> <span data-ttu-id="8d4d0-110">Дополнительные сведения см. в разделе [создать учетную запись служб мультимедиа Azure с помощью портала Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="8d4d0-111">Здравствуйте, последняя версия [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) пакета.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="8d4d0-112">Знакомство с разделом hello [доступ к Azure API служб мультимедиа с обзор проверки подлинности AAD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="8d4d0-113">Процесс аутентификации Azure AD в службах мультимедиа Azure можно выполнить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="8d4d0-114">**Проверка подлинности пользователя** проверяет подлинность пользователя, работающего с toointeract приложения hello с ресурсами Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="8d4d0-115">интерактивные приложения Hello должен сначала запросить учетные данные пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="8d4d0-116">Например, управления консольное приложение, которое используется заданий кодирования toomonitor авторизованных пользователей или динамической потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="8d4d0-117">**Аутентификация субъекта-службы** позволяет проверить подлинность службы.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="8d4d0-118">Этот метод аутентификации обычно используют приложения, которые выполняют службы управляющей программы, службы среднего уровня или запланированные задания, например веб-приложения, приложения-функции, приложения логики, интерфейсы API или микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8d4d0-119">Службы мультимедиа Azure в настоящее время поддерживают модель аутентификации с помощью службы контроля доступа Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="8d4d0-120">Тем не менее управление доступом авторизации будет toobe в 1 июня 2018 устаревшей.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="8d4d0-121">Рекомендуется как можно быстрее перейти tooan модель проверки подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="8d4d0-122">Получение маркера доступа Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d4d0-122">Get an Azure AD access token</span></span>

<span data-ttu-id="8d4d0-123">tooconnect toohello API служб мультимедиа Azure с проверкой подлинности Azure AD, клиентское приложение hello должен toorequest маркера доступа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="8d4d0-124">При использовании клиента hello Media Services .NET SDK, многие детали hello о оболочку tooacquire маркера доступа Azure AD и упрощены для вас в hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) и [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) классы.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="8d4d0-125">Например, нет необходимости использовать центр tooprovide hello Azure AD, URI ресурса служб мультимедиа или собственный подробные сведения о приложении Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="8d4d0-126">Это хорошо известного значения, которые уже настроены hello класс поставщика маркера доступа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="8d4d0-127">Если вы не используете пакет SDK .NET служб мультимедиа Azure, мы рекомендуем использовать hello [библиотеки аутентификации Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="8d4d0-128">tooget значения для параметров hello, необходимость toouse с библиотеки аутентификации Azure AD, в разделе [использовать параметры проверки подлинности Azure tooaccess портала Azure AD hello](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="8d4d0-129">Также имеется возможность замены реализация по умолчанию hello hello hello **AzureAdTokenProvider** собственной реализацией.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="8d4d0-130">Установка и настройка пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="8d4d0-131">проверки подлинности toouse Azure AD с hello Media Services .NET SDK, необходимо toohave hello последней [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) пакета.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="8d4d0-132">Кроме того, добавьте toohello ссылки **Microsoft.IdentityModel.Clients.ActiveDirectory** сборки.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="8d4d0-133">При использовании существующего приложения включают hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** сборки.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="8d4d0-134">Создайте в Visual Studio новое консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="8d4d0-135">Используйте hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall пакета NuGet **Azure Media Services .NET SDK**.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="8d4d0-136">tooadd ссылки с помощью NuGet, иметь hello следующие шаги: в **обозревателе решений**, щелкните правой кнопкой мыши имя проекта hello и выберите **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="8d4d0-137">Затем найдите **windowsazure.mediaservices** и щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="8d4d0-138">-или-</span><span class="sxs-lookup"><span data-stu-id="8d4d0-138">-or-</span></span>

    <span data-ttu-id="8d4d0-139">Выполнения hello следующую команду в **консоль диспетчера пакетов** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="8d4d0-140">Добавить **с помощью** tooyour исходного кода.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="8d4d0-141">Использование аутентификации пользователя</span><span class="sxs-lookup"><span data-stu-id="8d4d0-141">Use user authentication</span></span>

<span data-ttu-id="8d4d0-142">tooconnect toohello API служб мультимедиа Azure с проверкой подлинности пользователя hello, клиентское приложение hello должен toorequest hello маркера Azure AD с помощью следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="8d4d0-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="8d4d0-143">Конечная точка клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="8d4d0-144">сведения о клиенте Hello можно получить из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="8d4d0-145">Наведите указатель мыши hello пользователя, выполнившего вход в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="8d4d0-146">Универсальный код ресурса (URI) для ресурса служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-146">Media Services resource URI.</span></span>
- <span data-ttu-id="8d4d0-147">Идентификатор клиента (собственного) приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="8d4d0-148">Универсальный код ресурса (URI) перенаправления (собственного) приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="8d4d0-149">Hello значения для этих параметров можно найти в **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="8d4d0-150">Hello **AzureEnvironments.AzureCloudEnvironment** константы — это помощник в tooget .NET SDK hello hello параметров переменных среды вправо для открытого центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="8d4d0-151">Он содержит предопределенные переменные окружения для доступа к службам мультимедиа в hello открытые данные только для центров обработки.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="8d4d0-152">Для независимых облачных регионов или облачных регионов для государственных организаций можно использовать **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** или **AzureGermanCloudEnvironment** соответственно.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="8d4d0-153">Следующий пример кода Hello создает токен:</span><span class="sxs-lookup"><span data-stu-id="8d4d0-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="8d4d0-154">toostart программировании служб мультимедиа, необходимо toocreate **CloudMediaContext** экземпляр, представляющий контекст сервера hello.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="8d4d0-155">Hello **CloudMediaContext** содержит ссылки на коллекции tooimportant, включая задания, активы, файлы, политики доступа и указатели.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="8d4d0-156">Необходимо также toopass hello **ресурса (URI) для REST служб мультимедиа** toohello **CloudMediaContext** конструктор.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="8d4d0-157">tooget hello ресурса (URI) REST служб мультимедиа, вход toohello портал Azure, выберите учетную запись служб мультимедиа Azure, рекомендуется выбрать **доступ к API**и выберите **подключения служб мультимедиа tooAzure с пользователем Проверка подлинности**.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="8d4d0-158">Hello следующий пример кода создает **CloudMediaContext** экземпляр:</span><span class="sxs-lookup"><span data-stu-id="8d4d0-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="8d4d0-159">Hello в следующем примере показано, как toocreate hello Azure AD токен и hello контекст.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

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
><span data-ttu-id="8d4d0-160">Если возникнет исключение, сообщающее «hello удаленный сервер вернул ошибку: проверки подлинности (401), «hello. в разделе [управления доступом к](media-services-use-aad-auth-to-access-ams-api.md#access-control) часть доступа к API служб мультимедиа Azure с обзор проверки подлинности Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="8d4d0-161">Использование аутентификации субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="8d4d0-161">Use service principal authentication</span></span>
    
<span data-ttu-id="8d4d0-162">tooconnect toohello API служб мультимедиа Azure с основной параметр hello службы, приложения среднего уровня (веб-API или веб-приложение) должен toorequests маркера Azure AD hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="8d4d0-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="8d4d0-163">Конечная точка клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="8d4d0-164">сведения о клиенте Hello можно получить из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="8d4d0-165">Наведите указатель мыши hello пользователя, выполнившего вход в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="8d4d0-166">Универсальный код ресурса (URI) для ресурса служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-166">Media Services resource URI.</span></span>
- <span data-ttu-id="8d4d0-167">Значения приложения Azure AD: hello **идентификатор клиента** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="8d4d0-168">Здравствуйте, значения для hello **идентификатор клиента** и **секрет клиента** параметры можно найти в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="8d4d0-169">Дополнительные сведения см. в разделе [Приступая к работе с Azure AD с помощью проверки подлинности hello портал Azure](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="8d4d0-170">Hello следующий пример кода создает токен с помощью hello **AzureAdTokenCredentials** конструктор, принимающий **AzureAdClientSymmetricKey** как параметр:</span><span class="sxs-lookup"><span data-stu-id="8d4d0-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="8d4d0-171">Можно также указать hello **AzureAdTokenCredentials** конструктор, принимающий **AzureAdClientCertificate** как параметр.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="8d4d0-172">Инструкции о том, как toocreate и настроить сертификат в форме, которая может использоваться с Azure AD см. в разделе [tooAzure AD в приложениях управляющей программы с сертификатами - ручную настройку проверки подлинности](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="8d4d0-173">toostart программировании служб мультимедиа, необходимо toocreate **CloudMediaContext** экземпляр, представляющий контекст сервера hello.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="8d4d0-174">Необходимо также toopass hello **ресурса (URI) для REST служб мультимедиа** toohello **CloudMediaContext** конструктор.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="8d4d0-175">Вы можете получить hello **ресурса (URI) для REST служб мультимедиа** значение из hello также портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="8d4d0-176">Hello следующий пример кода создает **CloudMediaContext** экземпляр:</span><span class="sxs-lookup"><span data-stu-id="8d4d0-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="8d4d0-177">Hello в следующем примере показано, как toocreate hello Azure AD токен и hello контекст.</span><span class="sxs-lookup"><span data-stu-id="8d4d0-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8d4d0-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d4d0-178">Next steps</span></span>

<span data-ttu-id="8d4d0-179">Приступая к работе с [передача файлов учетная запись tooyour](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="8d4d0-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
