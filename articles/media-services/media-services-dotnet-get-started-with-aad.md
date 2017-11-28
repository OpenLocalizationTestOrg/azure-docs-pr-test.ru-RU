---
title: "Использование аутентификации Azure AD для доступа к API служб мультимедиа Azure с помощью .NET | Документация Майкрософт"
description: "В этом разделе показано, как использовать аутентификацию Azure Active Directory (Azure AD) для доступа к API служб мультимедиа Azure (AMS) с помощью .NET."
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
ms.openlocfilehash: a9355200a05a3aa1b494b76977d38ddc42bfe179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-ad-authentication-to-access-azure-media-services-api-with-net"></a><span data-ttu-id="70c2b-103">Использование аутентификации Azure AD для доступа к API служб мультимедиа Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="70c2b-103">Use Azure AD authentication to access Azure Media Services API with .NET</span></span>

<span data-ttu-id="70c2b-104">Начиная с windowsazure.mediaservices 4.0.0.4, службы мультимедиа Azure поддерживают аутентификацию на основе Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70c2b-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="70c2b-105">В этом разделе показано, как использовать аутентификацию Azure AD для доступа к API служб мультимедиа Azure (AMS) с помощью Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="70c2b-105">This topic shows you how to use Azure AD  authentication to access Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70c2b-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="70c2b-106">Prerequisites</span></span>

