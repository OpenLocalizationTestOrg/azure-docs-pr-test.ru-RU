---
title: "aaaQuery данных из HDFS-совместимой хранилище Azure — Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooquery данные из хранилища Azure и хранилища Озера данных Azure toostore результатов анализа."
keywords: "хранилище blob-объектов, hdfs, структурированные данные, неструктурированные данные, data lake store, входные данные hadoop, выходные данные hadoop, входные данные hdfs, выходные данные hdfs, хранилище hdfs, wasb azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Использование службы хранилища Azure с кластерами Azure HDInsight

данные tooanalyze в кластер HDInsight, можно хранить данные hello в хранилище Azure и/или в хранилище Озера данных Azure. Оба варианта хранилища позволяют удалить toosafely кластеров HDInsight, которые используются для вычисления без потери данных пользователя.

Hadoop поддерживает понятие файловой системы по умолчанию hello. файловой системы по умолчанию Hello подразумевается схема по умолчанию и центром. Его также можно использовать tooresolve относительные пути. Во время hello в процессе создания кластера HDInsight можно указать контейнер больших двоичных объектов в хранилище Azure в качестве файловой системы по умолчанию hello, или с HDInsight 3.5, можно выбрать хранилище Azure или хранилища Озера данных Azure как система файлов по умолчанию hello за некоторыми исключениями. Поддержка использования хранилища Озера данных по умолчанию hello и связанное хранение hello, в разделе [наличий для кластера HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).

Из этой статьи вы узнаете, как служба хранилища Azure работает с кластерами HDInsight. toolearn как хранилище Озера данных работает с кластерами HDInsight. в разделе [кластеры использования хранилища Озера данных Azure с Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md). Дополнительные сведения о создании кластера HDInsight см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

Служба хранилища Azure — это надежное, универсальное решение, которое полностью интегрируется с HDInsight. HDInsight можно использовать контейнер больших двоичных объектов в хранилище Azure в качестве файловой системы по умолчанию hello для hello кластера. Через интерфейс распределенной файловой системы (HDFS) Hadoop hello полный набор компонентов в HDInsight может работать непосредственно структурированных и неструктурированных данных, хранящихся в виде больших двоичных объектов.

> [!WARNING]
> При создании учетной записи хранения Azure доступно несколько параметров. Привет, в следующей таблице представлены сведения о какие параметры поддерживаются с HDInsight:
> 
> | Тип учетной записи хранения | Уровень хранилища | Поддерживается HDInsight |
> | ------- | ------- | ------- |
> | Учетная запись хранения общего назначения | Стандартная | __Да__ |
> | &nbsp; | Премиум | Нет |
> | Учетная запись хранения больших двоичных объектов | Горячий | Нет |
> | &nbsp; | Холодный | Нет |

Не рекомендуется использовать контейнер больших двоичных объектов по умолчанию hello для хранения бизнес-данных. Удаление контейнера больших двоичных объектов по умолчанию hello после каждого использования tooreduce хорошей практикой является затраты на хранение. Примечание контейнера по умолчанию hello содержит узлы приложений и системных журналов. Убедитесь что tooretrieve hello журналы перед удалением hello контейнера.

Совместное использование одного контейнера больших двоичных объектов для нескольких кластеров не поддерживается.

## <a name="hdinsight-storage-architecture"></a>Архитектура хранилища HDInsight
Следующая схема Hello обеспечивает абстрактное представление hello архитектуры хранилища HDInsight с помощью хранилища Azure:

