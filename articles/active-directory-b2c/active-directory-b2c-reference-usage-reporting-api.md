---
title: "Azure Active Directory B2C. Примеры и определения для API отчетов об использовании | Документация Майкрософт"
description: "Руководство по получению отчетов по пользователям, операциям аутентификации и Многофакторной идентификации для клиента Azure AD B2C (с примерами)."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="cf1cb-103">Доступ к отчетам об использовании в Azure AD B2C через hello reporting API</span><span class="sxs-lookup"><span data-stu-id="cf1cb-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="cf1cb-104">Azure Active Directory B2C (Azure AD B2C) предоставляет аутентификацию на основе имени для входа и Многофакторной идентификации Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="cf1cb-105">Аутентификация предоставляется для конечных пользователей всего семейства приложений у поставщиков удостоверений.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="cf1cb-106">Если известно hello число пользователей, зарегистрированному в клиенте hello, они используются в tooregister и hello количество проверок подлинности поставщиков hello по типу, можно ответить, например:</span><span class="sxs-lookup"><span data-stu-id="cf1cb-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="cf1cb-107">Сколько пользователей из каждого типа поставщика удостоверений (например, учетную запись Майкрософт или LinkedIn) зарегистрированы в hello последние 10 дней?</span><span class="sxs-lookup"><span data-stu-id="cf1cb-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="cf1cb-108">Количество проверок подлинности с помощью многофакторной проверки подлинности были завершены успешно в hello последний месяц?</span><span class="sxs-lookup"><span data-stu-id="cf1cb-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="cf1cb-109">Сколько успешных операций аутентификации на основе имени для входа было выполнено за последний месяц?</span><span class="sxs-lookup"><span data-stu-id="cf1cb-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="cf1cb-110">В день?</span><span class="sxs-lookup"><span data-stu-id="cf1cb-110">Per day?</span></span> <span data-ttu-id="cf1cb-111">На приложение?</span><span class="sxs-lookup"><span data-stu-id="cf1cb-111">Per application?</span></span>
* <span data-ttu-id="cf1cb-112">Как оценить что hello требуется Ежемесячная стоимость Мои действия клиента Azure AD B2C?</span><span class="sxs-lookup"><span data-stu-id="cf1cb-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="cf1cb-113">Эта статья посвящена отчеты с привязанным toobilling действия, основанной на hello число пользователей, оплачиваемых входа в основе проверок подлинности и многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cf1cb-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cf1cb-114">Prerequisites</span></span>
<span data-ttu-id="cf1cb-115">Перед началом работы необходимо toocomplete hello инструкциям [tooaccess предварительные требования hello отчетами Azure AD API-интерфейсы](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="cf1cb-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="cf1cb-116">Создание приложения, получения секрета и предоставить его доступ прав клиента Azure AD B2C tooyour отчеты.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="cf1cb-117">В статье также приведены примеры *сценария Bash* и *сценария Python*.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="cf1cb-118">Сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf1cb-118">PowerShell script</span></span>
<span data-ttu-id="cf1cb-119">В этом сценарии демонстрируется создание hello четыре отчета об использовании с помощью hello `TimeStamp` параметр и hello `ApplicationId` фильтра.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="cf1cb-120">Определения отчетов об использовании</span><span class="sxs-lookup"><span data-stu-id="cf1cb-120">Usage report definitions</span></span>
* <span data-ttu-id="cf1cb-121">**tenantUserCount**: hello число пользователей в клиенте hello по тип поставщика удостоверений, в день в hello последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="cf1cb-122">(При необходимости `TimeStamp` фильтр предоставляет количества пользователей из указанной даты toohello текущая дата).</span><span class="sxs-lookup"><span data-stu-id="cf1cb-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="cf1cb-123">предоставляет Hello отчета:</span><span class="sxs-lookup"><span data-stu-id="cf1cb-123">hello report provides:</span></span>
  * <span data-ttu-id="cf1cb-124">**TotalUserCount**: hello число всех объектов-пользователей.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="cf1cb-125">**OtherUserCount**: hello число пользователей Azure Active Directory (не пользователей Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="cf1cb-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="cf1cb-126">**LocalUserCount**: hello число учетных записей пользователей Azure AD B2C, созданных с помощью учетных данных локального toohello Azure AD B2C клиента.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="cf1cb-127">**AlternateIdUserCount**: hello количество пользователей Azure AD B2C, зарегистрированных с помощью внешних поставщиков (например, Facebook, учетной записи Майкрософт или другого клиента Azure Active Directory, также называется tooas `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="cf1cb-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="cf1cb-128">**b2cAuthenticationCountSummary**: Сводка hello ежедневно количество оплачиваемых подлинности через hello последние 30 дней, по дням и тип проверки подлинности потока.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="cf1cb-129">**b2cAuthenticationCount**: hello количество проверок подлинности в течение периода времени.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="cf1cb-130">по умолчанию Hello — hello последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="cf1cb-131">(Необязательно: hello открывающая и закрывающая `TimeStamp` параметры определяют период времени.) hello выходные данные содержат `StartTimeStamp` (раннюю дату действия для этого клиента) и `EndTimeStamp` (последнее обновление).</span><span class="sxs-lookup"><span data-stu-id="cf1cb-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="cf1cb-132">**b2cMfaRequestCountSummary**: Сводка hello количество ежедневно многофакторной проверки подлинности, по дням и тип (SMS или голоса).</span><span class="sxs-lookup"><span data-stu-id="cf1cb-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="cf1cb-133">Ограничения</span><span class="sxs-lookup"><span data-stu-id="cf1cb-133">Limitations</span></span>
<span data-ttu-id="cf1cb-134">Число пользовательских данных обновляется каждые 24 часа too48.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="cf1cb-135">Данные об операциях аутентификации обновляются несколько раз в день.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="cf1cb-136">При использовании hello `ApplicationId` фильтр, ответа на пустой отчет может быть из-за tooone из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="cf1cb-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="cf1cb-137">Идентификатор приложения Hello не существует в клиенте hello.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="cf1cb-138">Убедитесь, что он указан правильно.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="cf1cb-139">Идентификатор приложения Hello существует, но не было найдено данных в hello отчетный период.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="cf1cb-140">Проверьте параметры даты и времени.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cf1cb-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf1cb-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="cf1cb-142">Оценка ежемесячных счетов Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf1cb-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="cf1cb-143">В сочетании с [hello последние Azure AD B2C доступны цены](https://azure.microsoft.com/pricing/details/active-directory-b2c/), вы можете оценить ежедневно, еженедельных и ежемесячных использование Azure.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="cf1cb-144">Оценка особенно полезна при планировании изменений в поведении клиента, которые могут повлиять на общую стоимость.</span><span class="sxs-lookup"><span data-stu-id="cf1cb-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="cf1cb-145">Фактические затраты можно просмотреть в [связанной подписке Azure](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="cf1cb-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="cf1cb-146">Параметры для других форматов вывода</span><span class="sxs-lookup"><span data-stu-id="cf1cb-146">Options for other output formats</span></span>
<span data-ttu-id="cf1cb-147">Hello следующем коде приведены примеры отправки tooJSON выходных данных, имя списка значений и XML:</span><span class="sxs-lookup"><span data-stu-id="cf1cb-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
