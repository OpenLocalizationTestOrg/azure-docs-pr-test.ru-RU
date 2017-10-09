---
title: "aaaUse Hadoop Pig с REST в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как кластер задания toouse REST toorun латиница Pig в Hadoop в Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>Выполнение заданий Pig с помощью REST с использованием Hadoop в HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Узнайте, как toorun Pig латиница заданий, делая кластера Azure HDInsight tooan запросов REST. Перелистывание — используется toodemonstrate взаимодействие с HDInsight с помощью API-интерфейса REST WebHCat hello.

> [!NOTE]
> Если вы уже знакомы с использованием серверов под управлением Linux Hadoop, но являются новый tooHDInsight, см. раздел [советы HDInsight под управлением Linux](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Предварительные требования

* Кластер Azure HDInsight (Hadoop в HDInsight) (на платформе Linux или Windows).

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Curl](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Выполнение заданий Pig с помощью Curl

> [!NOTE]
> Hello API-интерфейса REST является защищен с помощью [базовая проверка подлинности доступа](http://en.wikipedia.org/wiki/Basic_access_authentication). Всегда выполнять запросы, используя свои учетные данные безопасно отправляются серверу toohello tooensure безопасного HTTP (HTTPS).
>
> При использовании команд hello в этом разделе, замените `USERNAME` tooauthenticate toohello hello пользователя кластера и заменить `PASSWORD` hello пароль для учетной записи пользователя hello. Замените `CLUSTERNAME` с hello имя кластера.
>


1. Из командной строки используйте следующие команды tooverify, возможность подключения кластера HDInsight tooyour hello:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Должно появиться после ответа JSON hello.

        {"status":"ok","version":"v1"}

    Ниже приведены параметры Hello, использованный в этой команде.

    * **-u**: hello имя пользователя и пароль используются tooauthenticate hello запроса
    * **-G** — указывает, что этот запрос является запросом GET.

     Здравствуйте, начало hello URL-адрес, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello одинаково для всех запросов. путь Hello **параметр/Status**, указывает, этот запрос hello состояние hello tooreturn WebHCat (также известный как Templeton) для сервера hello.

2. Используйте следующий код toosubmit кластера toohello задания Pig латиница hello.

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    Ниже приведены параметры Hello, использованный в этой команде.

    * **-d**: поскольку `-G` не используется, hello запроса по умолчанию используется метод POST toohello. `-d`Указывает hello значения данных, отправляемых с запросом hello.

    * **User.Name**: hello пользователь, выполняющий команду hello
    * **выполнение**: hello tooexecute инструкций Латинская Pig
    * **statusdir**: hello, hello состояния для этого задания является записи в каталог

    > [!NOTE]
    > Обратите внимание, что пробелы hello в инструкциях латиница Pig заменяются hello `+` символов при использовании с Curl.

    Эта команда должна возвращать идентификатора задания, который может быть используется toocheck hello состояние задания hello, например:

        {"id":"job_1415651640909_0026"}

3. состояние hello toocheck задания hello, hello используйте следующую команду

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     Замените `JOBID` с hello значение, возвращенное в предыдущем шаге hello. Например, если hello, возвращают значение было `{"id":"job_1415651640909_0026"}`, затем `JOBID` — `job_1415651640909_0026`.

    Если задание hello завершена, он имеет состояние hello **успешно**.

    > [!NOTE]
    > Этот запрос перелистывание возвращает документ JavaScript Object Notation (JSON) с сведения о задании hello и jq tooretrieve используется только hello значение состояния.

## <a id="results"></a>Просмотр результатов

При изменении состояния hello hello задания слишком**успешно**, можно получить результаты задания hello hello. Hello `statusdir` параметр, передаваемый с запросом hello содержит расположение hello hello выходного файла; в данном случае `/example/pigcurl`.

HDInsight можно использовать в качестве хранилища данных по умолчанию hello хранилища Azure или хранилища Озера данных Azure. Существуют различные способы tooget hello данных, в зависимости от того, какой из них использовать. Дополнительные сведения см. раздел хранилища hello hello [HDInsight под управлением Linux сведения](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) документа.

## <a id="summary"></a>Сводка

Как показано в этом документе, можно использовать необработанные toorun запроса HTTP, монитор и просмотреть результаты hello задания Pig в кластере HDInsight.

Дополнительные сведения о hello интерфейс REST, используемые в этой статье в разделе hello [WebHCat ссылка](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

## <a id="nextsteps"></a>Дальнейшие действия

Общая информация о Pig в HDInsight:

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)
