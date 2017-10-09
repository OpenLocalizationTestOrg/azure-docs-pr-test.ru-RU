---
title: "средства aaaMigrate tooAzure диспетчера ресурсов для HDInsight | Документы Microsoft"
description: "Как toomigrate tooAzure диспетчера ресурсов разработки средств для кластеров HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>Миграция средства разработки на основе диспетчера ресурсов tooAzure для кластеров HDInsight

Средства для HDInsight на основе диспетчера служб Azure (ASM) устарели. Если вы использовали Azure PowerShell, Azure CLI или toowork hello HDInsight .NET SDK с кластерами HDInsight, не рекомендуется toouse hello ARM диспетчера ресурсов Azure под управлением версий PowerShell, CLI и характер пакета SDK для .NET. В этой статье содержит указатели toomigrate toohello новый ARM подход на основе. Везде, где это применимо, в этой статье также указывает hello различия между способами ассемблерного кода и ARM hello, для HDInsight.

> [!IMPORTANT]
> Поддержка Hello ассемблерного кода на основе PowerShell, CLI, и пакет SDK для .NET перестанет работать на **1 января 2017**.
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>Миграция Azure CLI tooAzure диспетчера ресурсов
Hello Azure CLI теперь по умолчанию устанавливается режим tooAzure диспетчера ресурсов (ARM), если вы обновляете из предыдущей установки; в этом случае может потребоваться toouse hello `azure config mode arm` режим tooARM tooswitch команд.

Основные команды Hello, hello Azure CLI, HDInsight с помощью службы управления Azure (ASM) в состав toowork являются hello же при использовании ARM; Однако некоторые параметры и ключи могут иметь новые имена, а доступно много новых параметров при использовании ARM. Например, теперь можно использовать `azure hdinsight cluster create` toospecify hello виртуальной сети Azure, должны быть созданы в кластере или Hive и Oozie метахранилище сведения.

Вот основные команды для работы с HDInsight с использованием диспетчера ресурсов Azure:

* `azure hdinsight cluster create` — создает кластер HDInsight;
* `azure hdinsight cluster delete` — удаляет кластер HDInsight;
* `azure hdinsight cluster show` — отображает информацию о существующем кластере;
* `azure hdinsight cluster list` — выдает список кластеров HDInsight для подписки Azure.

Используйте hello `-h` переключения tooinspect hello параметры и параметры, доступные для каждой команды.

### <a name="new-commands"></a>Новые команды
В диспетчере ресурсов Azure появились следующие команды:

* `azure hdinsight cluster resize`-динамически изменения hello число рабочих узлов в кластере hello
* `azure hdinsight cluster enable-http-access`-позволяет кластера toohello доступа HTTPs (по по умолчанию)
* `azure hdinsight cluster disable-http-access`-Отключает кластера toohello доступа HTTPs
* `azure hdinsight script-action` — предоставляет команды для создания действий сценариев в кластере и управления этими действиями;
* `azure hdinsight config`-предоставляет команды для создания файла конфигурации, который может использоваться с hello `hdinsight cluster create` команды tooprovide сведения о конфигурации.

### <a name="deprecated-commands"></a>Устаревшие команды
Если вы используете hello `azure hdinsight job` кластера HDInsight tooyour заданий toosubmit команды, они недоступны через hello ARM команды. Если вам требуется tooHDInsight tooprogrammatically отправки задания, из сценариев, следует использовать REST API, предоставляемые HDInsight hello. Дополнительные сведения по отправке заданий с помощью API REST см. следующие документы hello.

* [Выполнение заданий MapReduce с помощью cURL с использованием Hadoop в HDInsight](hdinsight-hadoop-use-mapreduce-curl.md)
* [Выполнение запросов Hive с помощью cURL с использованием Hadoop в HDInsight](hdinsight-hadoop-use-hive-curl.md)
* [Выполнение запросов Pig с помощью cURL с использованием Hadoop в HDInsight](hdinsight-hadoop-use-pig-curl.md)

Сведения о других способах toorun MapReduce Hive и Pig в интерактивном режиме см. в разделе [используйте MapReduce в с Hadoop в HDInsight](hdinsight-use-mapreduce.md), [используйте Hive в с Hadoop в HDInsight](hdinsight-use-hive.md), и [использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).

