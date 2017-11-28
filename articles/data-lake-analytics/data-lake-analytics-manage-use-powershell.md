---
title: "Аналитика Озера данных Azure, с помощью Azure PowerShell aaaManage | Документы Microsoft"
description: "Узнайте, как учетные записи аналитики Озера данных toomanage, источники данных, заданий, а элементы каталога. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="6cb31-103">Управление аналитикой озера данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cb31-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="6cb31-104">Узнайте, как учетные записи аналитики Озера данных Azure toomanage, источники данных, заданий и элементов каталога, с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cb31-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6cb31-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6cb31-105">Prerequisites</span></span>

<span data-ttu-id="6cb31-106">При создании учетной записи аналитики Озера данных необходимо tooknow:</span><span class="sxs-lookup"><span data-stu-id="6cb31-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="6cb31-107">**Идентификатор подписки**: hello идентификатор подписки Azure, в котором находится ваша учетная запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6cb31-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="6cb31-108">**Группа ресурсов**: hello имя группы ресурсов Azure hello, содержащую учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6cb31-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="6cb31-109">**Имя учетной записи аналитики Озера данных**: hello учетной записи, имя должно содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="6cb31-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="6cb31-110">**Учетная запись Data Lake Store по умолчанию** — каждая учетная запись Data Lake Analytics содержит учетную запись Data Lake Store по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6cb31-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="6cb31-111">Эти учетные записи должны быть в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="6cb31-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="6cb31-112">**Расположение**: hello расположение учетной записи аналитики Озера данных, например, «Восточная часть США 2», или другими поддерживается расположения.</span><span class="sxs-lookup"><span data-stu-id="6cb31-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="6cb31-113">Поддерживаемые расположения можно просмотреть на [странице с расценками](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="6cb31-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="6cb31-114">фрагменты кода PowerShell Hello в этом учебнике эти сведения можно использовать эти переменные toostore</span><span class="sxs-lookup"><span data-stu-id="6cb31-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="6cb31-115">Вход в систему</span><span class="sxs-lookup"><span data-stu-id="6cb31-115">Log in</span></span>

<span data-ttu-id="6cb31-116">Вход с помощью идентификатора подписки.</span><span class="sxs-lookup"><span data-stu-id="6cb31-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="6cb31-117">Вход с помощью имени подписки.</span><span class="sxs-lookup"><span data-stu-id="6cb31-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="6cb31-118">Hello `Login-AzureRmAccount` командлет всегда запрашивает учетные данные.</span><span class="sxs-lookup"><span data-stu-id="6cb31-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="6cb31-119">Чтобы избежать многократных запросов с помощью следующих командлетов hello.</span><span class="sxs-lookup"><span data-stu-id="6cb31-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="6cb31-120">Управление учетными записями</span><span class="sxs-lookup"><span data-stu-id="6cb31-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="6cb31-121">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="6cb31-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="6cb31-122">Если у вас еще нет [группы ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, создайте его.</span><span class="sxs-lookup"><span data-stu-id="6cb31-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="6cb31-123">Для каждой учетной записи Data Lake Analytics необходима учетная запись Data Lake Store по умолчанию, которая используется для хранения журналов.</span><span class="sxs-lookup"><span data-stu-id="6cb31-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="6cb31-124">Можно повторно использовать существующую учетную запись или создать новую.</span><span class="sxs-lookup"><span data-stu-id="6cb31-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="6cb31-125">После создания группы ресурсов и учетной записи Data Lake Store создайте учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6cb31-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="6cb31-126">Получение сведений об учетной записи</span><span class="sxs-lookup"><span data-stu-id="6cb31-126">Get information about an account</span></span>

<span data-ttu-id="6cb31-127">Получение сведений об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6cb31-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="6cb31-128">Проверьте существование hello определенной учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6cb31-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="6cb31-129">Hello командлет возвращает либо `True` или `False`.</span><span class="sxs-lookup"><span data-stu-id="6cb31-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="6cb31-130">Проверьте существование hello определенной учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6cb31-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="6cb31-131">Hello командлет возвращает либо `True` или `False`.</span><span class="sxs-lookup"><span data-stu-id="6cb31-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="6cb31-132">Получение списка учетных записей</span><span class="sxs-lookup"><span data-stu-id="6cb31-132">Listing accounts</span></span>

<span data-ttu-id="6cb31-133">Учетные записи аналитики Озера данных списка в текущей подписке hello.</span><span class="sxs-lookup"><span data-stu-id="6cb31-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="6cb31-134">Вывод списка учетных записей Data Lake Analytics в конкретной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6cb31-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="6cb31-135">Управление правилами брандмауэра</span><span class="sxs-lookup"><span data-stu-id="6cb31-135">Managing firewall rules</span></span>

<span data-ttu-id="6cb31-136">Вывод списка правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="6cb31-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="6cb31-137">Добавление правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="6cb31-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="6cb31-138">Изменение правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="6cb31-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="6cb31-139">Удаление правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="6cb31-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="6cb31-140">Разрешение IP-адресов Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb31-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="6cb31-141">Управление источниками данных</span><span class="sxs-lookup"><span data-stu-id="6cb31-141">Managing data sources</span></span>
<span data-ttu-id="6cb31-142">Azure аналитики Озера данных в настоящее время поддерживает следующие источники данных hello:</span><span class="sxs-lookup"><span data-stu-id="6cb31-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="6cb31-143">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="6cb31-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="6cb31-144">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="6cb31-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="6cb31-145">При создании учетной записи аналитики, необходимо назначить хранилище Озера данных учетной записи toobe hello источник данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6cb31-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="6cb31-146">Hello учетной записи хранилища Озера данных по умолчанию используется toostore метаданные задания и задания журналы аудита.</span><span class="sxs-lookup"><span data-stu-id="6cb31-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="6cb31-147">После создания учетной записи Data Lake Analytics можно добавить дополнительные учетные записи Data Lake Store и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6cb31-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="6cb31-148">Найти учетную запись хранилища Озера данных по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="6cb31-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="6cb31-149">Учетная запись хранилища Озера данных по умолчанию hello можно найти с помощью фильтрации по hello hello список источников данных `IsDefault` свойство:</span><span class="sxs-lookup"><span data-stu-id="6cb31-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="6cb31-150">Добавление источника данных</span><span class="sxs-lookup"><span data-stu-id="6cb31-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="6cb31-151">Получение списка источников данных</span><span class="sxs-lookup"><span data-stu-id="6cb31-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="6cb31-152">Отправка заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="6cb31-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="6cb31-153">Отправка строки как скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="6cb31-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="6cb31-154">Отправка файла как скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="6cb31-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="6cb31-155">Получение списка заданий в учетной записи</span><span class="sxs-lookup"><span data-stu-id="6cb31-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="6cb31-156">Список всех заданий hello в учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="6cb31-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="6cb31-157">Вывод Hello включает hello выполняющихся заданий и задания, которые недавно завершена.</span><span class="sxs-lookup"><span data-stu-id="6cb31-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="6cb31-158">Получение списка определенного числа заданий</span><span class="sxs-lookup"><span data-stu-id="6cb31-158">List a specific number of jobs</span></span>

<span data-ttu-id="6cb31-159">По умолчанию они сортируются hello список заданий на время отправки.</span><span class="sxs-lookup"><span data-stu-id="6cb31-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="6cb31-160">Поэтому hello последней отправки заданий отображаются первыми.</span><span class="sxs-lookup"><span data-stu-id="6cb31-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="6cb31-161">По умолчанию hello учетной записи ADLA запоминает заданий на 180 дней, но hello Ge AdlJob командлет по умолчанию возвращает hello только первые 500.</span><span class="sxs-lookup"><span data-stu-id="6cb31-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="6cb31-162">Используйте параметр - Top параметр toolist ряд заданий.</span><span class="sxs-lookup"><span data-stu-id="6cb31-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="6cb31-163">Список заданий, на основе значения hello свойства задания</span><span class="sxs-lookup"><span data-stu-id="6cb31-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="6cb31-164">С помощью hello `-State` параметра.</span><span class="sxs-lookup"><span data-stu-id="6cb31-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="6cb31-165">Вы можете использовать любое сочетание следующих значений:</span><span class="sxs-lookup"><span data-stu-id="6cb31-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="6cb31-166">Используйте hello `-Result` toodetect параметр завершились ли задания завершается успешно.</span><span class="sxs-lookup"><span data-stu-id="6cb31-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="6cb31-167">Возможны следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6cb31-167">It has these values:</span></span>

* <span data-ttu-id="6cb31-168">Отменено</span><span class="sxs-lookup"><span data-stu-id="6cb31-168">Cancelled</span></span>
* <span data-ttu-id="6cb31-169">Сбой</span><span class="sxs-lookup"><span data-stu-id="6cb31-169">Failed</span></span>
* <span data-ttu-id="6cb31-170">None</span><span class="sxs-lookup"><span data-stu-id="6cb31-170">None</span></span>
* <span data-ttu-id="6cb31-171">Успешно</span><span class="sxs-lookup"><span data-stu-id="6cb31-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="6cb31-172">Hello `-Submitter` параметр помогает определить, кто отправил задание.</span><span class="sxs-lookup"><span data-stu-id="6cb31-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="6cb31-173">Hello `-SubmittedAfter` полезно при фильтрации tooa диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="6cb31-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="6cb31-174">Распространенные сценарии для получения списка заданий</span><span class="sxs-lookup"><span data-stu-id="6cb31-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="6cb31-175">Фильтрация списка заданий</span><span class="sxs-lookup"><span data-stu-id="6cb31-175">Filtering a list of jobs</span></span>

<span data-ttu-id="6cb31-176">После получения списка заданий в текущем сеансе PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cb31-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="6cb31-177">Можно использовать обычный список hello toofilter PowerShell командлеты.</span><span class="sxs-lookup"><span data-stu-id="6cb31-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="6cb31-178">Фильтр списка заданий toohello заданий, поступающими в hello последние 24 часа</span><span class="sxs-lookup"><span data-stu-id="6cb31-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="6cb31-179">Фильтровать список заданий toohello заданий, завершившихся hello последние 24 часа</span><span class="sxs-lookup"><span data-stu-id="6cb31-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="6cb31-180">Фильтрация списка заданий toohello заданий, которые была запущена.</span><span class="sxs-lookup"><span data-stu-id="6cb31-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="6cb31-181">Задание может завершиться сбоем во время компиляции и поэтому никогда не запускаться.</span><span class="sxs-lookup"><span data-stu-id="6cb31-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="6cb31-182">Давайте рассмотрим hello сбой задания, которые фактически запущен и завершилась неуспешно.</span><span class="sxs-lookup"><span data-stu-id="6cb31-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="6cb31-183">Анализ списка заданий</span><span class="sxs-lookup"><span data-stu-id="6cb31-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="6cb31-184">Используйте hello `Group-Object` tooanalyze командлет список заданий.</span><span class="sxs-lookup"><span data-stu-id="6cb31-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="6cb31-185">Выполнения анализа, бывает полезно tooadd свойства toohello задания объектов toomake фильтрацию и группирование проще.</span><span class="sxs-lookup"><span data-stu-id="6cb31-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="6cb31-186">Следующий фрагмент кода Hello показывает способ tooannotate a JobInfo с вычисления свойства.</span><span class="sxs-lookup"><span data-stu-id="6cb31-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="6cb31-187">Получение сведений о конвейерах и повторениях</span><span class="sxs-lookup"><span data-stu-id="6cb31-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="6cb31-188">Используйте hello `Get-AdlJobPipeline` командлет toosee hello конвейера ранее отправлять данные задания.</span><span class="sxs-lookup"><span data-stu-id="6cb31-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="6cb31-189">Используйте hello `Get-AdlJobRecurrence` командлет toosee hello повторений для ранее отправленные задания.</span><span class="sxs-lookup"><span data-stu-id="6cb31-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="6cb31-190">Получение информации о задании</span><span class="sxs-lookup"><span data-stu-id="6cb31-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="6cb31-191">Получение состояния задания</span><span class="sxs-lookup"><span data-stu-id="6cb31-191">Get job status</span></span>

<span data-ttu-id="6cb31-192">Получите состояние hello определенного задания.</span><span class="sxs-lookup"><span data-stu-id="6cb31-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="6cb31-193">Проверьте в выходных данных задания hello</span><span class="sxs-lookup"><span data-stu-id="6cb31-193">Examine hello job outputs</span></span>

<span data-ttu-id="6cb31-194">После завершения задания hello проверяет, существует ли hello выходной файл, указав hello файлов в папке.</span><span class="sxs-lookup"><span data-stu-id="6cb31-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="6cb31-195">Управление выполнением заданий</span><span class="sxs-lookup"><span data-stu-id="6cb31-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="6cb31-196">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="6cb31-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="6cb31-197">Дождитесь toofinish задания</span><span class="sxs-lookup"><span data-stu-id="6cb31-197">Wait for a job toofinish</span></span>

<span data-ttu-id="6cb31-198">Вместо того чтобы повторять `Get-AdlAnalyticsJob` до завершения задания, можно использовать hello `Wait-AdlJob` toowait командлет для задания tooend hello.</span><span class="sxs-lookup"><span data-stu-id="6cb31-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="6cb31-199">Управление политиками вычислений</span><span class="sxs-lookup"><span data-stu-id="6cb31-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="6cb31-200">Список существующих политик вычислений</span><span class="sxs-lookup"><span data-stu-id="6cb31-200">List existing compute policies</span></span>

<span data-ttu-id="6cb31-201">Hello `Get-AdlAnalyticsComputePolicy` командлет извлекает сведения о политиках вычислений для учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6cb31-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="6cb31-202">Создание политики вычислений</span><span class="sxs-lookup"><span data-stu-id="6cb31-202">Create a compute policy</span></span>

<span data-ttu-id="6cb31-203">Hello `New-AdlAnalyticsComputePolicy` создает новую политику вычислений для учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="6cb31-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="6cb31-204">В этом примере, что наборы hello максимальной доступной toohello Сиднейское указан too50 пользователя и too250 приоритет задания минимального hello.</span><span class="sxs-lookup"><span data-stu-id="6cb31-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="6cb31-205">Проверьте наличие файла hello.</span><span class="sxs-lookup"><span data-stu-id="6cb31-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="6cb31-206">Отправка и скачивание</span><span class="sxs-lookup"><span data-stu-id="6cb31-206">Uploading and downloading</span></span>

<span data-ttu-id="6cb31-207">Отправка файла.</span><span class="sxs-lookup"><span data-stu-id="6cb31-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="6cb31-208">Рекурсивная отправка всей папки.</span><span class="sxs-lookup"><span data-stu-id="6cb31-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="6cb31-209">Скачивание файла.</span><span class="sxs-lookup"><span data-stu-id="6cb31-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="6cb31-210">Рекурсивное скачивание всей папки.</span><span class="sxs-lookup"><span data-stu-id="6cb31-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="6cb31-211">Если hello отправки или загрузки процесс прерывается, может попытаться выполнить процесс hello tooresume выполнение hello командлет еще раз с hello ``-Resume`` флаг.</span><span class="sxs-lookup"><span data-stu-id="6cb31-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="6cb31-212">Управление элементами каталога</span><span class="sxs-lookup"><span data-stu-id="6cb31-212">Manage catalog items</span></span>

<span data-ttu-id="6cb31-213">каталог Hello U-SQL является toostructure используемых данных и кода, поэтому они могут совместно использоваться сценарии U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6cb31-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="6cb31-214">Hello каталога включает hello максимально возможную производительность с данными в Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb31-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="6cb31-215">Дополнительные сведения см. в разделе [Использование каталога U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="6cb31-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="6cb31-216">Элементы списка в каталоге hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="6cb31-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="6cb31-217">Список всех сборок hello во всех базах данных hello ADLA учетную запись.</span><span class="sxs-lookup"><span data-stu-id="6cb31-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="6cb31-218">Получение сведений об элементе каталога</span><span class="sxs-lookup"><span data-stu-id="6cb31-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="6cb31-219">Создание учетных данных в каталоге</span><span class="sxs-lookup"><span data-stu-id="6cb31-219">Create credentials in a catalog</span></span>

<span data-ttu-id="6cb31-220">В базе данных U-SQL создайте объект учетных данных для базы данных, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb31-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="6cb31-221">В настоящее время U-SQL учетных данных — единственный тип hello элемента каталога, которые можно создавать с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cb31-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="6cb31-222">Получение основных сведений об учетной записи ADLA</span><span class="sxs-lookup"><span data-stu-id="6cb31-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="6cb31-223">Данное имя учетной записи после кода hello ищет основные сведения об учетной записи hello</span><span class="sxs-lookup"><span data-stu-id="6cb31-223">Given an account name, hello following code looks up basic information about hello account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="6cb31-224">Работа с Azure</span><span class="sxs-lookup"><span data-stu-id="6cb31-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="6cb31-225">Получение сведений об ошибках AzureRm</span><span class="sxs-lookup"><span data-stu-id="6cb31-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="6cb31-226">Проверка выполнения с правами администратора</span><span class="sxs-lookup"><span data-stu-id="6cb31-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="6cb31-227">Поиск TenantID</span><span class="sxs-lookup"><span data-stu-id="6cb31-227">Find a TenantID</span></span>

<span data-ttu-id="6cb31-228">По имени подписки:</span><span class="sxs-lookup"><span data-stu-id="6cb31-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="6cb31-229">По идентификатору подписки:</span><span class="sxs-lookup"><span data-stu-id="6cb31-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="6cb31-230">По адресу домена, например contoso.com:</span><span class="sxs-lookup"><span data-stu-id="6cb31-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="6cb31-231">Получение списка всех подписок и идентификаторов клиентов</span><span class="sxs-lookup"><span data-stu-id="6cb31-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="6cb31-232">Создание учетной записи Data Lake Analytics с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="6cb31-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="6cb31-233">Можно также использовать шаблон группы ресурсов Azure, используя hello следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6cb31-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="6cb31-234">Дополнительные сведения см. в разделах [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) (Развертывание приложения с использованием шаблона Azure Resource Manager) и [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6cb31-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="6cb31-235">**Пример шаблона**</span><span class="sxs-lookup"><span data-stu-id="6cb31-235">**Example template**</span></span>

<span data-ttu-id="6cb31-236">Сохраните следующий текст в виде hello `.json` файл, а затем использовать hello, предшествующий шаблон hello toouse скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cb31-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="6cb31-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6cb31-237">Next steps</span></span>
* [<span data-ttu-id="6cb31-238">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6cb31-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="6cb31-239">Начало работы с Data Lake Analytics с помощью [портала Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="6cb31-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="6cb31-240">Управление Azure Data Lake Analytics с помощью [портала Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6cb31-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
