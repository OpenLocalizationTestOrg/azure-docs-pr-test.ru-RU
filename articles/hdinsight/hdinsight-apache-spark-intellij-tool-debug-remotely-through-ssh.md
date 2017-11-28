---
title: "Удаленная отладка приложений Spark через SSH с помощью набора средств Azure для IntelliJ | Документы Майкрософт"
description: "Пошаговые инструкции по использованию инструментов HDInsight из набора средств Azure для IntelliJ для удаленной отладки приложений на кластерах HDInsight через SSH."
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
ms.openlocfilehash: 19053e31d6eb097bc91a04ef9c6af5772aaa16da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="57a91-104">Отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH</span><span class="sxs-lookup"><span data-stu-id="57a91-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="57a91-105">В данной статье представлены пошаговые инструкции по использованию инструментов HDInsight из набора средств Azure для IntelliJ для удаленной отладки приложений в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57a91-105">This article provides step-by-step guidance on how to use HDInsight Tools in Azure Toolkit for IntelliJ to debug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="57a91-106">Для отладки проекта можно также просмотреть видео [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (Отладка приложений HDInsight Spark с помощью набора средств Azure для IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="57a91-106">To debug your project, you can also view the [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="57a91-107">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="57a91-107">**Prerequisites**</span></span>

* <span data-ttu-id="57a91-108">**Средства HDInsight из набора средств Azure для IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="57a91-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="57a91-109">Этот инструмент входит в состав набора средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="57a91-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="57a91-110">Дополнительные сведения см. в статье [Установка набора средств Azure для IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="57a91-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="57a91-111">**Набор средств Azure для IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="57a91-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="57a91-112">Этот набор средств используется для создания приложений Spark для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="57a91-112">Use this toolkit to create Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="57a91-113">Дополнительные сведения см. в статье [Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для IntelliJ](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="57a91-113">For more information, follow the instructions in [Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="57a91-114">**Служба SSH HDInsight с функцией управления именем пользователя и паролем.**</span><span class="sxs-lookup"><span data-stu-id="57a91-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="57a91-115">Дополнительные сведения см. в статьях [Подключение к HDInsight (Hadoop) с помощью SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) и [Использование туннелирования SSH для доступа к пользовательскому веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим пользовательским веб-интерфейсам](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="57a91-115">For more information, see [Connect to HDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="57a91-116">Создание приложения Spark Scala и его настройка для удаленной отладки</span><span class="sxs-lookup"><span data-stu-id="57a91-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="57a91-117">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="57a91-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="57a91-118">В диалоговом окне **Новый проект** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="57a91-118">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="57a91-119">а.</span><span class="sxs-lookup"><span data-stu-id="57a91-119">a.</span></span> <span data-ttu-id="57a91-120">Выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="57a91-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="57a91-121">b.</span><span class="sxs-lookup"><span data-stu-id="57a91-121">b.</span></span> <span data-ttu-id="57a91-122">Выберите шаблон Java или Scala (на свой выбор).</span><span class="sxs-lookup"><span data-stu-id="57a91-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="57a91-123">Выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="57a91-123">Select between the following options:</span></span>

      - <span data-ttu-id="57a91-124">**Spark on HDInsight (Scala)** (Spark в HDInsight [Scala])</span><span class="sxs-lookup"><span data-stu-id="57a91-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="57a91-125">**Spark on HDInsight (Java)** (Spark в HDInsight [Java])</span><span class="sxs-lookup"><span data-stu-id="57a91-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="57a91-126">**Spark on HDInsight Cluster Run Sample (Scala)** (Пример запуска Spark в кластере HDInsight [Scala])</span><span class="sxs-lookup"><span data-stu-id="57a91-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="57a91-127">В этом примере используется шаблон **Пример запуска Spark в кластере HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="57a91-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="57a91-128">c.</span><span class="sxs-lookup"><span data-stu-id="57a91-128">c.</span></span> <span data-ttu-id="57a91-129">В списке **средств сборки** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="57a91-129">In the **Build tool** list, select either of the following, according to your need:</span></span>

      - <span data-ttu-id="57a91-130">**Maven.** Для поддержки мастера создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="57a91-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="57a91-131">**SBT.** Для управления зависимостями и создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="57a91-131">**SBT**, for managing the dependencies and building for the Scala project</span></span> 

      ![Создание проекта отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="57a91-133">d.</span><span class="sxs-lookup"><span data-stu-id="57a91-133">d.</span></span> <span data-ttu-id="57a91-134">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="57a91-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="57a91-135">В следующем окне **New Project** (Новый проект) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="57a91-135">In the next **New Project** window, do the following:</span></span>

   ![Выбор пакета SDK для Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="57a91-137">а.</span><span class="sxs-lookup"><span data-stu-id="57a91-137">a.</span></span> <span data-ttu-id="57a91-138">Введите имя и расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="57a91-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="57a91-139">b.</span><span class="sxs-lookup"><span data-stu-id="57a91-139">b.</span></span> <span data-ttu-id="57a91-140">Из раскрывающегося списка **Project SDK** (Пакет SDK проекта) выберите **Java 1.8** для кластера **Spark 2.x** или **Java 1.7** для кластера **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="57a91-140">In the **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="57a91-141">c.</span><span class="sxs-lookup"><span data-stu-id="57a91-141">c.</span></span> <span data-ttu-id="57a91-142">В раскрывающемся списке **Spark version** (Версия Spark) мастер создания проекта Scala интегрирует правильную версию пакета SDK для Spark и пакета SDK для Scala.</span><span class="sxs-lookup"><span data-stu-id="57a91-142">In the **Spark Version** drop-down list, the Scala project creation wizard integrates the correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="57a91-143">Если версия кластера Spark ниже 2.0, выберите **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="57a91-143">If the spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="57a91-144">В противном случае выберите **Spark 2.x.**</span><span class="sxs-lookup"><span data-stu-id="57a91-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="57a91-145">В этом примере используется **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="57a91-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="57a91-146">d.</span><span class="sxs-lookup"><span data-stu-id="57a91-146">d.</span></span> <span data-ttu-id="57a91-147">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="57a91-147">Select **Finish**.</span></span>

4. <span data-ttu-id="57a91-148">Выберите **src** > **main** > **scala**, чтобы открыть код в проекте.</span><span class="sxs-lookup"><span data-stu-id="57a91-148">Select **src** > **main** > **scala** to open your code in the project.</span></span> <span data-ttu-id="57a91-149">В этом примере используется сценарий **SparkCore_wasbloTest**.</span><span class="sxs-lookup"><span data-stu-id="57a91-149">This example uses the **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="57a91-150">Чтобы перейти в меню **Edit Configurations** (Изменение конфигураций), щелкните значок в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="57a91-150">To access the **Edit Configurations** menu, select the icon in the upper-right corner.</span></span> <span data-ttu-id="57a91-151">В этом меню можно создавать и редактировать конфигурации для удаленной отладки.</span><span class="sxs-lookup"><span data-stu-id="57a91-151">From this menu, you can create or edit the configurations for remote debugging.</span></span>

   ![Меню Edit Configurations (Изменение конфигураций)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="57a91-153">В диалоговом окне **Run/Debug Configurations** (Конфигурации выполнения и отладки) щелкните знак "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="57a91-153">In the **Run/Debug Configurations** dialog box, select the plus sign (**+**).</span></span> <span data-ttu-id="57a91-154">Выберите **Submit Spark Job** (Отправить задание Spark).</span><span class="sxs-lookup"><span data-stu-id="57a91-154">Then select the **Submit Spark Job** option.</span></span>

   ![Добавление новой конфигурации](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="57a91-156">Введите сведения в полях **Name** (Имя), **Spark cluster** (Кластер Spark) и **Main class name** (Имя основного класса).</span><span class="sxs-lookup"><span data-stu-id="57a91-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="57a91-157">Затем выберите **Advanced configuration** (Расширенная конфигурация).</span><span class="sxs-lookup"><span data-stu-id="57a91-157">Then select **Advanced configuration**.</span></span> 

   ![Запуск конфигураций отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="57a91-159">В диалоговом окне **Spark Submission Advanced Configuration** (Расширенная конфигурация отправки Spark) установите флажок **Enable Spark remote debug** (Разрешить удаленную отладку Spark).</span><span class="sxs-lookup"><span data-stu-id="57a91-159">In the **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="57a91-160">Введите имя пользователя SSH, затем введите пароль либо воспользуйтесь файлом закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="57a91-160">Enter the SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="57a91-161">Нажмите кнопку **ОК**, чтобы сохранить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="57a91-161">To save the configuration, select **OK**.</span></span>

   ![Включение удаленной отладки Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="57a91-163">Теперь конфигурация сохранена под именем, которое вы указали.</span><span class="sxs-lookup"><span data-stu-id="57a91-163">The configuration is now saved with the name you provided.</span></span> <span data-ttu-id="57a91-164">Чтобы просмотреть сведения о конфигурации, выберите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="57a91-164">To view the configuration details, select the configuration name.</span></span> <span data-ttu-id="57a91-165">Чтобы внести изменения, выберите **Edit Configurations** (Изменить конфигурации).</span><span class="sxs-lookup"><span data-stu-id="57a91-165">To make changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="57a91-166">Завершив настройку конфигурации, можно запустить проект на удаленном кластере или выполнить удаленную отладку.</span><span class="sxs-lookup"><span data-stu-id="57a91-166">After you complete the configurations settings, you can run the project against the remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-to-perform-remote-debugging"></a><span data-ttu-id="57a91-167">Порядок выполнения удаленной отладки</span><span class="sxs-lookup"><span data-stu-id="57a91-167">Learn how to perform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="57a91-168">Сценарий 1. Удаленный запуск</span><span class="sxs-lookup"><span data-stu-id="57a91-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="57a91-169">В этом разделе мы покажем, как выполнить отладку драйверов и исполнителей.</span><span class="sxs-lookup"><span data-stu-id="57a91-169">In this section, we show you how to debug drivers and executors.</span></span>

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
        /** Tracks the total query count and number of aggregate bytes for a particular group. */
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


1. <span data-ttu-id="57a91-170">Настройте точки останова, а затем щелкните значок **Debug** (Отладка).</span><span class="sxs-lookup"><span data-stu-id="57a91-170">Set up breaking points, and then select the **Debug** icon.</span></span>

   ![Щелчок значка отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="57a91-172">Когда выполнение программы достигнет точки останова, в области **Debugger** (Отладчик) вы увидите вкладку **Driver** (Драйвер) и две вкладки **Executor** (Исполнитель).</span><span class="sxs-lookup"><span data-stu-id="57a91-172">When the program execution reaches the breaking point, you see a **Driver** tab and two **Executor** tabs in the **Debugger** pane.</span></span> <span data-ttu-id="57a91-173">Щелкните значок **Resume Program** (Возобновить выполнение программы), чтобы продолжить выполнение кода, который затем достигнет следующей точки останова и отобразится на соответствующей вкладке **Executor** (Исполнитель). Вы можете просмотреть журналы выполнения на соответствующей вкладке **Console** (Консоль).</span><span class="sxs-lookup"><span data-stu-id="57a91-173">Select the **Resume Program** icon to continue running the code, which then reaches the next breakpoint and focuses on the corresponding **Executor** tab. You can review the execution logs on the corresponding **Console** tab.</span></span>

   ![Вкладка отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="57a91-175">Сценарий 2. Удаленная отладка и исправление ошибок</span><span class="sxs-lookup"><span data-stu-id="57a91-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="57a91-176">В этом разделе мы покажем, как выполнять динамическое обновление значения переменной с помощью возможностей отладки IntelliJ для исправления простых ошибок.</span><span class="sxs-lookup"><span data-stu-id="57a91-176">In this section, we show you how to dynamically update the variable value by using the IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="57a91-177">В следующем примере кода возникает исключение из-за того, что целевой файл уже существует.</span><span class="sxs-lookup"><span data-stu-id="57a91-177">In the following code example, an exception is thrown because the target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find the rows that have only one digit in the sixth column.
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


#### <a name="to-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="57a91-178">Удаленная отладка и исправление ошибок</span><span class="sxs-lookup"><span data-stu-id="57a91-178">To perform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="57a91-179">Настройте две точки останова и щелкните значок **Debug** (Отладка), чтобы приступить к удаленной отладке.</span><span class="sxs-lookup"><span data-stu-id="57a91-179">Set up two breaking points, and then select the **Debug** icon to start the remote debugging process.</span></span>

2. <span data-ttu-id="57a91-180">Выполнение кода будет приостановлено в первой точке останова, а в области **Variables** (Переменные) отобразятся сведения о параметре и переменной.</span><span class="sxs-lookup"><span data-stu-id="57a91-180">The code stops at the first breaking point, and the parameter and variable information are shown in the **Variables** pane.</span></span> 

3. <span data-ttu-id="57a91-181">Щелкните значок **Resume Program** (Возобновить выполнение программы), чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="57a91-181">Select the **Resume Program** icon to continue.</span></span> <span data-ttu-id="57a91-182">Выполнение кода будет приостановлено во второй точке останова.</span><span class="sxs-lookup"><span data-stu-id="57a91-182">The code stops at the second point.</span></span> <span data-ttu-id="57a91-183">Как и ожидалось, возникнет исключение.</span><span class="sxs-lookup"><span data-stu-id="57a91-183">The exception is caught as expected.</span></span>

  ![Ошибка](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="57a91-185">Снова щелкните значок **Resume Program** (Возобновить выполнение программы).</span><span class="sxs-lookup"><span data-stu-id="57a91-185">Select the **Resume Program** icon again.</span></span> <span data-ttu-id="57a91-186">В окне **HDInsight Spark Submission** (Отправка HDInsight Spark) будет указано, что во время выполнения задания произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="57a91-186">The **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Ошибка отправки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="57a91-188">Чтобы динамически обновить значение переменной с помощью функции отладки IntelliJ, еще раз щелкните значок **Debug** (Отладка).</span><span class="sxs-lookup"><span data-stu-id="57a91-188">To dynamically update the variable value by using the IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="57a91-189">Снова появится область **Variables** (Переменные).</span><span class="sxs-lookup"><span data-stu-id="57a91-189">The **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="57a91-190">Щелкните правой кнопкой мыши целевой объект на вкладке **Debug** (Отладка), а затем выберите **Set Value** (Задать значение).</span><span class="sxs-lookup"><span data-stu-id="57a91-190">Right-click the target on the **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="57a91-191">Затем введите новое значение переменной.</span><span class="sxs-lookup"><span data-stu-id="57a91-191">Next, enter a new value for the variable.</span></span> <span data-ttu-id="57a91-192">Нажмите клавишу **ВВОД**, чтобы сохранить значение.</span><span class="sxs-lookup"><span data-stu-id="57a91-192">Then select **Enter** to save the value.</span></span> 

  ![Задание значения](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="57a91-194">Щелкните значок **Resume Program** (Возобновить выполнение программы), чтобы продолжить выполнение программы.</span><span class="sxs-lookup"><span data-stu-id="57a91-194">Select the **Resume Program** icon to continue to run the program.</span></span> <span data-ttu-id="57a91-195">На этот раз исключение не возникает.</span><span class="sxs-lookup"><span data-stu-id="57a91-195">This time, no exception is caught.</span></span> <span data-ttu-id="57a91-196">Проект выполняется успешно без исключений.</span><span class="sxs-lookup"><span data-stu-id="57a91-196">You can see that the project runs successfully without any exceptions.</span></span>

  ![Отладка без исключений](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="57a91-198"><a name="seealso"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57a91-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="57a91-199">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="57a91-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="57a91-200">Демонстрация</span><span class="sxs-lookup"><span data-stu-id="57a91-200">Demo</span></span>
* <span data-ttu-id="57a91-201">Создание проекта Scala (видео): [создание приложений Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="57a91-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="57a91-202">Удаленная отладка (видео): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (Удаленная отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="57a91-202">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="57a91-203">Сценарии</span><span class="sxs-lookup"><span data-stu-id="57a91-203">Scenarios</span></span>
* [<span data-ttu-id="57a91-204">Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="57a91-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="57a91-205">Создание приложений машинного обучения Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="57a91-205">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="57a91-206">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="57a91-206">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="57a91-207">Потоковая передача Apache Spark. Обработка данных из концентраторов событий Azure с помощью кластера Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="57a91-207">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="57a91-208">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="57a91-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="57a91-209">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="57a91-209">Create and run applications</span></span>
* [<span data-ttu-id="57a91-210">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="57a91-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="57a91-211">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="57a91-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="57a91-212">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="57a91-212">Tools and extensions</span></span>
* [<span data-ttu-id="57a91-213">Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="57a91-213">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="57a91-214">Удаленная отладка приложений Spark через VPN с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="57a91-214">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="57a91-215">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="57a91-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="57a91-216">Использование средств HDInsight в наборе средств Azure для Eclipse для создания приложений Spark</span><span class="sxs-lookup"><span data-stu-id="57a91-216">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="57a91-217">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="57a91-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="57a91-218">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="57a91-218">Kernels available for Jupyter notebook in the Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="57a91-219">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="57a91-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="57a91-220">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="57a91-220">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="57a91-221">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="57a91-221">Manage resources</span></span>
* [<span data-ttu-id="57a91-222">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="57a91-222">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="57a91-223">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="57a91-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
