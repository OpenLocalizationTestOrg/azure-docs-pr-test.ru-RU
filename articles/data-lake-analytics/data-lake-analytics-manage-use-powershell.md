---
title: "Управление Azure Data Lake Analytics с помощью Azure PowerShell | Документация Майкрософт"
description: "Узнайте, как управлять учетными записями, источниками данных, заданиями и элементами каталога Data Lake Analytics. "
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
ms.openlocfilehash: 862e9551f1e129b7bba06651fbae94e337c92dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="f2d6f-103">Управление аналитикой озера данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2d6f-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="f2d6f-104">Узнайте, как управлять учетными записями, источниками данных, заданиями и элементами каталога Azure Data Lake Analytics с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f2d6f-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2d6f-105">Prerequisites</span></span>

<span data-ttu-id="f2d6f-106">При создании учетной записи Data Lake Analytics необходимо знать следующее:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-106">When creating a Data Lake Analytics account, you need to know:</span></span>

* <span data-ttu-id="f2d6f-107">**Идентификатор подписки** — идентификатор подписки Azure, в которую входит ваша учетная запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-107">**Subscription ID**: The Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="f2d6f-108">**Группа ресурсов** — имя группы ресурсов Azure, содержащей учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-108">**Resource group**: The name of the Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="f2d6f-109">**Имя учетной записи Data Lake Analytics** — имя учетной записи должно содержать только буквы в нижнем регистре и цифры.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-109">**Data Lake Analytics account name**: The account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="f2d6f-110">**Учетная запись Data Lake Store по умолчанию** — каждая учетная запись Data Lake Analytics содержит учетную запись Data Lake Store по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="f2d6f-111">Эти учетные записи должны находиться в одном расположении.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-111">These accounts must be in the same location.</span></span>
* <span data-ttu-id="f2d6f-112">**Расположение** — расположение учетной записи Data Lake Analytics, например "Восточная часть США 2" или другое поддерживаемое расположение.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-112">**Location**: The location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="f2d6f-113">Поддерживаемые расположения можно просмотреть на [странице с расценками](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="f2d6f-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="f2d6f-114">Во фрагментах кода PowerShell в этом руководстве для хранения такой информации используются следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-114">The PowerShell snippets in this tutorial use these variables to store this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="f2d6f-115">Вход в систему</span><span class="sxs-lookup"><span data-stu-id="f2d6f-115">Log in</span></span>

<span data-ttu-id="f2d6f-116">Вход с помощью идентификатора подписки.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="f2d6f-117">Вход с помощью имени подписки.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="f2d6f-118">При использовании командлета `Login-AzureRmAccount` всегда запрашиваются учетные данные.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-118">The `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="f2d6f-119">Избежать появления запроса можно с помощью следующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-119">You can avoid being prompted by using the following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="f2d6f-120">Управление учетными записями</span><span class="sxs-lookup"><span data-stu-id="f2d6f-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="f2d6f-121">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="f2d6f-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="f2d6f-122">Если у вас еще нет [группы ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups), создайте ее.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) to use, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="f2d6f-123">Для каждой учетной записи Data Lake Analytics необходима учетная запись Data Lake Store по умолчанию, которая используется для хранения журналов.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="f2d6f-124">Можно повторно использовать существующую учетную запись или создать новую.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="f2d6f-125">После создания группы ресурсов и учетной записи Data Lake Store создайте учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="f2d6f-126">Получение сведений об учетной записи</span><span class="sxs-lookup"><span data-stu-id="f2d6f-126">Get information about an account</span></span>

<span data-ttu-id="f2d6f-127">Получение сведений об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="f2d6f-128">Проверка наличия конкретной учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-128">Check the existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="f2d6f-129">Командлет возвращает `True` или `False`.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-129">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="f2d6f-130">Проверка наличия конкретной учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-130">Check the existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="f2d6f-131">Командлет возвращает `True` или `False`.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-131">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="f2d6f-132">Получение списка учетных записей</span><span class="sxs-lookup"><span data-stu-id="f2d6f-132">Listing accounts</span></span>

