---
title: "образцы отчетов API действий aaaAzure входа в Active Directory | Документы Microsoft"
description: "Как tooget работу с Azure Active Directory Reporting API hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="5a5ac-103">Примеры для API отчета о действиях при входе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a5ac-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="5a5ac-104">Этот раздел является частью коллекции разделов, посвященных hello Azure Active Directory reporting API.</span><span class="sxs-lookup"><span data-stu-id="5a5ac-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="5a5ac-105">Отчетами Azure AD предоставляет API, который позволяет tooaccess данных действия при входе, с помощью кода или связанные средства.</span><span class="sxs-lookup"><span data-stu-id="5a5ac-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="5a5ac-106">Hello в этом разделе относится с образцом кода для hello tooprovide **входа в API действия**.</span><span class="sxs-lookup"><span data-stu-id="5a5ac-106">hello scope of this topic is tooprovide you with sample code for hello **sign-in activity API**.</span></span>

<span data-ttu-id="5a5ac-107">См.:</span><span class="sxs-lookup"><span data-stu-id="5a5ac-107">See:</span></span>

* <span data-ttu-id="5a5ac-108">Основные сведения см. в разделе [Журналы аудита](active-directory-reporting-azure-portal.md#activity-reports).</span><span class="sxs-lookup"><span data-stu-id="5a5ac-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="5a5ac-109">[Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) Дополнительные сведения о hello reporting API.</span><span class="sxs-lookup"><span data-stu-id="5a5ac-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5a5ac-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5a5ac-110">Prerequisites</span></span>
<span data-ttu-id="5a5ac-111">Прежде чем использовать hello образцы в этом разделе, необходимо toocomplete hello [API отчетов hello Azure AD tooaccess необходимых компонентов](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="5a5ac-111">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="5a5ac-112">Сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a5ac-112">PowerShell script</span></span>
    # This script will require hello Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a><span data-ttu-id="5a5ac-113">Выполнение скрипта hello</span><span class="sxs-lookup"><span data-stu-id="5a5ac-113">Executing hello script</span></span>
<span data-ttu-id="5a5ac-114">После завершения редактирования скрипта hello, запустите его и убедитесь, что ожидается, hello возвращаемых данных из отчета журналов аудита hello.</span><span class="sxs-lookup"><span data-stu-id="5a5ac-114">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="5a5ac-115">Hello скрипт возвращает выходные данные из hello входа в отчет в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="5a5ac-115">hello script returns output from hello sign-in report in JSON format.</span></span> <span data-ttu-id="5a5ac-116">Он также создает `SigninActivities.json` файл с hello же выходные данные.</span><span class="sxs-lookup"><span data-stu-id="5a5ac-116">It also creates an `SigninActivities.json` file with hello same output.</span></span> <span data-ttu-id="5a5ac-117">Можно поэкспериментировать, изменяя данные tooreturn hello скриптов из других отчетов и закомментируйте hello выходные форматы, которые не требуется.</span><span class="sxs-lookup"><span data-stu-id="5a5ac-117">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a5ac-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a5ac-118">Next Steps</span></span>
* <span data-ttu-id="5a5ac-119">Вы хотите toocustomize hello образцы в этом разделе?</span><span class="sxs-lookup"><span data-stu-id="5a5ac-119">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="5a5ac-120">Извлечение hello [Azure Active Directory действия при входе Справочник по API](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5a5ac-120">Check out hello [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="5a5ac-121">Если требуется полный обзор использования toosee hello Azure Active Directory reporting API см. в разделе [Приступая к работе с API отчетов Azure Active Directory "hello"](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5a5ac-121">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="5a5ac-122">Если вы хотите toofind дополнительных сведений об отчетах Azure Active Directory, см. раздел hello [Azure Active Directory руководство по отчетам](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5a5ac-122">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

