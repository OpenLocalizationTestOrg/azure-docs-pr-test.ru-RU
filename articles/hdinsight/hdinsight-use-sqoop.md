---
title: "aaaRun Apache Sqoop заданий с Azure HDInsight (Hadoop) | Документы Microsoft"
description: "Узнайте, как toouse Azure PowerShell из рабочей станции toorun Sqoop Импорт и экспорт между кластера Hadoop и базой данных Azure SQL."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>Использование Sqoop с Hadoop в HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Узнайте, как toouse Sqoop в HDInsight tooimport и экспорт между кластер HDInsight и база данных Azure SQL или база данных SQL Server.

Несмотря на то, что Hadoop является естественным выбором для обработки частично структурированные и неструктурированные данные, такие как журналы и файлы, может существовать необходимость tooprocess структурированных данных, хранящиеся в реляционных базах данных.

[Sqoop] [ sqoop-user-guide-1.4.4] — tootransfer средство данные между кластерами Hadoop и реляционных баз данных. Он используется tooimport данных из системы управления реляционной базы данных (RDBMS) SQL Server, MySQL или Oracle в hello распределенная файловая система Hadoop (HDFS), преобразования данных hello в Hadoop MapReduce или Hive, а затем экспортировать hello данные обратно в РЕЛЯЦИОННОЙ СУБД. В этом учебнике в качестве реляционной базы данных используется база данных SQL.

