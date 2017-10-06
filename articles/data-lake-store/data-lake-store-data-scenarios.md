---
title: "aaaData сценариях, включающих хранилище Озера данных | Документы Microsoft"
description: "Понять hello различных сценариев и средств с использованием данных, которые можно полученный, обработки, загрузки и визуализируется в хранилище Озера данных"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>Использование хранилища озера данных Azure для потребностей больших данных
Процесс обработки больших данных состоит из указанных далее четырех ключевых этапов.

* Прием больших объемов данных в хранилище данных в режиме реального времени или в пакетах
* Обработка данных hello
* Загрузка данных hello
* Визуализация данных hello

В этой статье мы рассмотрим эти этапы с учетом tooAzure хранилища Озера данных toounderstand hello параметры и инструменты, доступные toomeet потребностями большие наборы данных.

## <a name="ingest-data-into-data-lake-store"></a>Прием данных в хранилище озера данных
В этом разделе описываются различные источники данных и hello различными способами, в котором эти данные можно ingested в учетную запись хранилища Озера данных hello.

![Прием данных в Data Lake Store](./media/data-lake-store-data-scenarios/ingest-data.png "прием данных в Data Lake Store")

### <a name="ad-hoc-data"></a>Специальные данные
Это небольшие наборы данных, которые используются для создания прототипов приложений для работы с большими данными. Существуют различные способы Массовая передача данных ad hoc, в зависимости от источника данных, hello hello.

