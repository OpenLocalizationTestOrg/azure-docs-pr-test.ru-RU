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
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="4b03f-104">Устранение неполадок с YARN с помощью Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b03f-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="4b03f-105">Дополнительные сведения о hello основные проблемы и способы их устранения при работе с полезными данными Apache Hadoop YARN Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="4b03f-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="4b03f-106">Как создать очередь YARN в кластере?</span><span class="sxs-lookup"><span data-stu-id="4b03f-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="4b03f-107">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="4b03f-107">Resolution steps</span></span> 

<span data-ttu-id="4b03f-108">Используйте hello следующих действий в Ambari toocreate новую очередь YARN и затем сбалансировать выделение емкости hello среди всех очередей hello.</span><span class="sxs-lookup"><span data-stu-id="4b03f-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="4b03f-109">В этом примере два существующих очередей (**по умолчанию** и **thriftsvr**) и изменяются из 50% мощности too25% емкости, что дает hello новой очереди (spark) 50% емкости.</span><span class="sxs-lookup"><span data-stu-id="4b03f-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="4b03f-110">Очередь</span><span class="sxs-lookup"><span data-stu-id="4b03f-110">Queue</span></span> | <span data-ttu-id="4b03f-111">Capacity</span><span class="sxs-lookup"><span data-stu-id="4b03f-111">Capacity</span></span> | <span data-ttu-id="4b03f-112">Максимальная емкость</span><span class="sxs-lookup"><span data-stu-id="4b03f-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b03f-113">по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4b03f-113">default</span></span> | <span data-ttu-id="4b03f-114">25 %</span><span class="sxs-lookup"><span data-stu-id="4b03f-114">25%</span></span> | <span data-ttu-id="4b03f-115">50 %</span><span class="sxs-lookup"><span data-stu-id="4b03f-115">50%</span></span> |
| <span data-ttu-id="4b03f-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="4b03f-116">thrftsvr</span></span> | <span data-ttu-id="4b03f-117">25 %</span><span class="sxs-lookup"><span data-stu-id="4b03f-117">25%</span></span> | <span data-ttu-id="4b03f-118">50 %</span><span class="sxs-lookup"><span data-stu-id="4b03f-118">50%</span></span> |
| <span data-ttu-id="4b03f-119">spark</span><span class="sxs-lookup"><span data-stu-id="4b03f-119">spark</span></span> | <span data-ttu-id="4b03f-120">50 %</span><span class="sxs-lookup"><span data-stu-id="4b03f-120">50%</span></span> | <span data-ttu-id="4b03f-121">50 %</span><span class="sxs-lookup"><span data-stu-id="4b03f-121">50%</span></span> |

1. <span data-ttu-id="4b03f-122">Выберите hello **Ambari представления** значок и выберите hello сетка-шаблон.</span><span class="sxs-lookup"><span data-stu-id="4b03f-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="4b03f-123">После этого выберите **диспетчер очереди YARN**.</span><span class="sxs-lookup"><span data-stu-id="4b03f-123">Next, select **YARN Queue Manager**.</span></span>

    ![Выберите значок представления Ambari hello](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="4b03f-125">Выберите hello **по умолчанию** очереди.</span><span class="sxs-lookup"><span data-stu-id="4b03f-125">Select hello **default** queue.</span></span>

    ![Выберите очередь по умолчанию hello](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="4b03f-127">Для hello **по умолчанию** очередь, измените hello **емкость** из too25 50% %.</span><span class="sxs-lookup"><span data-stu-id="4b03f-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="4b03f-128">Для hello **thriftsvr** очередь, измените hello **емкость** too25%.</span><span class="sxs-lookup"><span data-stu-id="4b03f-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![Изменить % too25 hello емкости для очередей и thriftsvr по умолчанию hello](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="4b03f-130">Выберите новую очередь toocreate **добавить очередь**.</span><span class="sxs-lookup"><span data-stu-id="4b03f-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![Выбор кнопки Add Queue (Добавить очередь)](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="4b03f-132">Имя новой очереди hello.</span><span class="sxs-lookup"><span data-stu-id="4b03f-132">Name hello new queue.</span></span>

    ![Имя очереди hello Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="4b03f-134">Оставьте hello **емкость** значения на 50% и затем выберите hello **действия** кнопки.</span><span class="sxs-lookup"><span data-stu-id="4b03f-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![Нажмите кнопку "hello действия"](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="4b03f-136">Выберите команду **Save and Refresh Queues** (Сохранить и обновить очереди).</span><span class="sxs-lookup"><span data-stu-id="4b03f-136">Select **Save and Refresh Queues**.</span></span>

    ![Выбор Save and Refresh Queues (Сохранить и обновить очереди)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="4b03f-138">Эти изменения, отображаются сразу же при hello YARN интерфейса планировщика заданий.</span><span class="sxs-lookup"><span data-stu-id="4b03f-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="4b03f-139">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4b03f-139">Additional reading</span></span>

- <span data-ttu-id="4b03f-140">[Hadoop: Capacity Scheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html) (Hadoop: планировщик ресурсов)</span><span class="sxs-lookup"><span data-stu-id="4b03f-140">[YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)</span></span>


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="4b03f-141">Как скачать журналы YARN из кластера?</span><span class="sxs-lookup"><span data-stu-id="4b03f-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="4b03f-142">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="4b03f-142">Resolution steps</span></span> 

1. <span data-ttu-id="4b03f-143">Подключите кластер HDInsight toohello с помощью клиента Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="4b03f-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="4b03f-144">Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="4b03f-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="4b03f-145">toolist все hello идентификаторов приложения hello YARN приложений, запущенных в данный момент, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="4b03f-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="4b03f-146">Hello идентификаторы перечислены в hello **APPLICATIONID** столбца.</span><span class="sxs-lookup"><span data-stu-id="4b03f-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="4b03f-147">Вы можете загрузить журналы из hello **APPLICATIONID** столбца.</span><span class="sxs-lookup"><span data-stu-id="4b03f-147">You can download logs from hello **APPLICATIONID** column.</span></span>

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

3. <span data-ttu-id="4b03f-148">toodownload YARN контейнера журналы для всех шаблонов приложения, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4b03f-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="4b03f-149">Будет создан файл журнала с именем amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4b03f-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="4b03f-150">журналы контейнера YARN toodownload для только hello последние приложения базы данных master, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4b03f-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="4b03f-151">Будет создан файл журнала с именем latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4b03f-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="4b03f-152">журналы контейнера YARN toodownload для первого шаблонов два приложения hello, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4b03f-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="4b03f-153">Будет создан файл журнала с именем first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4b03f-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="4b03f-154">использовать все журналы YARN контейнера, toodownload hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4b03f-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="4b03f-155">Будет создан файл журнала с именем logs.txt.</span><span class="sxs-lookup"><span data-stu-id="4b03f-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="4b03f-156">toodownload hello YARN журнал контейнер для конкретного контейнера, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4b03f-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="4b03f-157">Будет создан файл журнала с именем containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4b03f-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="4b03f-158"><a name="additional-reading-2"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4b03f-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="4b03f-159">Подключиться с помощью SSH tooHDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="4b03f-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- <span data-ttu-id="4b03f-160">[APACHE HADOOP YARN — CONCEPTS AND APPLICATIONS](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Apache Hadoop YARN: приложения и основные понятия)</span><span class="sxs-lookup"><span data-stu-id="4b03f-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)</span></span>