- <span data-ttu-id="70c2b-107">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="70c2b-107">An Azure account.</span></span> <span data-ttu-id="70c2b-108">Дополнительные сведения см. на странице с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70c2b-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="70c2b-109">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="70c2b-109">A Media Services account.</span></span> <span data-ttu-id="70c2b-110">Дополнительные сведения см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="70c2b-110">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="70c2b-111">Последняя версия пакета [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices).</span><span class="sxs-lookup"><span data-stu-id="70c2b-111">The latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="70c2b-112">Ознакомление с разделом [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="70c2b-112">Familiarity with the topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="70c2b-113">Процесс аутентификации Azure AD в службах мультимедиа Azure можно выполнить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="70c2b-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="70c2b-114">**Аутентификация пользователя** позволяет проверить подлинность пользователя, который использует приложение для взаимодействия с ресурсами служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="70c2b-114">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span></span> <span data-ttu-id="70c2b-115">Интерактивное приложение должно сначала запросить у пользователя учетные данные.</span><span class="sxs-lookup"><span data-stu-id="70c2b-115">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="70c2b-116">Примером может послужить приложение консоли управления, которое используется авторизованными пользователями для мониторинга заданий кодирования или потоковой трансляции.</span><span class="sxs-lookup"><span data-stu-id="70c2b-116">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="70c2b-117">**Аутентификация субъекта-службы** позволяет проверить подлинность службы.</span><span class="sxs-lookup"><span data-stu-id="70c2b-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="70c2b-118">Этот метод аутентификации обычно используют приложения, которые выполняют службы управляющей программы, службы среднего уровня или запланированные задания, например веб-приложения, приложения-функции, приложения логики, интерфейсы API или микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="70c2b-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="70c2b-119">Службы мультимедиа Azure в настоящее время поддерживают модель аутентификации с помощью службы контроля доступа Azure.</span><span class="sxs-lookup"><span data-stu-id="70c2b-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="70c2b-120">Тем не менее авторизация посредством службы контроля доступа будет объявлена устаревшей 1 июня 2018 года.</span><span class="sxs-lookup"><span data-stu-id="70c2b-120">However, Access Control authorization is going to be deprecated on June 1, 2018.</span></span> <span data-ttu-id="70c2b-121">Мы рекомендуем как можно быстрее перейти на использование модели аутентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70c2b-121">We recommend that you migrate to an Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="70c2b-122">Получение маркера доступа Azure AD</span><span class="sxs-lookup"><span data-stu-id="70c2b-122">Get an Azure AD access token</span></span>

<span data-ttu-id="70c2b-123">Чтобы подключиться к API служб мультимедиа Azure, используя аутентификацию Azure AD, клиентскому приложению необходимо запросить маркер доступа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70c2b-123">To connect to the Azure Media Services API with Azure AD authentication, the client app needs to request an Azure AD access token.</span></span> <span data-ttu-id="70c2b-124">При использовании клиентского пакета SDK служб мультимедиа для .NET многие сведения о том, как получить маркер доступа Azure AD, упакованы в упрощенном виде в классы [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) и [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs).</span><span class="sxs-lookup"><span data-stu-id="70c2b-124">When you use the Media Services .NET client SDK, many of the details about how to acquire an Azure AD access token are wrapped and simplified for you in the [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="70c2b-125">Например, не требуется указывать центр Azure AD, универсальный код ресурса (URI) для ресурса служб мультимедиа или сведения о собственном приложении Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70c2b-125">For example, you don't need to provide the Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="70c2b-126">Это хорошо известные значения, которые уже настроены с помощью класса поставщика маркеров доступа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70c2b-126">These are well-known values that are already configured by the Azure AD access token provider class.</span></span> 

<span data-ttu-id="70c2b-127">Если вы не используете пакет SDK служб мультимедиа Azure для .NET, мы рекомендуем использовать [библиотеки аутентификации Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="70c2b-127">If you are not using Azure Media Service .NET SDK, we recommend that you use the [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="70c2b-128">Чтобы получить значения параметров, необходимых для использования библиотеки аутентификации Azure AD, ознакомьтесь с разделом [Приступая к работе с аутентификацией Azure AD с помощью портала Azure](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="70c2b-128">To get values for the parameters that you need to use with Azure AD Authentication Library, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="70c2b-129">Кроме того, вы можете заменить реализацию по умолчанию **AzureAdTokenProvider** собственной реализацией.</span><span class="sxs-lookup"><span data-stu-id="70c2b-129">You also have the option of replacing the default implementation of the **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="70c2b-130">Установка и настройка пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="70c2b-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="70c2b-131">Для использования аутентификации Azure AD с помощью пакета SDK служб мультимедиа для .NET необходима последняя версия пакета [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices).</span><span class="sxs-lookup"><span data-stu-id="70c2b-131">To use Azure AD authentication with the Media Services .NET SDK, you need to have the latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="70c2b-132">Кроме того, добавьте ссылку на сборку **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-132">Also, add a reference to the **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="70c2b-133">При использовании существующего приложения следует добавить сборку **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-133">If you are using an existing app, include the **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="70c2b-134">Создайте в Visual Studio новое консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="70c2b-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="70c2b-135">Используйте пакет Nuget [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices), чтобы установить **пакет SDK служб мультимедиа Azure для .NET**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-135">Use the [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package to install **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="70c2b-136">Чтобы добавить ссылки с помощью пакета NuGet, сделайте следующее: в **обозревателе решений** щелкните правой кнопкой мыши имя проекта и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-136">To add references by using NuGet, take the following steps: in **Solution Explorer**, right-click the project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="70c2b-137">Затем найдите **windowsazure.mediaservices** и щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="70c2b-138">-или-</span><span class="sxs-lookup"><span data-stu-id="70c2b-138">-or-</span></span>

    <span data-ttu-id="70c2b-139">В **консоли диспетчера пакетов** Visual Studio выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="70c2b-139">Run the following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="70c2b-140">Добавьте инструкцию **using** в исходный код.</span><span class="sxs-lookup"><span data-stu-id="70c2b-140">Add **using** to your source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="70c2b-141">Использование аутентификации пользователя</span><span class="sxs-lookup"><span data-stu-id="70c2b-141">Use user authentication</span></span>

<span data-ttu-id="70c2b-142">Для подключения к API служб мультимедиа Azure с помощью аутентификации пользователя клиентскому приложению требуется запросить маркер Azure AD со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="70c2b-142">To connect to the Azure Media Service API with the user authentication option, the client app needs to request an Azure AD token by using the following parameters:</span></span>  

- <span data-ttu-id="70c2b-143">Конечная точка клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70c2b-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="70c2b-144">Информацию о клиенте можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="70c2b-144">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="70c2b-145">Наведите указатель мыши на пользователя, выполнившего вход, в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="70c2b-145">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="70c2b-146">Универсальный код ресурса (URI) для ресурса служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="70c2b-146">Media Services resource URI.</span></span>
- <span data-ttu-id="70c2b-147">Идентификатор клиента (собственного) приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="70c2b-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="70c2b-148">Универсальный код ресурса (URI) перенаправления (собственного) приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="70c2b-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="70c2b-149">Значения этих параметров можно найти в **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-149">The values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="70c2b-150">Константа **AzureEnvironments.AzureCloudEnvironment** является константой вспомогательного класса в пакете SDK для .NET, которая используется для получения правильных параметров переменных среды для общедоступного центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="70c2b-150">The **AzureEnvironments.AzureCloudEnvironment** constant is a helper in the .NET SDK to get the right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="70c2b-151">Она содержит предопределенные параметры среды для доступа к службам мультимедиа только в общедоступных центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="70c2b-151">It contains pre-defined environment settings for accessing Media Services in the public data centers only.</span></span> <span data-ttu-id="70c2b-152">Для независимых облачных регионов или облачных регионов для государственных организаций можно использовать **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** или **AzureGermanCloudEnvironment** соответственно.</span><span class="sxs-lookup"><span data-stu-id="70c2b-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="70c2b-153">Приведенный ниже пример кода создает маркер.</span><span class="sxs-lookup"><span data-stu-id="70c2b-153">The following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="70c2b-154">Чтобы начать программирование для служб мультимедиа, необходимо создать экземпляр **CloudMediaContext**, представляющий контекст сервера.</span><span class="sxs-lookup"><span data-stu-id="70c2b-154">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="70c2b-155">**CloudMediaContext** содержит ссылки на важные коллекции, в том числе на задания, ресурсы, файлы, политики доступа и указатели.</span><span class="sxs-lookup"><span data-stu-id="70c2b-155">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="70c2b-156">Необходимо также передать **универсальный код ресурса (URI) для ресурса REST служб мультимедиа** в конструктор **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-156">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="70c2b-157">Чтобы получить универсальный код ресурса (URI) для ресурса REST служб мультимедиа, войдите на портал Azure, выберите учетную запись служб мультимедиа Azure, выберите **Доступ к API**, а затем щелкните **Подключение к API служб мультимедиа Azure с помощью проверки подлинности пользователя**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-157">To get the resource URI for Media REST Services, sign in to the Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect to Azure Media Services with user authentication**.</span></span> 

<span data-ttu-id="70c2b-158">Следующий пример кода создает экземпляр **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-158">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="70c2b-159">В следующем примере показано, как создать маркер Azure AD и контекст.</span><span class="sxs-lookup"><span data-stu-id="70c2b-159">The following example shows how to create the Azure AD token and the context:</span></span>

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
><span data-ttu-id="70c2b-160">Если возникнет исключение "Удаленный сервер возвратил ошибку: 401 - Не санкционировано", ознакомьтесь с разделом [Управление доступом](media-services-use-aad-auth-to-access-ams-api.md#access-control) обзора доступа к API служб мультимедиа Azure с помощью аутентификации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70c2b-160">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="70c2b-161">Использование аутентификации субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="70c2b-161">Use service principal authentication</span></span>
    
<span data-ttu-id="70c2b-162">Для подключения к API служб мультимедиа Azure в режиме аутентификации субъекта-службы приложению среднего уровня (веб-API или веб-приложению) требуется запросить маркер Azure AD со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="70c2b-162">To connect to the Azure Media Services API with the service principal option, your middle-tier app (web API or web application) needs to requests an Azure AD token with the following parameters:</span></span>  

- <span data-ttu-id="70c2b-163">Конечная точка клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70c2b-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="70c2b-164">Информацию о клиенте можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="70c2b-164">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="70c2b-165">Наведите указатель мыши на пользователя, выполнившего вход, в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="70c2b-165">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="70c2b-166">Универсальный код ресурса (URI) для ресурса служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="70c2b-166">Media Services resource URI.</span></span>
- <span data-ttu-id="70c2b-167">Значения приложения Azure AD: **идентификатор клиента** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-167">Azure AD application values: the **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="70c2b-168">Значения **идентификатора клиента** и **секрета клиента** можно найти на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="70c2b-168">The values for the **Client ID** and **Client secret** parameters can be found in the Azure portal.</span></span> <span data-ttu-id="70c2b-169">Дополнительные сведения см. в разделе [Приступая к работе с аутентификацией Azure AD с помощью портала Azure](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="70c2b-169">For more information, see [Getting started with Azure AD authentication using the Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="70c2b-170">Следующий пример кода создает маркер с помощью конструктора **AzureAdTokenCredentials**, принимающего **AzureAdClientSymmetricKey** как параметр.</span><span class="sxs-lookup"><span data-stu-id="70c2b-170">The following code example creates a token by using the **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="70c2b-171">Можно также указать конструктор **AzureAdTokenCredentials**, принимающий **AzureAdClientCertificate** как параметр.</span><span class="sxs-lookup"><span data-stu-id="70c2b-171">You can also specify the **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="70c2b-172">Инструкции по созданию и настройке сертификата в форме, которая может использоваться в Azure AD, см. в разделе [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md) (Ручная настройка аутентификации приложений управляющей программы в Azure AD с помощью сертификатов).</span><span class="sxs-lookup"><span data-stu-id="70c2b-172">For instructions about how to create and configure a certificate in a form that can be used by Azure AD, see [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="70c2b-173">Чтобы начать программирование для служб мультимедиа, необходимо создать экземпляр **CloudMediaContext**, представляющий контекст сервера.</span><span class="sxs-lookup"><span data-stu-id="70c2b-173">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="70c2b-174">Необходимо также передать **универсальный код ресурса (URI) для ресурса REST служб мультимедиа** в конструктор **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-174">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="70c2b-175">Значение **универсального кода ресурса (URI) для ресурса REST служб мультимедиа** можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="70c2b-175">You can get the **resource URI for Media REST Services** value from the Azure portal as well.</span></span>

<span data-ttu-id="70c2b-176">Следующий пример кода создает экземпляр **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="70c2b-176">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="70c2b-177">В следующем примере показано, как создать маркер Azure AD и контекст.</span><span class="sxs-lookup"><span data-stu-id="70c2b-177">The following example shows how to create the Azure AD token and the context:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="70c2b-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70c2b-178">Next steps</span></span>

<span data-ttu-id="70c2b-179">Приступите к [передаче файлов в учетную запись](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="70c2b-179">Get started with [uploading files to your account](media-services-dotnet-upload-files.md).</span></span>
