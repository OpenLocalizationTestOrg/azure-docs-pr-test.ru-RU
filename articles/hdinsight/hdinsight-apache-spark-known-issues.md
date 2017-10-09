---
title: "кластер aaaTroubleshoot проблемы с Apache Spark в Azure HDInsight | Документы Microsoft"
description: "Узнайте о проблемах, связанных tooApache кластеров Spark в Azure HDInsight и как toowork вокруг их."
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
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="2d0f9-103">Известные проблемы в работе кластера Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d0f9-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="2d0f9-104">В этом документе хранит информацию о всех hello известные проблемы для общедоступной предварительной версии HDInsight Spark hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="2d0f9-105">Утечка интерактивного сеанса Livy</span><span class="sxs-lookup"><span data-stu-id="2d0f9-105">Livy leaks interactive session</span></span>
<span data-ttu-id="2d0f9-106">При Livy перезапуске (из Ambari или из-за перезагрузки виртуальной машины tooheadnode 0) с помощью интерактивного сеанса жизнеспособность попасть задания интерактивного сеанса.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="2d0f9-107">По этой причине новые задания может находится в состоянии принято hello и не может быть запущена.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="2d0f9-108">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="2d0f9-108">**Mitigation:**</span></span>

<span data-ttu-id="2d0f9-109">Используйте следующие процедуры tooworkaround hello проблема hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="2d0f9-110">Подключитесь к головному узлу по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-110">Ssh into headnode.</span></span> <span data-ttu-id="2d0f9-111">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2d0f9-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2d0f9-112">Выполнения hello, следующая команда toofind hello приложения идентификаторы hello интерактивный заданий запущен через Livy.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="2d0f9-113">Hello имена заданий по умолчанию будет Livy Если hello задания были запущены с Livy интерактивный сеанс с явные имена не указан, для hello Livy сеанса, запущенную книжке Jupyter, hello имя задания будет начинаться с remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="2d0f9-114">Запустите следующие команды tookill hello этих заданий.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="2d0f9-115">После этого новые задания начнут выполняться.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="2d0f9-116">Сервер журналов Spark не запускается</span><span class="sxs-lookup"><span data-stu-id="2d0f9-116">Spark History Server not started</span></span>
<span data-ttu-id="2d0f9-117">Сервер журналов Spark не запускается автоматически после создания кластера.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="2d0f9-118">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="2d0f9-118">**Mitigation:**</span></span> 

<span data-ttu-id="2d0f9-119">Запустите hello журнала сервера Ambari вручную.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="2d0f9-120">Проблема разрешений в каталоге журналов Spark</span><span class="sxs-lookup"><span data-stu-id="2d0f9-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="2d0f9-121">При hdiuser отправляет задание с spark-submit, возникает ошибка java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Отказано в доступе) и hello драйвер журнал не записывается.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="2d0f9-122">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="2d0f9-122">**Mitigation:**</span></span>

1. <span data-ttu-id="2d0f9-123">Добавьте группу Hadoop toohello hdiuser.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="2d0f9-124">После создания кластера предоставьте разрешения 777 для каталога /var/log/spark.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="2d0f9-125">Обновите расположение журнала spark hello, с помощью Ambari toobe каталог с 777 разрешениями.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="2d0f9-126">Выполните команду spark-submit как sudo.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="2d0f9-127">Соединитель Spark-Phoenix не поддерживается</span><span class="sxs-lookup"><span data-stu-id="2d0f9-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="2d0f9-128">В настоящее время hello Spark Финиксе соединитель не поддерживается с кластером HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="2d0f9-129">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="2d0f9-129">**Mitigation:**</span></span>

