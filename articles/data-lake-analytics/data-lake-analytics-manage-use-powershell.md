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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Управление аналитикой озера данных Azure с помощью Azure PowerShell
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Узнайте, как учетные записи аналитики Озера данных Azure toomanage, источники данных, заданий и элементов каталога, с помощью Azure PowerShell. 

## <a name="prerequisites"></a>Предварительные требования

При создании учетной записи аналитики Озера данных необходимо tooknow:

* **Идентификатор подписки**: hello идентификатор подписки Azure, в котором находится ваша учетная запись аналитики Озера данных.
* **Группа ресурсов**: hello имя группы ресурсов Azure hello, содержащую учетную запись аналитики Озера данных.
* **Имя учетной записи аналитики Озера данных**: hello учетной записи, имя должно содержать только строчные буквы и цифры.
* **Учетная запись Data Lake Store по умолчанию** — каждая учетная запись Data Lake Analytics содержит учетную запись Data Lake Store по умолчанию. Эти учетные записи должны быть в hello местоположения.
* **Расположение**: hello расположение учетной записи аналитики Озера данных, например, «Восточная часть США 2», или другими поддерживается расположения. Поддерживаемые расположения можно просмотреть на [странице с расценками](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

фрагменты кода PowerShell Hello в этом учебнике эти сведения можно использовать эти переменные toostore

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Вход в систему

Вход с помощью идентификатора подписки.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Вход с помощью имени подписки.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Hello `Login-AzureRmAccount` командлет всегда запрашивает учетные данные. Чтобы избежать многократных запросов с помощью следующих командлетов hello.

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Управление учетными записями

### <a name="create-a-data-lake-analytics-account"></a>Создание учетной записи аналитики озера данных

Если у вас еще нет [группы ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, создайте его. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Для каждой учетной записи Data Lake Analytics необходима учетная запись Data Lake Store по умолчанию, которая используется для хранения журналов. Можно повторно использовать существующую учетную запись или создать новую. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

После создания группы ресурсов и учетной записи Data Lake Store создайте учетную запись Data Lake Analytics.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Получение сведений об учетной записи

Получение сведений об учетной записи.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Проверьте существование hello определенной учетной записи аналитики Озера данных. Hello командлет возвращает либо `True` или `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Проверьте существование hello определенной учетной записи хранилища Озера данных. Hello командлет возвращает либо `True` или `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Получение списка учетных записей

Учетные записи аналитики Озера данных списка в текущей подписке hello.

```powershell
Get-AdlAnalyticsAccount
```

Вывод списка учетных записей Data Lake Analytics в конкретной группе ресурсов.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Управление правилами брандмауэра

Вывод списка правил брандмауэра.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Добавление правила брандмауэра.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Изменение правила брандмауэра.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Удаление правила брандмауэра.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Разрешение IP-адресов Azure.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Управление источниками данных
Azure аналитики Озера данных в настоящее время поддерживает следующие источники данных hello:

* [Хранилище озера данных Azure](../data-lake-store/data-lake-store-overview.md)
* [Хранилище Azure](../storage/common/storage-introduction.md)

При создании учетной записи аналитики, необходимо назначить хранилище Озера данных учетной записи toobe hello источник данных по умолчанию. Hello учетной записи хранилища Озера данных по умолчанию используется toostore метаданные задания и задания журналы аудита. После создания учетной записи Data Lake Analytics можно добавить дополнительные учетные записи Data Lake Store и учетные записи хранения. 

### <a name="find-hello-default-data-lake-store-account"></a>Найти учетную запись хранилища Озера данных по умолчанию hello

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

Учетная запись хранилища Озера данных по умолчанию hello можно найти с помощью фильтрации по hello hello список источников данных `IsDefault` свойство:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Добавление источника данных

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Получение списка источников данных

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>Отправка заданий U-SQL

### <a name="submit-a-string-as-a-u-sql-script"></a>Отправка строки как скрипта U-SQL

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


### <a name="submit-a-file-as-a-u-sql-script"></a>Отправка файла как скрипта U-SQL

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Получение списка заданий в учетной записи

### <a name="list-all-hello-jobs-in-hello-account"></a>Список всех заданий hello в учетной записи hello. 

Вывод Hello включает hello выполняющихся заданий и задания, которые недавно завершена.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>Получение списка определенного числа заданий

По умолчанию они сортируются hello список заданий на время отправки. Поэтому hello последней отправки заданий отображаются первыми. По умолчанию hello учетной записи ADLA запоминает заданий на 180 дней, но hello Ge AdlJob командлет по умолчанию возвращает hello только первые 500. Используйте параметр - Top параметр toolist ряд заданий.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Список заданий, на основе значения hello свойства задания

С помощью hello `-State` параметра. Вы можете использовать любое сочетание следующих значений:

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

Используйте hello `-Result` toodetect параметр завершились ли задания завершается успешно. Возможны следующие значения:

* Отменено
* Сбой
* None
* Успешно

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Hello `-Submitter` параметр помогает определить, кто отправил задание.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Hello `-SubmittedAfter` полезно при фильтрации tooa диапазон времени.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>Распространенные сценарии для получения списка заданий


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

## <a name="filtering-a-list-of-jobs"></a>Фильтрация списка заданий

После получения списка заданий в текущем сеансе PowerShell Можно использовать обычный список hello toofilter PowerShell командлеты.

Фильтр списка заданий toohello заданий, поступающими в hello последние 24 часа

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Фильтровать список заданий toohello заданий, завершившихся hello последние 24 часа

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Фильтрация списка заданий toohello заданий, которые была запущена. Задание может завершиться сбоем во время компиляции и поэтому никогда не запускаться. Давайте рассмотрим hello сбой задания, которые фактически запущен и завершилась неуспешно.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>Анализ списка заданий

Используйте hello `Group-Object` tooanalyze командлет список заданий.

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
Выполнения анализа, бывает полезно tooadd свойства toohello задания объектов toomake фильтрацию и группирование проще. Следующий фрагмент кода Hello показывает способ tooannotate a JobInfo с вычисления свойства.

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

## <a name="get-information-about-pipelines-and-recurrences"></a>Получение сведений о конвейерах и повторениях

Используйте hello `Get-AdlJobPipeline` командлет toosee hello конвейера ранее отправлять данные задания.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Используйте hello `Get-AdlJobRecurrence` командлет toosee hello повторений для ранее отправленные задания.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Получение информации о задании

### <a name="get-job-status"></a>Получение состояния задания

Получите состояние hello определенного задания.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Проверьте в выходных данных задания hello

После завершения задания hello проверяет, существует ли hello выходной файл, указав hello файлов в папке.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Управление выполнением заданий

### <a name="cancel-a-job"></a>Отмена задания

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Дождитесь toofinish задания

Вместо того чтобы повторять `Get-AdlAnalyticsJob` до завершения задания, можно использовать hello `Wait-AdlJob` toowait командлет для задания tooend hello.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>Управление политиками вычислений

### <a name="list-existing-compute-policies"></a>Список существующих политик вычислений

Hello `Get-AdlAnalyticsComputePolicy` командлет извлекает сведения о политиках вычислений для учетной записи аналитики Озера данных.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Создание политики вычислений

Hello `New-AdlAnalyticsComputePolicy` создает новую политику вычислений для учетной записи аналитики Озера данных. В этом примере, что наборы hello максимальной доступной toohello Сиднейское указан too50 пользователя и too250 приоритет задания минимального hello.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Проверьте наличие файла hello.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Отправка и скачивание

Отправка файла.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Рекурсивная отправка всей папки.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Скачивание файла.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Рекурсивное скачивание всей папки.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Если hello отправки или загрузки процесс прерывается, может попытаться выполнить процесс hello tooresume выполнение hello командлет еще раз с hello ``-Resume`` флаг.

## <a name="manage-catalog-items"></a>Управление элементами каталога

каталог Hello U-SQL является toostructure используемых данных и кода, поэтому они могут совместно использоваться сценарии U-SQL. Hello каталога включает hello максимально возможную производительность с данными в Озера данных Azure. Дополнительные сведения см. в разделе [Использование каталога U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-items-in-hello-u-sql-catalog"></a>Элементы списка в каталоге hello U-SQL

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Список всех сборок hello во всех базах данных hello ADLA учетную запись.

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

### <a name="get-details-about-a-catalog-item"></a>Получение сведений об элементе каталога

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Создание учетных данных в каталоге

В базе данных U-SQL создайте объект учетных данных для базы данных, размещенной в Azure. В настоящее время U-SQL учетных данных — единственный тип hello элемента каталога, которые можно создавать с помощью PowerShell.

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

### <a name="get-basic-information-about-an-adla-account"></a>Получение основных сведений об учетной записи ADLA

Данное имя учетной записи после кода hello ищет основные сведения об учетной записи hello

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

## <a name="working-with-azure"></a>Работа с Azure

### <a name="get-details-of-azurerm-errors"></a>Получение сведений об ошибках AzureRm

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Проверка выполнения с правами администратора

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Поиск TenantID

По имени подписки:

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

По идентификатору подписки:

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

По адресу домена, например contoso.com:


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Получение списка всех подписок и идентификаторов клиентов

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Создание учетной записи Data Lake Analytics с помощью шаблона

Можно также использовать шаблон группы ресурсов Azure, используя hello следующий сценарий PowerShell:

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

Дополнительные сведения см. в разделах [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) (Развертывание приложения с использованием шаблона Azure Resource Manager) и [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

**Пример шаблона**

Сохраните следующий текст в виде hello `.json` файл, а затем использовать hello, предшествующий шаблон hello toouse скрипта PowerShell. 

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

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
* Начало работы с Data Lake Analytics с помощью [портала Azure](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)
* Управление Azure Data Lake Analytics с помощью [портала Azure](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 
