---
title: "aaaUse Hadoop Hive с перелистывание в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как отправить tooremotely Pig заданий с помощью перелистывание tooHDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>Выполнение запросов Hive с Hadoop в HDInsight с помощью REST

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Узнайте, как toouse hello WebHCat REST API toorun Hive запросы с Hadoop в кластере Azure HDInsight.

[Curl](http://curl.haxx.se/) — используется toodemonstrate о взаимодействии с HDInsight с помощью необработанных запросов HTTP. Hello [jq](http://stedolan.github.io/jq/) программа — используется tooprocess hello JSON данные, возвращенные из запросов REST.

> [!NOTE]
> Если вы уже знакомы с использованием серверов под управлением Linux Hadoop, но являются новый tooHDInsight, см. раздел hello [необходимые tooknow о Hadoop в HDInsight под управлением Linux](hdinsight-hadoop-linux-information.md) документа.

## <a id="curl"></a>Выполнение запросов Hive

> [!NOTE]
> При использовании перелистывания или любые другие связи REST с WebHCat, должен пройти проверку подлинности запросы hello, предоставляя hello имя пользователя и пароль администратора кластера HDInsight hello.
>
> Hello команды в этом разделе, замените **USERNAME** tooauthenticate toohello hello пользователя кластера и заменить **пароль** hello пароль для учетной записи пользователя hello. Замените **CLUSTERNAME** с hello имя кластера.
>
> Hello API-интерфейса REST является защищен с помощью [обычной проверки подлинности](http://en.wikipedia.org/wiki/Basic_access_authentication). toohelp убедитесь, что учетные данные безопасно всегда отправляются серверу toohello, выполнение запросов с использованием безопасного HTTP (HTTPS).

1. Из командной строки используйте следующие команды tooverify, возможность подключения кластера HDInsight tooyour hello:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Появится примерно toohello ответа, следующий текст:

        {"status":"ok","version":"v1"}

    Ниже приведены параметры Hello, использованный в этой команде.

   * **-u** -hello имя пользователя и пароль используются tooauthenticate hello запроса.
   * **-G** — указывает, что это запрос, являющийся операцией GET.

     Здравствуйте, начало hello URL-адрес, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello одинаково для всех запросов. путь Hello **параметр/Status**, указывает, что hello запрос tooreturn состояние WebHCat (также известный как Templeton) для сервера hello. Можно также запросить hello версии Hive с помощью hello следующую команду:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     Этот запрос возвращает аналогичные toohello ответа, следующий текст:

       {"module":"hive","version":"0.13.0.2.1.6.0-2103"}.

2. Используйте hello, следуя toocreate таблицу с именем **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Привет, следующие параметры, используемые с этим запросом:

   * **-d** — с момента `-G` не используется, hello запроса по умолчанию используется метод POST toohello. `-d`Указывает hello значения данных, отправляемых с запросом hello.

     * **User.Name** -hello пользователя, на котором выполняется команда hello.
     * **выполнение** -hello tooexecute операторы HiveQL.
     * **statusdir** -записывается hello каталог, в котором hello состояния для данного задания.

     Эти операторы выполняют hello, следующие действия:
   * **DROP TABLE** -Если hello таблица уже существует, она будет удалена.
   * **CREATE EXTERNAL TABLE** : создание новой "внешней" таблицы в Hive. Внешние таблицы хранить только определение таблицы hello в кусте. Hello данные остаются в исходном расположении hello.

     > [!NOTE]
     > Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника. Например, процессом автоматизированной передачи данных или другой операцией MapReduce.
     >
     > Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.

   * **ФОРМАТ СТРОК** — как формат данных hello. поля Hello в каждом журнале разделенные пробелом.
   * **ХРАНИМЫЕ РАСПОЛОЖЕНИЕ текстового файла AS** — там, где хранятся данные hello (hello данные примера и каталог) и что он хранится в виде текста.
   * **ВЫБЕРИТЕ** -выбирает число всех строк где столбца **t4** содержит значение hello **[ошибка]**. Эта инструкция возвращает значение **3**, так как данное значение содержат три строки.

     > [!NOTE]
     > Обратите внимание, что hello пробелы между инструкциями HiveQL заменяются hello `+` символов при использовании с Curl. Заключенные в кавычки значения, содержащие символ пробела, такие как разделитель hello не заменяется `+`.

   * **INPUT__FILE__NAME как «% 25.log»** — это инструкция ограничения hello поиска tooonly использовать файлы которых заканчиваются. журнала.

     > [!NOTE]
     > Hello `%25` является форма URL-кодированием hello %, поэтому фактические условия hello `like '%.log'`. Hello % имеет URL-адрес toobe кодировке, как он интерпретируется как специальный символ в URL-адресах.

     Эта команда должна возвращать идентификатора задания, который может быть используется toocheck hello состояние задания hello.

       {"id":"job_1415651640909_0026"}

3. состояние hello toocheck задания hello, hello используйте следующую команду:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Замените **JOBID** с hello значение, возвращенное в предыдущем шаге hello. Например, если hello, возвращают значение было `{"id":"job_1415651640909_0026"}`, затем **JOBID** бы `job_1415651640909_0026`.

    Если задание hello завершена, он имеет состояние hello **успешно**.

   > [!NOTE]
   > Этот запрос перелистывание возвращает документ нотации объектов JavaScript (JSON) с сведения о задании hello. Используется Jq tooretrieve только hello значение состояния.

4. После hello состояние задания hello изменилось слишком**успешно**, результаты hello hello задания можно получить из хранилища больших двоичных объектов Azure. Hello `statusdir` параметр, передаваемый с запросом hello содержит расположение hello hello выходного файла; в данном случае **/пример/перелистывание**. Этот адрес hello результаты сохраняются hello **примере/перелистывание** каталог в hello кластеров хранения по умолчанию.

    Можно перечислить и загрузить эти файлы с помощью hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Дополнительные сведения об использовании hello Azure CLI со службой хранилища Azure см. в разделе hello [использование Azure CLI 2.0 со службой хранилища Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) документа.

5. Hello используйте следующие инструкции toocreate новую таблицу «internal» с именем **журналы ошибок**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Эти операторы выполняют hello, следующие действия:

   * **CREATE TABLE IF NOT EXISTS** : создание таблицы, если она до этого не существовала. Эта инструкция создает внутренней таблицы, которые хранятся в хранилище данных Hive hello и полностью управляются Hive.

     > [!NOTE]
     > В отличие от внешних таблиц при удалении внутренней таблицы удаляются hello базовые данные.

   * **ORC ХРАНИМОЙ AS** -хранит данные hello в оптимизированные строк по столбцам (формат ORC.). Это высокооптимизированный и эффективный формат для хранения данных Hive.
   * **INSERT OVERWRITE ... ВЫБЕРИТЕ** -выбирает строки из hello **log4jLogs** таблицы, которые содержат **[ошибка]**, а затем вставки данных hello в hello **журналы ошибок** таблицы.
   * **ВЫБЕРИТЕ** -выбирает все строки из нового hello **журналы ошибок** таблицы.

6. Используйте идентификатор задания hello, возвращенное состояние hello toocheck hello задания. После его успешного использования hello Azure CLI, как описано ранее toodownload и просмотр результатов hello. Hello выход должен содержать три строки, которые содержат **[ошибка]**.

## <a id="nextsteps"></a>Дальнейшие действия

Общая информация об использовании Hive в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight.

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)

При использовании Tez с куста см. следующие документы отладочной информации hello:

* [Использовать hello Ambari Tez представление на основе Linux HDInsight](hdinsight-debug-ambari-tez-view.md)

Дополнительные сведения о hello API REST, используемые в этом документе в разделе hello [WebHCat ссылки](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) документа.

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