<span data-ttu-id="f2d6f-133">Вывод списка учетных записей Data Lake Analytics в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-133">List Data Lake Analytics accounts within the current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="f2d6f-134">Вывод списка учетных записей Data Lake Analytics в конкретной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="f2d6f-135">Управление правилами брандмауэра</span><span class="sxs-lookup"><span data-stu-id="f2d6f-135">Managing firewall rules</span></span>

<span data-ttu-id="f2d6f-136">Вывод списка правил брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="f2d6f-137">Добавление правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="f2d6f-138">Изменение правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="f2d6f-139">Удаление правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="f2d6f-140">Разрешение IP-адресов Azure.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="f2d6f-141">Управление источниками данных</span><span class="sxs-lookup"><span data-stu-id="f2d6f-141">Managing data sources</span></span>
<span data-ttu-id="f2d6f-142">Azure Data Lake Analytics в настоящее время поддерживает следующие источники данных:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-142">Azure Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="f2d6f-143">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="f2d6f-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="f2d6f-144">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="f2d6f-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="f2d6f-145">При создании учетной записи Analytics необходимо указать учетную запись Data Lake Store в качестве источника данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-145">When you create an Analytics account, you must designate a Data Lake Store account to be the default data source.</span></span> <span data-ttu-id="f2d6f-146">Учетная запись хранения озера данных по умолчанию используется для хранения метаданных задания и журналов аудита задания.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-146">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="f2d6f-147">После создания учетной записи Data Lake Analytics можно добавить дополнительные учетные записи Data Lake Store и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-the-default-data-lake-store-account"></a><span data-ttu-id="f2d6f-148">Поиск учетной записи хранения озера данных по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f2d6f-148">Find the default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="f2d6f-149">Чтобы найти учетную запись по умолчанию для Data Lake Store, отфильтруйте список источников данных по свойству `IsDefault`:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-149">You can find the default Data Lake Store account by filtering the list of datasources by the `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="f2d6f-150">Добавление источника данных</span><span class="sxs-lookup"><span data-stu-id="f2d6f-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="f2d6f-151">Получение списка источников данных</span><span class="sxs-lookup"><span data-stu-id="f2d6f-151">List data sources</span></span>

```powershell
# List all the data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="f2d6f-152">Отправка заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="f2d6f-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="f2d6f-153">Отправка строки как скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="f2d6f-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="f2d6f-154">Отправка файла как скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="f2d6f-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="f2d6f-155">Получение списка заданий в учетной записи</span><span class="sxs-lookup"><span data-stu-id="f2d6f-155">List jobs in an account</span></span>

### <a name="list-all-the-jobs-in-the-account"></a><span data-ttu-id="f2d6f-156">Откройте список всех заданий в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-156">List all the jobs in the account.</span></span> 

<span data-ttu-id="f2d6f-157">Результаты включают в себя текущие и недавно завершенные задания.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-157">The output includes the currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="f2d6f-158">Получение списка определенного числа заданий</span><span class="sxs-lookup"><span data-stu-id="f2d6f-158">List a specific number of jobs</span></span>

<span data-ttu-id="f2d6f-159">По умолчанию список заданий сортируется по времени отправки.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-159">By default the list of jobs is sorted on submit time.</span></span> <span data-ttu-id="f2d6f-160">Поэтому в его начале находятся последние отправленные задания.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-160">So the most recently submitted jobs appear first.</span></span> <span data-ttu-id="f2d6f-161">По умолчанию в учетной записи ADLA сохраняются сведения о заданиях за 180 дней, но командлет Ge-AdlJob по умолчанию возвращает только первые 500 заданий.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-161">By default, The ADLA account remembers jobs for 180 days, but the Ge-AdlJob  cmdlet by default returns only the first 500.</span></span> <span data-ttu-id="f2d6f-162">Чтобы получить список определенного количества заданий, используйте параметр -Top.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-162">Use -Top parameter to list a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-the-value-of-job-property"></a><span data-ttu-id="f2d6f-163">Получение списка заданий на основе значения свойства задания</span><span class="sxs-lookup"><span data-stu-id="f2d6f-163">List jobs based on the value of job property</span></span>