| источник данных | Средство для приема |
| --- | --- |
| Локальный компьютер |<ul> <li>[Портал Azure](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[Кроссплатформенный интерфейс командной строки Azure 2.0](data-lake-store-get-started-cli-2.0.md)</li> <li>[Data Lake Tools для Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Большой двоичный объект хранилища Azure |<ul> <li>[Фабрика данных Azure](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[инструмента AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[DistCp, запущенный на кластере HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>Потоковые данные
Это данные, создаваемые различными источниками, такими как приложения, устройства, датчики и т. д. Для ввода этих данных в хранилище озера данных можно использовать множество средств. Эти средства обычно будет запись и обработка данных hello на основе событий, событий в режиме реального времени и затем записывать события hello в пакеты в хранилище Озера данных, чтобы их можно дополнительно обработать.

Ниже перечислены средства, которые можно использовать:

* [Azure Stream Analytics](../stream-analytics/stream-analytics-data-lake-output.md) -события, полученный в концентраторы событий могут быть написаны Озера данных tooAzure выход хранилища Озера данных Azure.
* [Azure HDInsight Storm](../hdinsight/hdinsight-storm-write-data-lake-store.md) -данные можно записать напрямую в хранилище Озера tooData из hello Storm кластера.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) — может получать события из концентраторов событий и затем снова записывать ее хранилища Озера tooData с помощью hello [SDK .NET для хранилища Озера данных](data-lake-store-get-started-net-sdk.md).

### <a name="relational-data"></a>Реляционные данные
Можно также извлекать данные из реляционных баз данных. В течение определенного периода времени реляционные базы данных собирают огромные объемы данных, которые после обработки с помощью конвейера больших данных могут предоставлять ценные сведения. Можно использовать следующие средства toomove hello такие данные в хранилище Озера данных.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Фабрика данных Azure](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Данные журналов веб-сервера (отправка с помощью настраиваемых приложений)
Этот тип набора данных выявляется специально, поскольку анализа веб-сервера журнала данных является распространенным вариантом применения для больших данных приложения и требует больших объемов toobe файлы журнала отправлен toohello хранилища Озера данных. Можно использовать любой из hello следующие средства toowrite собственных сценариев или приложений tooupload таких данных.

* [Кроссплатформенный интерфейс командной строки Azure 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Пакет SDK для .NET хранилища озера данных Azure](data-lake-store-get-started-net-sdk.md)
* [Фабрика данных Azure](../data-factory/data-factory-data-movement-activities.md)

Для загрузки веб-сервера журнала данных, а также для отправки других типов данных (например социальных sentiments) — хорошее подход toowrite собственные пользовательские скрипты или приложения, так как она предоставляет hello tooinclude гибкости компонент в процессе передачи данных приложения больших данных большего размера. В некоторых случаях этот код может быть hello форме скрипта или простой командной строки. В других случаях hello код может быть используется toointegrate Обработка больших данных в бизнес-приложения или решения.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Данные, связанные с кластерами HDInsight Azure
Большинство типов кластера HDInsight (Hadoop, HBase, Storm) поддерживают хранилище озера данных в качестве репозитория хранения данных. Кластеры HDInsight обращаются к данным из BLOB-объектов хранилища Azure (WASB). Для повышения производительности можно скопировать данные hello WASB в учетную запись хранилища Озера данных, связанные с кластером hello. Можно использовать следующие средства toocopy hello данные hello.

* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)
* [Служба AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
* [Фабрика данных Azure](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>Данные, хранящиеся в локальных кластерах Hadoop или кластерах Hadoop в IaaS
Большие объемы данных могут храниться в кластерах Hadoop, размещенных локально на компьютерах, использующих HDFS. кластеры Hadoop Hello возможно при развертывании на локальном или в кластере IaaS в Azure. Возможно, существуют требования toocopy таких данных tooAzure хранилища Озера данных подходе одноразовых или повторяющихся образом. Существуют различные варианты, которые можно использовать tooachieve это. Ниже приведен список альтернативных вариантов и hello соответствующие компромиссы.

| Подход | Сведения | Преимущества | Рекомендации |
| --- | --- | --- | --- |
| Использовать данные toocopy фабрики данных Azure (ADF) напрямую из хранилища Озера данных tooAzure кластеров Hadoop |[ADF поддерживает HDFS в качестве источника данных.](../data-factory/data-factory-hdfs-connector.md) |ADF реализована готовая поддержка HDFS, а также первоклассные инструменты комплексного управления и мониторинга. |Требуется шлюз управления данными toobe развернуть локально или в кластере IaaS hello |
| Экспорт данных из Hadoop в виде файлов. Затем скопируйте hello файлы tooAzure хранилища Озера данных с помощью соответствующего механизма. |Можно скопировать файлы tooAzure хранилища Озера данных с помощью: <ul><li>[Azure PowerShell только для Windows](data-lake-store-get-started-powershell.md)</li><li>[Кроссплатформенный интерфейс командной строки Azure 2.0 для ОС, отличных от Windows](data-lake-store-get-started-cli-2.0.md)</li><li>Пользовательское приложение, использующее любой пакет SDK Data Lake Store</li></ul> |Tooget быстрого запуска. Возможны настраиваемые передачи данных. |Многоэтапный процесс с использованием нескольких технологий. Отслеживание и управление ими будет увеличиваться toobe запрос по времени, выделенного характер hello настроенные hello средства |
| Используйте Distcp toocopy данные из Hadoop tooAzure хранилища. Затем скопируйте данные из хранилища tooData хранилища Озера Azure с помощью соответствующего механизма. |Можно скопировать данные из хранилища Озера tooData хранилища Azure с помощью: <ul><li>[Фабрика данных Azure](../data-factory/data-factory-data-movement-activities.md)</li><li>[инструмента AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[Apache DistCp, запущенный в кластерах HDInsight](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |Можно использовать инструменты с открытым кодом. |Многоэтапный процесс с использованием нескольких технологий. |

### <a name="really-large-datasets"></a>Очень большие наборы данных
Для передачи данных наборы данных, которые изменяются в несколько терабайт, с помощью описанных выше методов hello иногда может быть медленной и дорогостоящей. В таких случаях можно использовать приведенные ниже параметры hello.

* **Использование Azure ExpressRoute.** Azure ExpressRoute позволяет создавать закрытые соединения между ЦОД Azure и вашей локальной инфраструктурой. Это надежный вариант для передачи больших объемов данных. Дополнительные сведения см. в [техническом обзоре ExpressRoute](../expressroute/expressroute-introduction.md).
* **Автономная передача данных**. Если с помощью Azure ExpressRoute не может быть выполнено по любой причине, можно использовать [службы импорта и экспорта Azure](../storage/common/storage-import-export-service.md) tooship жестких дисков с центре обработки данных Azure tooan данных. Данные будут первый загруженный tooAzure хранилища больших двоичных объектов. Затем можно использовать [фабрики данных Azure](../data-factory/data-factory-azure-datalake-connector.md) или [средство AdlCopy](data-lake-store-copy-data-azure-storage-blob.md) toocopy данные из хранилища Озера tooData больших двоичных объектов хранилища Azure.

  > [!NOTE]
  > Хотя с помощью hello службы импорта и экспорта, hello размеры файлов на приветствия center отправки данных tooAzure диски не должны иметь размер более 195 ГБ.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Обработка данных, хранящихся в хранилище озера данных 
После hello данные недоступны в хранилище Озера данных можно выполнить анализ что данных с помощью hello поддерживается больших данных приложений. В настоящее время можно использовать Azure HDInsight и аналитики Озера данных Azure задания анализа данных toorun на hello данные, хранящиеся в хранилище Озера данных.

![Анализ данных в Data Lake Store](./media/data-lake-store-data-scenarios/analyze-data.png "Анализ данных в Data Lake Store")

Можно найти в следующих примерах hello.

* [Создание кластера HDInsight с хранилищем озера данных в качестве хранилища](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Загрузка данных из хранилища озера данных
Может также требуется toodownload или переместить данные из хранилища Озера данных Azure для сценариев, таких как:

* Перемещение данных tooother репозиториев toointerface с существующие конвейеры обработки данных. Например, вам может потребоваться toomove данные из хранилища Озера данных tooAzure базы данных SQL или локальным SQL Server.
* Загрузка данных tooyour локального компьютера для обработки в среде IDE при построении прототипов приложений.

![Вывод данных из Data Lake Store](./media/data-lake-store-data-scenarios/egress-data.png "вывод данных из Data Lake Store")

В таких случаях можно использовать любой из следующих вариантов hello:

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Фабрика данных Azure](../data-factory/data-factory-data-movement-activities.md)
* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)

Также можно использовать следующие методы toowrite hello данные toodownload скрипта или приложения из хранилища Озера данных.

* [Кроссплатформенный интерфейс командной строки Azure 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Пакет SDK для .NET хранилища озера данных Azure](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Визуализация данных в хранилище озера данных
Можно использовать сочетание служб toocreate визуальных представлений данных, хранящихся в хранилище Озера данных.

![Визуализация данных в Data Lake Store](./media/data-lake-store-data-scenarios/visualize-data.png "визуализация данных в Data Lake Store")

* Можно запустить с помощью [фабрики данных Azure toomove данные из хранилища Озера данных tooAzure хранилище данных SQL](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* После этого вы можете [интеграции Power BI с хранилищем данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate визуальное представление данных hello.
