---
title: "aaaUse Hadoop Sqoop с перелистывание в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как tooremotely передан tooHDInsight Sqoop заданий, с помощью Curl."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Выполнение заданий Sqoop с Hadoop в HDInsight с помощью Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Узнайте, как кластер toouse Curl toorun Sqoop заданий на Hadoop в HDInsight.

Перелистывание — используется toodemonstrate о взаимодействии с HDInsight с помощью необработанных toorun запросов HTTP, монитор и получить результаты hello Sqoop заданий. Это работает с использованием hello WebHCat API-Интерфейсу REST (прежнее название — Templeton) с кластером HDInsight.

> [!NOTE]
> Если вы уже знакомы с использованием серверов под управлением Linux Hadoop, но являются новый tooHDInsight, см. раздел [сведения об использовании HDInsight в Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
в этой статье инструкциям toocomplete hello, вам потребуется hello следующие:

* Hadoop в кластере HDInsight (на платформе Linux или Windows)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Отправка заданий Sqoop с помощью Curl
> [!NOTE]
> При использовании перелистывания или любые другие связи REST с WebHCat, должен пройти проверку подлинности запросы hello, предоставляя hello имя пользователя и пароль администратора кластера HDInsight hello. Как использовать запросы toohello toosend hello server часть hello универсальный код ресурса (URI), необходимо также использовать имя кластера hello.
> 
> Hello команды в этом разделе, замените **USERNAME** tooauthenticate toohello hello пользователя кластера и заменить **пароль** hello пароль для учетной записи пользователя hello. Замените **CLUSTERNAME** с hello имя кластера.
> 
> Hello API-интерфейса REST является защищен с помощью [обычной проверки подлинности](http://en.wikipedia.org/wiki/Basic_access_authentication). Всегда должны выполнять запросы с помощью безопасного HTTP (HTTPS) toohelp убедитесь, что учетные данные безопасно отправляются toohello сервера.
> 
> 

1. Из командной строки используйте следующие команды tooverify, возможность подключения кластера HDInsight tooyour hello:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Должно появиться ответа аналогичные toohello следующее:
   
        {"status":"ok","version":"v1"}
   
    Ниже приведены параметры Hello, использованный в этой команде.
   
   * **-u** -hello имя пользователя и пароль используются tooauthenticate hello запроса.
   * **-G** — указывает, что это запрос GET.
     
     Здравствуйте, начало hello URL-адрес, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, будет hello одинаково для всех запросов. путь Hello **параметр/Status**, указывает, что hello запрос tooreturn состояние WebHCat (также известный как Templeton) для сервера hello. 
2. Используйте следующие toosubmit задание sqoop hello.

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    Ниже приведены параметры Hello, использованный в этой команде.

    * **-d** — с момента `-G` не используется, hello запроса по умолчанию используется метод POST toohello. `-d`Указывает hello значения данных, отправляемых с запросом hello.

        * **User.Name** -hello пользователя, на котором выполняется команда hello.

        * **команда** -hello tooexecute команда Sqoop.

        * **statusdir** -будет записан hello каталог, в котором hello состояния для данного задания.

    Эта команда должна возвращать идентификатора задания, который может быть используется toocheck hello состояние задания hello.

        {"id":"job_1415651640909_0026"}

1. состояние hello toocheck задания hello, hello используйте следующую команду. Замените **JOBID** с hello значение, возвращенное в предыдущем шаге hello. Например, если hello, возвращают значение было `{"id":"job_1415651640909_0026"}`, затем **JOBID** бы `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Если задание hello завершена, будет иметь состояние hello **успешно**.
   
   > [!NOTE]
   > Этот запрос перелистывание возвращает документ нотации объектов JavaScript (JSON) с сведения о задании hello; используется jq tooretrieve только hello значение состояния.
   > 
   > 
2. После hello состояние задания hello изменилось слишком**успешно**, результаты hello hello задания можно получить из хранилища больших двоичных объектов Azure. Hello `statusdir` параметр, передаваемый с запросом hello содержит расположение hello hello выходного файла; в данном случае **wasb: / / / пример/перелистывание**. Этот адрес сохраняет выходные данные hello задания hello в hello **примере/перелистывание** на контейнера хранилища по умолчанию hello, используемого кластером HDInsight.
   
    Можно перечислить и загрузить эти файлы с помощью hello [Azure CLI](../cli-install-nodejs.md). Например, файлы toolist в **примере/перелистывание**, использовать hello следующую команду:
   
        azure storage blob list <container-name> example/curl
   
    toodownload файл, используйте hello ниже:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > Необходимо указать имя учетной записи хранения hello, содержащее hello blob с помощью hello `-a` и `-k` параметры или набор hello **AZURE\_ХРАНЕНИЯ\_учетную запись** и **AZURE\_ХРАНЕНИЯ\_доступа\_ключ** переменные среды. См. также: <a href="hdinsight-upload-data.md" target="_blank".
   > 
   > 

## <a name="limitations"></a>Ограничения
* Для массового экспорта — под управлением Linux с HDInsight, hello Sqoop соединитель, используемый tooexport данных tooMicrosoft SQL Server или база данных SQL Azure в настоящее время не поддерживает операции массовой вставки.
* Пакетное выполнение — с hdinsight под управлением Linux, при использовании hello `-batch` переход при выполнении вставки, Sqoop будет выполнять вставку нескольких вместо Пакетная обработка операций вставки hello.

## <a name="summary"></a>Сводка
Как показано в этом документе, можно использовать необработанные toorun запроса HTTP, монитор и просмотр результатов hello Sqoop заданий в кластере HDInsight.

Дополнительные сведения о hello интерфейс REST, используемые в этой статье в разделе hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">руководство по Sqoop REST API</a>.

## <a name="next-steps"></a>Дальнейшие действия
Общая информация об использовании Hive в HDInsight:

* [Использование Sqoop с Hadoop в HDInsight (Windows)](hdinsight-use-sqoop.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight.

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)

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


