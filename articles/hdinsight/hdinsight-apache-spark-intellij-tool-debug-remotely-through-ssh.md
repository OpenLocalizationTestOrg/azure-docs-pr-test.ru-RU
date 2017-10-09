---
title: "Удаленная отладка приложений Spark через SSH с помощью набора средств Azure для IntelliJ | Документы Майкрософт"
description: "Пошаговые инструкции по как кластеры toouse средства HDInsight в набор средств Azure для приложений toodebug IntelliJ удаленно на HDInsight через SSH"
keywords: "удаленная отладка intellij, ssh, intellij, hdinsight, отладка intellij, отладка"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="e3b7e-104">Отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH</span><span class="sxs-lookup"><span data-stu-id="e3b7e-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="e3b7e-105">В этой статье содержатся пошаговые инструкции о том, как toouse средства HDInsight в набор средств Azure для приложений toodebug IntelliJ удаленно в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="e3b7e-106">toodebug проекта, вы также можете просмотреть hello [HDInsight Spark отладка приложений с помощью набора средств Azure для IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) видео.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="e3b7e-107">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="e3b7e-107">**Prerequisites**</span></span>

* <span data-ttu-id="e3b7e-108">**Средства HDInsight из набора средств Azure для IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="e3b7e-109">Этот инструмент входит в состав набора средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="e3b7e-110">Дополнительные сведения см. в статье [Установка набора средств Azure для IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="e3b7e-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="e3b7e-111">**Набор средств Azure для IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="e3b7e-112">Используйте этот набор средств toocreate Spark приложений для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="e3b7e-113">Дополнительные сведения, следуйте инструкциям hello [использования набора средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="e3b7e-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="e3b7e-114">**Служба SSH HDInsight с функцией управления именем пользователя и паролем.**</span><span class="sxs-lookup"><span data-stu-id="e3b7e-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="e3b7e-115">Дополнительные сведения см. в разделе [подключения tooHDInsight (Hadoop) с помощью SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) и [использование SSH туннелирования tooaccess Ambari веб-интерфейса пользователя, JobHistory, NameNode, Oozie и других сетевых интерфейсов](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="e3b7e-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="e3b7e-116">Создание приложения Spark Scala и его настройка для удаленной отладки</span><span class="sxs-lookup"><span data-stu-id="e3b7e-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="e3b7e-117">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="e3b7e-118">В hello **новый проект** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e3b7e-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="e3b7e-119">а.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-119">a.</span></span> <span data-ttu-id="e3b7e-120">Выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="e3b7e-121">b.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-121">b.</span></span> <span data-ttu-id="e3b7e-122">Выберите шаблон Java или Scala (на свой выбор).</span><span class="sxs-lookup"><span data-stu-id="e3b7e-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="e3b7e-123">Выбор между hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="e3b7e-123">Select between hello following options:</span></span>

      - <span data-ttu-id="e3b7e-124">**Spark on HDInsight (Scala)** (Spark в HDInsight [Scala])</span><span class="sxs-lookup"><span data-stu-id="e3b7e-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="e3b7e-125">**Spark on HDInsight (Java)** (Spark в HDInsight [Java])</span><span class="sxs-lookup"><span data-stu-id="e3b7e-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="e3b7e-126">**Spark on HDInsight Cluster Run Sample (Scala)** (Пример запуска Spark в кластере HDInsight [Scala])</span><span class="sxs-lookup"><span data-stu-id="e3b7e-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="e3b7e-127">В этом примере используется шаблон **Пример запуска Spark в кластере HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="e3b7e-128">c.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-128">c.</span></span> <span data-ttu-id="e3b7e-129">В hello **инструмент сборки** выберите либо hello следующие, tooyour потребность в соответствии с:</span><span class="sxs-lookup"><span data-stu-id="e3b7e-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="e3b7e-130">**Maven.** Для поддержки мастера создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="e3b7e-131">**SBT**, для управления зависимостями hello и построения для проекта Scala hello</span><span class="sxs-lookup"><span data-stu-id="e3b7e-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![Создание проекта отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="e3b7e-133">d.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-133">d.</span></span> <span data-ttu-id="e3b7e-134">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="e3b7e-135">В hello Далее **новый проект** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e3b7e-135">In hello next **New Project** window, do hello following:</span></span>

   ![Выберите hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="e3b7e-137">а.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-137">a.</span></span> <span data-ttu-id="e3b7e-138">Введите имя и расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="e3b7e-139">b.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-139">b.</span></span> <span data-ttu-id="e3b7e-140">В hello **проекта SDK** раскрывающемся списке выберите **Java 1.8** для **усилить 2.x** кластера и выберите **Java 1.7** для **Spark 1. x** кластера.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="e3b7e-141">c.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-141">c.</span></span> <span data-ttu-id="e3b7e-142">В hello **версии Spark** раскрывающегося списка, мастер создания проекта Scala hello интегрирует hello правильная версия пакета SDK Spark и Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="e3b7e-143">Если версия кластера spark hello является более ранней, чем 2.0, выберите **усилить 1.x**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="e3b7e-144">В противном случае выберите **Spark 2.x.**</span><span class="sxs-lookup"><span data-stu-id="e3b7e-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="e3b7e-145">В этом примере используется **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="e3b7e-146">d.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-146">d.</span></span> <span data-ttu-id="e3b7e-147">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-147">Select **Finish**.</span></span>

4. <span data-ttu-id="e3b7e-148">Выберите **src** > **основной** > **scala** tooopen кода в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="e3b7e-149">В этом примере используется hello **SparkCore_wasbloTest** сценария.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="e3b7e-150">tooaccess hello **изменение конфигураций** меню, выберите hello значок в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="e3b7e-151">В этом меню можно создавать и редактировать hello конфигурации для удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![Меню Edit Configurations (Изменение конфигураций)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="e3b7e-153">В hello **выполнения и отладки конфигураций** диалоговое окно, выберите hello "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="e3b7e-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="e3b7e-154">Затем выберите hello **отправки задания Spark** параметр.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-154">Then select hello **Submit Spark Job** option.</span></span>

   ![Добавление новой конфигурации](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="e3b7e-156">Введите сведения в полях **Name** (Имя), **Spark cluster** (Кластер Spark) и **Main class name** (Имя основного класса).</span><span class="sxs-lookup"><span data-stu-id="e3b7e-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="e3b7e-157">Затем выберите **Advanced configuration** (Расширенная конфигурация).</span><span class="sxs-lookup"><span data-stu-id="e3b7e-157">Then select **Advanced configuration**.</span></span> 

   ![Запуск конфигураций отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="e3b7e-159">В hello **Spark отправки Расширенная настройка** выберите **Spark Включение удаленной отладки**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="e3b7e-160">Введите имя пользователя SSH hello, затем введите пароль или использовать файл закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="e3b7e-161">toosave hello конфигурацию, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-161">toosave hello configuration, select **OK**.</span></span>

   ![Включение удаленной отладки Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="e3b7e-163">Конфигурация Hello теперь сохраняется с именем hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="e3b7e-164">tooview hello сведения о конфигурации, выберите hello имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="e3b7e-165">Выберите изменения toomake **изменить конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="e3b7e-166">После завершения настройки конфигурации hello, можно запустить проект hello для удаленного кластера hello или выполнять удаленную отладку.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="e3b7e-167">Узнайте, как tooperform удаленной отладки</span><span class="sxs-lookup"><span data-stu-id="e3b7e-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="e3b7e-168">Сценарий 1. Удаленный запуск</span><span class="sxs-lookup"><span data-stu-id="e3b7e-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="e3b7e-169">В этом разделе вы узнаете toodebug драйверы и исполнителей.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-169">In this section, we show you how toodebug drivers and executors.</span></span>

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. <span data-ttu-id="e3b7e-170">Настройка слабые места, а затем выберите hello **отладки** значок.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Выберите значок отладки hello](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="e3b7e-172">Когда выполнение программы hello достигает точки критические hello, см **драйвер** вкладку и два **исполнителя** вкладки в hello **отладчик** области.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="e3b7e-173">Выберите hello **программы Resume** toocontinue значок под управлением hello код, который затем достигает hello следующей точки останова и основное внимание уделяется соответствующий hello **исполнителя** вкладки. Изучите журналы выполнения hello на соответствующий hello **консоли** вкладки.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![Вкладка отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="e3b7e-175">Сценарий 2. Удаленная отладка и исправление ошибок</span><span class="sxs-lookup"><span data-stu-id="e3b7e-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="e3b7e-176">В этом разделе мы расскажем как toodynamically обновления hello значение переменной с помощью hello IntelliJ возможности для простого исправления отладки.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="e3b7e-177">В следующем примере кода hello исключение создается потому hello целевой файл уже существует.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="e3b7e-178">tooperform удаленная отладка и исправление ошибок</span><span class="sxs-lookup"><span data-stu-id="e3b7e-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="e3b7e-179">Настройка двух слабые места, а затем выберите hello **отладки** значок toostart hello удаленной отладки процесса.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="e3b7e-180">Hello кода останавливается на первой точки критические hello, а также параметр hello и сведения о переменных в hello **переменных** области.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="e3b7e-181">Выберите hello **программы Resume** toocontinue значок.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="e3b7e-182">Hello код останавливает hello второй точки.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-182">hello code stops at hello second point.</span></span> <span data-ttu-id="e3b7e-183">Hello исключение перехватывается, как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-183">hello exception is caught as expected.</span></span>

  ![Ошибка](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="e3b7e-185">Выберите hello **программы Resume** значок еще раз.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="e3b7e-186">Hello **HDInsight Spark отправки** окна отображается сообщение об ошибке «не удалось выполнить задание».</span><span class="sxs-lookup"><span data-stu-id="e3b7e-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Ошибка отправки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="e3b7e-188">Выберите toodynamically обновления hello значение переменной с помощью функции отладки IntelliJ hello, **отладки** еще раз.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="e3b7e-189">Hello **переменных** появится область.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="e3b7e-190">Щелкните правой кнопкой мыши целевой hello на hello **отладки** , а затем выберите **задание значения**.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="e3b7e-191">Затем введите новое значение для переменной hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="e3b7e-192">Выберите **ввод** toosave значение hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-192">Then select **Enter** toosave hello value.</span></span> 

  ![Задание значения](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="e3b7e-194">Выберите hello **программы Resume** значок toocontinue toorun hello программы.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="e3b7e-195">На этот раз исключение не возникает.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-195">This time, no exception is caught.</span></span> <span data-ttu-id="e3b7e-196">Вы увидите, что этот проект hello успешно выполняется без исключения.</span><span class="sxs-lookup"><span data-stu-id="e3b7e-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![Отладка без исключений](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="e3b7e-198"><a name="seealso"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e3b7e-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="e3b7e-199">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3b7e-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="e3b7e-200">Демонстрация</span><span class="sxs-lookup"><span data-stu-id="e3b7e-200">Demo</span></span>
* <span data-ttu-id="e3b7e-201">Создание проекта Scala (видео): [создание приложений Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e3b7e-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="e3b7e-202">Удаленной отладки (видео): [используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно на кластер HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e3b7e-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="e3b7e-203">Сценарии</span><span class="sxs-lookup"><span data-stu-id="e3b7e-203">Scenarios</span></span>
* [<span data-ttu-id="e3b7e-204">Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3b7e-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e3b7e-205">Spark с машинного обучения: используйте Spark в HDInsight tooanalyze построение с использованием данных Кондиционирования температуры</span><span class="sxs-lookup"><span data-stu-id="e3b7e-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e3b7e-206">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="e3b7e-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e3b7e-207">Spark потоковой передачи: Используйте Spark в HDInsight toobuild в режиме реального времени потоковую передачу приложений</span><span class="sxs-lookup"><span data-stu-id="e3b7e-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="e3b7e-208">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3b7e-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e3b7e-209">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="e3b7e-209">Create and run applications</span></span>
* [<span data-ttu-id="e3b7e-210">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="e3b7e-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e3b7e-211">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="e3b7e-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e3b7e-212">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="e3b7e-212">Tools and extensions</span></span>
* [<span data-ttu-id="e3b7e-213">Используйте набор средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3b7e-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e3b7e-214">Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через виртуальную частную сеть</span><span class="sxs-lookup"><span data-stu-id="e3b7e-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e3b7e-215">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="e3b7e-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="e3b7e-216">Используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений</span><span class="sxs-lookup"><span data-stu-id="e3b7e-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="e3b7e-217">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3b7e-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e3b7e-218">Ядер, доступных для записной книжки Jupyter hello кластера Spark для HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3b7e-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e3b7e-219">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="e3b7e-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e3b7e-220">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="e3b7e-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e3b7e-221">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="e3b7e-221">Manage resources</span></span>
* [<span data-ttu-id="e3b7e-222">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3b7e-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e3b7e-223">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="e3b7e-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
