---
title: "Хранилище Озера данных в с Hadoop в Azure HDInsight aaaUse | Документы Microsoft"
description: "Узнайте, как tooquery данные из хранилища Озера данных Azure и toostore результатов анализа."
keywords: "хранилище BLOB-объектов,hdfs,структурированные данные,неструктурированные данные,data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Использование Data Lake Store с кластерами Azure HDInsight

данные tooanalyze в кластер HDInsight, данные можно хранить hello либо в [хранилища Azure](../storage/common/storage-introduction.md), [хранилища Озера данных Azure](../data-lake-store/data-lake-store-overview.md), или оба. Оба варианта хранилища позволяют удалить toosafely кластеров HDInsight, которые используются для вычисления без потери данных пользователя.

Из этой статьи вы узнаете, как Data Lake Store работает с кластерами HDInsight. toolearn как хранилище Azure работает с кластерами HDInsight. в разделе [кластеры использования хранилища Azure с Azure HDInsight](hdinsight-hadoop-use-blob-storage.md). Дополнительные сведения о создании кластера HDInsight см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

> [!NOTE]
> Доступ к Data Lake Store всегда осуществляется по безопасному каналу, поэтому никогда не применяется имя схемы файловой системы `adls`. Всегда используется `adl`.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>Сведения о доступности для кластеров HDInsight

Hadoop поддерживает понятие файловой системы по умолчанию hello. файловой системы по умолчанию Hello подразумевается схема по умолчанию и центром. Его также можно использовать tooresolve относительные пути. Во время процесса создания кластера HDInsight hello, можно указать контейнер больших двоичных объектов в хранилище Azure в качестве файловой системы по умолчанию hello, или с HDInsight 3.5 и более новых версий, можно выбрать хранилище Azure или хранилища Озера данных Azure как система файлов по умолчанию hello с несколько исключений. 

Есть два способа использования Data Lake Store с кластерами HDInsight:

* Как хранилище по умолчанию hello
* в качестве дополнительного хранилища (при этом в качестве хранилища по умолчанию используется Azure Storage Blob).

Сейчас или только часть hello HDInsight кластер типы и версии поддерживают использование хранилища Озера данных в качестве хранилища по умолчанию и дополнительные учетные записи хранения.

| Тип кластера HDInsight | Data Lake Store как хранилище по умолчанию | Data Lake Store как дополнительное хранилище| Примечания |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight версии 3.6 | Да | Да | |
| HDInsight версии 3.5 | Да | Да | Исключением hello HBase|
| HDInsight версия 3.4 | Нет | Да | |
| HDInsight версии 3.3 | Нет | Нет | |
| HDInsight версии 3.2 | Нет | Да | |
| HDInsight "Премиум" (уровень)| Нет | Нет | |
| Storm | | |Можно использовать данные toowrite хранилища Озера данных из топологии Storm. Data Lake Store также может использоваться для хранения эталонных данных, которые затем можно будет считать с помощью топологии Storm.|

С помощью хранилища Озера данных от имени учетной записи дополнительное хранилище не влияет на производительность или возможность tooread hello и записи хранилища tooAzure кластере hello.


## <a name="use-data-lake-store-as-default-storage"></a>Использование Data Lake Store в качестве хранилища по умолчанию

При развертывании HDInsight с помощью хранилища Озера данных в качестве хранилища по умолчанию hello кластера связанные файлы хранятся в хранилище Озера данных hello следующие расположения:

    adl://mydatalakestore/<cluster_root_path>/

где `<cluster_root_path>` — hello имя папки, создаваемые в хранилище Озера данных. Указав корневой путь для каждого кластера, можно использовать одну учетную запись хранилища Озера данных для нескольких кластеров hello. Таким образом, у вас могут получиться такие настройки:

* Cluster1 можно использовать путь hello`adl://mydatalakestore/cluster1storage`
* Cluster2 можно использовать путь hello`adl://mydatalakestore/cluster2storage`

Обратите внимание, что оба hello использование кластеров hello же хранилища Озера данных **mydatalakestore**. Каждый кластер имеет доступ tooits владельцем корневой файловой системы в хранилище Озера данных. Hello опыт развертывания Azure портала в частности предложит toouse имя папки например **/clusters/\<имя_кластера >** для корневого пути hello.