### <a name="examples"></a>Примеры
**Создание кластера**

* Старая команда (ASM) — `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* Новая команда (ASM) — `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**Удаление кластера**

* Старая команда (ASM) — `azure hdinsight cluster delete myhdicluster`
* Новая команда (ASM) — `azure hdinsight cluster delete mycluster -g myresourcegroup`

**Получение списка кластеров**

* Старая команда (ASM) — `azure hdinsight cluster list`
* Новая команда (ASM) — `azure hdinsight cluster list`

> [!NOTE]
> Для команды перечисления hello, указав hello группы ресурсов с помощью `-g` будет возвращать только те кластеры, hello в hello определенной группе ресурсов.
> 
> 

**Отображение данных кластера**

* Старая команда (ASM) — `azure hdinsight cluster show myhdicluster`
* Новая команда (ASM) — `azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>Миграция tooAzure Azure PowerShell диспетчера ресурсов
Общие сведения о Azure PowerShell в режиме диспетчера ресурсов Azure (ARM) hello Hello можно найти в [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](../powershell-azure-resource-manager.md).

Hello Azure PowerShell ARM командлеты можно установленных-параллельных с hello ASM командлетов. командлеты Hello из двух режимов hello можно отличить по их именам.  режим Hello ARM имеет *AzureRmHDInsight* в имена командлетов hello сравнение слишком*AzureHDInsight* в режиме ассемблерного кода hello.  Например, *New-AzureRmHDInsightCluster* или *New-AzureHDInsightCluster*. Параметры и переключатели могут иметь новые имена, а при использовании ARM появляется доступ к множеству новых параметров.  Например, для некоторых командлетов требуется новый переключатель *-ResourceGroupName*. 

Прежде чем использовать командлеты HDInsight hello, необходимо подключиться tooyour учетная запись Azure и создать новую группу ресурсов:

* Login-AzureRmAccount или [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx). См. статью о [проверке подлинности субъекта-службы в Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).
* [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>Переименованные командлеты
hello toolist HDInsight ASM командлеты в консоли Windows PowerShell:

    help *azurermhdinsight*

Hello следующей таблице перечислены командлеты ассемблерного кода hello и их имена в режиме hello ARM.

| Командлеты ASM | Командлеты ARM |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Add-AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Add-AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Add-AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[Grant-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[Grant-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Invoke-AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[New-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[New-AzureRmHDInsightClusterConfig](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[New-AzureRmHDInsightHiveJobDefinition](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[New-AzureRmHDInsightMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[New-AzureRmHDInsightPigJobDefinition](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[New-AzureRmHDInsightSqoopJobDefinition](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[New-AzureRmHDInsightStreamingMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Remove-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[Revoke-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[Revoke-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Set-AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Set-AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Use-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[Wait-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>Новые командлеты
Здесь представлены Hello hello новых командлетов, которые доступны только в режиме hello ARM. 

**Командлеты, связанные с действиями сценариев:**

* **Get-AzureRmHDInsightPersistedScriptAction**: hello получает сохраняются действия скрипта для кластера и перечисляет их в хронологическом порядке или получает сведения для действия указанного сохраненный скрипт. 
* **Get-AzureRmHDInsightScriptActionHistory**: возвращает hello журнал действий скриптов для кластера и указанный в обратном хронологическом порядке или возвращает подробные сведения о действии ранее выполненного скрипта. 
* **Remove-AzureRmHDInsightPersistedScriptAction**: удаляет из кластера HDInsight сохраняемое действие сценария.
* **Набор AzureRmHDInsightPersistedScriptAction**: задает действие сохраненный скрипт toobe действия ранее выполненный скрипт.
* **Отправить AzureRmHDInsightScriptAction**: отправляет новый кластер Azure HDInsight tooan действия сценария. 

Дополнительные сведения об использовании см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

**Командлеты, связанные с удостоверениями кластеров:**

* **Добавить AzureRmHDInsightClusterIdentity**: Добавляет объект конфигурации кластера tooa удостоверение кластера hello кластера HDInsight доступ к хранилищам Озера данных Azure. См. статью [Создание кластера HDInsight с хранилищем озера данных с помощью Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).

### <a name="examples"></a>Примеры
**Создать кластер**

Старая команда (ASM): 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

Новая команда (ASM):

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**Удалить кластер**

Старая команда (ASM):

    Remove-AzureHDInsightCluster -name $clusterName 

Новая команда (ASM):

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**Список кластеров**

Старая команда (ASM):

    Get-AzureHDInsightCluster

Новая команда (ASM):

    Get-AzureRmHDInsightCluster 

**Отображение кластеров**

Старая команда (ASM):

    Get-AzureHDInsightCluster -Name $clusterName

Новая команда (ASM):

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>Другие примеры
* [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Отправка заданий Hive](hdinsight-hadoop-use-hive-powershell.md)
* [Отправка заданий Pig](hdinsight-hadoop-use-pig-powershell.md)
* [Отправка заданий Sqoop](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>Миграция toohello HDInsight .NET SDK с архитектурой ARM
Здравствуйте, на основе Azure Service Management [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) теперь считается устаревшим. Вы являетесь рекомендуется toouse hello управления ресурсами Azure под управлением [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx). Hello следующих пакетов на основе ASM HDInsight устарели.

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

Этот раздел содержит указатели toomore сведения о том, как tooperform некоторых задач с помощью hello SDK с архитектурой ARM.

| Как... Использование hello ARM под управлением SDK HDInsight | Ссылки |
| --- | --- |
| Создание кластеров HDInsight с помощью пакета SDK для .NET |См. статью [Создание кластеров под управлением Linux в HDInsight с помощью пакета SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md). |
| Настройка кластера с помощью действия сценария и пакета SDK для .NET |См. статью [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action). |
| Интерактивная проверка подлинности приложений с Azure Active Directory c использованием пакета SDK для .NET |См. статью [Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md). фрагмент кода Hello в этой статье используется подход hello интерактивной проверки подлинности. |
| Неинтерактивная проверка подлинности приложений с Azure Active Directory c использованием пакета SDK для .NET |См. статью [Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности](hdinsight-create-non-interactive-authentication-dotnet-applications.md). |
| Отправка задания Hive с помощью пакета SDK для .NET |См. раздел [Отправка запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md). |
| Отправка задания Pig с помощью пакета SDK для .NET |См. статью [Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md). |
| Отправка задания Sqoop с помощью пакета SDK для .NET |См. статью [Выполнение заданий Sqoop с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md). |
| Получение списка кластеров HDInsight с помощью пакета SDK для .NET |См. раздел [Получение списка кластеров](hdinsight-administer-use-dotnet-sdk.md#list-clusters). |
| Масштабирование кластеров HDInsight с помощью пакета SDK для .NET |См. раздел [Масштабирование кластеров](hdinsight-administer-use-dotnet-sdk.md#scale-clusters). |
| GRANT/revoke доступа tooHDInsight кластеров с помощью пакета SDK для .NET |В разделе [предоставления или отзыва доступа tooHDInsight кластеров](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| Обновление учетных данных пользователя HTTP для кластеров HDInsight с помощью пакета SDK для .NET |См. раздел [Обновление учетных данных пользователя HTTP](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials). |
| Найти учетную запись хранения по умолчанию hello для кластеров HDInsight с помощью пакета SDK для .NET |В разделе [найти учетную запись хранения по умолчанию hello для кластеров HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| Удаление кластеров HDInsight с помощью пакета SDK для .NET |См. раздел [Удаление кластеров](hdinsight-administer-use-dotnet-sdk.md#delete-clusters). |

### <a name="examples"></a>Примеры
Ниже приведены некоторые примеры на том, как операция, которая выполняется с помощью пакета SDK на основе ассемблерного кода hello и фрагмент кода hello эквивалентный код для hello SDK с архитектурой ARM.

**Создание CRUD-клиента кластера**

* Старая команда (ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* Новая команда (ARM) (основная авторизация службы)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* Новая команда (ARM) (авторизация пользователя)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**Создание кластера**

* Старая команда (ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* Новая команда (ASM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**Включение доступа по протоколу HTTP**

* Старая команда (ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* Новая команда (ASM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**Удаление кластера**

* Старая команда (ASM)
  
        client.DeleteCluster(dnsName);
* Новая команда (ASM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

