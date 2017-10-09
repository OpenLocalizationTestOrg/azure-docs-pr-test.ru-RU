---
title: "aaaInstall и использовать Giraph на HDInsight (Hadoop) - Azure | Документы Microsoft"
description: "Узнайте, как tooinstall Giraph на основе Linux HDInsight кластеры, использующие действий скрипта. Действия сценариев позволяют toocustomize hello кластера во время создания, путем изменения конфигурации кластера или установка служб и программ."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Установка Giraph в кластерах HDInsight Hadoop и крупномасштабных графы tooprocess Giraph

Узнайте, как tooinstall Apache Giraph в кластере HDInsight. Hello скрипт действие hdinsight, позволяет toocustomize кластера, запустив сценарий bash. Сценарии могут быть кластеров используется toocustomize во время и после создания кластера.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whatis"></a>Что такое Giraph

[Apache Giraph](http://giraph.apache.org/) дает graph tooperform обработки с помощью Hadoop и может использоваться с Azure HDInsight. Графы моделируют взаимоотношения между объектами. Например hello подключений между маршрутизаторами в больших сетях, например hello Интернет или связи между пользователями в социальных сетях. Обработка Graph позволяет tooreason о hello связей между объектами в граф, такие как:

* определение потенциальных друзей на основе текущих взаимоотношений;

* Определение hello кратчайший маршрут между двумя компьютерами в сети.

* Вычисление ранга hello страницы веб-страниц.

> [!WARNING]
> Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются - службу технической поддержки Майкрософт помогает tooisolate и разрешить проблемы toothese связанные компоненты.
>
> Пользовательские компоненты, такие как Giraph, получать toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello. Службу технической поддержки Майкрософт может быть проблема может tooresolving hello. В противном случае необходимо обратиться в сообщество разработчиков открытого кода, обладающих большим опытом в этой сфере. Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).


## <a name="what-hello-script-does"></a>Какие hello скрипта

Скрипт выполняет следующие действия hello.

* Устанавливает Giraph слишком`/usr/hdp/current/giraph`

* Копирует hello `giraph-examples.jar` toodefault хранилище файлов (WASB) для кластера:`/example/jars/giraph-examples.jar`

## <a name="install"></a>Установка Giraph с помощью действий сценария

Пример сценария tooinstall Giraph в кластере HDInsight доступна на hello следующие расположения:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

В этом разделе описано, как toouse hello образец скрипта при создании hello кластера с помощью портала Azure hello.

> [!NOTE]
> Действие сценария можно применить, используя любой из следующих методов hello:
> * Azure PowerShell
> * Hello Azure CLI
> * Hello HDInsight .NET SDK
> * Шаблоны диспетчера ресурсов Azure
> 
> Можно также применить tooalready действия сценария работающие кластеры. Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

1. Начать создание кластера с помощью действия hello в [кластеры HDInsight под управлением Linux, создать](hdinsight-hadoop-create-linux-clusters-portal.md), но не завершайте создания.

2. На hello **необязательная конфигурация** колонке выберите **действия скрипта**и укажите hello следующую информацию:

   * **ИМЯ**: Введите понятное имя для действия сценария hello.

   * **URI СКРИПТА**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh.

   * **Головной**: установите флажок.

   * **Рабочий**: не устанавливайте этот флажок.

   * **ZOOKEEPER**: не устанавливайте этот флажок.

   * **ПАРАМЕТРЫ**: оставьте это поле пустым.

3. Внизу hello hello **действия скрипта**, использовать hello **выберите** конфигурация hello toosave кнопок. Наконец, используйте hello **выберите** кнопку внизу hello hello **необязательная конфигурация** колонке toosave hello необязательная конфигурация сведения.

4. Продолжить создание кластера hello, как описано в [кластеры HDInsight под управлением Linux, создать](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>Как использовать Giraph в HDInsight

После создания hello кластера с помощью hello, входящий в состав Giraph SimpleShortestPathsComputation пример действия toorun hello ниже. В этом примере используется hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) реализацию для обнаружения hello кратчайшего пути между объектами в граф.

1. Подключите кластер HDInsight toohello с помощью SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Используйте hello следующая команда toocreate файл с именем **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Используйте hello после текста как hello содержимое этого файла:

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Эти данные описывает связь между объектами в направленный граф, используя формат hello `[source_id, source_value,[[dest_id], [edge_value],...]]`. Каждая строка представляет взаимоотношение между объектом `source_id` и одним или несколькими объектами `dest_id`. Hello `edge_value` можно рассматривать как стойкость hello или расстояние hello соединения между `source_id` и `dest\_id`.

    Рисования, используя значение hello (или вес) в качестве hello расстояния между объектами, hello данных может выглядеть, как hello, следующая схема:

    ![tiny_graph.txt начерчен в виде кругов с линиями различной длины между](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. toosave hello файла, используйте **Ctrl + X**, затем **Y**и, наконец, **ввод** имя файла tooaccept hello.

4. Используйте следующие данные toostore hello в основного хранилища для кластера HDInsight hello.

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Выполнение примера SimpleShortestPathsComputation hello, с помощью hello следующую команду:

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    в hello в следующей таблице описаны Hello параметров, используемых с помощью следующей команды:

   | Параметр | Действие |
   | --- | --- |
   | `jar` |Hello jar файл, содержащий примеры hello. |
   | `org.apache.giraph.GiraphRunner` |Класс Hello использовать примеры toostart hello. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |пример Hello, используется. В этом примере вычисляется hello кратчайшего пути между Идентификатором 1 и все идентификаторы в hello graph. |
   | `-ca mapred.job.tracker` |Hello головному узлу кластера hello. |
   | `-vif` |Hello toouse входной формат для hello входных данных. |
   | `-vip` |файл входных данных Hello. |
   | `-vof` |Формат вывода Hello. В данном примере — ИД и значение в виде обычного текста. |
   | `-op` |выходное расположение Hello. |
   | `-w 2` |Количество работников toouse Hello. В этом примере — 2. |

    Дополнительные сведения об этих и других параметров, используемых с образцами Giraph см. в разделе hello [краткое руководство Giraph](http://giraph.apache.org/quick_start.html).

6. По завершении задания hello hello результаты сохраняются в hello **/example/out/shotestpaths** каталога. Hello имена выходных файлов начинаются с **часть-m -** и заканчиваться число, указывающее hello во-первых, во-вторых, т. д. файл. Используйте следующие выходные данные команды tooview hello hello.

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    Hello вывод должен выглядеть примерно toohello после текста:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    Пример SimpleShortestPathComputation Hello является жестко заданный toostart с Идентификатором 1 объекта и поиска hello кратчайший путь tooother объектов. Hello выводится в формате hello `destination_id` и `distance`. Hello `distance` равно hello значение (вес) границ hello пути между объектом с Идентификатором 1 и идентификатором hello объекта.

    Визуализации, можно проверить результаты hello, проходящих hello кратчайшего пути между Идентификатором 1 и других объектов. Hello кратчайшего пути между 1 идентификатор и идентификатор 4 — 5. Это значение является hello общее расстояние между <span style="color:orange">идентификатор 1 и 3</span>, а затем <span style="color:red">идентификатор 3 и 4</span>.

    ![Представление объектов в виде кругов с кратчайшими путями между ними](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Установка и использование Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md).

* [Установка Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md).