<span data-ttu-id="f2d6f-164">Использование параметра `-State`.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-164">Using the `-State` parameter.</span></span> <span data-ttu-id="f2d6f-165">Вы можете использовать любое сочетание следующих значений:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-165">You can combine any of these values:</span></span>

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
# List the running jobs
Get-AdlJob -Account $adla -State Running

# List the jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List the jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="f2d6f-166">Используйте параметр `-Result`, чтобы определить, успешно ли выполнено завершенное задание.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-166">Use the `-Result` parameter to detect whether ended jobs completed successfully.</span></span> <span data-ttu-id="f2d6f-167">Возможны следующие значения:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-167">It has these values:</span></span>

* <span data-ttu-id="f2d6f-168">Отменено</span><span class="sxs-lookup"><span data-stu-id="f2d6f-168">Cancelled</span></span>
* <span data-ttu-id="f2d6f-169">Сбой</span><span class="sxs-lookup"><span data-stu-id="f2d6f-169">Failed</span></span>
* <span data-ttu-id="f2d6f-170">None</span><span class="sxs-lookup"><span data-stu-id="f2d6f-170">None</span></span>
* <span data-ttu-id="f2d6f-171">Успешно</span><span class="sxs-lookup"><span data-stu-id="f2d6f-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="f2d6f-172">Параметр `-Submitter` позволяет определить, кто отправил это задание.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-172">The `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="f2d6f-173">Параметр `-SubmittedAfter` используется для фильтрации по диапазону времени.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-173">The `-SubmittedAfter` is useful in filtering to a time range.</span></span>


```powershell
# List  jobs submitted in the last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in the last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="f2d6f-174">Распространенные сценарии для получения списка заданий</span><span class="sxs-lookup"><span data-stu-id="f2d6f-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in the last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within the past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="f2d6f-175">Фильтрация списка заданий</span><span class="sxs-lookup"><span data-stu-id="f2d6f-175">Filtering a list of jobs</span></span>

<span data-ttu-id="f2d6f-176">После получения списка заданий в текущем сеансе PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2d6f-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="f2d6f-177">можно использовать стандартные командлеты PowerShell для фильтрации этого списка.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-177">You can use normal PowerShell cmdlets to filter the list.</span></span>

<span data-ttu-id="f2d6f-178">Фильтрация заданий, отправленных за последние 24 часа</span><span class="sxs-lookup"><span data-stu-id="f2d6f-178">Filter a list of jobs to the jobs submitted in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="f2d6f-179">Фильтрация заданий, завершенных за последние 24 часа</span><span class="sxs-lookup"><span data-stu-id="f2d6f-179">Filter a list of jobs to the jobs that ended in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="f2d6f-180">Фильтрация заданий, выполнение которых началось.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-180">Filter a list of jobs to the jobs that started running.</span></span> <span data-ttu-id="f2d6f-181">Задание может завершиться сбоем во время компиляции и поэтому никогда не запускаться.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="f2d6f-182">Давайте просмотрим невыполненные задания, выполнение которых началось, но затем завершилось из-за сбоя.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-182">Let's look at the failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="f2d6f-183">Анализ списка заданий</span><span class="sxs-lookup"><span data-stu-id="f2d6f-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="f2d6f-184">Для анализа списка заданий используйте командлет `Group-Object`.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-184">Use the `Group-Object` cmdlet to analyze a list of jobs.</span></span>

