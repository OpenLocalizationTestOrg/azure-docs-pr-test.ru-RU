---
title: "данные задержки рейсов aaaAnalyze на Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse один Windows PowerShell скрипт toocreate кластер HDInsight запуска задания Hive, запустите задание Sqoop и удалить кластер hello."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>Анализ данных о задержке рейсов с помощью Hive в HDInsight
Hive предоставляет средства для выполнения заданий Hadoop MapReduce с помощью языка сценариев, аналогичного SQL, под названием *[HiveQL][hadoop-hiveql]*, который применяется для обобщения данных, создания запросов и анализа больших объемов данных.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight под управлением Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement). Инструкции по работе с кластерами под управлением Linux см. в статье [Анализ данных о задержке рейсов с помощью Hive в HDInsight в Linux](hdinsight-analyze-flight-delay-data-linux.md).

Одно из главных преимуществ hello Azure HDInsight — разделение hello хранения данных и вычислений. HDInsight использует для хранения данных хранилище BLOB-объектов Azure. Типичное задание состоит из 3 частей:

1. **Хранение данных в хранилище больших двоичных объектов Azure.**  Например, данные о погодных условиях, данные, получаемые от датчиков, журналы учета сетевой активности и, как в настоящем случае, данные о задержке авиарейсов сохраняются в хранилище больших двоичных объектов Azure.
2. **Выполнение заданий.** Когда данные hello tooprocess времени, запуска сценария Windows PowerShell (или клиентском приложении) toocreate кластер HDInsight выполнения заданий и удалить кластер hello. задания Hello сохранить tooAzure вывод данных хранилища больших двоичных объектов. Hello выходных данных сохраняется даже после удаления кластера hello. Такой подход позволяет платить только за использованные ресурсы.
3. **Извлечение выходных данных hello из хранилища больших двоичных объектов Azure**, или в этом учебнике экспорта базы данных Azure SQL tooan данных hello.

Hello следующей диаграмме показан сценарий hello и структура hello данного учебника:

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

Обратите внимание, что номера hello hello диаграмме соответствуют toohello названия разделов. **M** расшифровывается главный процесс hello. **Объект** расшифровывается hello содержимого в приложение hello.

Hello основной части hello учебника показано, как toouse один Windows PowerShell скрипт tooperform hello следующие задачи:

* Создание кластера HDInsight.
* Выполните задание куста hello кластера toocalculate Средняя задержка в аэропортах. Hello рейса задержки данные хранятся в учетной записи хранилища больших двоичных объектов Azure.
* Запустите Sqoop задания tooexport hello Hive задания вывода tooan базы данных Azure SQL.
* Удаление кластера HDInsight hello.

В приложения hello hello инструкции можно найти для отправки данных задержки рейсов, создание и отправка строку запроса Hive и подготовка базы данных Azure SQL hello задание Sqoop hello.

> [!NOTE]
> Hello действия в этом документе, определенных tooWindows основе кластеров HDInsight. Инструкции по работе с кластерами под управлением Linux см. в статье [Анализ данных о задержке рейсов с помощью Hive в HDInsight](hdinsight-analyze-flight-delay-data-linux.md) (для Linux).

