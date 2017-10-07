---
title: "PowerShell: создание эластичного пула SQL Azure и управление им | Документация Майкрософт"
description: "Узнайте, как toomanage toouse PowerShell эластичного пула."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Создание эластичного пула и управление им с помощью PowerShell
В этом разделе показано, как toocreate и управления ими масштабируемой [эластичные пулы](sql-database-elastic-pool.md) с помощью PowerShell.  Можно также создать и управлять Azure эластичного пула, с помощью hello [портал Azure](https://portal.azure.com/), REST API или [C#](sql-database-elastic-pool-manage-csharp.md). Вы также можете использовать [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), чтобы создавать новые базы данных в эластичных пулах и перемещать базы данных в пулы и обратно.

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Создание эластичного пула
Hello [New AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) создает пул эластичных БД. значения Hello eDTU на пул, min и max Dtu, ограничены hello значение уровня службы (Basic, Standard, Premium или Premium RS). См. раздел [eDTU и размеры хранилища для пулов эластичных БД](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Создание базы данных внутри эластичного пула
Используйте hello [New AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) командлета и набор hello **ElasticPoolName** параметр toohello целевой пул. toomove существующей базы данных в эластичный пул, в разделе [перемещение базы данных в эластичный пул](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Полный скрипт
Этот скрипт создает группу ресурсов Azure и сервер. При появлении запроса укажите имя пользователя администратора и пароль для нового сервера hello (не учетные данные Azure).

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Создание эластичного пула и добавление нескольких баз данных в пул
Создание много баз данных в пуле эластичных БД может занять время после завершения с помощью портала hello или командлеты PowerShell, одновременно создать только одну базу данных. Создание tooautomate в пуле эластичных БД. в разделе [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Перемещение базы данных в пул эластичных БД
Можно переместить базу данных в таблицу или из пула эластичных БД с hello [AzureRmSqlDatabase набор](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Изменение параметров производительности эластичного пула
Если производительность снижается, можно изменять параметры hello hello пула tooaccommodate роста. Используйте hello [AzureRmSqlElasticPool набор](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) командлета. Задайте параметр toohello hello - Dtu edtu, которое каждого пула. Возможные значения приведены в разделе [eDTU и размеры хранилища для эластичных баз данных и пулов эластичных баз данных](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>Изменить ограничение hello хранилища для эластичного пула

Используйте hello [AzureRmSqlElasticPool набор](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) hello командлет tooset _- StorageMB_ параметра. Укажите максимальный объем дискового пространства hello в МБ (например, 2097152 наборы hello хранилища ограничение too2 ТБ). Возможные значения приведены в разделе [eDTU и размеры хранилища для эластичных баз данных и пулов эластичных баз данных](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

> [!IMPORTANT]
> хранилища данных max по умолчанию Hello в пул для пулов Premium с edtu, которое 1500 доступна 750 ГБ. выше hello tooobtain _максимальный размер хранилища данных на пул_, необходимо явно задать ограничение хранилища hello. Пулы Premium с более 750 ГБ хранилища находится в общедоступной предварительной версии в hello следующие области: восточная часть США 2, Запад США, Вирджиния государственных организаций США, Западной Европе, Германия центра, Юго-Восточная Азия, восток Японии, Восточная Австралия, Канады центра и Восточная Канада.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Получить состояние операции пула hello
Создание эластичного пула может занять некоторое время. состояние пула операций, включая создание и обновления, используйте hello hello tootrack [Get AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) командлета.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Получить состояние hello переход базы данных в пуле эластичных БД
На перемещение базы данных может потребоваться время. Отслеживать состояние перемещения, с помощью hello [Get AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) командлета.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Получение данных об использовании ресурсов в эластичном пуле
Метрики, которые могут быть получены как процент от максимального пула ресурсов hello:

| Имя метрики | Описание |
|:--- |:--- |
| cpu\_percent |Среднее вычислительной мощности в процентах от предела hello hello пула. |
| physical\_data\_read\_percent |Среднее использование операций ввода-вывода в процентах от предела hello hello пула. |
| log\_write\_percent |Среднее использование ресурсов записи в процентах от предела hello hello пула. |
| DTU\_consumption\_percent |Использование среднего eDTU в процентах от предела eDTU hello в пуле |
| storage\_percent |Среднее использование хранилища в процентах от hello ограничение хранилища пула hello. |
| workers\_percent |Максимальная одновременных рабочих процессов (запросов) в процентах от предела hello hello пула. |
| sessions\_percent |Максимальное число одновременных сеансов в процентах от предела hello hello пула. |
| eDTU_limit |Текущее максимальное значение параметра DTU для этого пула эластичных БД в течение этого интервала. |
| storage\_limit |Текущее максимальное значение размера хранилища в мегабайтах для этого пула эластичных БД в течение этого интервала. |
| eDTU\_used |Среднее число Edtu, занятый пулом hello в этот промежуток времени. |
| storage\_used |Среднее хранилища, используемый пулом hello в этот промежуток времени, в байтах |

**Детализация показателей и сроки хранения:**

* Детализация данных с точностью до 5 минут.  
* Срок хранения данных — 35 дней.  

Этот командлет и API ограничивает hello число строк, которые могут быть извлечены в одном вызове too1000 строк (около 3 дня данных на уровне гранулярности 5 минут). Эта команда может вызываться несколько раз с tooretrieve интервалы времени различных начала и окончания больше данных, но

метрики tooretrieve hello.

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Получение данных об использовании ресурсов для базы данных в эластичном пуле
Эти API-интерфейсы так же, как hello API, используемые для наблюдения за использованием ресурсов hello одной базы данных, за исключением следующих семантической разницы hello hello: получить метрики выраженное в процентах hello на максимальное число Edtu базы данных (или эквивалентный cap для hello основной метрики, как ЦП или ввода-ВЫВОДА) установить для этого пула. Например 50% использования любой из этих метрик указывает конкретный ресурс потребления hello 50% от hello лимит cap базы данных для этого ресурса в hello родительского пула.

метрики tooretrieve hello.

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Добавление оповещений tooan эластичного пула ресурсов
Можно добавить правила оповещения toosend эластичного пула tooan уведомления по электронной почте или создание предупреждений строки слишком[конечные точки URL-адрес](https://msdn.microsoft.com/library/mt718036.aspx) при эластичного пула hello достигает порогового значения использования, можно настроить. С помощью командлета Add-AzureRmMetricAlertRule hello.

> [!IMPORTANT]
> Для данных мониторинга использования ресурсов в эластичных пулах задержка как минимум 5 минут является нормальной. Настройка интервала менее 10 минут для оповещений об эластичных пулах сейчас не поддерживается. Все оповещения, заданных для эластичных пулов с периодом (параметр с именем «-WindowSize» в PowerShell API) меньше, чем 10 минут может не запуститься. Проследите, чтобы во всех оповещениях, определяемых для эластичных пулов, использовался интервал (WindowSize) не менее 10 минут.
>
>

Этот пример добавляет оповещение, уведомляющее, когда потребление eDTU в эластичном пуле выходит за пределы определенного порогового значения.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

Дополнительные сведения см. в статье [Создание оповещений для базы данных SQL Azure с помощью портала Azure](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Добавлять базы данных tooall оповещения в пуле эластичных БД
Можно добавить правила оповещения tooall базы данных в эластичный пул toosend уведомления по электронной почте или предупреждения строки слишком[конечные точки URL-адрес](https://msdn.microsoft.com/library/mt718036.aspx) когда ресурс достигает порогового значения использования настроить предупреждения hello.

> [!IMPORTANT]
> Для данных мониторинга использования ресурсов в эластичных пулах задержка как минимум 5 минут является нормальной. Настройка интервала менее 10 минут для оповещений об эластичных пулах сейчас не поддерживается. Все оповещения, заданных для эластичных пулов с периодом (параметр с именем «-WindowSize» в PowerShell API) меньше, чем 10 минут может не запуститься. Проследите, чтобы во всех оповещениях, определяемых для эластичных пулов, использовался интервал (WindowSize) не менее 10 минут.
>

Этот пример добавляет предупреждения tooeach hello баз данных в пуле эластичных БД для получения уведомления, когда потребления DTU в этой базе данных выходит за пределы определенного порогового значения.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Сбор и отслеживание данных об использовании ресурсов для нескольких пулов в подписке
Когда имеется несколько баз данных в подписке, это сложно toomonitor каждого гибкому пул отдельно. Вместо этого командлеты PowerShell для базы данных SQL и запросами T-SQL могут быть toocollect объединенных данных об использовании ресурсов несколько пулов и их базы данных для мониторинга и анализа использования ресурсов. Объект [образец реализации](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) набора из powershell сценарии можно найти в репозитории примеров hello GitHub SQL Server вместе с документацией на действие и как toouse его.

toouse этот образец реализации, выполните следующие действия.

1. Загрузите hello [сценарии и документация](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Измените скрипты hello для вашей среды. Укажите один или несколько серверов, на которых размещаются пулы эластичных баз данных.
3. Укажите базу данных телеметрии, где hello собранные показатели, toobe хранятся.
4. Настройте hello toospecify сценария hello продолжительность выполнения скриптов hello.

На высоком уровне сценарии hello hello следующие:

* перечисляют все серверы в указанной подписке Azure (или в указанном списке серверов);
* запускают фоновое задание для каждого сервера. Hello задание выполняется в цикле через регулярные интервалы и собирает данные телеметрии для всех пулов hello в hello server. Затем она загружает hello собранные данные в базу данных указанного телеметрии hello.
* Перечисляет список баз данных в каждом пуле toocollect hello базы данных данные об использовании ресурсов. Затем она загружает hello собранные данные в базу данных телеметрии hello.

Hello собранных метрики телеметрии базы данных hello может быть проанализировано toomonitor hello исправности эластичные пулы и hello базы данных в ней. Hello скрипт устанавливает предварительно определенных возвращающей табличное значение функции (TVF) hello метрики телеметрии базы данных toohelp статистические hello для указанного интервала времени. Например, результаты hello возвращающей табличное значение функции можно использовать tooshow «первые N пулах эластичных БД с загрузкой максимального числа eDTU hello в за заданный период времени.» При необходимости использовать аналитические средства, такие как Excel или Power BI tooquery и анализа hello собранных данных.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Пример. Получение метрик потребления ресурсов в эластичном пуле и его базах данных
В этом примере извлекается hello метрики потребления для данного пула эластичных БД и все его базы данных. Собранные данные форматируются и записываются в файл CSV-файл tooa. Hello файл можно просмотреть с помощью Excel.

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a>Задержка операций эластичного пула
* Изменение hello min edtu, которое каждой базы данных или максимальное число Edtu на базу данных обычно завершает более 5 минут.
* Изменение hello число Edtu на пул, зависит от hello общий объем пространства, используемого всех баз данных в пуле hello. Изменение занимает порядка 90 минут или меньше на каждые 100 ГБ. Например если hello общее пространство, занимаемое всех баз данных в пуле hello составляет 200 ГБ, то hello ожидаемого задержка для изменения hello eDTU пула на пул — 3 часа или менее.



## <a name="next-steps"></a>Дальнейшие действия
* [Создать эластичный задания](sql-database-elastic-jobs-overview.md) эластичной заданий позволяют выполняться любое количество баз данных в пуле hello скриптов T-SQL.
* В разделе [горизонтального масштабирования с базой данных SQL Azure](sql-database-elastic-scale-introduction.md): использовать эластичной средства tooscale out, перемещение данных, запроса или создания транзакции.