```
# Count the number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count the number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count the number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count the number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="f2d6f-185">При проведении анализа может быть полезно добавить свойства в объекты Job, чтобы упростить фильтрацию и группировку.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-185">When performing an analysis, it can be useful to add properties to the Job objects to make filtering and grouping simpler.</span></span> <span data-ttu-id="f2d6f-186">В приведенном ниже фрагменте кода показано, как добавить вычисляемые свойства к JobInfo.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-186">The following  snippet shows how to annotate a JobInfo with calculated properties.</span></span>

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

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="f2d6f-187">Получение сведений о конвейерах и повторениях</span><span class="sxs-lookup"><span data-stu-id="f2d6f-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="f2d6f-188">Используйте командлет `Get-AdlJobPipeline`, чтобы получить сведения о конвейерах для ранее отправленных заданий.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-188">Use the `Get-AdlJobPipeline` cmdlet to see the pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="f2d6f-189">Используйте командлет `Get-AdlJobRecurrence`, чтобы получить сведения о повторениях для ранее отправленных заданий.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-189">Use the `Get-AdlJobRecurrence` cmdlet to see the recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="f2d6f-190">Получение информации о задании</span><span class="sxs-lookup"><span data-stu-id="f2d6f-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="f2d6f-191">Получение состояния задания</span><span class="sxs-lookup"><span data-stu-id="f2d6f-191">Get job status</span></span>

<span data-ttu-id="f2d6f-192">Получите состояние конкретного задания.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-192">Get the status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-the-job-outputs"></a><span data-ttu-id="f2d6f-193">Изучение выходных данных задания</span><span class="sxs-lookup"><span data-stu-id="f2d6f-193">Examine the job outputs</span></span>

<span data-ttu-id="f2d6f-194">По завершении задания проверьте, существует ли выходной файл, открыв список файлов в папке.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-194">After the job has ended, check if the output file exists by listing the files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="f2d6f-195">Управление выполнением заданий</span><span class="sxs-lookup"><span data-stu-id="f2d6f-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="f2d6f-196">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="f2d6f-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-to-finish"></a><span data-ttu-id="f2d6f-197">Ожидание завершения задания</span><span class="sxs-lookup"><span data-stu-id="f2d6f-197">Wait for a job to finish</span></span>

<span data-ttu-id="f2d6f-198">Вместо того чтобы повторно выполнять `Get-AdlAnalyticsJob`, пока задание не завершится, можно использовать командлет `Wait-AdlJob`, чтобы дождаться завершения задания.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use the `Wait-AdlJob` cmdlet to wait for the job to end.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="f2d6f-199">Управление политиками вычислений</span><span class="sxs-lookup"><span data-stu-id="f2d6f-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="f2d6f-200">Список существующих политик вычислений</span><span class="sxs-lookup"><span data-stu-id="f2d6f-200">List existing compute policies</span></span>

<span data-ttu-id="f2d6f-201">Командлет `Get-AdlAnalyticsComputePolicy` извлекает информацию о политиках вычислений для учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-201">The `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="f2d6f-202">Создание политики вычислений</span><span class="sxs-lookup"><span data-stu-id="f2d6f-202">Create a compute policy</span></span>

<span data-ttu-id="f2d6f-203">Командлет `New-AdlAnalyticsComputePolicy` создает новую политику вычислений для учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-203">The `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="f2d6f-204">Этот пример устанавливает для указанного пользователя максимальное количество единиц аналитики (50) и минимальный приоритет задания (250).</span><span class="sxs-lookup"><span data-stu-id="f2d6f-204">This example sets  the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-the-existence-of-a-file"></a><span data-ttu-id="f2d6f-205">Проверьте наличие файла.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-205">Check for the existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="f2d6f-206">Отправка и скачивание</span><span class="sxs-lookup"><span data-stu-id="f2d6f-206">Uploading and downloading</span></span>

<span data-ttu-id="f2d6f-207">Отправка файла.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="f2d6f-208">Рекурсивная отправка всей папки.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="f2d6f-209">Скачивание файла.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="f2d6f-210">Рекурсивное скачивание всей папки.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="f2d6f-211">Если процесс отправки или скачивания прервался, вы можете попытаться возобновить его, выполнив командлет еще раз с флагом ``-Resume``.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-211">If the upload or download process is interrupted, you can attempt to resume the process by running the cmdlet again with the ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="f2d6f-212">Управление элементами каталога</span><span class="sxs-lookup"><span data-stu-id="f2d6f-212">Manage catalog items</span></span>

