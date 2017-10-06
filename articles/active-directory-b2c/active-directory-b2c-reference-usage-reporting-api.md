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
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Доступ к отчетам об использовании в Azure AD B2C через hello reporting API

Azure Active Directory B2C (Azure AD B2C) предоставляет аутентификацию на основе имени для входа и Многофакторной идентификации Azure. Аутентификация предоставляется для конечных пользователей всего семейства приложений у поставщиков удостоверений. Если известно hello число пользователей, зарегистрированному в клиенте hello, они используются в tooregister и hello количество проверок подлинности поставщиков hello по типу, можно ответить, например:
* Сколько пользователей из каждого типа поставщика удостоверений (например, учетную запись Майкрософт или LinkedIn) зарегистрированы в hello последние 10 дней?
* Количество проверок подлинности с помощью многофакторной проверки подлинности были завершены успешно в hello последний месяц?
* Сколько успешных операций аутентификации на основе имени для входа было выполнено за последний месяц? В день? На приложение?
* Как оценить что hello требуется Ежемесячная стоимость Мои действия клиента Azure AD B2C?

Эта статья посвящена отчеты с привязанным toobilling действия, основанной на hello число пользователей, оплачиваемых входа в основе проверок подлинности и многофакторной проверки подлинности.


## <a name="prerequisites"></a>Предварительные требования
Перед началом работы необходимо toocomplete hello инструкциям [tooaccess предварительные требования hello отчетами Azure AD API-интерфейсы](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Создание приложения, получения секрета и предоставить его доступ прав клиента Azure AD B2C tooyour отчеты. В статье также приведены примеры *сценария Bash* и *сценария Python*. 

## <a name="powershell-script"></a>Сценарий PowerShell
В этом сценарии демонстрируется создание hello четыре отчета об использовании с помощью hello `TimeStamp` параметр и hello `ApplicationId` фильтра.

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


## <a name="usage-report-definitions"></a>Определения отчетов об использовании
* **tenantUserCount**: hello число пользователей в клиенте hello по тип поставщика удостоверений, в день в hello последние 30 дней. (При необходимости `TimeStamp` фильтр предоставляет количества пользователей из указанной даты toohello текущая дата). предоставляет Hello отчета:
  * **TotalUserCount**: hello число всех объектов-пользователей.
  * **OtherUserCount**: hello число пользователей Azure Active Directory (не пользователей Azure AD B2C).
  * **LocalUserCount**: hello число учетных записей пользователей Azure AD B2C, созданных с помощью учетных данных локального toohello Azure AD B2C клиента.

* **AlternateIdUserCount**: hello количество пользователей Azure AD B2C, зарегистрированных с помощью внешних поставщиков (например, Facebook, учетной записи Майкрософт или другого клиента Azure Active Directory, также называется tooas `OrgId`).

* **b2cAuthenticationCountSummary**: Сводка hello ежедневно количество оплачиваемых подлинности через hello последние 30 дней, по дням и тип проверки подлинности потока.

* **b2cAuthenticationCount**: hello количество проверок подлинности в течение периода времени. по умолчанию Hello — hello последние 30 дней.  (Необязательно: hello открывающая и закрывающая `TimeStamp` параметры определяют период времени.) hello выходные данные содержат `StartTimeStamp` (раннюю дату действия для этого клиента) и `EndTimeStamp` (последнее обновление).

* **b2cMfaRequestCountSummary**: Сводка hello количество ежедневно многофакторной проверки подлинности, по дням и тип (SMS или голоса).


## <a name="limitations"></a>Ограничения
Число пользовательских данных обновляется каждые 24 часа too48. Данные об операциях аутентификации обновляются несколько раз в день. При использовании hello `ApplicationId` фильтр, ответа на пустой отчет может быть из-за tooone из следующих условий:
  * Идентификатор приложения Hello не существует в клиенте hello. Убедитесь, что он указан правильно.
  * Идентификатор приложения Hello существует, но не было найдено данных в hello отчетный период. Проверьте параметры даты и времени.


## <a name="next-steps"></a>Дальнейшие действия
### <a name="monthly-bill-estimates-for-azure-ad"></a>Оценка ежемесячных счетов Azure AD
В сочетании с [hello последние Azure AD B2C доступны цены](https://azure.microsoft.com/pricing/details/active-directory-b2c/), вы можете оценить ежедневно, еженедельных и ежемесячных использование Azure.  Оценка особенно полезна при планировании изменений в поведении клиента, которые могут повлиять на общую стоимость. Фактические затраты можно просмотреть в [связанной подписке Azure](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Параметры для других форматов вывода
Hello следующем коде приведены примеры отправки tooJSON выходных данных, имя списка значений и XML:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
