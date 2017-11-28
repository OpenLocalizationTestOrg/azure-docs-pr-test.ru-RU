---
title: "Устранение неполадок с YARN с помощью Azure HDInsight | Документация Майкрософт"
description: "Получите ответы на распространенные вопросы о работе с Apache Hadoop YARN и Azure HDInsight."
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
ms.openlocfilehash: 63f2d88ad59661b7fbcffd0aaeb94c58d40bdb73
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="4a227-104">Устранение неполадок с YARN с помощью Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4a227-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="4a227-105">Ознакомьтесь с основными проблемами и их разрешением при работе с полезными данными Apache Hadoop YARN в Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="4a227-105">Learn about the top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="4a227-106">Как создать очередь YARN в кластере?</span><span class="sxs-lookup"><span data-stu-id="4a227-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="4a227-107">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="4a227-107">Resolution steps</span></span> 

<span data-ttu-id="4a227-108">Чтобы создать очередь YARN и выполнить балансировку выделения емкости для всех очередей, выполните следующие шаги с помощью Ambari.</span><span class="sxs-lookup"><span data-stu-id="4a227-108">Use the following steps in Ambari to create a new YARN queue, and then balance the capacity allocation among all the queues.</span></span> 

<span data-ttu-id="4a227-109">В этом примере емкость двух имеющихся очередей (**default** и **thriftsvr**) изменяется с 50 % на 25 %, что позволяет обеспечить для новой очереди (spark) емкость 50 %.</span><span class="sxs-lookup"><span data-stu-id="4a227-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity to 25% capacity, which gives the new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="4a227-110">Очередь</span><span class="sxs-lookup"><span data-stu-id="4a227-110">Queue</span></span> | <span data-ttu-id="4a227-111">Capacity</span><span class="sxs-lookup"><span data-stu-id="4a227-111">Capacity</span></span> | <span data-ttu-id="4a227-112">Максимальная емкость</span><span class="sxs-lookup"><span data-stu-id="4a227-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4a227-113">по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4a227-113">default</span></span> | <span data-ttu-id="4a227-114">25 %</span><span class="sxs-lookup"><span data-stu-id="4a227-114">25%</span></span> | <span data-ttu-id="4a227-115">50 %</span><span class="sxs-lookup"><span data-stu-id="4a227-115">50%</span></span> |
| <span data-ttu-id="4a227-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="4a227-116">thrftsvr</span></span> | <span data-ttu-id="4a227-117">25 %</span><span class="sxs-lookup"><span data-stu-id="4a227-117">25%</span></span> | <span data-ttu-id="4a227-118">50 %</span><span class="sxs-lookup"><span data-stu-id="4a227-118">50%</span></span> |
| <span data-ttu-id="4a227-119">spark</span><span class="sxs-lookup"><span data-stu-id="4a227-119">spark</span></span> | <span data-ttu-id="4a227-120">50 %</span><span class="sxs-lookup"><span data-stu-id="4a227-120">50%</span></span> | <span data-ttu-id="4a227-121">50 %</span><span class="sxs-lookup"><span data-stu-id="4a227-121">50%</span></span> |

