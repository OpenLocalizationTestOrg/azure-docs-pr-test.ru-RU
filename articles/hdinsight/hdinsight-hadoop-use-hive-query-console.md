---
title: "aaaUse Hadoop Hive на hello консоль запросов в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse hello веб-консоль запросов toorun запросов Hive в HDInsight Hadoop кластера из браузера."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>Выполнять запросы Hive, с помощью hello консоль запросов
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

В этой статье вы узнаете, как запросы toouse hello консоль запросов HDInsight toorun Hive в HDInsight Hadoop кластера из браузера.

> [!IMPORTANT]
> Hello консоль запросов HDInsight доступна только в кластерах HDInsight под управлением Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> При использовании HDInsight 3.4 или более поздней версии см. сведения о выполнении запросов Hive из браузера: [Использование представления Hive с Hadoop в HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).

## <a id="prereq"></a>Предварительные требования
в этой статье инструкциям toocomplete hello, необходимо будет ниже hello.

* Кластер HDInsight Hadoop на платформе Windows
* Современный браузер

## <a id="run"></a>Выполнять запросы Hive, с помощью hello консоль запросов
1. Откройте веб-браузер и перейдите в слишком**https://CLUSTERNAME.azurehdinsight.net**, где **CLUSTERNAME** — hello имя кластера HDInsight. Если необходимо, введите имя пользователя hello и пароль, который использовался при создании кластера hello.
2. Hello ссылки вверху hello страницы приветствия, выберите **редактор Hive**. Это отображает форму, которая может быть используется tooenter hello HiveQL инструкций, которые должны toorun в кластере HDInsight hello.

    ![Редактор куста Hello](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    Замените текст hello `Select * from hivesampletable` с hello, следующие инструкции HiveQL:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Эти операторы выполняют hello, следующие действия:

   * **DROP TABLE**: Удаляет hello таблицы и файла данных hello, существует ли таблица hello.
   * **CREATE EXTERNAL TABLE**: создание новой "внешней" таблицы в Hive. Внешние таблицы хранят только определение таблицы hello в кусте; Hello данные остаются в исходном расположении hello.

     > [!NOTE]
     > Предполагается, что базовые данные toobe обновлены из внешнего источника (например, в процессе загрузки данных) или другой операцией MapReduce hello, когда требуется, чтобы последние данные toouse hello запросов Hive, следует использовать внешние таблицы.
     >
     > Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.
     >
     >
   * **ФОРМАТ СТРОК**: сообщает Hive форматирование данных hello. В этом случае hello полей в каждом журнале разделенные пробелом.
   * **ХРАНИМЫЕ РАСПОЛОЖЕНИЕ текстового файла AS**: сообщает Hive, где данные hello хранимых (hello данные примера и каталог), которые он хранится в виде текста
   * **ВЫБЕРИТЕ**: выберите количество всех строк где столбца **t4** содержат значение hello **[ошибка]**. Эта команда должна вернуть значение **3** , так как данное значение содержат три строки.
   * **INPUT__FILE__NAME LIKE '%.log'** — указывает Hive, что вернуть нужно только данные из файлов с расширением LOG. Это ограничивает hello toohello поиска sample.log файл, содержащий данные hello и предотвращает возвращение данных из других примере файлы данных, которые не соответствуют схеме hello, который мы определили.
3. Нажмите кнопку **Submit**(Отправить). Hello **сеанса для задания** на hello нижней части страницы приветствия отображать подробные сведения для задания hello.
4. Здравствуйте, когда **состояние** изменяется поле слишком**завершено**выберите **Просмотр сведений о** для задания hello. На странице приветствия, hello **выходные данные задания** содержит `[ERROR]    3`. Можно использовать hello **загрузки** под заголовком toodownload этого поля файла, содержащего hello выходные данные задания hello.

## <a id="summary"></a>Сводка
Как видите, приветствия консоль Query Console предоставляет простой способ toorun запросы Hive в кластер HDInsight наблюдения за состоянием задания hello и получение выходных данных hello.

Выберите toolearn Подробнее об использовании задания Hive toorun консоль запросов Hive, **Приступая к работе** вверху hello hello консоль запросов, воспользуйтесь представленные образцы hello. Каждый пример проведет через процесс использования данных tooanalyze Hive, включая пояснения о операторы HiveQL hello, используемые в образце hello hello.

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
