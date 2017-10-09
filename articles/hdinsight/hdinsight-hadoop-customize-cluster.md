---
title: "aaaCustomize кластеров HDInsight с помощью сценария действий - Azure | Документы Microsoft"
description: "Узнайте, как toocustomize HDInsight кластеры, использующие действие сценария."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>Настройка кластеров HDInsight под управлением Windows с помощью действия сценария
**Записать действие в скрипт** может быть используется tooinvoke [пользовательские сценарии](hdinsight-hadoop-script-actions.md) во время создания кластера hello для установки дополнительного программного обеспечения в кластере.

Hello сведения в этой статье — конкретных tooWindows основе кластеров HDInsight. О кластерах под управлением Linux читайте в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Кластеров HDInsight могут быть настроены в различных других целей, такие как включение дополнительных учетных записей хранилища Azure, изменение hello Hadoop (core-site.xml, hive-site.xml, т. д.), файлы конфигурации и добавление общие библиотеки (например, Hive, Oozie) в стандартных расположениях в кластере hello. Эти настройки можно сделать с помощью Azure PowerShell, hello Azure HDInsight .NET SDK или hello портал Azure. Дополнительные сведения см. в статье [Создание кластеров Hadoop в HDInsight][hdinsight-provision-cluster].

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Действие сценария в процессе создания кластера hello
Действие сценария используется только в том случае, пока кластер находится в процессе создания hello. Hello следующей схеме показана при выполнении сценария действия во время создания hello.

![Настройка кластера HDInsight и этапы создания кластера][img-hdi-cluster-states]

При выполнении скрипта hello, кластер hello вводит hello **ClusterCustomization** рабочей области. На этом этапе сценария hello запускается под учетной записью администратора системы hello, параллельно на всех hello указан узлов в кластере hello и предоставляет права полного администратора на узлах hello.

> [!NOTE]
> Если у вас права администратора на узлах кластера hello во время **ClusterCustomization** рабочей области, можно использовать hello сценария tooperform операции, такие как остановка и запуск служб, включая службы, связанные с Hadoop. Так как часть сценария hello, необходимо убедиться, hello Ambari службы и другие службы, связанные с Hadoop доступны и запущены перед hello сценарий завершает работу. Эти службы необходимы toosuccessfully выяснить hello работоспособности и состояние кластера hello во время создания. Если изменить какой-либо настройки в кластере, который влияет на эти службы, необходимо использовать hello вспомогательные функции, которые предоставляются. Подробнее о вспомогательных функциях см. в статье [Разработка скриптов действия сценария для HDInsight][hdinsight-write-script].
>
>

Вывод Hello и hello журналы ошибок для скрипта hello хранятся в учетной записи хранилища hello по умолчанию, заданные для кластера hello. Hello журналы хранятся в таблице с именем hello **u < \cluster-name-fragment >< \time-stamp > setuplog**. Это совокупное журналы из hello сценариев, запускаемых на всех узлах hello (головного узла и рабочих узлов) в кластере hello.

Каждый кластер может принимать несколько действий скрипта, которые вызываются в порядке hello, в котором они указаны. Сценарий можно работали на головном узле hello и hello рабочих узлов.

HDInsight предоставляет несколько сценариев tooinstall hello, следующие компоненты в кластерах HDInsight.

