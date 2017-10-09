---
title: "кластеры aaaManage Hadoop в HDInsight с помощью PowerShell, Azure | Документы Microsoft"
description: "Узнайте, как tooperform административные задачи для hello кластеров Hadoop в HDInsight с помощью Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Управление кластерами Hadoop в HDInsight с помощью Azure PowerShell
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell — это мощная среда сценариев, можно использовать toocontrol и автоматизации развертывания hello и управления ими рабочих нагрузок в Azure. В этой статье вы узнаете, как использовать toomanage кластеров Hadoop в Azure HDInsight с помощью локальной консоли Azure PowerShell через hello оболочки Windows PowerShell. Список hello hello командлеты HDInsight PowerShell см. в разделе [Справочник по командлетам HDInsight][hdinsight-powershell-reference].

**Предварительные требования**

Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Установка Azure PowerShell
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Если вы установили Azure PowerShell версии 0.9x, то перед установкой новой версии ее необходимо удалить.

toocheck hello hello версии PowerShell:

    Get-Module *azure*

старая версия hello toouninstall, запустить программы и компоненты панели управления hello.

## <a name="create-clusters"></a>Создание кластеров
Ознакомьтесь с разделом [Создание кластеров под управлением Linux в HDInsight с помощью Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Получение списка кластеров
Используйте следующие команды toolist hello всех кластеров в текущей подписке hello:

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Отображение кластеров
Используйте приведенные ниже сведения tooshow команду к конкретному кластеру в текущей подписке hello hello.

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Удаление кластеров
Используйте следующие команды toodelete кластера hello:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

Можно также удалить кластер, удалив hello группы ресурсов, содержащий hello кластера. Обратите внимание, это приведет к удалению всех ресурсов группы hello, включая учетную запись хранения по умолчанию hello hello.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Масштабирование кластеров
масштабирование функции кластера Hello позволяет toochange hello число рабочих узлов в кластере, который выполняется в Azure HDInsight без необходимости toore-создать кластер hello.

> [!NOTE]
> Поддерживаются только кластеры HDInsight версии 3.1.3 или более поздней. Если вы не знаете hello версии кластера, можно проверить свойства страницы приветствия.  См. раздел [Отображение кластеров](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

Hello последствия изменения hello количество узлов данных для каждого типа поддерживаемых HDInsight кластера:

* Hadoop

    Можно легко увеличить hello число рабочих узлов в кластере Hadoop, на котором выполняется без ущерба для все ожидающие или выполняемые задания. Также можно отправлять новые задания, hello операции во время выполнения. Ошибки в операции масштабирования обрабатываются правильно, чтобы hello кластер всегда оставался в рабочем состоянии.

    Когда кластер Hadoop уменьшено за счет уменьшения hello количество узлов данных, некоторые службы hello в кластере hello перезапускаются. В результате все выполняющиеся и ожидающие задания toofail окончании hello hello операцию масштабирования. Можно Однако повторно отправить задания hello после завершения операции hello.
* HBase

    Можно легко добавить или удалить узлы tooyour HBase кластера при выполнении. Региональные серверы распределяются автоматически через несколько минут после завершения hello операция масштабирования. Тем не менее можно также вручную сбалансировать региональные серверы hello войдите в систему в toohello головному узлу кластера, и выполнение hello, следующие команды из окна командной строки:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    Можно легко добавить или удалить кластер Storm tooyour узлы данных при выполнении. Однако после успешного завершения hello операция масштабирования потребуется toorebalance hello топологии.

    Повторную балансировку можно выполнить двумя способами:

  * с помощью веб-интерфейса Storm;
  * с помощью программы командной строки.

    См. toohello [документации Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) для получения дополнительных сведений.

    в кластере HDInsight hello доступен Hello Storm пользовательского веб-интерфейса:

    ![HDInsight, storm, масштабирование, перераспределение](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Ниже приведен пример как toouse hello CLI команды toorebalance hello Storm топологии:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

hello toochange размер кластера Hadoop с помощью Azure PowerShell, запустите следующую команду с клиентского компьютера hello:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>Предоставление и отмена доступа
Кластеры HDInsight имеют hello следующие веб-службы HTTP (все эти службы имеют RESTful конечные точки):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

По умолчанию эти службы предоставляются для доступа. Вы можете revoke или предоставления доступа hello. toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> Предоставление или Отмена доступа hello, восстановится hello кластера имя и пароль пользователя.
>
>

Это можно сделать через портал hello. В разделе [Здравствуйте, администрировать HDInsight с помощью портала Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Обновление учетных данных пользователя HTTP
Это же hello процедуры как [доступа для предоставления или отзыва HTTP](#grant/revoke-access). Если кластер hello было предоставлено hello доступа по протоколу HTTP, то необходимо отозвать.  А затем предоставить доступ hello с новыми учетными данными пользователя HTTP.

## <a name="find-hello-default-storage-account"></a>Найти учетную запись хранения по умолчанию hello
Следующий сценарий Powershell Hello демонстрируется tooget hello имя учетной записи хранения по умолчанию и hello ключ учетной записи хранения по умолчанию для кластера.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Найти группу ресурсов hello
В режиме hello диспетчера ресурсов каждый кластер HDInsight принадлежит tooan группы ресурсов Azure.  Группа ресурсов hello toofind:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>Отправка заданий
**задания MapReduce toosubmit**

См. статью [Выполнение примеров Hadoop MapReduce в HDInsight на базе Windows](hdinsight-run-samples.md).

**задания Hive toosubmit**

См. статью [Выполнение запросов Hive с помощью PowerShell](hdinsight-hadoop-use-hive-powershell.md).

**задания Pig toosubmit**

См. статью [Выполнение заданий Pig с помощью PowerShell](hdinsight-hadoop-use-pig-powershell.md).

**toosubmit Sqoop заданий**

См. статью [Использование Sqoop с Hadoop в HDInsight](hdinsight-use-sqoop.md).

**toosubmit Oozie заданий**

В разделе [Oozie использования с Hadoop toodefine и выполнения рабочего процесса в HDInsight](hdinsight-use-oozie.md).

## <a name="upload-data-tooazure-blob-storage"></a>Отправка больших двоичных объектов хранилища данных tooAzure
В разделе [отправить данные tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>См. также
* [Справочная документация по командлетам HDInsight][hdinsight-powershell-reference]
* [Администрирование с помощью hello портал Azure HDInsight][hdinsight-admin-portal]
* [Администрирование HDInsight с помощью интерфейса командной строки][hdinsight-admin-cli]
* [Создание кластеров Hadoop в HDInsight][hdinsight-provision]
* [Отправка данных tooHDInsight][hdinsight-upload-data]
* [Отправка заданий Hadoop в HDInsight][hdinsight-submit-jobs]
* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
