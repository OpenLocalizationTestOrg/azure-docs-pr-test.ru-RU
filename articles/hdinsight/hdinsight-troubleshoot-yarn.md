---
title: "aaaTroubleshoot YARN с помощью Azure HDInsight | Документы Microsoft"
description: "Ответы toocommon вопросов о работе с Apache Hadoop YARN и Azure HDInsight."
keywords: "Azure HDInsight, YARN, вопросы и ответы, руководство по устранению неполадок, часто задаваемые вопросы"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>Устранение неполадок с YARN с помощью Azure HDInsight

Дополнительные сведения о hello основные проблемы и способы их устранения при работе с полезными данными Apache Hadoop YARN Apache Ambari.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>Как создать очередь YARN в кластере?


### <a name="resolution-steps"></a>Способы устранения 

Используйте hello следующих действий в Ambari toocreate новую очередь YARN и затем сбалансировать выделение емкости hello среди всех очередей hello. 

В этом примере два существующих очередей (**по умолчанию** и **thriftsvr**) и изменяются из 50% мощности too25% емкости, что дает hello новой очереди (spark) 50% емкости.
| Очередь | Capacity | Максимальная емкость |
| --- | --- | --- | --- |
| по умолчанию | 25 % | 50 % |
| thrftsvr | 25 % | 50 % |
| spark | 50 % | 50 % |

1. Выберите hello **Ambari представления** значок и выберите hello сетка-шаблон. После этого выберите **диспетчер очереди YARN**.

    ![Выберите значок представления Ambari hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. Выберите hello **по умолчанию** очереди.

    ![Выберите очередь по умолчанию hello](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Для hello **по умолчанию** очередь, измените hello **емкость** из too25 50% %. Для hello **thriftsvr** очередь, измените hello **емкость** too25%.

    ![Изменить % too25 hello емкости для очередей и thriftsvr по умолчанию hello](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. Выберите новую очередь toocreate **добавить очередь**.

    ![Выбор кнопки Add Queue (Добавить очередь)](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Имя новой очереди hello.

    ![Имя очереди hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Оставьте hello **емкость** значения на 50% и затем выберите hello **действия** кнопки.

    ![Нажмите кнопку "hello действия"](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. Выберите команду **Save and Refresh Queues** (Сохранить и обновить очереди).

    ![Выбор Save and Refresh Queues (Сохранить и обновить очереди)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

Эти изменения, отображаются сразу же при hello YARN интерфейса планировщика заданий.

### <a name="additional-reading"></a>Дополнительные материалы

- [Hadoop: Capacity Scheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html) (Hadoop: планировщик ресурсов)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>Как скачать журналы YARN из кластера?


### <a name="resolution-steps"></a>Способы устранения 

1. Подключите кластер HDInsight toohello с помощью клиента Secure Shell (SSH). Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-2).

2. toolist все hello идентификаторов приложения hello YARN приложений, запущенных в данный момент, выполните следующую команду hello:

    ```apache
    yarn top
    ```
    Hello идентификаторы перечислены в hello **APPLICATIONID** столбца. Вы можете загрузить журналы из hello **APPLICATIONID** столбца.

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. toodownload YARN контейнера журналы для всех шаблонов приложения, используйте hello следующую команду:
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    Будет создан файл журнала с именем amlogs.txt. 

4. журналы контейнера YARN toodownload для только hello последние приложения базы данных master, используйте hello следующую команду:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    Будет создан файл журнала с именем latestamlogs.txt. 

4. журналы контейнера YARN toodownload для первого шаблонов два приложения hello, используйте hello следующую команду:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    Будет создан файл журнала с именем first2amlogs.txt. 

5. использовать все журналы YARN контейнера, toodownload hello следующую команду:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    Будет создан файл журнала с именем logs.txt. 

6. toodownload hello YARN журнал контейнер для конкретного контейнера, hello используйте следующую команду:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    Будет создан файл журнала с именем containerlogs.txt.

### <a name="additional-reading-2"></a>Дополнительные материалы

- [Подключиться с помощью SSH tooHDInsight (Hadoop)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [APACHE HADOOP YARN — CONCEPTS AND APPLICATIONS](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Apache Hadoop YARN: приложения и основные понятия)







