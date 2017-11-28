---
title: "aaaAuthenticate с API REST для Mobile Engagement"
description: "Описывает способ tooauthenticate с API REST Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="45c66-103">Аутентификация с помощью интерфейсов REST API Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="45c66-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="45c66-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="45c66-104">Overview</span></span>
<span data-ttu-id="45c66-105">В этом документе описывается, как tooget допустимым Oauth AAD токен tooauthenticate с hello API-интерфейс REST Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="45c66-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="45c66-106">Предполагается, что у вас есть действующая подписка Azure и вы создали приложение Служб мобильного взаимодействия, используя одно из наших [руководств для разработчиков](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="45c66-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="45c66-107">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="45c66-107">Authentication</span></span>
<span data-ttu-id="45c66-108">Для проверки подлинности необходимо использовать маркер OAuth на основе Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45c66-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="45c66-109">Запрос заказа tooauthentication API заголовок авторизации должны быть добавлены tooevery запрос, который имеет hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="45c66-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="45c66-110">Срок действия токенов Azure Active Directory — 1 час.</span><span class="sxs-lookup"><span data-stu-id="45c66-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="45c66-111">Существует несколько способов tooget маркер.</span><span class="sxs-lookup"><span data-stu-id="45c66-111">There are several ways tooget a token.</span></span> <span data-ttu-id="45c66-112">С момента hello API-интерфейсы обычно вызываются из облачной службы требуется toouse ключ API.</span><span class="sxs-lookup"><span data-stu-id="45c66-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="45c66-113">Ключ API в Azure — это пароль субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="45c66-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="45c66-114">Hello следующая процедура описывает один из способов toosetting его настройка вручную.</span><span class="sxs-lookup"><span data-stu-id="45c66-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="45c66-115">Однократная настройка (с использованием сценария)</span><span class="sxs-lookup"><span data-stu-id="45c66-115">One-time setup (using script)</span></span>
<span data-ttu-id="45c66-116">Необходимо следовать hello набор инструкций ниже tooperform hello установки с помощью сценария PowerShell, который принимает hello минимальное время для программы установки, но использует hello наиболее допустимые значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="45c66-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="45c66-117">При необходимости можно также выполнить hello инструкциям hello [ручная установка](mobile-engagement-api-authentication-manual.md) для этого hello непосредственно портал Azure и настройку точно.</span><span class="sxs-lookup"><span data-stu-id="45c66-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="45c66-118">Получить последнюю версию Azure PowerShell из hello [здесь](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="45c66-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="45c66-119">Дополнительные сведения о инструкции по загрузке hello вы увидите это [ссылку](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45c66-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="45c66-120">После установки Azure PowerShell, используйте hello следующими командами наличие hello tooensure **модуль Azure** установлены:</span><span class="sxs-lookup"><span data-stu-id="45c66-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="45c66-121">а.</span><span class="sxs-lookup"><span data-stu-id="45c66-121">a.</span></span> <span data-ttu-id="45c66-122">Убедитесь, что hello модуля Azure PowerShell доступна в список доступных модулей hello.</span><span class="sxs-lookup"><span data-stu-id="45c66-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Доступные модули Azure][1]
   
    <span data-ttu-id="45c66-124">b.</span><span class="sxs-lookup"><span data-stu-id="45c66-124">b.</span></span> <span data-ttu-id="45c66-125">Если не удается найти модуль Azure PowerShell hello в hello над списком необходимо toorun hello следующее:</span><span class="sxs-lookup"><span data-stu-id="45c66-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="45c66-126">Здравствуйте, toohello входа диспетчера ресурсов Azure из PowerShell, выполнив следующую команду и имя пользователя и пароль для учетной записи Azure:</span><span class="sxs-lookup"><span data-stu-id="45c66-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="45c66-127">Если у вас несколько подписок необходимо запускать следующую hello.</span><span class="sxs-lookup"><span data-stu-id="45c66-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="45c66-128">а.</span><span class="sxs-lookup"><span data-stu-id="45c66-128">a.</span></span> <span data-ttu-id="45c66-129">Получение списка всех подписок и копирования hello SubscriptionId hello подписки, которые нужно toouse.</span><span class="sxs-lookup"><span data-stu-id="45c66-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="45c66-130">Убедитесь, что эта подписка hello того же, имеющая hello Mobile Engagement приложения, которое будет toointeract с помощью hello API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="45c66-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="45c66-131">b.</span><span class="sxs-lookup"><span data-stu-id="45c66-131">b.</span></span> <span data-ttu-id="45c66-132">Выполнения hello следующая команда обеспечивает hello SubscriptionId tooconfigure hello подписки toobe используется.</span><span class="sxs-lookup"><span data-stu-id="45c66-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="45c66-133">Скопируйте текст hello для hello [New AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) сценариев tooyour локального компьютера и сохранить его как командлет PowerShell (например `APIAuth.ps1`) и выполните его `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="45c66-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="45c66-134">Hello скрипт запросит tooprovide во входных данных для **principalName**.</span><span class="sxs-lookup"><span data-stu-id="45c66-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="45c66-135">Укажите подходящее имя должно toouse toocreate приложение Active Directory (например APIAuth).</span><span class="sxs-lookup"><span data-stu-id="45c66-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="45c66-136">После завершения скрипта hello, будут показаны следующие четыре значения, которые потребуются hello tooauthenticate программными средствами с помощью AD, поэтому следует убедиться, что toocopy их.</span><span class="sxs-lookup"><span data-stu-id="45c66-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="45c66-137">**TenantId**, **SubscriptionId**, **ApplicationId** и **Secret**.</span><span class="sxs-lookup"><span data-stu-id="45c66-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="45c66-138">Вы будете использовать TenantId в качестве `{TENANT_ID}`, ApplicationId — в качестве `{CLIENT_ID}`, а секрет — в качестве `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="45c66-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="45c66-139">Политика безопасности по умолчанию может блокировать выполнение сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45c66-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="45c66-140">В этом случае временно настройте выполнение сценария выполнения политики tooallow с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="45c66-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="45c66-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="45c66-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="45c66-142">Ниже показано, как hello набор командлетов PS выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="45c66-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="45c66-143">Проверьте на портале управления Azure hello новое приложение AD создания с именем hello при условии вызов сценария toohello **principalName** под **Показать приложений, которыми владеет Моя компания**.</span><span class="sxs-lookup"><span data-stu-id="45c66-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="45c66-144">Действия tooget допустимый токен</span><span class="sxs-lookup"><span data-stu-id="45c66-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="45c66-145">Вызвать hello API с hello следующие параметры и убедитесь, что tooreplace hello КЛИЕНТА\_идентификатор, клиент\_идентификатор и клиент\_СЕКРЕТ:</span><span class="sxs-lookup"><span data-stu-id="45c66-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="45c66-146">**URL-адрес запроса** — в формате *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="45c66-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="45c66-147">**Заголовок Content-Type HTTP** как *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="45c66-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="45c66-148">**Текст запроса HTTP** — в формате *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="45c66-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="45c66-149">Hello ниже приведен пример запроса:</span><span class="sxs-lookup"><span data-stu-id="45c66-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="45c66-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="45c66-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="45c66-151">Вот пример ответа на запрос:</span><span class="sxs-lookup"><span data-stu-id="45c66-151">Here is an example response:</span></span>
     
       <span data-ttu-id="45c66-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="45c66-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="45c66-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="45c66-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="45c66-154">В этом примере включены, параметры отправки hello, кодирование URL-адресов `resource` значение имеет `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="45c66-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="45c66-155">Будьте внимательны, кодирование URL-адрес tooalso `{CLIENT_SECRET}` как она может содержать специальные символы.</span><span class="sxs-lookup"><span data-stu-id="45c66-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="45c66-156">Для тестирования можно использовать средство клиента HTTP, такое как [Fiddler](http://www.telerik.com/fiddler) или [расширение Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop).</span><span class="sxs-lookup"><span data-stu-id="45c66-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="45c66-157">Теперь в все вызовы API, включите заголовок запроса авторизации hello.</span><span class="sxs-lookup"><span data-stu-id="45c66-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="45c66-158">Если получить код состояния 401 возвращается, текст ответа для проверки hello, его может подсказать, истек токен hello.</span><span class="sxs-lookup"><span data-stu-id="45c66-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="45c66-159">В этом случае следует получить новый маркер.</span><span class="sxs-lookup"><span data-stu-id="45c66-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="45c66-160">С помощью API-интерфейсы hello</span><span class="sxs-lookup"><span data-stu-id="45c66-160">Using hello APIs</span></span>
<span data-ttu-id="45c66-161">Теперь, у вас есть действительный токен, все вызовы hello API toomake готовности.</span><span class="sxs-lookup"><span data-stu-id="45c66-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="45c66-162">В каждом запросе API необходимо toopass допустимый, неистекшим сроком действия маркера, который вы получили в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="45c66-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="45c66-163">Вам потребуется tooplug некоторыми параметрами в hello запрос URI, который идентифицирует приложение.</span><span class="sxs-lookup"><span data-stu-id="45c66-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="45c66-164">Hello URI запроса выглядит как следующий hello</span><span class="sxs-lookup"><span data-stu-id="45c66-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="45c66-165">Параметры tooget hello, щелкните имя приложения и выберите команду панели мониторинга и как следующие hello со всеми тремя параметрами Здравствуйте, откроется страница.</span><span class="sxs-lookup"><span data-stu-id="45c66-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="45c66-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="45c66-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="45c66-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="45c66-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="45c66-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="45c66-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="45c66-169">**4** имя вашей группы ресурсов будет toobe **MobileEngagement** Если не был создан новый.</span><span class="sxs-lookup"><span data-stu-id="45c66-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Параметры URI API Служб мобильного взаимодействия][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="45c66-171">Не обращайте внимания hello корневой адрес API, как это было для hello предыдущих API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="45c66-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="45c66-172">Если вы создали приложение hello, с помощью портала Azure Classic требуется toouse hello ресурса приложения имя, отличных от само имя приложения hello.</span><span class="sxs-lookup"><span data-stu-id="45c66-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="45c66-173">Если вы создали приложение hello в hello портал Azure следует использовать hello само (нет никакой разницы между имени ресурсов приложения и приложения для приложений, созданных на новом портале hello) имя приложения.</span><span class="sxs-lookup"><span data-stu-id="45c66-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



