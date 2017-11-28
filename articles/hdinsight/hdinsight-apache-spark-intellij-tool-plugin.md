---
title: "Набор средств Azure для IntelliJ. Создание приложений Spark для кластера HDInsight | Документация Майкрософт"
description: "Использовать hello Azure Toolkit для IntelliJ toodevelop Spark приложений, написанных в Scala и их отправки tooan кластера HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="f2fbf-103">Используйте набор средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2fbf-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="f2fbf-104">Использовать hello набора средств Azure для приложений Spark toodevelop подключаемый модуль IntelliJ, написанных на Scala, а затем отправьте их tooan кластера HDInsight Spark непосредственно из hello IntelliJ интегрированной среды разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="f2fbf-105">Можно использовать hello подключаемого модуля, несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="f2fbf-106">разрабатывать и отправлять приложения Scala Spark в кластер HDInsight Spark;</span><span class="sxs-lookup"><span data-stu-id="f2fbf-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="f2fbf-107">получать доступ к ресурсам кластера Azure HDInsight Spark;</span><span class="sxs-lookup"><span data-stu-id="f2fbf-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="f2fbf-108">разрабатывать и запускать приложения Scala Spark в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="f2fbf-109">toocreate проекта, представление hello [создания приложений Spark с помощью средств Azure для IntelliJ hello](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) видео.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2fbf-110">Можно использовать этот подключаемый модуль toocreate и отправьте свои приложения только для кластера HDInsight Spark для Linux.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="f2fbf-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2fbf-111">Prerequisites</span></span>

