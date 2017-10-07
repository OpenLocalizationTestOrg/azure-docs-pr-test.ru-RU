---
title: "Хранилище Озера данных с другими службами Azure aaaIntegrating | Документы Microsoft"
description: "Принципы интеграции хранилища озера данных с другими службами Azure"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>Интеграция хранилища озера данных с другими службами Azure
Хранилище Озера данных Azure можно использовать в сочетании с другими службами Azure tooenable более широкого круга сценариев. Hello следующую статью список служб hello, может быть интегрировано хранилища Озера данных.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Использование хранилища озера данных с Azure HDInsight
Можно подготовить [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) кластера, использующего хранилище Озера данных хранения hello HDFS-совместимым. В этом выпуске для кластеров Hadoop и Storm в Windows и Linux можно использовать хранилище озера данных только в качестве дополнительного. Такие кластеры использовать хранилище Azure (WASB) в качестве хранилища по умолчанию hello. Тем не менее для HBase кластеров в Windows и Linux, можно использовать как хранилище по умолчанию hello или дополнительное хранилище хранилища Озера данных.

Инструкции по как tooprovision HDInsight кластер с хранилища Озера данных см.:

* [Подготовка кластера HDInsight и хранилища озера данных с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Подготовка кластера HDInsight с использованием Data Lake Store (как хранилища по умолчанию) и Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Подготовка кластера HDInsight с использованием Data Lake Store (как дополнительного хранилища) и Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Использование хранилища озера данных с аналитикой озера данных Azure
[Azure аналитики Озера данных](../data-lake-analytics/data-lake-analytics-overview.md) позволяет toowork с большими данными при масштабировании в облаке. Она динамически подготавливает ресурсы и позволяет выполнять аналитические операции с терабайтами и даже эксабайтами данных, которые могут храниться в разных поддерживаемых источниках данных, одним из которых является хранилище озера данных. Аналитика Озера данных является специально оптимизированного toowork с хранилища Озера данных Azure — предоставление hello высокий уровень производительности, пропускной способности и параллелизма для вас рабочих нагрузок больших данных.

Дополнительные сведения о toouse аналитики Озера данных с хранилищу Озера данных. в разделе [Приступая к работе с аналитики Озера данных с помощью хранилища Озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md).

## <a name="use-data-lake-store-with-azure-data-factory"></a>Использование хранилища озера данных с фабрикой данных Azure
Можно использовать [фабрики данных Azure](https://azure.microsoft.com/services/data-factory/) tooingest данные из таблицы Azure, база данных SQL Azure, хранилище данных SQL Azure, большие двоичные объекты хранилища Azure и локальных баз данных. Будучи угла в hello Azure экосистемы, фабрики данных Azure может быть используется tooorchestrate hello приема данных из этих tooAzure исходного хранилища Озера данных.

Инструкции по toouse фабрика данных Azure с хранилищу Озера данных. в статье [переместить tooand данных из хранилища Озера данных, с помощью фабрики данных](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Копирование данных из больших двоичных объектов хранилища Azure в хранилище озера данных
Хранилище Озера данных Azure предоставляет средство командной строки, AdlCopy, которого можно toocopy данные из хранилища больших двоичных объектов в учетную запись хранилища Озера данных. Дополнительные сведения см. в разделе [скопировать данные из хранилища Озера tooData больших двоичных объектов хранилища Azure](data-lake-store-copy-data-azure-storage-blob.md).

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Копирования данных между базой данных SQL Azure и хранилищем озера данных
Можно использовать tooimport Apache Sqoop и экспорт данных между базой данных SQL Azure и хранилища Озера данных. Дополнительные сведения см. в статье [Копирование данных между хранилищем озера данных и базой данных SQL Azure с помощью Sqoop](data-lake-store-data-transfer-sql-sqoop.md).

## <a name="use-data-lake-store-with-stream-analytics"></a>Использование хранилища озера данных со Stream Analytics
Хранилище Озера данных можно использовать как один из hello выводит toostore данных потоковой передачи с помощью Azure Stream Analytics. Дополнительные сведения см. в разделе [Потоковая передача данных из большого двоичного объекта службы хранилища Azure в хранилище озера данных с помощью Azure Stream Analytics](data-lake-store-stream-analytics.md).

## <a name="use-data-lake-store-with-power-bi"></a>Использование хранилища озера данных с Power BI
Можно использовать данные tooimport Power BI из учетной записи хранилища Озера данных tooanalyze и визуализации данных hello. Дополнительные сведения см. в разделе [Анализ данных в хранилище озера данных с помощью Power BI](data-lake-store-power-bi.md).

## <a name="use-data-lake-store-with-data-catalog"></a>Использование хранилища озера данных с каталогом данных
Можно зарегистрировать данные из хранилища Озера данных в hello обнаруживаемой hello организации данных hello toomake каталога данных Azure. Дополнительные сведения см. в разделе [Регистрация данных из хранилища озера данных в каталоге данных Azure](data-lake-store-with-data-catalog.md).

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>Использование Data Lake Store со службами SQL Server Integration Services (SSIS)
Можно использовать диспетчер соединений для хранилища Озера данных Azure hello в SSIS tooconnect пакет служб SSIS с хранилища Озера данных Azure. См. дополнительные сведения об [использовании Data Lake Store со службами SSIS](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager).

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>Использование Data Lake Store с хранилищем данных SQL
Можно использовать PolyBase tooload данных из хранилища Озера данных Azure в хранилище данных SQL. См. дополнительные сведения об [использовании Data Lake Store с хранилищем данных SQL](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md).

## <a name="see-also"></a>См. также
* [Обзор хранилища озера данных Azure](data-lake-store-overview.md)
* [Начало работы с хранилищем озера данных с помощью портала](data-lake-store-get-started-portal.md)
* [Начало работы с хранилищем озера данных с помощью PowerShell](data-lake-store-get-started-powershell.md)  

