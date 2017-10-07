---
title: "aaaCopy tooand данных из WASB в хранилище Озера данных с помощью Distcp | Документы Microsoft"
description: "Использовать Distcp средство toocopy данных tooand из хранилища Озера tooData больших двоичных объектов хранилища Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Использовать данные toocopy Distcp между BLOB-объектов хранилища Azure и хранилища Озера данных
> [!div class="op_single_selector"]
> * [С помощью DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [С помощью AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

После создания кластера HDInsight учетной записью хранилища Озера данных tooa доступ, можно использовать средства экосистемы Hadoop как данные toocopy Distcp **tooand из** хранилище кластера HDInsight (WASB) в учетную запись хранилища Озера данных. Эта статья содержит инструкции о том, как tooachieve это.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись Azure Data Lake Store.** Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)
* **Кластер Azure HDInsight** с tooa доступа к учетной записи хранилища Озера данных. См. статью [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md). Убедитесь, что включить удаленный рабочий стол для кластера hello.

## <a name="do-you-learn-fast-with-videos"></a>Учитесь быстрее с помощью видео?
[В этом видеоролике](https://mix.office.com/watch/1liuojvdx6sie) о том, как toocopy данных между Azure хранилища больших двоичных объектов и с помощью DistCp хранилища Озера данных.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Использование Distcp из кластера HDInsight на платформе Linux

Кластер HDInsight поставляется с Distcp hello служебная программа, которая может быть используется toocopy данными из различных источников в кластер HDInsight. После настройки хранилища Озера данных toouse кластера HDInsight hello как дополнительное хранилище hello Distcp программа может быть используется toocopy out of box tooand данных с учетной записью хранилища Озера данных. В этом разделе мы рассмотрим как toouse hello Distcp программы.

1. С рабочего стола используйте SSH tooconnect toohello кластера. В разделе [кластера HDInsight под управлением Linux tooa Connect](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Выполните команды hello из строки hello SSH.

2. Убедитесь, может ли доступ к hello хранилища больших двоичных объектов Azure (WASB). Выполните следующую команду hello.

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Это должен предоставить список содержимого в BLOB-объекта хранилища hello.
3. Аналогично убедитесь, доступен ли из кластера hello hello хранилища Озера данных. Выполните следующую команду hello.

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Это необходимо предоставить список всех файлов и папок в hello хранилища Озера данных.
4. Используйте данные toocopy Distcp из WASB tooa хранилища Озера данных.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Это будет копировать содержимое hello hello **/пример/данных/gutenberg/** папки в WASB слишком**/myfolder** в hello хранилища Озера данных.
5. Аналогичным образом используйте данные toocopy Distcp из tooWASB учетной записи хранилища Озера данных.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Это будет копировать содержимое hello **/myfolder** в hello хранилища Озера данных учетной записи слишком**/пример/данных/gutenberg/** папки в WASB.

## <a name="performance-considerations-while-using-distcp"></a>Рекомендации по производительности при использовании DistCp

Поскольку DistCp наименьшее гранулярности является отдельным файлом, параметр hello максимальное число одновременных копий является наиболее важным параметром toooptimize hello его к хранилищу Озера данных. Это поведение управляется задание количества hello модули сопоставления (am ") параметр в командной строке hello. Этот параметр задает максимальное число hello модули сопоставления, которые будут использоваться toocopy данных. Значение по умолчанию — 20.

**Пример**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>Как определить количество hello toouse модули сопоставления?

Ниже представлены некоторые полезные рекомендации.

* **Шаг 1: Определение общий объем памяти YARN** -hello первым шагом является toodetermine hello YARN памяти доступных toohello кластера где выполнения задания DistCp hello. Эта информация доступна на портале Ambari hello, связанные с кластером hello. Перейти tooYARN и открыть hello конфигураций вкладку toosee hello YARN памяти. tooget hello общего объема YARN памяти умножить hello YARN памяти на узел с hello количество узлов, что кластер.

* **Шаг 2: Рассчитайте hello количество модули сопоставления** -hello значение **m** является равно toohello частное от общего объема памяти YARN, деленное на размер контейнера YARN hello. сведения о размере контейнера YARN Hello доступна на портале Ambari hello также. Перейдите tooYARN и в этом окне отображается представление hello конфигураций вкладку hello YARN размер контейнера. Здравствуйте tooarrive формулы в числе hello модули сопоставления (**m**) —

        m = (number of nodes * YARN memory for each node) / YARN container size

**Пример**

Предположим, что имеется 4 D14v2s узлов в кластере hello и вы пытаетесь tootransfer 10 ТБ данных из 10 разных папках. Hello папок, содержащих различных объемов данных и размеры файлов hello в каждой папке отличаются.

* Общий объем памяти YARN - из hello портала Ambari выяснится, что hello YARN памяти составляет 96 ГБ для узла D14. Таким образом, общий объем памяти YARN для кластера из 4 узлов равен: 

        YARN memory = 4 * 96GB = 384GB

* Число модули сопоставления - из портала Ambari вы определите, что размер контейнера YARN hello не большего 3072 пикселей для узла кластера D14 hello. Таким образом, число модулей сопоставления равно:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Если другие приложения используют память, то вы можете tooonly используется часть памяти, YARN вашего кластера для DistCp.

### <a name="copying-large-datasets"></a>Копирование больших наборов данных

При перемещении hello размер toobe hello набор данных очень большой (например > 1 ТБ) или если у вас есть много различных папок, можно использовать несколько заданий DistCp. Скорее всего, нет никакого прироста производительности, но он будет распределения hello заданий, чтобы при сбое задания, достаточно будет toorestart этого конкретного задания, а не всего задания hello.

### <a name="limitations"></a>Ограничения

* DistCp пытается toocreate модули сопоставления, аналогичные размер toooptimize производительности. При увеличении числа hello модули сопоставления может не всегда увеличить производительность.

* DistCp — ограниченный tooonly одного сопоставления каждого файла. Поэтому количество модулей сопоставления не должно превышать количество файлов. Поскольку DistCp можно назначить только одного сопоставления файлов tooa, это ограничивает объем hello параллелизма, который можно использовать toocopy больших файлов.

* Если у вас есть малого числа больших файлов, то их следует разбить на 256 МБ файла блоки toogive вам несколько потенциальных параллелизма. 
 
* При копировании из учетной записи хранилища больших двоичных объектов может регулировать задание копирования на стороне хранилища больших двоичных объектов hello. Это может повлиять на производительность hello задания копирования. toolearn более об ограничениях hello хранилища больших двоичных объектов Azure, см. ограничения хранилища Azure при [подписка Azure и ограничения служб](../azure-subscription-service-limits.md).

## <a name="see-also"></a>См. также
* [Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure](data-lake-store-copy-data-azure-storage-blob.md)
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
