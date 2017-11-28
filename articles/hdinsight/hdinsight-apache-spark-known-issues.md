---
title: "Устранение неполадок кластера Apache Spark в Azure HDInsight | Документы Майкрософт"
description: "Сведения о проблемах, связанных с кластерами Apache Spark в Azure HDInsight, и их решении."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="a5c09-103">Известные проблемы в работе кластера Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a5c09-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="a5c09-104">В этом документе отслеживаются все известные проблемы с общедоступной предварительной версией Spark HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a5c09-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="a5c09-105">Утечка интерактивного сеанса Livy</span><span class="sxs-lookup"><span data-stu-id="a5c09-105">Livy leaks interactive session</span></span>
<span data-ttu-id="a5c09-106">При перезапуске Livy во время работы интерактивного сеанса (из Ambari или в связи с перезагрузкой виртуальной машины headnode 0) произойдет утечка сеанса интерактивного задания.</span><span class="sxs-lookup"><span data-stu-id="a5c09-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="a5c09-107">Из-за этого новые задания застревают в состоянии "Принято" и не могут быть запущены.</span><span class="sxs-lookup"><span data-stu-id="a5c09-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="a5c09-108">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="a5c09-108">**Mitigation:**</span></span>

<span data-ttu-id="a5c09-109">Для решения этой проблемы выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="a5c09-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="a5c09-110">Подключитесь к головному узлу по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="a5c09-110">Ssh into headnode.</span></span> <span data-ttu-id="a5c09-111">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a5c09-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a5c09-112">Выполните следующую команду, чтобы найти идентификаторы приложений для интерактивных заданий, запущенных из Livy:</span><span class="sxs-lookup"><span data-stu-id="a5c09-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="a5c09-113">По умолчанию задания, запущенные в интерактивном сеансе Livy без прямо заданных имен, будут иметь имя Livy. Если сеанс Livy запускается из записной книжки Jupyter, имя задания будет начинаться с remotesparkmagics_*.</span><span class="sxs-lookup"><span data-stu-id="a5c09-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="a5c09-114">Чтобы аннулировать эти задания, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a5c09-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="a5c09-115">После этого новые задания начнут выполняться.</span><span class="sxs-lookup"><span data-stu-id="a5c09-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="a5c09-116">Сервер журналов Spark не запускается</span><span class="sxs-lookup"><span data-stu-id="a5c09-116">Spark History Server not started</span></span>
<span data-ttu-id="a5c09-117">Сервер журналов Spark не запускается автоматически после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="a5c09-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="a5c09-118">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="a5c09-118">**Mitigation:**</span></span> 

<span data-ttu-id="a5c09-119">Вручную запустите сервер журналов из Ambari.</span><span class="sxs-lookup"><span data-stu-id="a5c09-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="a5c09-120">Проблема разрешений в каталоге журналов Spark</span><span class="sxs-lookup"><span data-stu-id="a5c09-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="a5c09-121">Когда hdiuser отправляет задание с параметром spark-submit, возникает ошибка java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Отказано в доступе), а журнал драйверов не перезаписывается.</span><span class="sxs-lookup"><span data-stu-id="a5c09-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="a5c09-122">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="a5c09-122">**Mitigation:**</span></span>

1. <span data-ttu-id="a5c09-123">Добавьте hdiuser в группу Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a5c09-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="a5c09-124">После создания кластера предоставьте разрешения 777 для каталога /var/log/spark.</span><span class="sxs-lookup"><span data-stu-id="a5c09-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="a5c09-125">В Ambari измените путь размещения журнала Spark на каталог с разрешениями 777.</span><span class="sxs-lookup"><span data-stu-id="a5c09-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="a5c09-126">Выполните команду spark-submit как sudo.</span><span class="sxs-lookup"><span data-stu-id="a5c09-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="a5c09-127">Соединитель Spark-Phoenix не поддерживается</span><span class="sxs-lookup"><span data-stu-id="a5c09-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="a5c09-128">В настоящее время в кластере HDInsight Spark не поддерживается соединитель Spark-Phoenix.</span><span class="sxs-lookup"><span data-stu-id="a5c09-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="a5c09-129">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="a5c09-129">**Mitigation:**</span></span>