toouse toobe возможности хранилища Озера данных хранения по умолчанию, необходимо предоставить hello службы доступа toohello следующие пути:

- корневой учетной записи хранилища Озера данных Hello.  Например: adl://mydatalakestore/.
- Hello папки для всех папок кластера.  Например: adl://mydatalakestore/clusters.
- Папка Hello для hello кластера.  Например: adl://mydatalakestore/clusters/cluster1storage.

Дополнительные сведения о создании субъекта-службы и предоставлении доступа см. в разделе [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).


## <a name="use-data-lake-store-as-additional-storage"></a>Использование Data Lake Store в качестве дополнительного хранилища

Хранилище Озера данных можно использовать как дополнительное хранилище для кластера hello также. В таких случаях хранилище по умолчанию hello кластера может быть BLOB-объект хранилища Azure или учетную запись хранилища Озера данных. При выполнении задания HDInsight к hello данным, хранящимся в хранилище Озера данных как дополнительное хранилище, необходимо использовать файлы toohello hello полный путь. Например:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Следует отметить, что не **cluster_root_path** в URL-АДРЕСЕ hello теперь. Это, так как хранилище Озера данных не хранилища по умолчанию в этом случае поэтому все, что нужно toodo предоставляют файлы toohello путь hello.

toouse toobe возможности хранилища Озера данных как дополнительное хранилище, требуется только toogrant hello службы доступа toohello пути где хранятся файлы.  Например:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Дополнительные сведения о создании субъекта-службы и предоставлении доступа см. в разделе [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).


## <a name="use-more-than-one-data-lake-store-accounts"></a>Использование нескольких учетных записей Data Lake Store

Добавление учетной записи хранилища Озера данных как дополнительный и Добавление более одного хранилища Озера данных выполняется учетных записей, предоставляя разрешение кластера HDInsight hello на данные в учетных записях хранилища Озера данных для одной или нескольких. См. раздел [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Настройка доступа к Data Lake Store

tooconfigure доступ к хранилищу Озера данных с кластером HDInsight, необходимо иметь Azure Active directory (Azure AD) участника-службы. Создать субъект-службу может только администратор Azure AD. Hello участника-службы должны создаваться с помощью сертификата. Дополнительные сведения см. в разделах [Настройка доступа к Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) и [Создание субъекта-службы с самозаверяющим сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

> [!NOTE]
> Если вы собираетесь хранилища Озера данных Azure toouse как дополнительное хранилище для кластера HDInsight, настоятельно рекомендуется это сделать, при создании кластера hello, как описано в этой статье. Добавление хранилища Озера данных Azure в качестве дополнительного хранилища tooan существующий кластер HDInsight является сложным процессом и ошибкам tooerrors.
>

## <a name="access-files-from-hello-cluster"></a>Доступ к файлам из кластера hello

Существует несколько способов, можно обратиться к файлам hello в хранилище Озера данных из кластера HDInsight.

* **Используя полное имя hello**. При таком подходе, укажите файл toohello hello полный путь, которые должны tooaccess.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **С использованием формата сокращенный путь hello**. При таком подходе вы замените hello пути до корневого кластера toohello adl: / / /. Таким образом, в приведенном выше примере hello, можно заменить `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` с `adl:///`.

        adl:///<file path>

* **С помощью относительного пути hello**. При таком подходе можно только указать файл toohello hello относительного пути, которые должны tooaccess. Например, если файл toohello hello полный путь:

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    Вы можете получить доступ к Здравствуйте того же файла sample.log, используя это относительный путь.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>Создать кластеры HDInsight с доступа к хранилищу Озера tooData

Используйте следующие ссылки на подробные инструкции на как toocreate кластеров HDInsight с доступа к хранилищу Озера tooData hello.

* [Использование портала](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [Создание кластера HDInsight с Data Lake Store (как хранилище по умолчанию) с помощью Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Создание кластера HDInsight с Data Lake Store (как дополнительное хранилище) с помощью Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Создание кластера HDInsight с Data Lake Store с помощью шаблона Azure Resource Manager](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, каким образом toouse хранилища Озера данных Azure HDFS-совместимой с HDInsight. Это позволяет вам toobuild масштабируемые и долгосрочной, архивация данных приобретения решения и использования HDInsight toounlock hello данные, содержащиеся в hello хранятся структурированные и неструктурированные данные.

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
