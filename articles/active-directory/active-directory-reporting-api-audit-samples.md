---
title: "aaaAzure Active Directory отчетов аудита примеры API | Документы Microsoft"
description: "Как tooget работу с Azure Active Directory Reporting API hello"
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
ms.openlocfilehash: 6ada8a7184d7baacaba5ba9c1b9130653b1cf7fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-audit-api-samples"></a><span data-ttu-id="accaa-103">Примеры API аудита инструментов создания отчетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="accaa-103">Azure Active Directory reporting audit API samples</span></span>
<span data-ttu-id="accaa-104">Этот раздел является частью коллекции разделов, посвященных hello Azure Active Directory reporting API.</span><span class="sxs-lookup"><span data-stu-id="accaa-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="accaa-105">Отчетами Azure AD предоставляет API, который позволяет tooaccess данные аудита, с помощью кода или связанные средства.</span><span class="sxs-lookup"><span data-stu-id="accaa-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="accaa-106">Hello в этом разделе относится с образцом кода для hello tooprovide **audit API**.</span><span class="sxs-lookup"><span data-stu-id="accaa-106">hello scope of this topic is tooprovide you with sample code for hello **audit API**.</span></span>

<span data-ttu-id="accaa-107">См.:</span><span class="sxs-lookup"><span data-stu-id="accaa-107">See:</span></span>