<span data-ttu-id="a5c09-130">Вместо него необходимо использовать соединитель Spark-HBase.</span><span class="sxs-lookup"><span data-stu-id="a5c09-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="a5c09-131">Инструкции см. в записи блога [HDinsight – How to use Spark-HBase connector?](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/) (HDinsight: как использовать соединитель Spark-HBase?)</span><span class="sxs-lookup"><span data-stu-id="a5c09-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="a5c09-132">Проблемы, связанные с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="a5c09-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="a5c09-133">Ниже приведены некоторые известные проблемы, связанные с записными книжками Jupyter.</span><span class="sxs-lookup"><span data-stu-id="a5c09-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="a5c09-134">Записные книжки со знаками не из набора ASCII в именах файлов</span><span class="sxs-lookup"><span data-stu-id="a5c09-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="a5c09-135">Записные книжки Jupyter, которые могут использоваться в кластерах Spark HDInsight, не должны содержать в именах файлов знаки не из набора ASCII.</span><span class="sxs-lookup"><span data-stu-id="a5c09-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="a5c09-136">При попытке передать через пользовательский интерфейс Jupyter файл, имя которого содержит знаки не из набора ASCII, операция просто не будет выполнена без оповещения пользователя (то есть Jupyter не позволит передать файл и не сообщит об ошибке).</span><span class="sxs-lookup"><span data-stu-id="a5c09-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="a5c09-137">Ошибка при загрузке записных книжек большого размера</span><span class="sxs-lookup"><span data-stu-id="a5c09-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="a5c09-138">При загрузке записных книжек большого размера может возникнуть ошибка **`Error loading notebook`** .</span><span class="sxs-lookup"><span data-stu-id="a5c09-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="a5c09-139">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="a5c09-139">**Mitigation:**</span></span>

<span data-ttu-id="a5c09-140">Появление этой ошибки не означает, что данные повреждены или утрачены.</span><span class="sxs-lookup"><span data-stu-id="a5c09-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="a5c09-141">Записные книжки по-прежнему хранятся на диске в каталоге `/var/lib/jupyter`, и вы можете получить к ним доступ, подключившись к кластеру по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="a5c09-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="a5c09-142">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a5c09-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="a5c09-143">После подключения к кластеру с помощью SSH во избежание потери важных данных записные книжки можно скопировать из кластера на локальный компьютер (с помощью SCP или WinSCP), тем самым создав резервную копию.</span><span class="sxs-lookup"><span data-stu-id="a5c09-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="a5c09-144">Затем вы сможете использовать туннель SSH к головному узлу через порт 8001, чтобы получить доступ к Jupyter без прохождения через шлюз.</span><span class="sxs-lookup"><span data-stu-id="a5c09-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="a5c09-145">В Jupyter можно очистить выходные данные записной книжки и повторно сохранить их, чтобы уменьшить ее размер.</span><span class="sxs-lookup"><span data-stu-id="a5c09-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="a5c09-146">Чтобы избежать этой ошибки в будущем, необходимо следовать некоторым рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="a5c09-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="a5c09-147">Записная книжка должна быть небольшого размера.</span><span class="sxs-lookup"><span data-stu-id="a5c09-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="a5c09-148">В записной книжке сохраняются любые выходные данные заданий Spark, которые отправляются обратно в Jupyter.</span><span class="sxs-lookup"><span data-stu-id="a5c09-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="a5c09-149">Рекомендуется не выполнять команду `.collect()` для устойчивых распределенных наборов данных или кадров данных большого размера в Jupyter. Вместо этого, чтобы просмотреть содержимое устойчивого распределенного набора данных, выполните команду `.take()` или `.sample()`. В этом случае выходные данные не будут слишком большими.</span><span class="sxs-lookup"><span data-stu-id="a5c09-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="a5c09-150">Кроме того, если при сохранении записной книжки очистить все ячейки выходных данных, это также поможет уменьшить размер.</span><span class="sxs-lookup"><span data-stu-id="a5c09-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="a5c09-151">Начальная загрузка записной книжки загружается дольше ожидаемого</span><span class="sxs-lookup"><span data-stu-id="a5c09-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="a5c09-152">Выполнение первой инструкции кода в записной книжке Jupyter с использованием волшебного слова Spark может занимать больше минуты.</span><span class="sxs-lookup"><span data-stu-id="a5c09-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="a5c09-153">**Пояснение**</span><span class="sxs-lookup"><span data-stu-id="a5c09-153">**Explanation:**</span></span>

