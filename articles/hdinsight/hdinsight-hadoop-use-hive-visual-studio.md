---
title: "aaaHive со средствами Озера данных (Hadoop) для Visual Studio — Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse hello Озера данных tools для Visual Studio toorun Apache Hive запросов с помощью Apache Hadoop в Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Выполнять запросы Hive, с помощью средств hello Озера данных для Visual Studio

Узнайте, как Озера данных hello toouse tools для Visual Studio tooquery Apache Hive. Hello Озера данных средства позволяют tooeasily создавать, отправлять и отслеживать tooHadoop запросов Hive в Azure HDInsight.

## <a id="prereq"></a>Предварительные требования

* Кластер Azure HDInsight (Hadoop в HDInsight).

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (один из следующих версий hello):

    * Visual Studio 2013 Community, Professional, Premium или Ultimate с обновлением 4

    * Visual Studio 2015 (любой выпуск)

    * Visual Studio 2017 (любой выпуск)

* Средства HDInsight для Visual Studio или инструменты Azure Data Lake Tools для Visual Studio. В разделе [приступить к работе со средствами Visual Studio Hadoop для HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) сведения об установке и настройке средства hello.

## <a id="run"></a>Выполнять запросы Hive, с помощью Visual Studio hello

1. Откройте **Visual Studio** и выберите **Создать** > **Проект** > **Azure Data Lake** > **HIVE** > **Hive Application** (Приложение Hive). Введите имя этого проекта.

2. Откройте hello **Script.hql** файла, созданного с помощью этого проекта и вставить в следующие инструкции HiveQL hello:

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    Эти операторы выполняют hello, следующие действия:

   * `DROP TABLE`: Если hello таблица существует, эта инструкция удаляет его.

   * `CREATE EXTERNAL TABLE`: создает новую "внешнюю" таблицу в Hive. Внешние таблицы хранить только определение таблицы hello в кусте (приветствия данные остаются в исходном расположении hello).

     > [!NOTE]
     > Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника. Например, с помощью задания MapReduce или службы Azure.
     >
     > Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.

   * `ROW FORMAT`: Указывает способ форматирования hello данных Hive. В этом случае hello полей в каждом журнале разделенные пробелом.

   * `STORED AS TEXTFILE LOCATION`: Указывает Hive там, где hello хранения данных (hello данные примера и каталог) и что он хранится в виде текста.

   * `SELECT`: Установите количество всех строк где столбца `t4` содержит значение hello `[ERROR]`. Эта инструкция должна вернуть значение `3`, так как данное значение содержат три строки.

   * `INPUT__FILE__NAME LIKE '%.log'`: указывает Hive, что вернуть нужно только данные из файлов с расширением LOG. Это предложение ограничивает hello toohello поиска sample.log файл, содержащий данные hello.

3. Выберите hello инструментов hello **кластера HDInsight** требуется toouse для этого запроса. Выберите **отправить** toorun hello инструкциях, как задание куста.

   ![Панель отправки](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. Hello **Hive Сводка заданий** появляется и отображает сведения о выполнении задания hello. Используйте hello **обновление** toorefresh hello задания сведения о ссылке, пока hello **состояние задания** изменяет слишком**завершено**.

   ![Сводка по завершенному заданию](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. Используйте hello **выходные данные задания** связать tooview hello выходные данные этого задания. Он отображает `[ERROR] 3`, которое является значением hello, возвращаемых этим запросом.

6. Запросы Hive можно также отправлять без создания проекта. С помощью **обозревателя сервера** разверните узлы **Azure** > **HDInsight**, щелкните правой кнопкой мыши сервер HDInsight, а затем выберите **Написать запрос Hive**.

7. В hello **temp.hql** документа, отображаемого, добавьте следующие инструкции HiveQL hello:

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    Эти операторы выполняют hello, следующие действия:

   * `CREATE TABLE IF NOT EXISTS`: создает таблицу, если она не существует. Поскольку hello `EXTERNAL` не используется ключевое слово, эта инструкция создает внутреннюю таблицу. Внутренние таблицы хранятся в хранилище данных Hive hello и управляются Hive.

     > [!NOTE]
     > В отличие от `EXTERNAL` таблиц, удаление внутренней таблицы также удаляет hello базовым данным.

   * `STORED AS ORC`-Сохраняет hello данных в табличном формате (ORC) оптимизированного строки. Это высокооптимизированный и эффективный формат для хранения данных Hive.

   * `INSERT OVERWRITE ... SELECT`: Выбирает строки из hello `log4jLogs` таблицы, которые содержат `[ERROR]`, а затем вставки данных hello в hello `errorLogs` таблицы.

8. Панель инструментов hello, выберите **отправить** toorun hello задания. Используйте hello **состояние задания** toodetermine hello задания успешно завершена.

9. tooverify, hello задание создано hello таблицы, используйте **обозревателя серверов** и разверните **Azure** > **HDInsight** > кластеру HDInsight > **Баз данных hive** > **по умолчанию**. Hello **журналы ошибок** таблицы и hello **log4jLogs** , перечислены в таблице.

## <a id="nextsteps"></a>Дальнейшие действия

Как можно видеть, hello средства HDInsight для Visual Studio предоставляют простой способ toowork с запросов Hive в HDInsight.

Общая информация о Hive в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)

* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)

Дополнительные сведения о hello средства HDInsight для Visual Studio:

* [Приступая к работе с инструментами Azure Data Lake (в HDInsight) для Visual Studio для выполнения запроса Hive](hdinsight-hadoop-visual-studio-tools-get-started.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