1. <span data-ttu-id="4a227-122">Выберите значок **просмотров Ambari**, а затем выберите шаблон сетки.</span><span class="sxs-lookup"><span data-stu-id="4a227-122">Select the **Ambari Views** icon, and then select the grid pattern.</span></span> <span data-ttu-id="4a227-123">После этого выберите **диспетчер очереди YARN**.</span><span class="sxs-lookup"><span data-stu-id="4a227-123">Next, select **YARN Queue Manager**.</span></span>

    ![Выбор значка просмотров Ambari](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="4a227-125">Выберите очередь **по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="4a227-125">Select the **default** queue.</span></span>

    ![Выбор очереди default](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="4a227-127">Для очереди **default** измените **емкость** с 50 % на 25 %.</span><span class="sxs-lookup"><span data-stu-id="4a227-127">For the **default** queue, change the **capacity** from 50% to 25%.</span></span> <span data-ttu-id="4a227-128">Для очереди **thriftsvr** измените **емкость** на 25 %.</span><span class="sxs-lookup"><span data-stu-id="4a227-128">For the **thriftsvr** queue, change the **capacity** to 25%.</span></span>

    ![Изменение емкости до 25 % для очередей default и thriftsvr](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="4a227-130">Нажмите кнопку **Add Queue** (Добавить очередь), чтобы создать очередь.</span><span class="sxs-lookup"><span data-stu-id="4a227-130">To create a new queue, select **Add Queue**.</span></span>

    ![Выбор кнопки Add Queue (Добавить очередь)](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="4a227-132">Присвойте имя новой очереди.</span><span class="sxs-lookup"><span data-stu-id="4a227-132">Name the new queue.</span></span>

    ![Имя Spark для новой очереди](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="4a227-134">Оставьте значение **емкости** 50 %, а затем выберите кнопку **Действия**.</span><span class="sxs-lookup"><span data-stu-id="4a227-134">Leave the **capacity** values at 50%, and then select the **Actions** button.</span></span>

    ![Выбор кнопки "Действия"](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="4a227-136">Выберите команду **Save and Refresh Queues** (Сохранить и обновить очереди).</span><span class="sxs-lookup"><span data-stu-id="4a227-136">Select **Save and Refresh Queues**.</span></span>

    ![Выбор Save and Refresh Queues (Сохранить и обновить очереди)](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="4a227-138">После применения эти изменения сразу же появятся на пользовательском интерфейсе планировщика YARN.</span><span class="sxs-lookup"><span data-stu-id="4a227-138">These changes are visible immediately on the YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="4a227-139">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4a227-139">Additional reading</span></span>

- <span data-ttu-id="4a227-140">[Hadoop: Capacity Scheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html) (Hadoop: планировщик ресурсов)</span><span class="sxs-lookup"><span data-stu-id="4a227-140">[YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)</span></span>


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="4a227-141">Как скачать журналы YARN из кластера?</span><span class="sxs-lookup"><span data-stu-id="4a227-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="4a227-142">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="4a227-142">Resolution steps</span></span> 

1. <span data-ttu-id="4a227-143">Подключитесь к кластеру HDInsight с помощью клиента Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="4a227-143">Connect to the HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="4a227-144">Подробные сведения см. в разделе [Дополнительные материалы](#additional-reading-2).</span><span class="sxs-lookup"><span data-stu-id="4a227-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="4a227-145">Чтобы получить список всех идентификаторов текущих выполняемых приложений YARN, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4a227-145">To list all the application IDs of the YARN applications that are currently running, run the following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="4a227-146">Идентификаторы перечислены в столбце **APPLICATIONID**.</span><span class="sxs-lookup"><span data-stu-id="4a227-146">The IDs are listed in the **APPLICATIONID** column.</span></span> <span data-ttu-id="4a227-147">Вы можете скачать журналы из столбца **APPLICATIONID**.</span><span class="sxs-lookup"><span data-stu-id="4a227-147">You can download logs from the **APPLICATIONID** column.</span></span>

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

3. <span data-ttu-id="4a227-148">Чтобы скачать журналы для всех основных контейнеров приложения YARN, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4a227-148">To download YARN container logs for all application masters, use the following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="4a227-149">Будет создан файл журнала с именем amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4a227-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="4a227-150">Чтобы скачать журналы только для последнего основного контейнера приложения YARN, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4a227-150">To download YARN container logs for only the latest application master, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="4a227-151">Будет создан файл журнала с именем latestamlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4a227-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="4a227-152">Чтобы скачать журналы для первых двух основных контейнеров приложения YARN, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4a227-152">To download YARN container logs for the first two application masters, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="4a227-153">Будет создан файл журнала с именем first2amlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4a227-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="4a227-154">Чтобы скачать все журналы контейнеров приложения YARN, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4a227-154">To download all YARN container logs, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="4a227-155">Будет создан файл журнала с именем logs.txt.</span><span class="sxs-lookup"><span data-stu-id="4a227-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="4a227-156">Чтобы скачать журнал контейнера YARN для определенного контейнера, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4a227-156">To download the YARN container log for a specific container, use the following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="4a227-157">Будет создан файл журнала с именем containerlogs.txt.</span><span class="sxs-lookup"><span data-stu-id="4a227-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="4a227-158"><a name="additional-reading-2"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4a227-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="4a227-159">Подключение к HDInsight (Hadoop) с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="4a227-159">Connect to HDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- <span data-ttu-id="4a227-160">[APACHE HADOOP YARN — CONCEPTS AND APPLICATIONS](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/) (Apache Hadoop YARN: приложения и основные понятия)</span><span class="sxs-lookup"><span data-stu-id="4a227-160">[Apache Hadoop YARN concepts and applications](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)</span></span>







