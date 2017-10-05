---
title: "Примеры для API отчета о событии входа в Azure Active Directory | Документация Майкрософт"
description: "Как начать работу с API отчетов Azure Active Directory"
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
ms.openlocfilehash: 7fc2b59fe37ed2ffe85925c457300ef8fd83c3c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="bfa46-103">Примеры для API отчета о действиях при входе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfa46-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="bfa46-104">Эта статья входит в серию статей об API отчетов Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bfa46-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="bfa46-105">Инструмент создания отчетов Azure AD предоставляет API, с помощью которого можно получить доступ к данным о действиях при входе, используя код или связанные инструменты.</span><span class="sxs-lookup"><span data-stu-id="bfa46-105">Azure AD reporting provides you with an API that enables you to access sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="bfa46-106">Цель этой статьи — предоставить пример кода для **API действий при входе**.</span><span class="sxs-lookup"><span data-stu-id="bfa46-106">The scope of this topic is to provide you with sample code for the **sign-in activity API**.</span></span>

<span data-ttu-id="bfa46-107">См.:</span><span class="sxs-lookup"><span data-stu-id="bfa46-107">See:</span></span>

* <span data-ttu-id="bfa46-108">Основные сведения см. в разделе [Журналы аудита](active-directory-reporting-azure-portal.md#activity-reports).</span><span class="sxs-lookup"><span data-stu-id="bfa46-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="bfa46-109">Дополнительные сведения об API отчетов см. в статье [Приступая к работе с API отчетов Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="bfa46-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bfa46-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bfa46-110">Prerequisites</span></span>
<span data-ttu-id="bfa46-111">Перед использованием примеров в этой статье выполните [предварительные требования для доступа к API отчетов Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="bfa46-111">Before you can use the samples in this topic, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="bfa46-112">Сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfa46-112">PowerShell script</span></span>
    # This script will require the Web Application and permissions setup in Azure Active Directory
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
        Write-Output "Save the output to a file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-the-script"></a><span data-ttu-id="bfa46-113">Выполнение сценария</span><span class="sxs-lookup"><span data-stu-id="bfa46-113">Executing the script</span></span>
<span data-ttu-id="bfa46-114">Завершив редактирование сценария, запустите его и убедитесь, что он вернул ожидаемые данные из отчета о журналах аудита.</span><span class="sxs-lookup"><span data-stu-id="bfa46-114">Once you finish editing the script, run it and verify that the expected data from the Audit logs report is returned.</span></span>

<span data-ttu-id="bfa46-115">Сценарий возвращает выходные данные из отчета о входе в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="bfa46-115">The script returns output from the sign-in report in JSON format.</span></span> <span data-ttu-id="bfa46-116">Он также создает файл `SigninActivities.json` с такими же выходными данными.</span><span class="sxs-lookup"><span data-stu-id="bfa46-116">It also creates an `SigninActivities.json` file with the same output.</span></span> <span data-ttu-id="bfa46-117">Вы можете поэкспериментировать, изменив сценарий так, чтобы он возвращал данные из других отчетов, и закомментировав ненужные форматы выходных данных.</span><span class="sxs-lookup"><span data-stu-id="bfa46-117">You can experiment by modifying the script to return data from other reports, and comment out the output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfa46-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bfa46-118">Next Steps</span></span>
* <span data-ttu-id="bfa46-119">Хотите настроить примеры в этой статье?</span><span class="sxs-lookup"><span data-stu-id="bfa46-119">Would you like to customize the samples in this topic?</span></span> <span data-ttu-id="bfa46-120">Просмотрите [API отчета о действиях при входе Azure Active Directory](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="bfa46-120">Check out the [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="bfa46-121">Полный обзор использования API отчетов Azure Active Directory см. в статье [Приступая к работе с API отчетов Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="bfa46-121">If you want to see a complete overview of using the Azure Active Directory reporting API, see [Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="bfa46-122">Дополнительные сведения об отчетах Azure Active Directory см. в статье [Руководство по отчетам Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="bfa46-122">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

