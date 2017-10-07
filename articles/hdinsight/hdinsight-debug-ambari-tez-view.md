---
title: "aaaUse Ambari Tez представление с HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как hello toouse Ambari Tez Просмотр заданий Tez toodebug на HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Использование представления Ambari toodebug Tez заданий в HDInsight

Hello Ambari веб-интерфейса для HDInsight содержит Tez представление, которое может быть используется toounderstand и отладка задания, использующие Tez. представление Tez Hello позволяет toovisualize hello задания как граф соединенными элементами можно перейти к каждому элементу и получить статистические данные и сведения о ведении журнала.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md#hdinsight-windows-retirement)

## <a name="prerequisites"></a>Предварительные требования

* Кластер HDInsight под управлением Linux. Инструкции по созданию кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).
* Современный веб-браузер, который поддерживает HTML5.

## <a name="understanding-tez"></a>Общие сведения о Tez

Tez — это расширяемая платформа для обработки данных в Hadoop, которая характеризуется более высокими скоростями по сравнению с традиционной обработкой MapReduce. Для кластеров HDInsight под управлением Linux именно модуль по умолчанию hello для куста.

Tez создает направленный ациклического графа (DAG), описывающий hello порядок действий, которые требуются для работы. Индивидуальные действия, называются вершин и выполнять часть hello задание в целом. Hello фактическое выполнение работы hello, описываемого вершина вызывается задача и могут быть распределены по нескольким узлам в кластере hello.

### <a name="understanding-hello-tez-view"></a>Основные сведения о hello Tez представление

Hello Tez представление предоставляет исторические данные и сведения для процессов, работающих под управлением. Здесь можно просмотреть, как задание распределяется по кластерам. Она также отображает счетчики, используемые задачи и вершин и сведения об ошибках, связанных с toohello задания. Он может предложить полезную информацию в hello следующие сценарии:

* Наблюдение за процессами длительное время, просмотр hello ход выполнения сопоставления и сокращения.
* Анализ исторических данных для toolearn успешной или неуспешной процессы, как можно улучшить обработку или причину сбоя.

## <a name="generate-a-dag"></a>Создание DAG

представление содержит данные, только если задание, использующее hello Tez ядра Tez Hello выполняется в данный момент или ранее выполнялись. Простые запросы Hive можно разрешить без использования Tez. Подсистема Tez требуется для работы с более сложными запросами, которые выполняют фильтрацию, группировку, следует используйте механизм Tez hello.

Используйте следующие шаги toorun запрос Hive, который использует Tez hello.

1. В веб-браузере перейдите toohttps://CLUSTERNAME.azurehdinsight.net, где **CLUSTERNAME** — hello имя кластера HDInsight.

2. Hello меню вверху hello страницы приветствия выберите hello **представления** значок. Он выглядит как набор квадратов. В раскрывающемся списке hello, который отображается, выберите **Hive представление**.

    ![Выбор представления Hive](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. При загрузке hello представление Hive, вставить hello ниже запроса в редактор запросов hello и нажмите кнопку **выполнение**.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    После завершения задания hello, вы должны увидеть результаты hello, отображаемых в hello **результаты процесса запроса** раздела. Hello результаты должны быть примерно toohello следующий текст:

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. Выберите hello **журнала** вкладки. Можно увидеть примерно toohello сведения после текста:

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Сохранить hello **идентификатор приложения** значение, так как это значение используется в следующем разделе hello.

## <a name="use-hello-tez-view"></a>Используйте представление Tez hello

1. Hello меню вверху hello страницы приветствия выберите hello **представления** значок. В раскрывающемся списке hello, который отображается, выберите **Tez представление**.

    ![Выбор представления Tez](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. При загрузке hello представление Tez видно, что список запросов hive, выполняющихся в данный момент, или была выполнена на hello кластера.

    ![Все DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. Если имеется только одна запись, он предназначен для запроса hello, выполнялись в предыдущем разделе hello. Если у вас есть несколько записей, можно выполнить поиск с помощью полей hello вверху hello страницы приветствия.

4. Выберите hello **идентификатор запроса** для запроса Hive. Отображаются сведения о запросе hello.

    ![Сведения о DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. Hello вкладки на этой странице разрешить hello tooview следующую информацию:

    * **Запрос сведений**: сведения о запроса Hive hello.
    * **Временная шкала**: сведения о том, сколько времени занял каждый этап обработки.
    * **Конфигурации**: hello конфигурацию, используемую для этого запроса.

    Из __сведения о запросе__ можно использовать ссылки на сведения toofind hello о hello __приложения__ или hello __DAG__ для этого запроса.
    
    * Hello __приложения__ связи отображаются сведения о hello YARN приложения для этого запроса. Здесь можно получить доступ к журналы приложений YARN hello.
    * Hello __DAG__ связи отображаются сведения о hello ориентированного ациклического графа для этого запроса. Здесь можно просмотреть графическое представление hello DAG. Также можно найти сведения о hello вершин в hello DAG.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как просмотреть toouse hello Tez, Дополнительные сведения о [с помощью Hive в HDInsight](hdinsight-use-hive.md).

Более подробные технические сведения о Tez см. в разделе hello [Tez страницу в Hortonworks](http://hortonworks.com/hadoop/tez/).

Дополнительные сведения об использовании Ambari с HDInsight см. в разделе [управление кластерами HDInsight с помощью hello Ambari веб-интерфейса](hdinsight-hadoop-manage-ambari.md)
