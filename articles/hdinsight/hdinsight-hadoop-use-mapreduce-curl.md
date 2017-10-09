---
title: "aaaUse MapReduce и Curl на Hadoop в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как tooremotely запуска задания MapReduce с Hadoop в HDInsight с помощью Перелистывание."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>Выполнение заданий MapReduce с помощью REST в Hadoop в HDInsight

Узнайте, как toouse hello WebHCat REST API toorun MapReduce заданий на Hadoop в кластере HDInsight. Перелистывание — используется toodemonstrate о взаимодействии с HDInsight с помощью необработанных задания MapReduce toorun запросов HTTP.

> [!NOTE]
> Если вы уже знакомы с использованием серверов под управлением Linux Hadoop, но существует новый tooHDInsight, см. раздел hello [необходимые tooknow о под управлением Linux Hadoop в HDInsight](hdinsight-hadoop-linux-information.md) документа.


## <a id="prereq"></a>Предварительные требования

* Hadoop в кластере HDInsight.
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Выполнение заданий MapReduce с помощью Curl

> [!NOTE]
> При использовании с WebHCat перелистывания или любые другие связи REST должен пройти проверку подлинности запросы hello, указав имя пользователя администратора кластера HDInsight hello и пароль. Имя кластера hello необходимо использовать как часть URI, который является сервером toohello запросы hello используется toosend hello.
>
> Hello команды в этом разделе, замените **USERNAME** с кластером toohello tooauthenticate hello пользователя, и **пароль** hello пароль для учетной записи пользователя hello. Замените **CLUSTERNAME** с hello имя кластера.
>
> Hello REST API обеспечивается с помощью [базовая проверка подлинности доступа](http://en.wikipedia.org/wiki/Basic_access_authentication). Всегда должны выполнять запросы, используя свои учетные данные безопасно отправляются серверу toohello tooensure HTTPS.


1. Из командной строки используйте следующие команды tooverify, возможность подключения кластера HDInsight tooyour hello:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Должно появиться примерно toohello ответа, следуя JSON.

        {"status":"ok","version":"v1"}

    Ниже приведены параметры Hello, использованный в этой команде.

   * **-u**: указывает hello имя пользователя и пароль используются tooauthenticate hello запроса
   * **-G**: указывает, что это запрос GET.

     Здравствуйте, начало hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello одинаково для всех запросов.

2. toosubmit задание MapReduce hello используйте следующую команду:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    конец Hello hello URI (/ mapreduce и jar) сообщает WebHCat, этот запрос запускает задание MapReduce из класса в jar-файл. Ниже приведены параметры Hello, использованный в этой команде.

   * **-d**: `-G` не используется, поэтому hello запроса по умолчанию используется метод POST toohello. `-d`Указывает hello значения данных, отправляемых с запросом hello.
    * **User.Name**: hello пользователь, выполняющий команду hello
    * **JAR**: hello расположение hello jar-файл, содержащий класс toobe выполнялись
    * **Класс**: hello класса, содержащего логику MapReduce hello
    * **arg**: hello аргументы toobe передан toohello задания MapReduce. В этом случае hello входной текстовый файл и hello каталог, которые используются для вывода hello

     Эта команда должна возвращать идентификатора задания, который может быть состояние hello используется toocheck hello задания:

       {"id":"job_1415651640909_0026"}

3. состояние hello toocheck задания hello, hello используйте следующую команду:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Замените hello **JOBID** с hello значение, возвращенное в предыдущем шаге hello. Например, если hello, возвращают значение было `{"id":"job_1415651640909_0026"}`, затем hello JOBID бы `job_1415651640909_0026`.

    При задании hello hello состояние возвращается `SUCCEEDED`.

   > [!NOTE]
   > Этот запрос перелистывание возвращает документ JSON с сведения о задании hello. Используется Jq tooretrieve только hello значение состояния.

4. При изменении состояния hello hello задания слишком`SUCCEEDED`, можно получить результаты задания hello hello из хранилища больших двоичных объектов Azure. Hello `statusdir` параметр, передаваемый с запросом hello содержит расположение hello hello выходного файла. В этом примере — расположение hello `/example/curl`. Этот адрес сохраняет hello выходные данные задания hello в хранилище по умолчанию hello кластеров в `/example/curl`.

Можно перечислить и загрузить эти файлы с помощью hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Дополнительные сведения о работе с большими двоичными объектами из hello Azure CLI см. в разделе hello [использование hello Azure CLI 2.0 со службой хранилища Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) документа.

## <a id="nextsteps"></a>Дальнейшие действия

Общая информация о заданиях MapReduce в HDInsight:

* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)

Дополнительные сведения о hello интерфейс REST, который используется в этой статье в разделе hello [WebHCat ссылка](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).
