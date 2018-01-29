---
title: "Копирование данных из WASB в Data Lake Store и обратно с помощью Distcp | Документация Майкрософт"
description: "Использование средства Distcp для копирования данных из BLOB-объектов хранилища Azure в хранилище озера данных и обратно"
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
ms.date: 01/09/2018
ms.author: nitinme
ms.openlocfilehash: 8a5052f69eee7f53bb304524fc3ea4d375c76227
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a>Использование Distcp для копирования данных между BLOB-объектами и хранилищем озера данных
> [!div class="op_single_selector"]
> * [С помощью DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [С помощью AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

При наличии кластера HDInsight с доступом к Data Lake Store можно использовать такие средства экосистемы Hadoop, как DistCp, для **копирования** данных из хранилища кластера HDInsight (WASB) в учетную запись Data Lake Store и обратно. В этой статье содержатся инструкции по использованию средства DistCp.

## <a name="prerequisites"></a>Необходимые компоненты

* **Подписка Azure**. См. страницу [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись хранения озера данных Azure**. Инструкции по созданию учетной записи см. в статье [Начало работы с Azure Data Lake Store с помощью портала Azure](data-lake-store-get-started-portal.md).
* **Кластер Azure HDInsight** с доступом к учетной записи Data Lake Store. См. статью [Создание кластера HDInsight с Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Убедитесь, что вы включили удаленный рабочий стол для кластера.

## <a name="do-you-learn-fast-with-videos"></a>Учитесь быстрее с помощью видео?
[Просмотрите это видно](https://mix.office.com/watch/1liuojvdx6sie) об использовании Distcp для копирования данных между большими двоичными объектами службы хранилища Azure и хранилищем озера данных Azure.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Использование Distcp из кластера HDInsight на платформе Linux

В состав кластера HDInsight входит служебная программа Distcp, которую можно использовать для копирования данных из различных источников в кластер HDInsight. При настройке кластера HDInsight для использования хранилища Data Lake Store в качестве дополнительного хранилища служебную программу DistCp можно использовать для копирования данных в учетную запись Data Lake Store и обратно без дополнительной настройки. В этом разделе мы рассмотрим, как использовать служебную программу DistCp.

1. На своем настольном компьютере используйте SSH, чтобы подключиться к кластеру. См. раздел [Подключение к кластеру HDInsight на основе Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Выполните команды в командной строке SSH.

2. Проверьте, доступны ли вам BLOB-объекты хранилища Azure (WASB). Выполните следующую команду:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Она должна вывести список содержимого в хранилище BLOB-объектов.

3. Аналогичным образом проверьте, доступна ли учетная запись хранилища озера данных из кластера. Выполните следующую команду:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Она должна вывести список файлов и папок в учетной записи Data Lake Store.

4. Используйте Distcp для копирования данных из WASB в учетную запись хранилища озера данных.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Эта команда копирует содержимое папки **/example/data/gutenberg/** в WASB в папку **/myfolder** в учетной записи Data Lake Store.

5. Аналогичным образом используйте Distcp для копирования данных из учетной записи хранилища озера данных в WASB.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Эта команда копирует содержимое папки **/myfolder** в учетной записи Data Lake Store в папку **/example/data/gutenberg/** в WASB.

## <a name="performance-considerations-while-using-distcp"></a>Рекомендации по производительности при использовании DistCp

Так как наименьшей степенью детализации DistCp является один файл, установка максимального количества одновременных копий является самым важным параметром оптимизации для Data Lake Store. Количество одновременных копий регулируется установкой параметра, отвечающего за количество модулей сопоставления (m), в командной строке. Этот параметр указывает максимальное количество модулей сопоставления, которые используются для копирования данных. Значение по умолчанию — 20.

**Пример**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a>Как определить количество модулей сопоставления, которые следует использовать?

Ниже представлены некоторые полезные рекомендации.

* **Шаг 1. Определение общего объема памяти YARN.** Первым шагом является определение объема памяти YARN, доступной для кластера, в котором выполняется задание DistCp. Эта информация доступна на портале Ambari, связанном с кластером. Перейдите к YARN и откройте вкладку конфигураций, чтобы определить объем памяти YARN. Чтобы определить общий объем памяти YARN, умножьте объем памяти YARN для одного узла на количество узлов в кластере.

* **Шаг 2. Расчет количества модулей сопоставления.** Чтобы узнать значение **m**, разделите целую часть общего объема памяти YARN на размер контейнера YARN. Сведения о размере контейнера YARN также доступны на портале Ambari. Перейдите к YARN и откройте вкладку конфигураций. Размер контейнера YARN отобразится в этом окне. Уравнение для получения количества модулей сопоставления (**m**):

        m = (number of nodes * YARN memory for each node) / YARN container size

**Пример**

Предположим, что в кластере есть 4 узла D14v2s, и вы пытаетесь передать 10 ТБ данных из 10 разных папок. Эти папки содержат различные объемы данных, и размеры файлов в каждой папке отличаются.

* Общий объем памяти YARN. На портале Ambari вы узнали, что объем памяти YARN составляет 96 ГБ для узла D14. Таким образом, общий объем памяти YARN для кластера из четырех узлов равен: 

        YARN memory = 4 * 96GB = 384GB

* Число модулей сопоставления. На портале Ambari вы узнали, что размер контейнера YARN равен 3072 для узла кластера D14. Таким образом, число модулей сопоставления равно:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Если другие приложения используют память, то для DistCp можно использовать только часть памяти YARN кластера.

### <a name="copying-large-datasets"></a>Копирование больших наборов данных

Если размер перемещаемого набора данных большой (например, больше 1 ТБ), или в наборе много различных папок, рекомендуем использовать несколько заданий DistCp. Вряд ли это увеличит производительность, однако будет создано несколько заданий. В результате, если возникнет сбой одного из заданий, нужно будет перезапустить только это задание, а не все задание по перемещению.

### <a name="limitations"></a>Ограничения

* DistCp пытается создать модули сопоставления одинакового размера для оптимизации производительности. Увеличение количества модулей сопоставления не всегда приводит к увеличению производительности.

* DistCp ограничивается только одним модулем сопоставления для каждого файла. Поэтому количество модулей сопоставления не должно превышать количество файлов. Так как DistCp может назначать только один модуль сопоставления для одного файла, это ограничивает объем параллелизма, который можно использовать для копирования больших файлов.

* При наличии небольшого количества больших файлов следует разбить их на фрагменты по 256 МБ для повышения степени параллелизма. 
 
* При копировании из учетной записи хранилища BLOB-объектов Azure задание копирования может регулироваться на стороне хранилища BLOB-объектов. Это снижает производительность задания копирования. Дополнительные сведения об ограничениях хранилища BLOB-объектов Azure см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md).

## <a name="see-also"></a>См. также
* [Copy data from Azure Storage Blobs to Data Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