| Имя | Скрипт |
| --- | --- |
| **Установка Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Ознакомьтесь со статьей [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]. |
| **Установка R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Ознакомьтесь со статьей [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]. |
| **Установка Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Ознакомьтесь со статьей [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Установка Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Ознакомьтесь со статьей [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md). |
| **Предварительная загрузка библиотек Hive** |https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1. Ознакомьтесь со статьей [Добавление библиотек Hive в кластеры HDInsight](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Вызов сценариев с помощью портала Azure hello
**Из портала Azure hello**

1. Начните создание кластера, как описано в разделе [Создание кластеров Hadoop под управлением Windows в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
2. В разделе дополнительной конфигурации hello **действия скрипта** колонке нажмите кнопку **добавьте действия скрипта** tooprovide сведений о hello действие скрипта, как показано ниже:

    ![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize действия скрипта для использования кластера")

    <table border='1'>
        <tr><th>Свойство</th><th>Значение</th></tr>
        <tr><td>Имя</td>
            <td>Укажите имя для действия сценария hello.</td></tr>
        <tr><td>URI-адрес сценария</td>
            <td>Укажите сценарий toohello URI hello, вызванный toocustomize hello кластера. s</td></tr>
        <tr><td>Головной/рабочий</td>
            <td>Укажите узлы hello (**Head** или **рабочих**) на какие hello настройки выполнения скрипта.</b>.
        <tr><td>Параметры</td>
            <td>Укажите параметры hello, если это требуется для сценария hello.</td></tr>
    </table>

    Нажмите клавишу ВВОД tooadd больше, чем один скрипт действие tooinstall несколько компонентов в кластере hello.
3. Нажмите кнопку **выберите** toosave hello скрипт конфигурации действия и продолжите создание кластера.

## <a name="call-scripts-using-azure-powershell"></a>Вызов сценариев с помощью Azure PowerShell
Это следующий сценарий PowerShell показано, как tooinstall Spark в Windows на основе кластеров HDInsight.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall другого программного обеспечения, вам потребуется файл сценария tooreplace hello в скрипте hello:

При появлении запроса введите учетные данные hello hello кластера. Он может занять несколько минут, перед созданием кластера hello.

## <a name="call-scripts-using-net-sdk"></a>Вызов сценариев с помощью пакета SDK для .NET
Hello следующий пример демонстрирует, как tooinstall Spark в Windows на основе кластеров HDInsight. tooinstall другого программного обеспечения, вам потребуется файл сценария tooreplace hello в коде hello.

**кластер HDInsight с Spark toocreate**

1. Создайте в Visual Studio консольное приложение C#.
2. Запустите следующую команду hello из hello консоль диспетчера пакетов Nuget.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. Используйте hello после с помощью инструкций в файле Program.cs hello:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Поместите код hello в классе hello hello следующее:

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. Нажмите клавишу **F5** toorun приложения hello.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Поддержка программного обеспечения с открытым исходным кодом, используемого в кластере HDInsight
Hello службы Microsoft Azure HDInsight — это гибкая платформа, обеспечивающий toobuild больших данных приложений в облаке hello с помощью экосистему технологий открытым исходным кодом, сформированный вокруг Hadoop. Microsoft Azure предоставляет общие уровень поддержки для технологий с открытым исходным кодом, как описано в hello **область поддерживает** раздел hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">веб-сайта Azure поддерживают часто задаваемые вопросы о</a>. Hello службы HDInsight предоставляет дополнительный уровень поддержки для некоторых компонентов hello, как описано ниже.

Существует два типа компонентов открытым исходным кодом, доступных в hello службы HDInsight:

* **Встроенные компоненты** -эти компоненты предустановлен в кластерах HDInsight и предоставляют основные функциональные возможности кластера hello. Например YARN ResourceManager, язык запросов Hive hello (HiveQL) и библиотеку Mahout hello принадлежать toothis категории. Полный список компонентов кластера доступен в [новые возможности, предоставляемые HDInsight версиями кластеров Hadoop hello?](hdinsight-component-versioning.md) </a>.
* **Пользовательские компоненты** -, как пользователь кластера hello, можно установить или использовать любой компонент, доступные в сообществе hello или созданный вами в рабочей нагрузке.

Встроенные компоненты, полностью поддерживаются и поддержки Майкрософт способствуют tooisolate и разрешить проблемы toothese связанные компоненты.

> [!WARNING]
> Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются и поддержки Майкрософт способствуют tooisolate и разрешить проблемы toothese связанные компоненты.
>
> Пользовательские компоненты получают toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello. Это может привести к устранению проблемы hello и без tooengage доступных каналов для hello открытии источника технологий, которых находится глубокие знания для данной технологии. Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, проекты Apache можно просмотреть на соответствующих сайтах по адресу [http://apache.org](http://apache.org), например для [Hadoop](http://hadoop.apache.org/) и [Spark](http://spark.apache.org/).
>
>

Служба HDInsight Hello предоставляет несколько способов toouse пользовательские компоненты. Независимо от того, как компонент используется, или установлена на кластере hello hello же уровнем поддержки применяется. Ниже приведен список наиболее распространенными способами hello, что пользовательские компоненты можно использовать в кластерах HDInsight.

1. Отправки заданий - Hadoop или других типов заданий, обрабатываемых или использовать пользовательские компоненты может быть отправлено toohello кластера.
2. Настройка кластера - во время создания кластера можно указать дополнительные параметры и пользовательские компоненты, которые будут устанавливаться на узлах кластера hello.
3. Примеры — для популярных пользовательские компоненты, корпорация Майкрософт и другие могут предоставлять примеры использования этих компонентов в кластерах HDInsight hello. Эти примеры представляются без поддержки.

## <a name="develop-script-action-scripts"></a>Разработка скрипта действия сценария
Ознакомьтесь со статьей [Разработка скриптов действия сценария для HDInsight][hdinsight-write-script].

## <a name="see-also"></a>См. также
* [Создание кластеров Hadoop в HDInsight] [ hdinsight-provision-cluster] описано, как toocreate HDInsight кластер с помощью другие настраиваемые параметры.
* [Разработка скриптов действия сценария для HDInsight][hdinsight-write-script]
* [Установка и использование Spark в кластерах HDInsight Hadoop с помощью действия сценария][hdinsight-install-spark]
* [Установка и использование R на кластерах HDInsight Hadoop][hdinsight-install-r]
* [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install.md).
* [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Этапы создания кластера"