* <span data-ttu-id="accaa-108">Основные сведения см. в разделе [Журналы аудита](active-directory-reporting-azure-portal.md#activity-reports).</span><span class="sxs-lookup"><span data-stu-id="accaa-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="accaa-109">[Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) Дополнительные сведения о hello reporting API.</span><span class="sxs-lookup"><span data-stu-id="accaa-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>

<span data-ttu-id="accaa-110">Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, обратитесь в [службу поддержки по инструментам создания отчетов AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="accaa-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="accaa-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="accaa-111">Prerequisites</span></span>
<span data-ttu-id="accaa-112">Прежде чем использовать hello образцы в этом разделе, необходимо toocomplete hello [API отчетов hello Azure AD tooaccess необходимых компонентов](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="accaa-112">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="known-issue"></a><span data-ttu-id="accaa-113">Известная проблема</span><span class="sxs-lookup"><span data-stu-id="accaa-113">Known issue</span></span>
<span data-ttu-id="accaa-114">Проверки подлинности приложения не будет работать, если клиент находится в регионе ЕС hello.</span><span class="sxs-lookup"><span data-stu-id="accaa-114">App Auth will not work if your tenant is in hello EU region.</span></span> <span data-ttu-id="accaa-115">Используйте проверка подлинности пользователей для доступа к API аудита hello обойти эту проблему, пока мы будем устранять проблему hello.</span><span class="sxs-lookup"><span data-stu-id="accaa-115">Please use User Auth for accessing hello Audit API as a workaround until we fix hello issue.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="accaa-116">Сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="accaa-116">PowerShell script</span></span>
    # This script will require registration of a Web Application in Azure Active Directory (see https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)

    # Constants
    $ClientID       = "your-client-application-id-here"       # Insert your application's Client ID, a Globally Unique ID (registered by Global Admin)
    $ClientSecret   = "your-client-application-secret-here"   # Insert your application's Client Key/Secret string
    $loginURL       = "https://login.microsoftonline.com"     # AAD Instance; for example https://login.microsoftonline.com
    $tenantdomain   = "your-tenant-domain.onmicrosoft.com"    # AAD Tenant; for example, contoso.onmicrosoft.com
    $resource       = "https://graph.windows.net"             # Azure AD Graph API resource URI
    $7daysago       = "{0:s}" -f (get-date).AddDays(-7) + "Z" # Use 'AddMinutes(-5)' toodecrement minutes, for example
    Write-Output "Searching for events starting $7daysago"

    # Create HTTP header, get an OAuth2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    # Parse audit report items, save output toofile(s): auditX.json, where X = 0 thru n for number of nextLink pages
    if ($oauth.access_token -ne $null) {   
        $i=0
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}
        $url = 'https://graph.windows.net/' + $tenantdomain + '/activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago

        # loop through each query page (1 through n)
        Do{
            # display each event on hello console window
            Write-Output "Fetching data using Uri: $url"
            $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
            foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
                Write-Output ($event | ConvertTo-Json)
            }

            # save hello query page tooan output file
            Write-Output "Save hello output tooa file audit$i.json"
            $myReport.Content | Out-File -FilePath audit$i.json -Force
            $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
            $i = $i+1
        } while($url -ne $null)
    } else {
        Write-Host "ERROR: No Access Token"
        }

    Write-Host "Press any key toocontinue ..."
    $x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")


### <a name="executing-hello-powershell-script"></a><span data-ttu-id="accaa-117">Выполнение скрипта PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="accaa-117">Executing hello PowerShell script</span></span>
<span data-ttu-id="accaa-118">После завершения редактирования скрипта hello, запустите его и убедитесь, что ожидается, hello возвращаемых данных из отчета журналов аудита hello.</span><span class="sxs-lookup"><span data-stu-id="accaa-118">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="accaa-119">Hello скрипт возвращает выходные данные из отчета об аудите hello в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="accaa-119">hello script returns output from hello audit report in JSON format.</span></span> <span data-ttu-id="accaa-120">Он также создает `audit.json` файл с hello же выходные данные.</span><span class="sxs-lookup"><span data-stu-id="accaa-120">It also creates an `audit.json` file with hello same output.</span></span> <span data-ttu-id="accaa-121">Можно поэкспериментировать, изменяя данные tooreturn hello скриптов из других отчетов и закомментируйте hello выходные форматы, которые не требуется.</span><span class="sxs-lookup"><span data-stu-id="accaa-121">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="bash-script"></a><span data-ttu-id="accaa-122">Сценарий Bash</span><span class="sxs-lookup"><span data-stu-id="accaa-122">Bash script</span></span>
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

## <a name="python-script"></a><span data-ttu-id="accaa-123">Сценарий Python</span><span class="sxs-lookup"><span data-stu-id="accaa-123">Python script</span></span>
    # Author: Michael McLaughlin (michmcla@microsoft.com)
    # Date: January 20, 2016
    # This requires hello Python Requests module: http://docs.python-requests.org

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

    # Use hello access token toomake hello API request
    yesterday = datetime.date.strftime(datetime.date.today() - datetime.timedelta(days=1), '%Y-%m-%d')

    header_params = {'Authorization': token_type + ' ' + access_token}
    request_string = 'https://graph.windows.net/' + tenant_domain + 'activities/audit?api-version=beta&$filter=activityDate%20gt%20' + yesterday   
    response = requests.get(request_string, headers = header_params)

    if response.status_code is 200:
        print response.content
    else:
        print 'ERROR: API request failed'





## <a name="next-steps"></a><span data-ttu-id="accaa-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="accaa-124">Next steps</span></span>
* <span data-ttu-id="accaa-125">Вы хотите toocustomize hello образцы в этом разделе?</span><span class="sxs-lookup"><span data-stu-id="accaa-125">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="accaa-126">Извлечение hello [аудита Azure Active Directory Справочник по API](active-directory-reporting-api-audit-reference.md).</span><span class="sxs-lookup"><span data-stu-id="accaa-126">Check out hello [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md).</span></span> 
* <span data-ttu-id="accaa-127">Если требуется полный обзор использования toosee hello Azure Active Directory reporting API см. в разделе [Приступая к работе с API отчетов Azure Active Directory "hello"](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="accaa-127">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="accaa-128">Если вы хотите toofind дополнительных сведений об отчетах Azure Active Directory, см. раздел hello [Azure Active Directory руководство по отчетам](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="accaa-128">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