<span data-ttu-id="a5c09-154">Это происходит из-за выполнения первой ячейки кода.</span><span class="sxs-lookup"><span data-stu-id="a5c09-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="a5c09-155">В фоновом режиме инициируется конфигурация сеанса и задается контекст Spark, SQL и Hive.</span><span class="sxs-lookup"><span data-stu-id="a5c09-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="a5c09-156">После настройки этих контекстов выполняется первая инструкция, и из-за этого кажется, что она выполняется долго.</span><span class="sxs-lookup"><span data-stu-id="a5c09-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="a5c09-157">Приостановка записной книжки Jupyter при создании сеанса</span><span class="sxs-lookup"><span data-stu-id="a5c09-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="a5c09-158">Если кластеру Spark не хватает ресурсов, при попытке создания сеанса ядра Spark и Pyspark в записной книжке Jupyter будут приостановлены.</span><span class="sxs-lookup"><span data-stu-id="a5c09-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="a5c09-159">**Устранение**</span><span class="sxs-lookup"><span data-stu-id="a5c09-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="a5c09-160">Освободите часть ресурсов в кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="a5c09-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="a5c09-161">Остановите другие записные книжки Spark в меню "Закрыть и остановить" или нажмите кнопку "Завершить" в обозревателе записных книжек.</span><span class="sxs-lookup"><span data-stu-id="a5c09-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="a5c09-162">Остановите другие приложения Spark из YARN.</span><span class="sxs-lookup"><span data-stu-id="a5c09-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="a5c09-163">Перезапустите записную книжку, которую вы пытались запустить.</span><span class="sxs-lookup"><span data-stu-id="a5c09-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="a5c09-164">Теперь ресурсов должно быть достаточно для создания сеанса.</span><span class="sxs-lookup"><span data-stu-id="a5c09-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="a5c09-165">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a5c09-165">See also</span></span>
* [<span data-ttu-id="a5c09-166">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a5c09-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="a5c09-167">Сценарии</span><span class="sxs-lookup"><span data-stu-id="a5c09-167">Scenarios</span></span>
* [<span data-ttu-id="a5c09-168">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="a5c09-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a5c09-169">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="a5c09-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="a5c09-170">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="a5c09-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a5c09-171">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="a5c09-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="a5c09-172">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a5c09-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a5c09-173">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="a5c09-173">Create and run applications</span></span>
* [<span data-ttu-id="a5c09-174">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="a5c09-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a5c09-175">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="a5c09-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a5c09-176">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="a5c09-176">Tools and extensions</span></span>
* [<span data-ttu-id="a5c09-177">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="a5c09-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a5c09-178">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="a5c09-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="a5c09-179">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a5c09-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="a5c09-180">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a5c09-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a5c09-181">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="a5c09-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="a5c09-182">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="a5c09-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a5c09-183">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="a5c09-183">Manage resources</span></span>
* [<span data-ttu-id="a5c09-184">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a5c09-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a5c09-185">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="a5c09-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

