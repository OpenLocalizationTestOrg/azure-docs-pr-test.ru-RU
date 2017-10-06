---
title: "Действие сценария aaaUse tooinstall Solr на HDInsight под управлением Linux — в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall Solr на основе Linux HDInsight Hadoop кластеры, использующие действий скрипта."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>Установка и использование Solr на кластерах HDInsight Hadoop

Узнайте, как tooinstall Solr на Azure HDInsight с помощью действия сценария. Solr представляет собой многофункциональную платформу поиска и предоставляет возможности поиска корпоративного уровня на основе данных, управляемых Hadoop.

> [!IMPORTANT]
    > Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!IMPORTANT]
> Пример сценария Hello, используемые в этом документе устанавливает Solr 4.9 с указанной конфигурацией. Следует tooconfigure hello Solr кластера с помощью различных коллекций, сегментами, схемы, реплики, т. д. необходимо изменить скрипт hello и двоичные файлы Solr.

## <a name="whatis"></a>Что такое Solr

[Apache Solr](http://lucene.apache.org/solr/features.html) — это корпоративная платформа поиска, предоставляющая многофункциональные инструменты полнотекстового поиска данных. Хотя Hadoop позволяет хранения и управления огромный объем данных, Apache Solr предоставляет возможности поиска hello tooquickly извлекать данные hello.

> [!WARNING]
> Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются корпорацией Майкрософт.
>
> Пользовательские компоненты, такие как Solr, получать toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello. Службы поддержки Майкрософт не может быть может tooresolve проблемы при пользовательские компоненты. Может потребоваться tooengage hello сообществе открытого для получения помощи. Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).

## <a name="what-hello-script-does"></a>Какие hello скрипта

Этот сценарий вносит следующие изменения кластера HDInsight toohello hello:

* Устанавливает Solr 4.9 в `/usr/hdp/current/solr`.
* Создает пользователя, **solrusr**, являющееся hello используется toorun Solr службы
* Наборы **solruser** как владелец hello`/usr/hdp/current/solr`
* Добавляет конфигурацию [Upstart](http://upstart.ubuntu.com/), которая автоматически запускает Solr.

## <a name="install"></a>Установка Solr с помощью действий сценария

Пример сценария tooinstall Solr в кластере HDInsight доступна на hello следующие расположения:

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

toocreate кластер с Solr установлен hello используйте шаги в hello [HDInsight, создания кластеров](hdinsight-hadoop-create-linux-clusters-portal.md) документа. Во время процесса создания hello используйте следующие шаги tooinstall Solr hello.

1. Из hello __Сводка кластера__ колонки, select__Advanced settings__, затем __скрипт действия__. Используйте следующие сведения toopopulate hello формы hello.

   * **ИМЯ**: Введите понятное имя для действия сценария hello.
   * **Универсальный код ресурса скрипта**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/r-installer-v01.sh.
   * **ГОЛОВНОЙ**: установите флажок.
   * **Рабочая роль**: установите флажок.
   * **ZOOKEEPER**: Проверьте tooinstall этот параметр на узле Zookeeper hello
   * **ПАРАМЕТРЫ**: оставьте это поле пустым.

2. Внизу hello hello **скрипт действия** колонки, используйте hello **выберите** конфигурация hello toosave кнопок. Наконец, используйте hello **Далее** toohello tooreturn кнопку __Сводка кластера__

3. Из hello __Сводка кластера__ выберите __создать__ toocreate hello кластера.

## <a name="usesolr"></a>Как использовать Solr в HDInsight

> [!IMPORTANT]
> Hello шаги в этом разделе показывают основные функциональные возможности Solr. Дополнительные сведения об использовании Solr см. в разделе hello [Apache Solr сайта](http://lucene.apache.org/solr/).

### <a name="index-data"></a>Данные индекса

Используйте следующие шаги tooadd пример данных tooSolr hello и затем запрос:

1. Подключите кластер HDInsight toohello с помощью SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

     > [!IMPORTANT]
     > Позже в данном пошаговом руководстве используется SSL туннеля tooconnect toohello Solr пользовательского веб-интерфейса. toouse следующие действия, необходимо установить SSL туннелирования, а затем настройте Ваш браузер toouse его.
     >
     > Дополнительные сведения см. в разделе hello [использование SSH туннелирование с HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) документа.

2. Используйте hello, следующие команды toohave Solr индекс образец данных:

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    Hello следующие выходные данные возвращаются в консоли toohello:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Hello `post.jar` программа добавляет hello **solr.xml** и **monitor.xml** документов toohello индекса.
  
3. Используйте hello следующая команда hello tooquery Solr REST API:

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    Эта команда ищет **collection1** для документов, соответствующих  **\*:\***  (кодируются как \*% 3A\* в строке запроса hello). Следующий документ JSON Hello приведен пример ответа hello.

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>С помощью панели мониторинга Solr hello

панель мониторинга Solr Hello является веб-интерфейса, который позволяет вам toowork с Solr через веб-браузере. панель мониторинга Solr Hello не представлено напрямую в hello Интернет из кластера HDInsight. Можно использовать tooaccess туннель SSH его. Дополнительные сведения об использовании туннель SSH см. в разделе hello [использование SSH туннелирование с HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) документа.

После установления туннель SSH, используйте следующие шаги toouse hello Solr мониторинга hello:

1. Укажите имя узла hello для основной hello головному узлу:

   1. Использование SSH tooconnect toohello головного узла кластера. Например, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       Дополнительные сведения об использовании SSH см. в разделе hello [использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

   2. Используйте следующую команду, tooget hello полное имя узла hello.

        ```bash
        hostname -f
        ```

        Эта команда возвращает значение аналогичные toohello, за которым следует имя узла:

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        Сохраните возвращенное hello, как будет использоваться позднее.

2. В окне браузера подключитесь слишком**http://HOSTNAME:8983/solr / #/**, где **HOSTNAME** является именем hello, определенным в предыдущих шагах hello.

    Hello запросы направляются через hello SSH туннеля toohello Solr веб-интерфейса в кластере. Откроется страница приветствия аналогичные toohello после изображения:

    ![Изображение панели мониторинга Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. В левой области hello, используйте hello **селектор Core** tooselect раскрывающегося списка **collection1**. В разделе **collection1** будет отображено несколько записей.

4. В следующих операциях hello **collection1**выберите **запроса**. Используйте следующие страницы поиска значений toopopulate hello hello.

   * В hello **q** текста введите  **\*:**\*. Этот запрос возвращает все документы hello, которые индексируются в Solr. Если требуется toosearch конкретную строку в документах hello, можно ввести здесь строку.
   * В hello **wt** текстовое поле, выберите hello выходной формат. По умолчанию используется **JSON**.

     Наконец, выберите hello **выполнить запрос** кнопку внизу hello pate поиска hello.

     ![Используйте действие скрипта toocustomize кластера](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     Hello выходных данных возвращается hello, в которых два документа, что вы добавили toohello индекса более ранних версий. Hello выходные данные, аналогичные toohello следовать документ JSON:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>Запуск и остановка Solr

Используйте следующие команды toomanually остановить и запустить Solr hello.

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>Резервное копирование индексированных данных

Используйте следующие шаги tooback хранилищ Solr данных toohello по умолчанию для кластера hello.

1. Подключите кластер toohello с помощью SSH, а затем использовать после имени узла hello tooget команды для головного узла hello hello:

    ```bash
    hostname -f
    ```

2. Следующая команда toocreate моментальный снимок hello hello использование индексированных данных. Замените **HOSTNAME** с именем hello, возвращенные hello предыдущей команде:

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    Hello ответ — примерно toohello следующий XML-код:

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. Измените каталоги слишком`/usr/hdp/current/solr/example/solr`. В нем находятся подкаталоги для каждой коллекции. Каждый каталог коллекции содержит `data` каталог, содержащий hello моментальных снимков для hello коллекции.

4. toocreate собой сжатый архив папки моментальных снимков hello, hello используйте следующую команду:

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Замените hello `snapshot.20150806185338855` значения с именем hello hello моментального снимка для коллекции.

    Эта команда создает архив с именем **snapshot.20150806185338855.tgz**, который содержит содержимое hello hello **snapshot.20150806185338855** каталога.

5. Затем можно сохранить основное хранилище hello архив toohello кластера с помощью hello следующую команду:

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Дополнительные сведения о резервном копировании и восстановлении Solr см. на странице [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).

## <a name="next-steps"></a>Дальнейшие действия

* [Установка Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md). Используйте tooinstall настройки кластера кластеров Giraph на HDInsight Hadoop. Giraph дает graph tooperform обработки с помощью Hadoop и может использоваться с Azure HDInsight.

* [Установка Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md). Используйте оттенка tooinstall настройки кластера в кластерах HDInsight Hadoop. Цветовой тон представляет собой набор веб-приложений, используемых toointeract в кластере Hadoop.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