<span data-ttu-id="f2d6f-213">Каталог U-SQL используется для структурирования данных и кода, чтобы их могли совместно использовать сценарии U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-213">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="f2d6f-214">Каталог обеспечивает максимальную производительность, возможную с данными в озере данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-214">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="f2d6f-215">Дополнительные сведения см. в разделе [Использование каталога U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="f2d6f-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-the-u-sql-catalog"></a><span data-ttu-id="f2d6f-216">Получение списка элементов в каталоге U-SQL</span><span class="sxs-lookup"><span data-stu-id="f2d6f-216">List items in the U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="f2d6f-217">Получение списка всех сборок во всех базах данных в учетной записи ADLA.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-217">List all the assemblies in all the databases in an ADLA Account.</span></span>

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

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="f2d6f-218">Получение сведений об элементе каталога</span><span class="sxs-lookup"><span data-stu-id="f2d6f-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="f2d6f-219">Создание учетных данных в каталоге</span><span class="sxs-lookup"><span data-stu-id="f2d6f-219">Create credentials in a catalog</span></span>

<span data-ttu-id="f2d6f-220">В базе данных U-SQL создайте объект учетных данных для базы данных, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="f2d6f-221">В настоящее время учетные данные U-SQL — это единственный тип элементов каталога, который можно создавать с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-221">Currently, U-SQL credentials are the only type of catalog item that you can create through PowerShell.</span></span>

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

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="f2d6f-222">Получение основных сведений об учетной записи ADLA</span><span class="sxs-lookup"><span data-stu-id="f2d6f-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="f2d6f-223">Приведенный ниже код выполняет поиск основных сведений об учетной записи, указанной по имени.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-223">Given an account name, the following code looks up basic information about the account</span></span>

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

## <a name="working-with-azure"></a><span data-ttu-id="f2d6f-224">Работа с Azure</span><span class="sxs-lookup"><span data-stu-id="f2d6f-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="f2d6f-225">Получение сведений об ошибках AzureRm</span><span class="sxs-lookup"><span data-stu-id="f2d6f-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="f2d6f-226">Проверка выполнения с правами администратора</span><span class="sxs-lookup"><span data-stu-id="f2d6f-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="f2d6f-227">Поиск TenantID</span><span class="sxs-lookup"><span data-stu-id="f2d6f-227">Find a TenantID</span></span>

<span data-ttu-id="f2d6f-228">По имени подписки:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="f2d6f-229">По идентификатору подписки:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="f2d6f-230">По адресу домена, например contoso.com:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="f2d6f-231">Получение списка всех подписок и идентификаторов клиентов</span><span class="sxs-lookup"><span data-stu-id="f2d6f-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="f2d6f-232">Создание учетной записи Data Lake Analytics с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="f2d6f-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="f2d6f-233">Вы также можете использовать шаблон группы ресурсов Azure с помощью следующего скрипта PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f2d6f-233">You can also use an Azure Resource Group template using the following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update the JSON template path 

# Log in to Azure
Login-AzureRmAccount -SubscriptionId $subId

# Create the resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create the Data Lake Analytics account with the default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="f2d6f-234">Дополнительные сведения см. в разделах [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) (Развертывание приложения с использованием шаблона Azure Resource Manager) и [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f2d6f-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="f2d6f-235">**Пример шаблона**</span><span class="sxs-lookup"><span data-stu-id="f2d6f-235">**Example template**</span></span>

<span data-ttu-id="f2d6f-236">Сохраните приведенный ниже текст в файле `.json`, а затем воспользуйтесь предыдущим скриптом PowerShell для применения шаблона.</span><span class="sxs-lookup"><span data-stu-id="f2d6f-236">Save the following text as a `.json` file, and then use the preceding PowerShell script to use the template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Analytics account to create."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Store account to create."
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

## <a name="next-steps"></a><span data-ttu-id="f2d6f-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f2d6f-237">Next steps</span></span>
* [<span data-ttu-id="f2d6f-238">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f2d6f-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="f2d6f-239">Начало работы с Data Lake Analytics с помощью [портала Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="f2d6f-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="f2d6f-240">Управление Azure Data Lake Analytics с помощью [портала Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f2d6f-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