### <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* <seg>
  **Рабочая станция с Azure PowerShell**.</seg>

    > [!IMPORTANT]
    > Поддержка Azure PowerShell для управления ресурсами HDInsight с помощью диспетчера служб Azure (ASM) объявлена **устаревшей** и будет прекращена с 1 января 2017 г. шаги Hello в этот документ используйте hello новые командлеты для HDInsight, работающие с помощью диспетчера ресурсов Azure.
    >
    > Выполните шаги hello в [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello последнюю версию Azure PowerShell. При наличии скриптов, toobe необходимость изменить toouse hello новые дополнительные командлеты для работы с диспетчером ресурсов Azure см. в разделе [tooAzure перенос разработки на основе диспетчера ресурсов средства для кластеров HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) для получения дополнительной информации.

**Файлы, используемые в этом учебнике**

В этом учебнике используется hello производительность на время данных рейса авиакомпании из [исследований и инновационных технологий администрирования, бюро статистики Транспортировка и РИТУ][rita-website].
Копия данных была hello загружен tooan контейнер хранилища больших двоичных объектов Azure с разрешения на доступ к большой двоичный объект открытого hello.
Часть скрипта PowerShell hello данных копируется из hello большой двоичный объект открытого контейнера toohello по умолчанию контейнер больших двоичных объектов кластера. Hello HiveQL сценария можно скопировать toohello же контейнер больших двоичных объектов.
Toolearn как tooyour данных hello tooget "или" отправлять рабочие учетной записи хранилища и как файл, toocreate "или" отправлять hello HiveQL скрипта. в разделе [приложение A](#appendix-a) и [приложении Б](#appendix-b).

Hello следующей таблице перечислены файлы hello, используемые в этом учебнике.

<table border="1">
<tr><th>Файлы</th><th>Описание</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>использовать файл сценария HiveQL Hello задания Hive hello. Этот скрипт был загруженного tooan учетной записи хранилища больших двоичных объектов Azure с hello общего доступа. <a href="#appendix-b">Приложение Б</a> содержит инструкции по подготовке и загрузке файла tooyour собственные Azure BLOB-объектов учетной записи хранения.</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>Входные данные для задания Hive hello. Hello данные были отправленного tooan учетной записи хранилища больших двоичных объектов Azure с hello общего доступа. <a href="#appendix-a">Приложение А</a> имеет инструкции на получение данных hello и передачи hello данных tooyour собственные Azure BLOB-объектов учетной записи хранилища.</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>Hello выходной путь для задания Hive hello. контейнер по умолчанию Hello используется для хранения выходных данных hello.</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>Hello Hive папка состояние задания на контейнер по умолчанию hello.</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>Создание кластера и выполнение заданий Hive и Sqoop
Hadoop MapReduce представляет из себя пакетную обработку данных. Hello большинство toorun экономически эффективным способом задания Hive toocreate кластер состоит из задания hello и удалите hello задание после завершения задания hello. Hello следующий скрипт охватывает весь процесс hello.
Дополнительные сведения о создании кластера HDInsight и выполнении заданий Hive см. в статьях [Создание кластеров Hadoop в HDInsight][hdinsight-provision] и [Использование Hive с HDInsight][hdinsight-use-hive].

**запросы Hive hello toorun по Azure PowerShell**

1. Создать таблицу базы данных и hello Azure SQL для выходных данных задания Sqoop hello с помощью инструкций hello в [приложении C](#appendix-c).
2. Откройте Windows PowerShell ISE и выполните следующий скрипт hello:

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. База данных SQL tooyour подключиться и задержки рейсов среднее по городам в таблице AvgDelays hello:

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>Приложение А передачи рейса задержка данных tooAzure хранилища больших двоичных объектов.
Отправка файла данных hello и файлы сценариев HiveQL hello (см. [приложении Б](#appendix-b)) требует решения некоторых вопросов. Hello идея состоит, файлы данных toostore hello и hello HiveQL файла до создания кластера HDInsight и запуск задания Hive hello. Существует два варианта.

* **Используйте hello же учетную запись хранилища Azure, который будет использоваться кластером HDInsight hello как файловой системы по умолчанию hello.** Так как кластер HDInsight hello будет ключ доступа учетной записи хранения hello, нет необходимости toomake дополнительные изменения.
* **Используйте другую учетную запись хранилища Azure hello HDInsight кластера по умолчанию файловой системы.** Если это так hello, необходимо изменить часть создания hello hello сценарий, найденных в Windows PowerShell [кластера HDInsight, создания и выполнения задания Hive и Sqoop](#runjob) toolink hello учетной записи хранилища, дополнительной учетной записи хранения. Инструкции см. в статье [Создание кластеров Hadoop в HDInsight][hdinsight-provision]. Затем кластер HDInsight Hello знает hello ключ доступа для учетной записи хранилища hello.

> [!NOTE]
> Здравствуйте, путь к хранилищу BLOB-объекта для файла данных закодирована в файле сценария HiveQL hello приветствия. Его следует обновлять соответствующим образом.

**toodownload hello рейса данных**

1. Обзор слишком[исследования и инновационные технологии администрирования бюро статистики Транспортировка][rita-website].
2. На странице приветствия выберите hello следующие значения:

    <table border="1">
    <tr><th>Имя</th><th>Значение</th></tr>
    <tr><td>Фильтр года</td><td>2013 </td></tr>
    <tr><td>Период фильтра</td><td>Январь</td></tr>
    <tr><td>Поля</td><td>*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (очистите остальные поля)</td></tr>
    </table>
3. Щелкните элемент **Скачать**.
4. Распакуйте файл toohello hello **C:\Tutorials\FlightDelay\2013Data** папки. Каждый файл представляет собой CSV-файл и имеет размер около 60 ГБ.
5. Изменение имени toohello файла hello hello месяца с данными для. Например, будет называться hello файл, содержащий данные за январь hello *January.csv*.
6. Повторите шаги 2 и 5 toodownload файл для каждого из hello 12 месяцев в 2013. Вам потребуется как минимум один файл toorun hello учебника.

**tooAzure tooupload hello рейса задержка данных хранилища больших двоичных объектов**

1. Подготовка параметров hello:

    <table border="1">
    <tr><th>Имя переменной</th><th>Примечания</th></tr>
    <tr><td>$storageAccountName</td><td>Здравствуйте, где вы хотите tooupload hello данные учетной записи хранилища Azure.</td></tr>
    <tr><td>$blobContainerName</td><td>Здравствуйте, контейнер больших двоичных объектов, где вы хотите tooupload hello данные.</td></tr>
    </table>
2. Откройте интегрированную среду сценариев Azure PowerShell.
3. Вставьте следующий сценарий в области сценариев hello hello:

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. Нажмите клавишу **F5** toorun hello скрипта.

При выборе другого метода для передачи файлов hello toouse убедитесь, что путь к файлу hello учебники, данных или flightdelay. Hello для доступа к файлам hello используется синтаксис:

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

путь Hello учебники/flightdelay/данные — hello виртуальная папка, созданный при отправке файлов hello. Убедитесь, что присутствует 12 файлов — по одному для каждого месяца.

> [!NOTE]
> Необходимо обновить tooread запроса Hive hello в новом расположении hello.
>
> Необходимо настроить hello контейнера доступа разрешение toobe public или привязать toohello учетной записи хранилища hello кластера HDInsight. В противном случае строка запроса Hive hello не будут файлы данных могут tooaccess hello.

- - -

## <a id="appendix-b"></a>Приложение Б. Создание и загрузка скрипта HiveQL
С помощью Azure PowerShell, можно выполнения нескольких инструкций HiveQL один во время или пакет hello HiveQL инструкции в файл скрипта. В этом разделе показано, как toocreate сценарий HiveQL и передачи hello скрипт tooAzure хранилища больших двоичных объектов с помощью Azure PowerShell. Куст требует toobe сценариев HiveQL hello, хранящиеся в хранилище больших двоичных объектов Azure.

сценарий HiveQL Hello выполнит hello следующее:

1. **Удалить таблицу delays_raw hello**, в случае, если таблица hello уже существует.
2. **Создайте внешнюю таблицу Hive hello delays_raw** указывает место хранения большого двоичного объекта toohello с файлами задержки рейсов hello. Этот запрос задает то, что поля разделяются с помощью "," и что строки завершаются с помощью "\n". Это создает проблему, если значения полей содержать запятые, так как Hive не различает запятую, которая является разделителем полей и один, который является частью значения поля (бывает hello в значения полей для источника\_Город\_имя и DEST\_ Город\_имя). tooaddress hello, этот запрос создает столбцы TEMP toohold данных, который неправильно разбит на столбцы.
3. **Удалить таблицу задержки hello**, в случае, если таблица hello уже существует.
4. **Создание таблицы задержек hello**. Это полезно tooclean hello данные перед дальнейшей обработкой. Этот запрос создает новую таблицу, *задержки*, из таблицы delays_raw hello. Примечание hello TEMP столбцов (как было упомянуто ранее), не копируются и что hello **подстроки** функция является используется tooremove кавычки из данных hello.
5. **Hello среднее погоды задержки и группы hello результаты вычислений по названию города.** Он также будет выводить hello результаты tooBlob хранилища. Обратите внимание, этот запрос hello апострофы приведет к удалению из данных hello и исключает строки, где значение hello **weather_delay** имеет значение null. Это необходимо, так как Sqoop, используемый в этом руководстве, не обрабатывает эти значения надлежащим образом по умолчанию.

Полный список команд HiveQL hello см. в разделе [язык описания данных DDL Hive][hadoop-hiveql]. Каждая команда HiveQL должна завершаться точкой с запятой.

**файл скрипта HiveQL toocreate**

1. Подготовка параметров hello:

    <table border="1">
    <tr><th>Имя переменной</th><th>Примечания</th></tr>
    <tr><td>$storageAccountName</td><td>Здравствуйте, место сценарий HiveQL hello tooupload для учетной записи хранилища Azure.</td></tr>
    <tr><td>$blobContainerName</td><td>Здравствуйте, место сценарий HiveQL tooupload hello в контейнер больших двоичных объектов.</td></tr>
    </table>
2. Откройте интегрированную среду сценариев Azure PowerShell.
3. Скопируйте и вставьте следующий сценарий в области сценариев hello hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    Ниже приведены hello переменных, используемых в скрипте hello.

   * **$hqlLocalFileName** -скрипт hello сохраняет файл сценария HiveQL hello локально перед передачей его tooBlob хранилища. Это имя файла hello. значение по умолчанию Hello — <u>C:\tutorials\flightdelay\flightdelays.hql</u>.
   * **$hqlBlobName** -это hello HiveQL имя файла скрипта BLOB-объект используется в hello хранилища больших двоичных объектов Azure. значение по умолчанию Hello — tutorials/flightdelay/flightdelays.hql. Поскольку hello будет записан файл напрямую tooAzure хранилища больших двоичных объектов, не «/» в начале hello hello имя большого двоичного объекта. Если требуется файл hello tooaccess из хранилища больших двоичных объектов, необходимо будет tooadd «/» в начале имени файла hello hello.
   * **$srcDataFolder** и **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"

- - -
## <a id="appendix-c"></a>Приложение C — Подготовка базы данных Azure SQL для hello Sqoop выходные данные задания
**База данных SQL tooprepare hello (слияние с hello Sqoop сценарий)**

1. Подготовка параметров hello:

    <table border="1">
    <tr><th>Имя переменной</th><th>Примечания</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>Имя сервера базы данных Azure SQL hello Hello. Введите ничего не toocreate нового сервера.</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>Hello имя входа для сервера базы данных Azure SQL hello. Если $sqlDatabaseServerName существующий сервер, hello входа и пароль для входа, используется tooauthenticate с сервером hello. В противном случае они не используется toocreate нового сервера.</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>пароль для входа для сервера базы данных Azure SQL hello Hello.</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>Это значение используется только при создании нового сервера базы данных SQL Azure.</td></tr>
    <tr><td>$sqlDatabaseName</td><td>База данных SQL Hello toocreate hello AvgDelays таблицы используется для задание Sqoop hello. Если это значение не задано, то будет создана база данных с именем HDISqoop. Имя таблицы Hello hello Sqoop выходные данные задания будет AvgDelays. </td></tr>
    </table>
2. Откройте интегрированную среду сценариев Azure PowerShell.
3. Скопируйте и вставьте следующий сценарий в области сценариев hello hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > Hello скрипт использует службы передачи репрезентативного состояния (REST) передачи, http://bot.whatismyipaddress.com, tooretrieve внешнего IP-адреса. Hello IP-адрес используется для создания правила брандмауэра для сервера базы данных SQL.

    Ниже приведены некоторые переменные, используемые в скрипте hello.

   * **$ipAddressRestService** -hello значение по умолчанию — http://bot.whatismyipaddress.com. Это общедоступный IP-адрес службы REST для получения внешнего IP-адреса. При необходимости можно использовать и другие службы. внешний IP-адрес Hello извлечь с помощью службы hello будет toocreate используется правило брандмауэра для сервера базы данных Azure SQL, можно доступа к базе данных hello с рабочей станции (с помощью сценария Windows PowerShell).
   * **$fireWallRuleName** -это имя hello hello правила брандмауэра для сервера базы данных Azure SQL hello. имя по умолчанию Hello — <u>FlightDelay</u>. При необходимости можно использовать другое имя.
   * **$sqlDatabaseMaxSizeGB** — это значение используется только при создании нового сервера базы данных SQL Azure. значение по умолчанию Hello составляет 10 ГБ. Размера 10ГБ достаточно для примеров из данного учебника.
   * **$sqlDatabaseName** — это значение используется только при создании новой базы данных SQL Azure. значение по умолчанию Hello — HDISqoop. Если переименовать, необходимо соответствующим образом обновить сценарий Sqoop Windows PowerShell hello.
4. Нажмите клавишу **F5** toorun hello скрипта.
5. Проверьте выходные данные сценария hello. Убедитесь, что скрипт hello выполнено успешно.

## <a id="nextsteps"></a> Дальнейшие действия
Теперь вы понимаете как tooupload tooAzure файл хранилища больших двоичных объектов, как таблицы toopopulate куст, используя hello данные из хранилища больших двоичных объектов Azure, как toorun Hive запросы и как toouse Sqoop tooexport данные из базы данных Azure SQL tooan HDFS. toolearn более, см. следующие статьи hello.

* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]
* [Использование Hive с HDInsight][hdinsight-use-hive]
* [Использование Oozie с HDInsight][hdinsight-use-oozie]
* [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]
* [Использование Pig с HDInsight][hdinsight-use-pig]
* [Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