Версии Sqoop, которые поддерживаются в кластерах HDInsight, в разделе [новые возможности, предоставляемые HDInsight версии кластера hello?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Понять сценарии hello

Кластер HDInsight имеет несколько примеров данных. Привет, следующие два примера используется:

* Файл журнала log4j, расположенный в */example/data/sample.log*. из файла hello извлекаются Hello следующие журналы:
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* Таблицу Hive с именем *hivesampletable*, который Здравствуйте, ссылки на файлы данных, расположенные в */hive/warehouse/hivesampletable*. Hello таблица содержит данные на мобильных устройствах. 
  
  | Поле | Тип данных |
  | --- | --- |
  | clientid |string |
  | querytime |string |
  | market |string |
  | deviceplatform |string |
  | devicemake |string |
  | devicemodel |string |
  | state |string |
  | country |string |
  | querydwelltime |double |
  | sessionid |bigint |
  | sessionpagevieworder |bigint |

Во-первых, вы экспортируете *sample.log* и *hivesampletable* toohello базы данных Azure SQL или tooSQL сервера, а затем импорта hello таблицу, которая содержит данные на мобильных устройствах hello резервное tooHDInsight с помощью hello следующий путь:

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>Создание кластера и базы данных SQL
В этом разделе показано, как toocreate кластера, базы данных SQL и hello схемы базы данных SQL для запущенным hello учебника с помощью hello Azure и шаблона диспетчера ресурсов Azure. Hello шаблон можно найти в [шаблоны быстрый запуск Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/). шаблон диспетчера ресурсов Hello вызывает bacpac пакета toodeploy hello таблицы схемы tooSQL базы данных.  пакет bacpac Hello находится в контейнере большой двоичный объект открытого https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac. Toouse закрытый контейнер для файлов bacpac hello, используйте следующие значения в шаблоне hello hello:
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Если вы предпочитаете toouse Azure PowerShell toocreate hello кластера и hello базы данных SQL, см. [приложение A](#appendix-a---a-powershell-sample).

1. Щелкните hello, следуя tooopen образ шаблона диспетчера ресурсов в hello портал Azure.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Введите hello следующие свойства:

    - **Подписка** — введите подписку Azure.
    - **Группа ресурсов** — создайте группу ресурсов Azure или выберите имеющуюся.  Группа ресурсов нужна для управления.  Это контейнер для объектов.
    - **Расположение** — выберите регион.
    - **Имя_кластера**: Введите имя для кластера Hadoop hello.
    - **Имя входа и пароль кластера**: hello имя входа по умолчанию — admin.
    - **Имя пользователя SSH и пароль**.
    - **Имя для входа на сервер базы данных SQL Azure и пароль**.
    - **расположение _artifacts**: использовать значение по умолчанию hello, если не требуется toouse свой собственный файл backpac в другом месте.
    - **Маркер SAS расположения артефактов** — оставьте это свойство пустым.
    - **Имя файла Bacpac**: использовать значение по умолчанию hello, если не требуется toouse backpac файл.
     
     следующие значения Hello жестко запрограммированы в разделе hello переменных:
     
     | Имя учетной записи хранения по умолчанию | <CluterName>store |
     | --- | --- |
     | Имя сервера базы данных SQL Azure |<ClusterName>dbserver |
     | Имя базы данных SQL Azure |<ClusterName>db |
     
     Запишите эти значения.  Они необходимы далее в учебнике hello.

3. Откройте **ОК** toosave hello параметров.

4. из hello **развертывания пользовательского** колонке нажмите кнопку **группы ресурсов** раскрывающийся список, а затем щелкните **New** toocreate новую группу ресурсов. Группа ресурсов Hello является контейнером, который группирует hello кластера, учетной записи хранилища зависимых hello и других связанных ресурсов.

5. Щелкните **Юридические условия** и **Создать**.

6. Нажмите кнопку **Создать**. Появится новый элемент под названием "Выполняется отправка развертывания для развертывания шаблона". Это занимает около кластера hello toocreate около 20 минут и базы данных SQL.

При выборе toouse существующей базы данных Azure SQL или Microsoft SQL Server

* **База данных SQL Azure**: необходимо настроить правила брандмауэра для hello доступа tooallow сервера базы данных Azure SQL с рабочей станции. Сведения о создании базы данных Azure SQL и настройка брандмауэра hello содержатся в разделе [приступить к работе с базой данных Azure SQL][sqldatabase-get-started]. 
  
  > [!NOTE]
  > По умолчанию в базе данных SQL Azure разрешены подключения из служб Azure, таких как Azure HDInsight. Если при отключении этого параметра брандмауэра, необходимо tooenable его из hello портал Azure. Инструкции по созданию базы данных SQL Azure и настройке правил брандмауэра см. в статье [Начало работы с серверами баз данных SQL Azure, базами данных и правилами брандмауэра с использованием портала Azure и SQL Server Management Studio][sqldatabase-create-configue].
  > 
  > 
* **SQL Server**: Если кластеру HDInsight на hello одной виртуальной сети в Azure с SQL Server, можно использовать шаги hello в этой статье tooimport и экспорт данных tooa базы данных SQL Server.
  
  > [!NOTE]
  > HDInsight поддерживает только географически привязанные виртуальные сети и на данный момент не работает с виртуальными сетями на основе территориальных групп.
  > 
  > 
  
  * toocreate и настройка виртуальной сети см. в разделе [создать виртуальную сеть с помощью портала Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    
    * При использовании SQL Server в центре обработки данных, необходимо настроить hello виртуальной сети, что *сайт сайт* или *точки сайтами*.
      
      > [!NOTE]
      > Для **точки сайтами** виртуальных сетей, SQL Server должна быть запущена hello VPN-клиента конфигурации приложения, которое доступно из hello **мониторинга** конфигурации виртуальной сети Azure.
      > 
      > 
    * При использовании SQL Server на виртуальной машине Azure какой-либо настройки виртуальной сети может использоваться, если hello виртуальной машины, где размещен SQL Server является членом hello HDInsight же виртуальной сети.
  * toocreate кластер HDInsight в виртуальной сети, в разделе [кластеров создать Hadoop в HDInsight с использованием пользовательских параметров](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > Кроме того, SQL Server должен разрешать проверку подлинности. Необходимо использовать SQL Server, hello toocomplete входа шаги в этой статье.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Выполнение заданий Sqoop
HDInsight может выполнять задания Sqoop с помощью различных методов. Используйте следующие таблицы toodecide, какой метод подходит для вас hello, затем по ссылке hello Пошаговое руководство.

| **Используйте** , если требуется... | ... **интерактивная** оболочка | ...**пакетная** обработка | ...with этим **кластером операционной системы** | ...из этого **кластера операционной системы** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X или Windows |
| [.NET SDK для Hadoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux или Windows |Windows (сейчас) |
| [Azure PowerShell](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux или Windows |Windows |

## <a name="limitations"></a>Ограничения
* Для массового экспорта — под управлением Linux с HDInsight, hello Sqoop соединитель, используемый tooexport данных tooMicrosoft SQL Server или база данных SQL Azure в настоящее время не поддерживает операции массовой вставки.
* Пакетное выполнение — с hdinsight под управлением Linux, при использовании hello `-batch` переход при выполнении вставки, Sqoop выполняет вставку нескольких вместо Пакетная обработка операций вставки hello.

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы узнали, как toouse Sqoop. toolearn более, см.:

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование Oozie с HDInsight][hdinsight-use-oozie]: используйте действие Sqoop в рабочем процессе Oozie.
* [Анализ данных задержки рейсов, с помощью HDInsight][hdinsight-analyze-flight-data]: используйте Hive рейса tooanalyze задержка данных, а затем использовать базы данных Azure SQL tooan Sqoop tooexport данных.
* [Отправка данных tooHDInsight][hdinsight-upload-data]: найти другие методы для отправки данных tooHDInsight/Azure BLOB-объекта хранилища.

## <a name="appendix-a---a-powershell-sample"></a>Приложение А. Пример PowerShell
Образец Hello PowerShell выполняет hello следующие шаги:

1. Подключите tooAzure.
2. Создание группы ресурсов Azure. Дополнительные сведения см. в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).
3. Создание сервера базы данных SQL Azure, базы данных SQL Azure и двух таблиц. 
   
    При использовании SQL Server вместо них используйте следующие инструкции toocreate hello таблицы hello:
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    Hello простым способом tooexamine hello базы данных и таблиц — toouse Visual Studio. Hello сервера базы данных и hello базы данных можно просмотреть с помощью портала Azure hello.
4. Создание кластера HDInsight.
   
    tooexamine hello кластера, можно использовать hello портал Azure или Azure PowerShell.
5. Предварительно обработать hello исходного файла данных.
   
    В этом учебнике экспортировать файл журнала log4j (с разделителями-файл), таблица Hive tooan базы данных Azure SQL. Hello файла с разделителями называется */example/data/sample.log*. Ранее в учебнике hello вы увидели несколько образцов log4j журналы. В файле журнала hello существуют некоторые пустые строки и аналогичные toothese некоторых строк:
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    Это хорошо работает для других примеров, использующих эти данные, но мы необходимо удалить эти исключения, прежде чем мы можно импортировать в базу данных Azure SQL hello или SQL Server. Экспорт Sqoop завершается сбоем, если пустая строка или строка с меньшего элементов, чем hello количество полей, определенных в таблице базы данных Azure SQL hello. Таблица log4jlogs Hello содержит 7 полей строкового типа.
   
    Данная процедура создает новый файл в кластере hello: tutorials/usesqoop/data/sample.log. tooexamine hello измененные данные файла, можно использовать hello портал Azure, средства обозревателя хранилищ Azure или Azure PowerShell. [Начало работы с HDInsight] [ hdinsight-get-started] имеет код образца с помощью Azure PowerShell toodownload файла и отобразить содержимое файла hello.
6. Экспортируйте файл данных toohello базы данных Azure SQL.
   
    Hello исходный файл является tutorials/usesqoop/data/sample.log. Hello таблицу, где данные hello экспортированного toois вызывается log4jlogs.
   
   > [!NOTE]
   > Кроме строки соединения hello шаги в этом разделе подойдут для базы данных Azure SQL или SQL Server. Эти шаги были проверены с использованием hello следующая конфигурация:
   > 
   > * **Конфигурация точки сайтами виртуальной сети Azure**: tooa кластера HDInsight hello SQL Server в центре обработки данных частного подключения виртуальной сети. В разделе [настроить VPN-Подключение точка-сеть в hello портала управления](../vpn-gateway/vpn-gateway-point-to-site-create.md) для получения дополнительной информации.
   > * **Azure HDInsight 3.1**. Cм. статью [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md), чтобы получить более подробную информацию о создании кластера в виртуальной сети.
   > * **SQL Server 2014**: tooallow проверки подлинности и выполнения hello tooconnect пакет конфигурации VPN клиента настроены безопасно toohello виртуальной сети.
   > 
   > 
7. Экспорт базы данных Azure SQL toohello таблицу Hive.
8. Импорт кластера HDInsight toohello таблицы mobiledata hello.
   
    tooexamine hello измененные данные файла, можно использовать hello портал Azure, средства обозревателя хранилищ Azure или Azure PowerShell.  [Начало работы с HDInsight] [ hdinsight-get-started] имеет код образца об использовании Azure PowerShell toodownload файла и отобразить содержимое файла hello.

### <a name="hello-powershell-sample"></a>Образец Hello PowerShell
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

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
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
