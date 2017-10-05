---
title: "Примеры API аудита инструментов создания отчетов Azure Active Directory | Документация Майкрософт"
description: "Как начать работу с API отчетов Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: de8b8ec3-49b3-4aa8-93fb-e38f52c99743
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 6e3e127fbdc228ff0535be64fe4a4a696731a897
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-audit-api-samples"></a><span data-ttu-id="01d96-103">Примеры API аудита инструментов создания отчетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01d96-103">Azure Active Directory reporting audit API samples</span></span>
<span data-ttu-id="01d96-104">Эта статья входит в серию статей об API отчетов Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01d96-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="01d96-105">Инструмент создания отчетов Azure AD предоставляет API, с помощью которого можно получить доступ к данным аудита, используя код или связанные инструменты.</span><span class="sxs-lookup"><span data-stu-id="01d96-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="01d96-106">Цель этой статьи — предоставить пример кода для **API аудита**.</span><span class="sxs-lookup"><span data-stu-id="01d96-106">The scope of this topic is to provide you with sample code for the **audit API**.</span></span>

<span data-ttu-id="01d96-107">См.:</span><span class="sxs-lookup"><span data-stu-id="01d96-107">See:</span></span>

* <span data-ttu-id="01d96-108">Основные сведения см. в разделе [Журналы аудита](active-directory-reporting-azure-portal.md#activity-reports).</span><span class="sxs-lookup"><span data-stu-id="01d96-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="01d96-109">Дополнительные сведения об API отчетов см. в статье [Приступая к работе с API отчетов Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="01d96-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>

<span data-ttu-id="01d96-110">Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, обратитесь в [службу поддержки по инструментам создания отчетов AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="01d96-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="01d96-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="01d96-111">Prerequisites</span></span>
<span data-ttu-id="01d96-112">Перед использованием примеров в этой статье выполните [предварительные требования для доступа к API отчетов Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="01d96-112">Before you can use the samples in this topic, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="known-issue"></a><span data-ttu-id="01d96-113">Известная проблема</span><span class="sxs-lookup"><span data-stu-id="01d96-113">Known issue</span></span>
<span data-ttu-id="01d96-114">Вы не сможете пройти аутентификацию приложения, если клиент находится в регионе Европы.</span><span class="sxs-lookup"><span data-stu-id="01d96-114">App Auth will not work if your tenant is in the EU region.</span></span> <span data-ttu-id="01d96-115">Используйте аутентификацию пользователя для доступа к API аудита в качестве обходного решения, пока мы не решим эту проблему.</span><span class="sxs-lookup"><span data-stu-id="01d96-115">Please use User Auth for accessing the Audit API as a workaround until we fix the issue.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="01d96-116">Сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="01d96-116">PowerShell script</span></span>
    # This script will require registration of a Web Application in Azure Active Directory (see https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)

    # Constants
    $ClientID       = "your-client-application-id-here"       # Insert your application's Client ID, a Globally Unique ID (registered by Global Admin)
    $ClientSecret   = "your-client-application-secret-here"   # Insert your application's Client Key/Secret string
    $loginURL       = "https://login.microsoftonline.com"     # AAD Instance; for example https://login.microsoftonline.com
    $tenantdomain   = "your-tenant-domain.onmicrosoft.com"    # AAD Tenant; for example, contoso.onmicrosoft.com
    $resource       = "https://graph.windows.net"             # Azure AD Graph API resource URI
    $7daysago       = "{0:s}" -f (get-date).AddDays(-7) + "Z" # Use 'AddMinutes(-5)' to decrement minutes, for example
    Write-Output "Searching for events starting $7daysago"

    # Create HTTP header, get an OAuth2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    # Parse audit report items, save output to file(s): auditX.json, where X = 0 thru n for number of nextLink pages
    if ($oauth.access_token -ne $null) {   
        $i=0
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}
        $url = 'https://graph.windows.net/' + $tenantdomain + '/activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago

        # loop through each query page (1 through n)
        Do{
            # display each event on the console window
            Write-Output "Fetching data using Uri: $url"
            $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
            foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
                Write-Output ($event | ConvertTo-Json)
            }

            # save the query page to an output file
            Write-Output "Save the output to a file audit$i.json"
            $myReport.Content | Out-File -FilePath audit$i.json -Force
            $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
            $i = $i+1
        } while($url -ne $null)
    } else {
        Write-Host "ERROR: No Access Token"
        }

    Write-Host "Press any key to continue ..."
    $x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")


### <a name="executing-the-powershell-script"></a><span data-ttu-id="01d96-117">Выполнение сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="01d96-117">Executing the PowerShell script</span></span>
<span data-ttu-id="01d96-118">Завершив редактирование сценария, запустите его и убедитесь, что он вернул ожидаемые данные из отчета о журналах аудита.</span><span class="sxs-lookup"><span data-stu-id="01d96-118">Once you finish editing the script, run it and verify that the expected data from the Audit logs report is returned.</span></span>

<span data-ttu-id="01d96-119">Сценарий возвращает выходные данные из отчета об аудите в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="01d96-119">The script returns output from the audit report in JSON format.</span></span> <span data-ttu-id="01d96-120">Он также создает файл `audit.json` с такими же выходными данными.</span><span class="sxs-lookup"><span data-stu-id="01d96-120">It also creates an `audit.json` file with the same output.</span></span> <span data-ttu-id="01d96-121">Вы можете поэкспериментировать, изменив сценарий так, чтобы он возвращал данные из других отчетов, и закомментировав ненужные форматы выходных данных.</span><span class="sxs-lookup"><span data-stu-id="01d96-121">You can experiment by modifying the script to return data from other reports, and comment out the output formats that you do not need.</span></span>

## <a name="bash-script"></a><span data-ttu-id="01d96-122">Сценарий Bash</span><span class="sxs-lookup"><span data-stu-id="01d96-122">Bash script</span></span>
    #!/bin/bash

    # Author: Ken Hoff (kenhoff@microsoft.com)
    # Date: 2015.08.20
    # NOTE: This script requires jq (https://stedolan.github.io/jq/)

    CLIENT_ID="your-application-client-id-here"         # Should be a ~35 character string insert your info here
    CLIENT_SECRET="your-application-client-secret-here" # Should be a ~44 character string insert your info here
    LOGIN_URL="https://login.microsoftonline.com"
    TENANT_DOMAIN="your-directory-name-here.onmicrosoft.com"    # For example, contoso.onmicrosoft.com

    TOKEN_INFO=$(curl -s --data-urlencode "grant_type=client_credentials" --data-urlencode "client_id=$CLIENT_ID" --data-urlencode "client_secret=$CLIENT_SECRET" "$LOGIN_URL/$TENANT_DOMAIN/oauth2/token?api-version=1.0")

    TOKEN_TYPE=$(echo $TOKEN_INFO | ./jq-win64.exe -r '.token_type')
    ACCESS_TOKEN=$(echo $TOKEN_INFO | ./jq-win64.exe -r '.access_token')

    # get yesterday's date

    YESTERDAY=$(date --date='1 day ago' +'%Y-%m-%d')

    URL="https://graph.windows.net/$TENANT_DOMAIN/activities/audit?api-version=beta&$filter=activityDate%20gt%20$YESTERDAY"


    REPORT=$(curl -s --header "Authorization: $TOKEN_TYPE $ACCESS_TOKEN" $URL)

    echo $REPORT | ./jq-win64.exe -r '.value' | ./jq-win64.exe -r ".[]"

## <a name="python-script"></a><span data-ttu-id="01d96-123">Сценарий Python</span><span class="sxs-lookup"><span data-stu-id="01d96-123">Python script</span></span>
    # Author: Michael McLaughlin (michmcla@microsoft.com)
    # Date: January 20, 2016
    # This requires the Python Requests module: http://docs.python-requests.org

    import requests
    import datetime
    import sys

    client_id = 'your-application-client-id-here'
    client_secret = 'your-application-client-secret-here'
    login_url = 'https://login.microsoftonline.com/'
    tenant_domain = 'your-directory-name-here.onmicrosoft.com'

    # Get an OAuth access token
    bodyvals = {'client_id': client_id,
                'client_secret': client_secret,
                'grant_type': 'client_credentials'}

    request_url = login_url + tenant_domain + '/oauth2/token?api-version=1.0'
    token_response = requests.post(request_url, data=bodyvals)

    access_token = token_response.json().get('access_token')
    token_type = token_response.json().get('token_type')

    if access_token is None or token_type is None:
        print "ERROR: Couldn't get access token"
        sys.exit(1)

    # Use the access token to make the API request
    yesterday = datetime.date.strftime(datetime.date.today() - datetime.timedelta(days=1), '%Y-%m-%d')

    header_params = {'Authorization': token_type + ' ' + access_token}
    request_string = 'https://graph.windows.net/' + tenant_domain + 'activities/audit?api-version=beta&$filter=activityDate%20gt%20' + yesterday   
    response = requests.get(request_string, headers = header_params)

    if response.status_code is 200:
        print response.content
    else:
        print 'ERROR: API request failed'





## <a name="next-steps"></a><span data-ttu-id="01d96-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01d96-124">Next steps</span></span>
* <span data-ttu-id="01d96-125">Хотите настроить примеры в этой статье?</span><span class="sxs-lookup"><span data-stu-id="01d96-125">Would you like to customize the samples in this topic?</span></span> <span data-ttu-id="01d96-126">См. статью [Справочник по API аудита Azure Active Directory](active-directory-reporting-api-audit-reference.md).</span><span class="sxs-lookup"><span data-stu-id="01d96-126">Check out the [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md).</span></span> 
* <span data-ttu-id="01d96-127">Полный обзор использования API отчетов Azure Active Directory см. в статье [Приступая к работе с API отчетов Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="01d96-127">If you want to see a complete overview of using the Azure Active Directory reporting API, see [Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="01d96-128">Дополнительные сведения об отчетах Azure Active Directory см. в статье [Руководство по отчетам Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="01d96-128">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