<span data-ttu-id="2d0f9-130">Вместо этого необходимо использовать соединитель Spark HBase hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="2d0f9-131">Инструкции см. в разделе [как соединитель toouse Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="2d0f9-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="2d0f9-132">Проблемы, связанные с tooJupyter ноутбуков</span><span class="sxs-lookup"><span data-stu-id="2d0f9-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="2d0f9-133">Ниже перечислены некоторые известные проблемы связанные tooJupyter ноутбуков.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="2d0f9-134">Записные книжки со знаками не из набора ASCII в именах файлов</span><span class="sxs-lookup"><span data-stu-id="2d0f9-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="2d0f9-135">Записные книжки Jupyter, которые могут использоваться в кластерах Spark HDInsight, не должны содержать в именах файлов знаки не из набора ASCII.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="2d0f9-136">При попытке tooupload в файл с помощью hello Jupyter пользовательского интерфейса, имеющая имя файла не ASCII, то возникнет ошибка без вмешательства пользователя (т. е Jupyter не позволит передать файл hello, но он не будет выдавать ошибку видимым либо).</span><span class="sxs-lookup"><span data-stu-id="2d0f9-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="2d0f9-137">Ошибка при загрузке записных книжек большого размера</span><span class="sxs-lookup"><span data-stu-id="2d0f9-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="2d0f9-138">При загрузке записных книжек большого размера может возникнуть ошибка **`Error loading notebook`** .</span><span class="sxs-lookup"><span data-stu-id="2d0f9-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="2d0f9-139">**Устранение.**</span><span class="sxs-lookup"><span data-stu-id="2d0f9-139">**Mitigation:**</span></span>

<span data-ttu-id="2d0f9-140">Появление этой ошибки не означает, что данные повреждены или утрачены.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="2d0f9-141">Записных книжек, по-прежнему на диске в `/var/lib/jupyter`, и вы можете SSH в tooaccess кластера hello их.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="2d0f9-142">См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2d0f9-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="2d0f9-143">После подключения toohello кластера с помощью SSH записных книжек можно скопировать из кластера tooyour локального компьютера (с помощью SCP или WinSCP) как потеря hello tooprevent резервной копии всех важных данных в записной книжке hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="2d0f9-144">Можно затем туннель SSH в к головному узлу на порт 8001 tooaccess Jupyter без прохода через шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="2d0f9-145">Оттуда снимите вывода hello записной и повторно сохраните размер toominimize hello портативного компьютера.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="2d0f9-146">tooprevent ошибки ситуации в hello в будущем, необходимо выполнить некоторые рекомендации:</span><span class="sxs-lookup"><span data-stu-id="2d0f9-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="2d0f9-147">Это важные tookeep hello записной книжки размер небольшой.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="2d0f9-148">Любые выходные данные Spark заданиям, отправляется обратно tooJupyter, хранящихся в записной книжке hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="2d0f9-149">Рекомендации по Jupyter он находится в общие tooavoid под управлением `.collect()` на больших RDD или блоки данных; вместо этого, если вы хотите toopeek RDD содержимого, рекомендуется запускать `.take()` или `.sample()` , где выходные данные не слишком велик.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="2d0f9-150">Кроме того при сохранении записной книжке, снимите все выходные размер hello tooreduce ячеек.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="2d0f9-151">Начальная загрузка записной книжки загружается дольше ожидаемого</span><span class="sxs-lookup"><span data-stu-id="2d0f9-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="2d0f9-152">Выполнение первой инструкции кода в записной книжке Jupyter с использованием волшебного слова Spark может занимать больше минуты.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="2d0f9-153">**Пояснение**</span><span class="sxs-lookup"><span data-stu-id="2d0f9-153">**Explanation:**</span></span>

<span data-ttu-id="2d0f9-154">Это происходит потому, что при запуске первую ячейку кода hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="2d0f9-155">В фоновом режиме hello это инициирует конфигурации сеанса и Spark, SQL и контекстах Hive устанавливаются.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="2d0f9-156">После задания этих контекстов выполнения первой инструкции hello, и это дает hello впечатление, что инструкция hello заняло toocomplete много времени.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="2d0f9-157">Время ожидания записной книжки Jupyter в создании сеанса hello</span><span class="sxs-lookup"><span data-stu-id="2d0f9-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="2d0f9-158">Если недостаточно ресурсов для кластера Spark, hello Spark и Pyspark ядер в записной книжке Jupyter hello будет истекло время ожидания при toocreate hello сеанса.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="2d0f9-159">**Устранение**</span><span class="sxs-lookup"><span data-stu-id="2d0f9-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="2d0f9-160">Освободите часть ресурсов в кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="2d0f9-161">Остановка других записных книжек Spark переходом toohello закрыть и остановке меню или нажав кнопку завершения работы в обозревателе записной книжки hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="2d0f9-162">Остановите другие приложения Spark из YARN.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="2d0f9-163">Перезапустите hello ноутбук, который выполняется копирование toostart.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="2d0f9-164">Недостаточно ресурсов должны быть доступны для вас toocreate теперь сеанса.</span><span class="sxs-lookup"><span data-stu-id="2d0f9-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="2d0f9-165">См. также</span><span class="sxs-lookup"><span data-stu-id="2d0f9-165">See also</span></span>
* [<span data-ttu-id="2d0f9-166">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d0f9-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="2d0f9-167">Сценарии</span><span class="sxs-lookup"><span data-stu-id="2d0f9-167">Scenarios</span></span>
* [<span data-ttu-id="2d0f9-168">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="2d0f9-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2d0f9-169">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="2d0f9-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="2d0f9-170">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="2d0f9-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2d0f9-171">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="2d0f9-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="2d0f9-172">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d0f9-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="2d0f9-173">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="2d0f9-173">Create and run applications</span></span>
* [<span data-ttu-id="2d0f9-174">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="2d0f9-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2d0f9-175">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="2d0f9-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="2d0f9-176">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="2d0f9-176">Tools and extensions</span></span>
* [<span data-ttu-id="2d0f9-177">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений</span><span class="sxs-lookup"><span data-stu-id="2d0f9-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="2d0f9-178">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="2d0f9-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="2d0f9-179">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d0f9-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="2d0f9-180">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d0f9-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="2d0f9-181">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="2d0f9-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="2d0f9-182">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="2d0f9-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="2d0f9-183">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="2d0f9-183">Manage resources</span></span>
* [<span data-ttu-id="2d0f9-184">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d0f9-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="2d0f9-185">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="2d0f9-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