- <span data-ttu-id="f2fbf-112">Кластер Apache Spark в HDInsight на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="f2fbf-113">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="f2fbf-114">Комплект разработчика Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="f2fbf-115">Его можно установить из hello [веб-сайте Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="f2fbf-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-116">IntelliJ IDEA.</span></span> <span data-ttu-id="f2fbf-117">В этой статье используется версия 2017.1.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-117">This article uses version 2017.1.</span></span> <span data-ttu-id="f2fbf-118">Его можно установить из hello [JetBrains веб-сайт](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="f2fbf-119">Установка набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f2fbf-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="f2fbf-120">Инструкции по установке см. в статье [Установка набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="f2fbf-121">Войдите в tooyour подписки Azure</span><span class="sxs-lookup"><span data-stu-id="f2fbf-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="f2fbf-122">Запустите hello IntelliJ интегрированной среды разработки и откройте обозреватель Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="f2fbf-123">На hello **представление** выберите пункт **окна инструментов**, а затем выберите **обозреватель Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![ссылку Azure обозреватель Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="f2fbf-125">Щелкните правой кнопкой мыши hello **Azure** узел, а затем выберите **входа**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="f2fbf-126">В hello **входа в Azure** установите флажок **входа**, а затем введите учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Hello Azure входа в диалоговое окно](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="f2fbf-128">После подписи hello **подписки выберите** диалоговом появляется список всех hello подписок Azure, которые связаны с hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="f2fbf-129">Выберите hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-129">Select hello **Select** button.</span></span>

    ![диалоговое окно Выбор подписки Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="f2fbf-131">На hello **обозреватель Azure** , раскройте **HDInsight** hello tooview кластеры HDInsight Spark, которые в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Кластеры HDInsight Spark в Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="f2fbf-133">tooview hello ресурсов (например, учетные записи хранения), связанных с кластером hello, можно далее развернуть узел имя кластера.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![Развернутый узел имени кластера](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="f2fbf-135">Запуск приложения Spark Scala в кластере HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="f2fbf-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="f2fbf-136">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="f2fbf-137">В hello **новый проект** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="f2fbf-138">а.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-138">a.</span></span> <span data-ttu-id="f2fbf-139">Выберите **HDInsight** > **Spark on HDInsight (Scala)** (Spark в HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="f2fbf-140">b.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-140">b.</span></span> <span data-ttu-id="f2fbf-141">В hello **инструмент сборки** выберите либо hello следующие, tooyour потребность в соответствии с:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="f2fbf-142">**Maven.** Для поддержки мастера создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="f2fbf-143">**SBT**, для управления зависимостями hello и построения для проекта Scala hello</span><span class="sxs-lookup"><span data-stu-id="f2fbf-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![диалоговое окно нового проекта Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="f2fbf-145">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-145">Select **Next**.</span></span>

3. <span data-ttu-id="f2fbf-146">Мастер создания проектов Scala Hello автоматически обнаруживает после установки hello Scala подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="f2fbf-147">Щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-147">Select **Install**.</span></span>

   ![Проверка подключаемого модуля Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="f2fbf-149">hello toodownload Scala подключаемый модуль, выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="f2fbf-150">Следуйте инструкциям hello toorestart IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![диалоговое окно приветствия подключаемого модуля Scala установки](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="f2fbf-152">В hello **новый проект** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-152">In hello **New Project** window, do hello following:</span></span>  

    ![При выборе hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="f2fbf-154">а.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-154">a.</span></span> <span data-ttu-id="f2fbf-155">Введите имя и расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-155">Enter a project name and location.</span></span>

   <span data-ttu-id="f2fbf-156">b.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-156">b.</span></span> <span data-ttu-id="f2fbf-157">В hello **проекта SDK** раскрывающемся списке выберите **Java 1.8** для кластера 2.x Spark hello, или выберите **Java 1.7** для hello Spark 1.x кластера.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="f2fbf-158">c.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-158">c.</span></span> <span data-ttu-id="f2fbf-159">В hello **версии Spark** раскрывающегося списка, мастер создания проекта Scala интегрируется hello правильной версии пакета SDK Spark и Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="f2fbf-160">Если версия кластера Spark hello является более ранней, чем 2.0, выберите **усилить 1.x**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="f2fbf-161">В противном случае выберите **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="f2fbf-162">В этом примере используется **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="f2fbf-163">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-163">Select **Finish**.</span></span>

7. <span data-ttu-id="f2fbf-164">Hello Spark проекта автоматически создается артефакта.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="f2fbf-165">артефакт tooview hello, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="f2fbf-166">а.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-166">a.</span></span> <span data-ttu-id="f2fbf-167">На hello **файл** последовательно выберите пункты **структура проекта**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="f2fbf-168">b.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-168">b.</span></span> <span data-ttu-id="f2fbf-169">В hello **структура проекта** выберите **артефакты** tooview hello по умолчанию артефакт, который будет создан.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="f2fbf-170">Можно также создать свои собственные артефакта, выбрав hello "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Сведения о артефакта в диалоговое окно «hello»](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="f2fbf-172">Добавьте исходный код приложения, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="f2fbf-173">а.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-173">a.</span></span> <span data-ttu-id="f2fbf-174">Щелкните правой кнопкой мыши в обозревателе проектов **src**, слишком точки**New**и выберите **Scala класса**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![Команды для создания класса Scala в обозревателе проектов](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="f2fbf-176">b.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-176">b.</span></span> <span data-ttu-id="f2fbf-177">В hello **создать новый класс Scala** диалогового окна поле, укажите имя, выберите **объекта** в hello **вид** поле, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![Диалоговое окно создания класса Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="f2fbf-179">c.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-179">c.</span></span> <span data-ttu-id="f2fbf-180">В hello **MyClusterApp.scala** файла, вставьте следующий код hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="f2fbf-181">Hello кода hello данные считываются из HVAC.csv (доступно на всех кластерах HDInsight Spark), извлекает hello строки, которые имеют только одну цифру в столбце седьмой hello в hello CSV-файл и записывает выходные данные hello слишком**/HVACOut** в группе по умолчанию hello Контейнер хранилища для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="f2fbf-182">Запустите приложение hello в кластере HDInsight Spark, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="f2fbf-183">а.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-183">a.</span></span> <span data-ttu-id="f2fbf-184">В обозревателе решений, щелкните правой кнопкой мыши имя проекта hello и выберите **tooHDInsight отправить приложение Spark**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![Команда tooHDInsight отправить Spark приложения Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="f2fbf-186">b.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-186">b.</span></span> <span data-ttu-id="f2fbf-187">Вы являются tooenter запрашиваемые учетные данные подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="f2fbf-188">В hello **отправки Spark** диалоговое окно, укажите следующие значения hello, а затем выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="f2fbf-189">Для **усилить кластеров (Linux)**, выберите hello кластера HDInsight Spark, на котором будет toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="f2fbf-190">Выберите артефакт проекта IntelliJ hello, или выберите его из hello жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="f2fbf-191">В hello **имя класса Main** поле hello выберите кнопку с многоточием (**...** ), выберите основной класс hello в исходном коде приложения, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![диалоговое окно Выбор класса Main Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="f2fbf-193">Так как в данном примере кода приложение hello не требуются аргументы командной строки или ссылаться на JAR-файлов или файлы, можно оставить hello оставшихся пустые поля.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="f2fbf-194">После ввода всех сведений hello, диалоговое окно «hello» должен быть похож hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![диалоговое окно отправки Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="f2fbf-196">c.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-196">c.</span></span> <span data-ttu-id="f2fbf-197">Hello **отправки Spark** вкладку hello нижней части окна hello следует начинать отображение хода выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="f2fbf-198">Также можно остановить приложение hello, выбрав кнопку hello красным в hello **отправки Spark** окна.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![окна отправки Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="f2fbf-200">toolearn tooaccess hello выходные данные задания, разделе hello «доступ и управление кластерами HDInsight Spark с помощью набора средств Azure для IntelliJ» далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="f2fbf-201">Запуск или отладка приложения Spark Scala в кластере HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="f2fbf-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="f2fbf-202">Также рекомендуется еще один способ отправки кластера toohello приложения hello Spark.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="f2fbf-203">Это можно сделать, задав параметры hello в hello **выполнения и отладки конфигураций** интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="f2fbf-204">Дополнительные сведения см. в статье [Удаленная отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="f2fbf-205">Доступ к кластерам HDInsight Spark и управление ими с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f2fbf-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="f2fbf-206">При помощи набора средств Azure для IntelliJ можно выполнять разные операции.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="f2fbf-207">Режим доступа к задания hello</span><span class="sxs-lookup"><span data-stu-id="f2fbf-207">Access hello job view</span></span>
1. <span data-ttu-id="f2fbf-208">В обозревателе Azure разверните **HDInsight**, разверните имя кластера Spark hello и выберите **задания**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![Узел представления задания](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="f2fbf-210">В правой области hello hello **представлении задания Spark** вкладка отображает все приложения hello, выполняющихся на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="f2fbf-211">Выберите имя hello приложения hello, для которого требуется toosee Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![Сведения о приложении](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="f2fbf-213">toodisplay основные сведения, наведите на него схемы hello заданий.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="f2fbf-214">этапы graph tooview hello и информацию, которая создает каждого задания, выберите узел на диаграмме задания hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![Сведения об этапе задания](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="f2fbf-216">tooview часто используемые журналы, такие как *Stderr драйвер*, *Stdout драйвер*, и *сведений о каталоге*выберите hello **журнала** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![Подробные сведения журнала](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="f2fbf-218">Можно также просмотреть hello Spark журнала пользовательского интерфейса и hello YARN пользовательского интерфейса (на уровне приложения hello), выбрав ссылку hello верхней части окна hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="f2fbf-219">Доступ к серверу журнал Spark hello</span><span class="sxs-lookup"><span data-stu-id="f2fbf-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="f2fbf-220">В Azure Explorer разверните **HDInsight**, щелкните имя кластера Spark правой кнопкой мыши и выберите **Open Spark History UI** (Открыть пользовательский интерфейс журнала Spark).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="f2fbf-221">Когда появится запрос, введите учетные данные администратора кластера hello, которых указан при настройке кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="f2fbf-222">На сервере мониторинга hello Spark журнала можно использовать для только что завершили выполнение приложения hello toolook имя приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="f2fbf-223">В hello предшествующий код, можно задать имя приложения hello с помощью `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="f2fbf-224">Следовательно, приложение Spark называется **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="f2fbf-225">Запустите портал Ambari hello</span><span class="sxs-lookup"><span data-stu-id="f2fbf-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="f2fbf-226">В Azure Explorer разверните **HDInsight**, щелкните имя кластера Spark правой кнопкой мыши и выберите **Open Cluster Management Portal (Ambari)** (Открыть портал управления кластерами (Ambari)).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="f2fbf-227">Когда появится запрос, введите учетные данные администратора hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="f2fbf-228">Эти учетные данные указанным пользователем во время процесса установки кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="f2fbf-229">Управление подписками Azure</span><span class="sxs-lookup"><span data-stu-id="f2fbf-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="f2fbf-230">По умолчанию набор средств Azure для IntelliJ приведены кластеры Spark hello из всех подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="f2fbf-231">При необходимости можно указать hello подписок, которые должны tooaccess.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="f2fbf-232">В обозревателе Azure, щелкните правой кнопкой мыши hello **Azure** корневой узел, а затем выберите **управление подписками**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="f2fbf-233">В диалоговом окне приветствия снимите подписок hello флажки Далее toohello, вы не хотите tooaccess, а затем выберите **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="f2fbf-234">Можно также выбрать **выйти** Если вам нужны toosign подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="f2fbf-235">Запуск приложения Spark Scala на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="f2fbf-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="f2fbf-236">Можно использовать набор средств Azure для приложений Spark Scala toorun IntelliJ локально на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="f2fbf-237">Hello приложений обычно не требуется доступ к toocluster ресурсы, такие как контейнеры хранилища, и можно выполнить и проверить их локально.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="f2fbf-238">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2fbf-238">Prerequisite</span></span>
<span data-ttu-id="f2fbf-239">Во время выполнения локального Spark Scala приложения hello на компьютере Windows может появиться исключение, как описано в статье [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="f2fbf-240">Hello исключение возникает из-за отсутствия WinUtils.exe в Windows.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="f2fbf-241">tooresolve эту ошибку, [загрузить исполняемый hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa расположением, например **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="f2fbf-242">Добавьте переменную среды hello **HADOOP_HOME**и задайте значение hello hello переменной слишком**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="f2fbf-243">Запуск локального приложения Spark Scala</span><span class="sxs-lookup"><span data-stu-id="f2fbf-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="f2fbf-244">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="f2fbf-245">В hello **новый проект** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="f2fbf-246">а.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-246">a.</span></span> <span data-ttu-id="f2fbf-247">Выберите **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Пример локального запуска Spark в HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="f2fbf-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="f2fbf-248">b.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-248">b.</span></span> <span data-ttu-id="f2fbf-249">В hello **инструмент сборки** выберите либо hello следующие, tooyour потребность в соответствии с:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="f2fbf-250">**Maven.** Для поддержки мастера создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="f2fbf-251">**SBT**, для управления зависимостями hello и построения для проекта Scala hello</span><span class="sxs-lookup"><span data-stu-id="f2fbf-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![диалоговое окно нового проекта Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="f2fbf-253">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="f2fbf-254">В следующем окне приветствия hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="f2fbf-255">а.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-255">a.</span></span> <span data-ttu-id="f2fbf-256">Введите имя и расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-256">Enter a project name and location.</span></span>

    <span data-ttu-id="f2fbf-257">b.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-257">b.</span></span> <span data-ttu-id="f2fbf-258">В hello **проекта SDK** раскрывающегося списка выберите версию Java, которая является более поздней, чем версия 1.7.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="f2fbf-259">c.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-259">c.</span></span> <span data-ttu-id="f2fbf-260">В hello **версии Spark** раскрывающегося списка, выберите hello версию Scala нужных toouse: Scala 2.11.x Spark 2.0 или Scala 2.10.x для Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![диалоговое окно нового проекта Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="f2fbf-262">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-262">Select **Finish**.</span></span>

6. <span data-ttu-id="f2fbf-263">пример кода добавляет шаблон Hello (**LogQuery**) в группе hello **src** папку, можно запустить локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![Расположение LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="f2fbf-265">Щелкните правой кнопкой мыши hello **LogQuery** приложение, а затем выберите **выполнения «LogQuery»**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="f2fbf-266">На hello **запуска** вкладку внизу hello вывод hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Результат локального запуска приложения Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="f2fbf-268">Преобразование существующего toouse приложений IntelliJ ИДЕЯ набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f2fbf-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="f2fbf-269">Можно преобразовать существующие Spark Scala приложения hello, созданных в toobe IntelliJ ИДЕЯ совместимые с Azure Toolkit для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="f2fbf-270">Затем можно использовать hello подключаемый модуль toosubmit hello приложений tooan кластера HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="f2fbf-271">Для существующих приложений Spark Scala, была создана с помощью IntelliJ ИДЕЯ откройте файл связанного .iml hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="f2fbf-272">Hello корневой уровень является **модуль** элемент hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="f2fbf-273">Изменить элемент tooadd hello `UniqueKey="HDInsightTool"` таким образом, hello **модуль** элемент выглядит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="f2fbf-274">Сохраните изменения hello.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-274">Save hello changes.</span></span> <span data-ttu-id="f2fbf-275">Ваше приложение станет совместимым с набором средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="f2fbf-276">Можно проверить его, щелкнув правой кнопкой мыши имя проекта hello в обозревателе проектов.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="f2fbf-277">во всплывающем меню Hello теперь имеет параметр hello **tooHDInsight отправить приложение Spark**.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f2fbf-278">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f2fbf-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="f2fbf-279">Ошибка *Please use a larger heap size* (Используйте больший размер кучи) в локальной среде</span><span class="sxs-lookup"><span data-stu-id="f2fbf-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="f2fbf-280">Если вы используете 32-разрядных Java SDK во время локального запуска в Spark 1.6, может возникнуть hello следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

<span data-ttu-id="f2fbf-281">Эти ошибки возникают потому, что размер кучи hello недостаточно велик для Spark toorun.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="f2fbf-282">Для Spark требуется не меньше 471 МБ.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="f2fbf-283">(Дополнительные сведения см. в статье о [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) Простое решение – toouse 64-разрядных Java SDK.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="f2fbf-284">Можно также изменить параметры виртуальной машины Java hello в IntelliJ путем добавления hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f2fbf-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Добавление параметров toohello поле «Параметры виртуальной Машины» в IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="f2fbf-286">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="f2fbf-286">FAQ</span></span>
<span data-ttu-id="f2fbf-287">Выберите toosubmit хранилище Озера данных приложения tooAzure **Interactive** режим во время процесса hello Azure вход.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="f2fbf-288">Если выбрать **автоматический** режим, может произойти ошибка.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-288">If you select **Automated** mode, you can get an error.</span></span>

![Интерактивный вход](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="f2fbf-290">Теперь мы устранили ее.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-290">Now, we resolved it.</span></span> <span data-ttu-id="f2fbf-291">Вы можете toosubmit кластера Озера данных Azure приложения с помощью метода входа.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="f2fbf-292">Отзывы и известные проблемы</span><span class="sxs-lookup"><span data-stu-id="f2fbf-292">Feedback and known issues</span></span>
<span data-ttu-id="f2fbf-293">Сейчас просмотр выходных данных Spark напрямую не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="f2fbf-294">С любыми отзывами и предложениями, а также в случае возникновения проблем при работе с этим подключаемым модулем вы можете отправить сообщение по электронному адресу hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="f2fbf-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="f2fbf-295"><a name="seealso"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f2fbf-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="f2fbf-296">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2fbf-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="f2fbf-297">Демонстрация</span><span class="sxs-lookup"><span data-stu-id="f2fbf-297">Demo</span></span>
* <span data-ttu-id="f2fbf-298">Создание проекта Scala (видео): [создание приложений Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f2fbf-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="f2fbf-299">Удаленной отладки (видео): [используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно на кластер HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="f2fbf-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="f2fbf-300">Сценарии</span><span class="sxs-lookup"><span data-stu-id="f2fbf-300">Scenarios</span></span>
* [<span data-ttu-id="f2fbf-301">Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2fbf-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="f2fbf-302">Spark с машинного обучения: используйте Spark в HDInsight tooanalyze построение с использованием данных Кондиционирования температуры</span><span class="sxs-lookup"><span data-stu-id="f2fbf-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="f2fbf-303">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="f2fbf-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="f2fbf-304">Spark потоковой передачи: Используйте Spark в HDInsight toobuild в режиме реального времени потоковую передачу приложений</span><span class="sxs-lookup"><span data-stu-id="f2fbf-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="f2fbf-305">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2fbf-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="f2fbf-306">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="f2fbf-306">Creating and running applications</span></span>
* [<span data-ttu-id="f2fbf-307">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="f2fbf-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="f2fbf-308">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="f2fbf-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="f2fbf-309">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="f2fbf-309">Tools and extensions</span></span>
* [<span data-ttu-id="f2fbf-310">Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через виртуальную частную сеть</span><span class="sxs-lookup"><span data-stu-id="f2fbf-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="f2fbf-311">Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через SSH</span><span class="sxs-lookup"><span data-stu-id="f2fbf-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="f2fbf-312">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="f2fbf-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="f2fbf-313">Используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений</span><span class="sxs-lookup"><span data-stu-id="f2fbf-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="f2fbf-314">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2fbf-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f2fbf-315">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2fbf-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="f2fbf-316">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="f2fbf-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="f2fbf-317">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="f2fbf-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="f2fbf-318">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="f2fbf-318">Managing resources</span></span>
* [<span data-ttu-id="f2fbf-319">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="f2fbf-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="f2fbf-320">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="f2fbf-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

