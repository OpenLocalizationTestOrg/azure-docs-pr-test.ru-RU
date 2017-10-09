---
title: "aaaUse Hadoop Hive и удаленного рабочего стола в HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как tooconnect tooHadoop кластера в HDInsight с помощью удаленного рабочего стола, а затем запустите запросов Hive с помощью hello Hive интерфейс командной строки."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Использование Hive с Hadoop в HDInsight с помощью удаленного рабочего стола
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

В этой статье вы узнаете, как tooan tooconnect HDInsight кластер с помощью удаленного рабочего стола, а затем запустите Hive запросов с использованием hello Hive интерфейс командной строки (CLI).

> [!IMPORTANT]
> Удаленный рабочий стол доступен только в кластерах HDInsight, использование в качестве hello операционной системы Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Для HDInsight 3.4 или выше в разделе [используйте Hive с HDInsight и Beeline](hdinsight-hadoop-use-hive-beeline.md) сведения об использовании запросов Hive непосредственно на hello кластера из командной строки.

## <a id="prereq"></a>Предварительные требования
в этой статье инструкциям toocomplete hello, вам потребуется hello следующие:

* Кластер HDInsight на платформе Windows (Hadoop в HDInsight).
* Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.

## <a id="connect"></a>Подключение к удаленному рабочему столу
Включить удаленный рабочий стол для кластера HDInsight hello, а затем соедините tooit в соответствии с инструкциями hello в [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Команда Hive hello
При подключении toohello рабочий стол для кластера HDInsight hello, используйте следующие шаги toowork с Hive hello:

1. С рабочего стола HDInsight hello, запустите hello **командной строки Hadoop**.
2. Введите следующая команда toostart hello Hive CLI hello:

        %hive_home%\bin\hive

    При запуске hello CLI, вы увидите строку hello Hive CLI: `hive>`.
3. С помощью hello (CLI), введите следующие инструкции toocreate новую таблицу с именем hello **log4jLogs** использует образец данных:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Эти операторы выполняют hello, следующие действия:

   * **DROP TABLE**: Удаляет hello таблицы и файла данных hello, существует ли таблица hello.
   * **CREATE EXTERNAL TABLE**: создание новой "внешней" таблицы в Hive. Внешние таблицы хранить только определение таблицы hello в кусте (приветствия данные остаются в исходном расположении hello).

     > [!NOTE]
     > Предполагается, что базовые данные toobe обновлены из внешнего источника (например, в процессе загрузки данных) или другой операцией MapReduce hello, когда требуется, чтобы последние данные toouse hello запросов Hive, следует использовать внешние таблицы.
     >
     > Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.
     >
     >
   * **ФОРМАТ СТРОК**: сообщает Hive форматирование данных hello. В этом случае hello полей в каждом журнале разделенные пробелом.
   * **ХРАНИМЫЕ РАСПОЛОЖЕНИЕ текстового файла AS**: сообщает Hive, где данные hello хранимых (hello данные примера и каталог), которые он хранится в виде текста.
   * **ВЫБЕРИТЕ**: выбирает число всех строк где столбца **t4** содержит значение hello **[ошибка]**. Эта команда должна вернуть значение **3** , так как данное значение содержат три строки.
   * **INPUT__FILE__NAME LIKE '%.log'** — указывает Hive, что вернуть нужно только данные из файлов с расширением LOG. Это ограничивает hello toohello поиска sample.log файл, содержащий данные hello и предотвращает возвращение данных из других примере файлы данных, которые не соответствуют схеме hello, который мы определили.
4. Hello используйте следующие инструкции toocreate новую таблицу «internal» с именем **журналы ошибок**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Эти операторы выполняют hello, следующие действия:

   * **CREATE TABLE IF NOT EXISTS**: создание таблицы, если она до этого не существовала. Поскольку hello **ВНЕШНИХ** не используется ключевое слово, это внутренней таблицы, которые хранятся в хранилище данных Hive hello и полностью управляются Hive.

     > [!NOTE]
     > В отличие от **ВНЕШНИХ** таблиц, удаление внутренней таблицы также удаляет hello базовым данным.
     >
     >
   * **ORC ХРАНИМОЙ AS**: сохраняет hello данные в табличном формате (ORC) оптимизированного строки. Это высокооптимизированный и эффективный формат для хранения данных Hive.
   * **INSERT OVERWRITE ... ВЫБЕРИТЕ**: выбирает строки из hello **log4jLogs** таблицы, которые содержат **[ошибка]**, а затем вставки данных hello в hello **журналы ошибок** таблицы.

     tooverify, только строки, которые содержат **[ошибка]** в столбец t4 были хранимых toohello **журналы ошибок** таблицы, используйте hello, следующая инструкция tooreturn Здравствуйте, все строки из **журналы ошибок**:

       SELECT * from errorLogs;

     В результате операции должны быть возвращены три строки, в которых столбец t4 содержит значение **[ERROR]** .

## <a id="summary"></a>Сводка
Как видите, hello hello Hive команда предоставляет toointeractively простой способ выполнения запросов Hive в кластере HDInsight, монитор hello состояние задания и получение выходных данных hello.

## <a id="nextsteps"></a>Дальнейшие действия
Общая информация о Hive в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)

При использовании Tez с куста см. следующие документы отладочной информации hello:

* [Использовать hello Tez пользовательского интерфейса на основе Windows HDInsight](hdinsight-debug-tez-ui.md)
* [Использовать hello Ambari Tez представление на основе Linux HDInsight](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