![Кластеры Hadoop использовать HDFS API tooaccess hello и хранить структурированные и неструктурированные данные в хранилище больших двоичных объектов. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Архитектуры хранилища HDInsight")

HDInsight предоставляет доступ toohello распределенной файловой системы, локально присоединенного toohello вычислительных узлов. Эта файловая система может осуществляться с помощью hello полный URI-адрес, например:

    hdfs://<namenodehost>/<path>

Кроме того HDInsight позволяет tooaccess данные, которые хранятся в хранилище Azure. используется синтаксис Hello:

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

Ниже приведены некоторые рекомендации для использования учетной записи хранения Azure с кластерами HDInsight.

* **Контейнеры в hello учетные записи хранения, подключенные tooa кластера:** поскольку hello имя учетной записи и ключ, связанные с hello кластера во время создания, у вас есть полный доступ toohello BLOB-объектов в этих контейнерах.

* **Общедоступных контейнеров или общедоступных больших двоичных объектов в учетных записях хранения, которые не подключены tooa кластера:** у вас есть разрешение только для чтения toohello BLOB-объектов в контейнеры hello.
  
  > [!NOTE]
  > Открытые контейнеры позволяют tooget список все большие двоичные объекты, доступные в этом контейнере и получение метаданных контейнера. Открытые большие двоичные объекты позволяют tooaccess hello большие двоичные объекты только в том случае, если известно точное hello URL-адрес. Дополнительные сведения см. в разделе <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">ограничить доступ toocontainers и большие двоичные объекты</a>.
  > 
  > 
* **Частные контейнеры в учетных записях хранения, которые не подключены tooa кластера:** доступ hello больших двоичных объектов в контейнеры hello невозможен до определения учетной записи хранилища hello при отправке задания WebHCat hello. Это объясняется далее в статье.

Hello учетных записей хранилища, которые определены в процессе создания hello и их ключи хранятся в %HADOOP_HOME%/conf/core-site.xml на узлах кластера hello. поведение по умолчанию Hello HDInsight не toouse hello хранилища учетные записи, определенные в файле core-site.xml hello. Этот параметр можно изменить с помощью [Ambari](./hdinsight-hadoop-manage-ambari.md).

Несколько заданий WebHCat, включая Hive, MapReduce, потоковую передачу Hadoop и Pig, могут переносить описание учетных записей хранения и метаданные вместе с ними. (В настоящее время эта функция работает для Pig с учетными записями хранения, но не с метаданными). Дополнительные сведения см. в разделе [Использование кластера HDInsight с дополнительными учетными записями хранения и метахранилищами](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).

Большие двоичные объекты могут использоваться для хранения как структурированных, так и неструктурированных данных. В контейнерах больших двоичных объектов данные хранятся в виде пар "ключ — значение" и отсутствует иерархия каталогов. Однако hello косой черты (/), которые могут использоваться в hello toomake имя ключа, он отображается, как если бы файл хранится в структуре каталогов. Например, ключ BLOB-объекта может выглядеть следующим образом: *input/log1.txt*. Не фактические *ввода* каталог существует, но из-за наличия toohello hello косой черты в имени ключа hello, он имеет вид hello пути к файлу.

## <a id="benefits"></a>Преимущества службы хранилища Azure
снижение производительности не совместного размещения вычислительных кластеров и ресурсами хранения, уменьшается путем способом hello hello вычислительные кластеры создаются ресурсами учетных записей хранилища закрыть toohello внутри hello регион Azure, где hello высокоскоростной сети упрощает неявная Hello эффективным для вычислительных узлов hello tooaccess hello данных внутри хранилища Azure.

Ниже перечислены некоторые преимущества, связанные с хранением данных hello в хранилище Azure вместо HDFS:

* **Данные повторного и совместного использования:** hello данные в HDFS, расположенный внутри hello вычислительного кластера. Только приложения hello, которые имеют доступ toohello вычислений hello данные можно использовать в кластере с помощью API-интерфейсов HDFS. Hello данных в хранилище Azure может осуществляться через API-интерфейсы HDFS hello или hello [API REST хранилища больших двоичных объектов][blob-storage-restAPI]. Таким образом большего набора приложений (включая другие кластеры HDInsight) и средств может быть используется tooproduce и использования данных hello.
* **Архивация данных:** хранения данных в хранилище Azure позволяет кластеров HDInsight hello, используемый для вычисления toobe безопасно удалить без потери данных пользователя.
* **Затраты на хранение данных:** хранение данных в DFS для долговременного hello дороже, чем хранения данных hello в хранилище Azure, так как стоимость hello вычислительного кластера больше, чем стоимость hello хранилища Azure. Кроме того поскольку данные hello не имеет toobe перезагружен для каждого поколения кластера вычислений, также сохраняются затраты на загрузку данных.
* **Гибкое масштабирование:** HDFS, несмотря на то что предоставляет масштабируемых файловой системы, hello шкалы определяется hello количество узлов, создаваемых для кластера. Изменение масштаба hello может стать более сложный процесс, чем полагаться на hello гибкому масштабированию возможности, которые автоматически появляются в хранилище Azure.
* **Репликация.** Доступна функция георепликации службы хранилища Azure. Несмотря на то, что этот метод позволяет географического восстановления и обеспечения избыточности данных, расположение георепликацией toohello отработки отказа серьезно влияет на производительность, и он может повлечь дополнительные затраты. Поэтому мы рекомендуем георепликации toochoose hello центрах и только в том случае, если значение hello hello данных стоит hello дополнительных затрат.

Некоторые задания MapReduce и пакетов может создавать промежуточные результаты, что вы не хотите действительно toostore в хранилище Azure. В этом случае можно выбрать данные toostore hello в hello локальной HDFS. На деле HDInsight использует DFS для некоторых таких промежуточных результатов в заданиях Hive и других процессах.

> [!NOTE]
> Большинство команд HDFS (например, <b>ls</b>, <b>copyFromLocal</b> и <b>mkdir</b>) по-прежнему работают приавильно. Здравствуйте, только команды, которые являются определенной toohello собственной HDFS реализацией (который является ссылка tooas DFS), например <b>fschk</b> и <b>dfsadmin</b>, Показать другое поведение в хранилище Azure.
> 
> 

## <a name="create-blob-containers"></a>Создание контейнеров BLOB-объектов
toouse больших двоичных объектов, сначала создать [учетной записи хранилища Azure][azure-storage-create]. В рамках этого укажите регион Azure, где создается учетная запись хранения hello. кластер Hello и hello учетной записи хранения должна быть размещена в hello одного региона. базы данных SQL Server метахранилища Hive Hello и метахранилище Oozie SQL Server, базы данных также должен быть расположен в hello в одном регионе.

Везде, где он находится, каждый BLOB-объектов, создаваемых принадлежит tooa контейнера в учетной записи хранилища Azure. Этим контейнером может быть существующий контейнер хранилища BLOB-объектов, созданный вне HDInsight, или контейнер, созданный для кластера HDInsight.

контейнер больших двоичных объектов по умолчанию Hello хранит данные о кластере, такие как журнал заданий и журналов. Не используйте стандартный контейнер BLOB-объектов с несколькими кластерами HDInsight. Это может привести к искажению истории заданий. Рекомендуется toouse другой контейнер для каждого кластера и записать на связанной учетной записи хранения указан в развертывании всех соответствующих кластеров, а не учетной записи хранения по умолчанию hello общих данных. Дополнительные сведения о настройке связанных учетных записей хранения см. в статье [Создание кластеров HDInsight][hdinsight-creation]. Тем не менее можно повторно использовать контейнер хранилища по умолчанию, после удаления исходного кластера HDInsight hello. HBase кластеров вы можете фактически сохранить hello HBase схемы и данных таблицы, создав новый кластер HBase с помощью контейнера больших двоичных объектов по умолчанию hello, используемый кластер HBase, который был удален.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Использовать hello портал Azure
При создании кластера HDInsight из hello портала, можно выбрать сведения учетной записи хранилища hello tooprovide hello параметры (как показано ниже). Также можно указать, будет ли дополнительная учетная запись хранения, связанного с hello кластера и если да, выберите из хранилища Озера данных или другой большой двоичный объект хранилища Azure как дополнительное хранилище hello.

![источник данных для создания hadoop в HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> С использованием учетной записи дополнительный объем хранилища в другом месте, чем hello кластера HDInsight не поддерживается.


### <a name="use-azure-powershell"></a>Использование Azure PowerShell
Если вы [установить и настроить Azure PowerShell][powershell-install], можно использовать следующую из запроса toocreate hello Azure PowerShell, учетная запись хранения и контейнер hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Использование интерфейса командной строки Azure

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

Если у вас есть [установлен и настроен hello Azure CLI](../cli-install-nodejs.md), hello следующая команда, может быть tooa используется учетная запись хранения и контейнер.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> Hello `--type` параметр показывает, как учетная запись хранения hello реплицируются. Дополнительные сведения см. в статье [Репликация службы хранилища Azure](../storage/storage-redundancy.md). Не используйте хранилище, избыточное в пределах зоны (ZRS), так как оно не поддерживает страничные BLOB-объекты, файлы, таблицы и очереди.
> 
> 

Вы являетесь географического региона hello запрашиваемые toospecify, созданной учетной записи хранилища hello. Следует создать учетную запись хранения hello hello же регионе, можно запланировать создание кластера HDInsight.

После создания учетной записи хранилища hello, используйте следующие ключи учетной записи хранения hello tooretrieve команда hello:

    azure storage account keys list <storageaccountname>

toocreate контейнер, hello используйте следующую команду:

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Обращение к файлам в службе хранилища Azure
Схема URI Hello для доступа к файлам в хранилище Azure с HDInsight является:

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

Схема URI Hello предоставляет незашифрованные доступ (с hello *wasb:* префикс) и SSL-шифрованием доступа (с *wasbs*). Мы рекомендуем использовать *wasbs* везде, где это возможно, даже в том случае, если доступ к данным, которые находятся внутри hello в одном регионе в Azure.

Hello &lt;BlobStorageContainerName&gt; определяет имя hello hello контейнера BLOB-объектов в хранилище Azure.
Hello &lt;StorageAccountName&gt; определяет имя учетной записи хранилища Azure hello. Обязательно использовать полное доменное имя (FQDN).

Если ни одна из &lt;BlobStorageContainerName&gt; , ни &lt;StorageAccountName&gt; был указан, используется файловая система по умолчанию hello. Файлы hello в системе по умолчанию hello можно использовать относительный путь или абсолютный путь. Например, hello *mapreduce-hadoop-examples.jar* файл, который поставляется с кластерами HDInsight может быть tooby ссылка, с помощью одного из следующих hello:

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> Имя файла Hello <i>hadoop-examples.jar</i> в кластерах HDInsight версии 2.1 и 1.6.
> 
> 

Hello &lt;путь&gt; — hello имя файла или каталога HDFS пути. Так как контейнеры службы хранилища Azure содержат данные типа "ключ — значение", подлинная иерархическая файловая система в них отсутствует. Знак косой черты "/" в ключе BLOB-объекта интерпретируется как разделитель каталогов. Например, имя hello большого двоичного объекта для *hadoop mapreduce-examples.jar* является:

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> При работе с большими двоичными объектами за пределами HDInsight, большинство программ не распознает формат WASB hello и вместо этого ожидается, что в формате базовый путь, например `example/jars/hadoop-mapreduce-examples.jar`.
> 
> 

## <a name="access-blobs"></a>Доступ к большим двоичным объектам 


### <a name="access-blobs-using-azure-powershell"></a> С помощью Azure PowerShell
> [!NOTE]
> Hello команды в этом разделе предоставляют простой пример использования PowerShell tooaccess данные, хранящиеся в больших двоичных объектов. Пример большей функциональностью, настроенном для работы с HDInsight см. в разделе hello [средства HDInsight](https://github.com/Blackmist/hdinsight-tools).
> 
> 

Используйте hello следующая команда toolist hello blob командлеты:

    Get-Command *blob*

![Список связанных с BLOB-объектами командлетов PowerShell.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>Отправка файлов
В разделе [отправить данные tooHDInsight][hdinsight-upload-data].

#### <a name="download-files"></a>Скачивание файлов
Hello следующий скрипт загружает большой двоичный объект блока toohello текущей папки. Перед выполняемого сценария hello измените папку tooa каталога hello, которой предоставлены разрешения записи.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Предоставления hello имя группы ресурсов и hello имя кластера, можно использовать hello, следующий код:

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>Удаление файлов
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>Перечень файлов
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>Выполнение запросов Hive с использованием неопределенной учетной записи хранения
Этот пример показывает, как toolist папки из учетной записи хранилища, которая не определена во время hello процессом.
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Использование интерфейса командной строки Azure
Используйте hello следующая команда toolist hello большого двоичного объекта команды:

    azure storage blob

**Пример использования Azure CLI tooupload файла**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Пример использования Azure CLI toodownload файла**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Пример использования Azure CLI toodelete файла**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Пример использования файлов toolist Azure CLI**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>Использование дополнительных учетных записей хранения

При создании кластера HDInsight, укажите учетную запись хранилища Azure hello, требуется tooassociate с ним. В дополнение к этому toothis учетной записи хранилища, можно добавить дополнительные учетные записи хранения из hello же подписки Azure или разных подписках Azure во время процесса создания hello, или после создания кластера. Инструкции по добавлению дополнительных учетных записей хранения см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!WARNING]
> С использованием учетной записи дополнительный объем хранилища в другом месте, чем hello кластера HDInsight не поддерживается.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, как toouse HDFS-совместимой хранилища Azure с HDInsight. Это позволяет вам toobuild масштабируемые и долгосрочной, архивация данных приобретения решения и использования HDInsight toounlock hello данные, содержащиеся в hello хранятся структурированные и неструктурированные данные.

Дополнительные сведения можно найти в разделе 

* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]
* [Начало работы с Azure Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-get-started-portal.md)
* [Отправка данных tooHDInsight][hdinsight-upload-data]
* [Использование Hive с HDInsight][hdinsight-use-hive]
* [Использование Pig с HDInsight][hdinsight-use-pig]
* [Использование подписей общего доступа Azure хранилища toorestrict доступа toodata с HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
