---
title: "aaaTroubleshoot Hive с помощью Azure HDInsight | Документы Microsoft"
description: "Ответы toocommon вопросов о работе с Apache Hive и Azure HDInsight."
keywords: "Azure HDInsight, Hive, вопросы и ответы, руководство по устранению неполадок, часто задаваемые вопросы"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Устранение неполадок в Hive с помощью Azure HDInsight

Дополнительные сведения о наиболее важные вопросы hello и способы их устранения при работе с Apache Hive полезных данных в Apache Ambari.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Как экспортировать хранилище метаданных Hive и импортировать его в другой кластер?


### <a name="resolution-steps"></a>Способы устранения

1. Подключите кластер HDInsight toohello с помощью клиента Secure Shell (SSH). Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-end).

2. Выполните следующую команду в кластере HDInsight hello, из которого нужно метахранилище hello tooexport hello.

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  Эта команда создает файл с именем allatables.sql.

3. Скопируйте hello файл alltables.sql toohello новый кластер HDInsight, а затем запустите hello следующую команду:

  ```apache
  hive -f alltables.sql
  ```

Hello кода hello устранению предполагает, что данные, которые являются пути на новый кластер hello hello таким же как пути к данным hello hello старом кластере. Если отличаются пути к данным hello, можно вручную отредактировать созданные hello alltables.sql файл tooreflect любые изменения.

### <a name="additional-reading"></a>Дополнительные материалы

- [Подключите кластер HDInsight tooan с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Как найти журналы Hive в кластере?

### <a name="resolution-steps"></a>Способы устранения

1. Подключите кластер HDInsight toohello с помощью SSH. Подробные сведения см. в разделе **Дополнительные материалы**.

2. журналы клиента куст tooview, hello используйте следующую команду:

  ```apache
  /tmp/<username>/hive.log 
  ```

3. журналы метахранилища Hive tooview, hello используйте следующую команду:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. журналы Hiveserver tooview, используйте hello следующую команду:

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Дополнительные материалы

- [Подключите кластер HDInsight tooan с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Как запустить hello оболочки Hive с определенных конфигураций в кластере

### <a name="resolution-steps"></a>Способы устранения

1. Укажите пару ключ значение конфигурации при запуске hello Hive оболочки. Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist все действующие конфигурации Hive оболочки, hello используйте следующие команды:

  ```apache
  hive> set;
  ```

  Например можно используйте следующие командной оболочки куст toostart журнала отладки на консоль hello hello:

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Дополнительные материалы

- [Свойства конфигурации Hive](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Как анализировать данные направленного ациклического графа Tez по критическому пути кластера?


### <a name="resolution-steps"></a>Способы устранения
 
1. подключение toohello кластера HDInsight с помощью SSH, tooanalyze Tez Apache направленный ациклического графа (DAG) на диаграмме кластеров с точки зрения безопасности. Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-end).

2. В командной строке выполните следующую команду hello.
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist других анализаторы, которые можно использовать tooanalyze Tez DAG использовать hello следующую команду:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Пример программы необходимо указать в качестве первого аргумента hello.

  Допустимые имена программы:
    - **ContainerReuseAnalyzer** — печать сведений о повторном использовании контейнера в DAG;
    - **CriticalPath**: критический путь поиска hello в DAG
    - **LocalityAnalyzer** — печать сведений о местоположении в DAG;
    - **ShuffleTimeAnalyzer**: анализ подробностями времени смещения hello в группе DAG
    - **SkewAnalyzer**: анализ hello наклона сведений в группе DAG
    - **SlowNodeAnalyzer** — печать сведений об узле в DAG;
    - **SlowTaskIdentifier** — печать сведений о медленных задачах в DAG;
    - **SlowestVertexAnalyzer** — печать сведений о медленных вершинах в DAG;
    - **SpillAnalyzer** — печать сведений о перемещении в DAG;
    - **TaskConcurrencyAnalyzer**: печать параллелизма сведения о задаче hello в группе DAG
    - **VertexLevelCriticalPathAnalyzer**: hello критическим поиска на уровне вершин в группе DAG


### <a name="additional-reading"></a>Дополнительные материалы

- [Подключите кластер HDInsight tooan с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>Как скачать данные направленного ациклического графа Tez из кластера?


#### <a name="resolution-steps"></a>Способы устранения

Существует два способа toocollect hello Tez DAG данных:

- Из командной строки hello:
 
    Подключите кластер HDInsight toohello с помощью SSH. Hello командной строки выполнив следующую команду hello:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Используйте представление Ambari Tez hello.
   
  1. Go tooAmbari. 
  2. Последовательно выберите tooTez представление (под значком плитки hello в правом верхнем углу hello). 
  3. Выберите hello требуется tooview DAG.
  4. Выберите **Скачать данные**.

### <a name="additional-reading-end"></a>Дополнительные материалы

[Подключите кластер HDInsight tooan с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md)






