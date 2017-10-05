---
title: "Набор средств Azure для IntelliJ. Создание приложений Spark для кластера HDInsight | Документация Майкрософт"
description: "Сведения о разработке приложений Spark на языке Scala и их отправке в кластер HDInsight Spark с помощью набора средств Azure для IntelliJ."
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
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="c9255-103">Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c9255-103">Use Azure Toolkit for IntelliJ to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="c9255-104">Подключаемый модуль из набора средств Azure для IntelliJ позволяет разрабатывать приложения Spark на языке Scala и отправлять их в кластер HDInsight Spark непосредственно из интегрированной среды разработки IntelliJ (IDE).</span><span class="sxs-lookup"><span data-stu-id="c9255-104">Use the Azure Toolkit for IntelliJ plug-in to develop Spark applications written in Scala, and then submit them to an HDInsight Spark cluster directly from the IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="c9255-105">С помощью подключаемого модуля можно выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9255-105">You can use the plug-in in a few ways:</span></span>

* <span data-ttu-id="c9255-106">разрабатывать и отправлять приложения Scala Spark в кластер HDInsight Spark;</span><span class="sxs-lookup"><span data-stu-id="c9255-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="c9255-107">получать доступ к ресурсам кластера Azure HDInsight Spark;</span><span class="sxs-lookup"><span data-stu-id="c9255-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="c9255-108">разрабатывать и запускать приложения Scala Spark в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="c9255-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="c9255-109">Чтобы создать проект, просмотрите видео о [создании приложений Spark с помощью набора средств Azure для IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ).</span><span class="sxs-lookup"><span data-stu-id="c9255-109">To create your project, view the [Create Spark Applications with the Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9255-110">Вы можете использовать этот подключаемый модуль, чтобы создавать и отправлять приложения только в кластер HDInsight Spark на Linux.</span><span class="sxs-lookup"><span data-stu-id="c9255-110">You can use this plug-in to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="c9255-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c9255-111">Prerequisites</span></span>

- <span data-ttu-id="c9255-112">Кластер Apache Spark в HDInsight на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="c9255-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="c9255-113">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c9255-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="c9255-114">Комплект разработчика Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="c9255-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="c9255-115">Его можно установить с [веб-сайта Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="c9255-115">You can install it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="c9255-116">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="c9255-116">IntelliJ IDEA.</span></span> <span data-ttu-id="c9255-117">В этой статье используется версия 2017.1.</span><span class="sxs-lookup"><span data-stu-id="c9255-117">This article uses version 2017.1.</span></span> <span data-ttu-id="c9255-118">Его можно установить с [веб-сайта JetBrains](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="c9255-118">You can install it from the [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="c9255-119">Установка набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c9255-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="c9255-120">Инструкции по установке см. в статье [Установка набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="c9255-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="c9255-121">Войдите в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="c9255-121">Sign in to your Azure subscription</span></span>

1. <span data-ttu-id="c9255-122">Запустите IntelliJ IDE и откройте Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="c9255-122">Start the IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="c9255-123">В меню **View** (Вид) выберите **Tool Windows** (Окна инструментов) и выберите **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c9255-123">On the **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![Ссылка на Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="c9255-125">Щелкните правой кнопкой мыши узел **Azure**, а затем выберите **Sign In** (Войти).</span><span class="sxs-lookup"><span data-stu-id="c9255-125">Right-click the **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="c9255-126">В диалоговом окне **Azure Sign In** (Вход в Azure) нажмите кнопку **Sign in** (Войти), а затем введите свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="c9255-126">In the **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Диалоговое окно входа в Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="c9255-128">После входа в диалоговом окне **Select Subscriptions** (Выбор подписок) будут перечислены все подписки Azure, связанные с указанными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="c9255-128">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions that are associated with the credentials.</span></span> <span data-ttu-id="c9255-129">Нажмите кнопку **Select** (Выбрать).</span><span class="sxs-lookup"><span data-stu-id="c9255-129">Select the **Select** button.</span></span>

    ![Диалоговое окно выбора подписок](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="c9255-131">На вкладке **Azure Explorer** разверните **HDInsight**, чтобы просмотреть кластеры HDInsight Spark в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="c9255-131">On the **Azure Explorer** tab, expand **HDInsight** to view the HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Кластеры HDInsight Spark в Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="c9255-133">Далее можно развернуть узел имени кластера, чтобы увидеть ресурсы (например, учетные записи хранения), связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="c9255-133">To view the resources (for example, storage accounts) that are associated with the cluster, you can further expand a cluster-name node.</span></span>
   
    ![Развернутый узел имени кластера](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="c9255-135">Запуск приложения Spark Scala в кластере HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="c9255-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="c9255-136">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="c9255-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="c9255-137">В диалоговом окне **Новый проект** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9255-137">In the **New Project** dialog box, do the following:</span></span> 

   <span data-ttu-id="c9255-138">а.</span><span class="sxs-lookup"><span data-stu-id="c9255-138">a.</span></span> <span data-ttu-id="c9255-139">Выберите **HDInsight** > **Spark on HDInsight (Scala)** (Spark в HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="c9255-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="c9255-140">b.</span><span class="sxs-lookup"><span data-stu-id="c9255-140">b.</span></span> <span data-ttu-id="c9255-141">В списке **средств сборки** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="c9255-141">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="c9255-142">**Maven.** Для поддержки мастера создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="c9255-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="c9255-143">**SBT.** Для управления зависимостями и создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="c9255-143">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Диалоговое окно нового проекта](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="c9255-145">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c9255-145">Select **Next**.</span></span>

3. <span data-ttu-id="c9255-146">Мастер создания проектов Scala автоматически определяет, установлен ли подключаемый модуль Scala.</span><span class="sxs-lookup"><span data-stu-id="c9255-146">The Scala project-creation wizard automatically detects whether you've installed the Scala plug-in.</span></span> <span data-ttu-id="c9255-147">Щелкните **Установить**.</span><span class="sxs-lookup"><span data-stu-id="c9255-147">Select **Install**.</span></span>

   ![Проверка подключаемого модуля Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="c9255-149">Чтобы скачать подключаемый модуль Scala, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9255-149">To download the Scala plug-in, select **OK**.</span></span> <span data-ttu-id="c9255-150">Следуйте инструкциям, чтобы перезапустить IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c9255-150">Follow the instructions to restart IntelliJ.</span></span> 

   ![Диалоговое окно установки подключаемого модуля Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="c9255-152">В окне **нового проекта** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9255-152">In the **New Project** window, do the following:</span></span>  

    ![Выбор пакета SDK для Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="c9255-154">а.</span><span class="sxs-lookup"><span data-stu-id="c9255-154">a.</span></span> <span data-ttu-id="c9255-155">Введите имя и расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="c9255-155">Enter a project name and location.</span></span>

   <span data-ttu-id="c9255-156">b.</span><span class="sxs-lookup"><span data-stu-id="c9255-156">b.</span></span> <span data-ttu-id="c9255-157">В раскрывающемся списке для параметра **Project SDK** (Пакет SDK проекта) выберите **Java 1.8** для кластера Spark 2.x или **Java 1.7** для кластера Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="c9255-157">In the **Project SDK** drop-down list, select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span>

   <span data-ttu-id="c9255-158">c.</span><span class="sxs-lookup"><span data-stu-id="c9255-158">c.</span></span> <span data-ttu-id="c9255-159">В раскрывающемся списке для параметра **Spark version** (Версия Spark) мастер создания проекта Scala интегрирует правильную версию пакета SDK для Spark и пакета SDK для Scala.</span><span class="sxs-lookup"><span data-stu-id="c9255-159">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="c9255-160">Если версия кластера Spark ниже 2.0, выберите **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="c9255-160">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="c9255-161">В противном случае выберите **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="c9255-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="c9255-162">В этом примере используется **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="c9255-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="c9255-163">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c9255-163">Select **Finish**.</span></span>

7. <span data-ttu-id="c9255-164">Проект Spark автоматически создаст артефакт.</span><span class="sxs-lookup"><span data-stu-id="c9255-164">The Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="c9255-165">Чтобы просмотреть артефакт, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9255-165">To view the artifact, do the following:</span></span>

   <span data-ttu-id="c9255-166">а.</span><span class="sxs-lookup"><span data-stu-id="c9255-166">a.</span></span> <span data-ttu-id="c9255-167">В меню **File** (Файл) выберите **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="c9255-167">On the **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="c9255-168">b.</span><span class="sxs-lookup"><span data-stu-id="c9255-168">b.</span></span> <span data-ttu-id="c9255-169">В диалоговом окне **Project Structure** (Структура проекта) щелкните **артефакты**, чтобы просмотреть созданный по умолчанию артефакт.</span><span class="sxs-lookup"><span data-stu-id="c9255-169">In the **Project Structure** dialog box, select **Artifacts** to view the default artifact that is created.</span></span> <span data-ttu-id="c9255-170">Вы также можете создать собственный артефакт, щелкнув значок "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="c9255-170">You can also create your own artifact by selecting the plus sign (**+**).</span></span>

      ![Сведения об артефакте в диалоговом окне](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="c9255-172">Добавьте исходный код приложения, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="c9255-172">Add your application source code by doing the following:</span></span>

   <span data-ttu-id="c9255-173">а.</span><span class="sxs-lookup"><span data-stu-id="c9255-173">a.</span></span> <span data-ttu-id="c9255-174">В обозревателе проектов щелкните правой кнопкой мыши **src**, наведите указатель мыши на пункт **New** (Создать) и выберите **Scala Class** (Класс Scala).</span><span class="sxs-lookup"><span data-stu-id="c9255-174">In Project Explorer, right-click **src**, point to **New**, and then select **Scala Class**.</span></span>
      
      ![Команды для создания класса Scala в обозревателе проектов](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="c9255-176">b.</span><span class="sxs-lookup"><span data-stu-id="c9255-176">b.</span></span> <span data-ttu-id="c9255-177">В диалоговом окне **Create New Scala Class** (Создание класса Scala) введите имя, в поле **Kind** (Вид) выберите **Object** (Объект) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9255-177">In the **Create New Scala Class** dialog box, provide a name, select **Object** in the **Kind** box, and then select **OK**.</span></span>
      
      ![Диалоговое окно создания класса Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="c9255-179">c.</span><span class="sxs-lookup"><span data-stu-id="c9255-179">c.</span></span> <span data-ttu-id="c9255-180">Вставьте в файл **MyClusterApp.scala** следующий код.</span><span class="sxs-lookup"><span data-stu-id="c9255-180">In the **MyClusterApp.scala** file, paste the following code.</span></span> <span data-ttu-id="c9255-181">Этот код считывает данные из файла HVAC.csv (доступного для всех кластеров HDInsight Spark), извлекает строки, содержащие только одну цифру в седьмом столбце CSV-файла, и записывает результат в **/HVACOut** в используемом по умолчанию контейнере хранилища для кластера.</span><span class="sxs-lookup"><span data-stu-id="c9255-181">The code reads the data from HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that have only one digit in the seventh column in the CSV file, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="c9255-182">Запустите приложение в кластере HDInsight Spark следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c9255-182">Run the application on an HDInsight Spark cluster by doing the following:</span></span>

   <span data-ttu-id="c9255-183">а.</span><span class="sxs-lookup"><span data-stu-id="c9255-183">a.</span></span> <span data-ttu-id="c9255-184">В обозревателе проектов щелкните имя проекта правой кнопкой мыши и выберите **Submit Spark Application to HDInsight** (Отправить приложение Spark в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="c9255-184">In Project Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>
      
      ![Команда Submit Spark Application to HDInsight (Отправить приложение Spark в HDInsight)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="c9255-186">b.</span><span class="sxs-lookup"><span data-stu-id="c9255-186">b.</span></span> <span data-ttu-id="c9255-187">Вам будет предложено ввести учетные данные подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c9255-187">You are prompted to enter your Azure subscription credentials.</span></span> <span data-ttu-id="c9255-188">В диалоговом окне **Spark Submission** (Отправка в Spark) введите следующие значения и нажмите кнопку **Submit** (Отправить).</span><span class="sxs-lookup"><span data-stu-id="c9255-188">In the **Spark Submission** dialog box, provide the following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="c9255-189">В поле **Spark clusters (Linux only)**(Кластеры Spark (только для Linux)) выберите кластер HDInsight Spark, в котором вы хотите запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="c9255-189">For **Spark clusters (Linux only)**, select the HDInsight Spark cluster on which you want to run your application.</span></span>

      * <span data-ttu-id="c9255-190">Выберите артефакт из проекта IntelliJ или с жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="c9255-190">Select an artifact from the IntelliJ project, or select one from the hard drive.</span></span>

      * <span data-ttu-id="c9255-191">В текстовом поле **Main class name** (Имя основного класса) щелкните многоточие (**...**), выберите основной класс в исходном коде приложения и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9255-191">In the **Main class name** box, select the ellipsis (**...**), select the main class in your application source code, and then select **OK**.</span></span>

        ![Диалоговое окно выбора основного класса](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="c9255-193">Так как для кода приложения в этом примере не требуются аргументы командной строки, справочные JAR или файлы, остальные текстовые поля можно не заполнять.</span><span class="sxs-lookup"><span data-stu-id="c9255-193">Because the application code in this example does not require command-line arguments or reference JARs or files, you can leave the remaining boxes empty.</span></span> <span data-ttu-id="c9255-194">После ввода необходимой информации диалоговое окно должно выглядеть как на следующем изображении.</span><span class="sxs-lookup"><span data-stu-id="c9255-194">After you provide all the information, the dialog box should resemble the following image.</span></span>
        
        ![Диалоговое окно Spark Submission (Отправка в Spark)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="c9255-196">c.</span><span class="sxs-lookup"><span data-stu-id="c9255-196">c.</span></span> <span data-ttu-id="c9255-197">На вкладке **Spark Submission** (Отправка в Spark) в нижней части окна начнет отображаться ход выполнения.</span><span class="sxs-lookup"><span data-stu-id="c9255-197">The **Spark Submission** tab at the bottom of the window should start displaying the progress.</span></span> <span data-ttu-id="c9255-198">Приложение также можно остановить, выбрав красную кнопку в окне **Spark Submission** (Отправка в Spark).</span><span class="sxs-lookup"><span data-stu-id="c9255-198">You can also stop the application by selecting the red button in the **Spark Submission** window.</span></span>
      
      ![Окно Spark Submission (Отправка в Spark)](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="c9255-200">В разделе "Доступ к кластерам HDInsight Spark и управление ими с помощью набора средств Azure для IntelliJ" ниже в этой статье показано, как получить доступ к выходным данным задачи.</span><span class="sxs-lookup"><span data-stu-id="c9255-200">To learn how to access the job output, see the "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="c9255-201">Запуск или отладка приложения Spark Scala в кластере HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="c9255-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="c9255-202">Мы также рекомендуем еще один способ отправки приложения Spark в кластер.</span><span class="sxs-lookup"><span data-stu-id="c9255-202">We also recommend another way of submitting the Spark application to the cluster.</span></span> <span data-ttu-id="c9255-203">Он заключается в задании параметров **конфигураций запуска и отладки** в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="c9255-203">You can do so by setting the parameters in the **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="c9255-204">Дополнительные сведения см. в статье [Удаленная отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="c9255-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="c9255-205">Доступ к кластерам HDInsight Spark и управление ими с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c9255-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="c9255-206">При помощи набора средств Azure для IntelliJ можно выполнять разные операции.</span><span class="sxs-lookup"><span data-stu-id="c9255-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="c9255-207">Доступ к представлению задания</span><span class="sxs-lookup"><span data-stu-id="c9255-207">Access the job view</span></span>
1. <span data-ttu-id="c9255-208">В Azure Explorer разверните **HDInsight**, а затем выберите имя кластера Spark, после чего щелкните **Задания**.</span><span class="sxs-lookup"><span data-stu-id="c9255-208">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then select **Jobs**.</span></span>  

    ![Узел представления задания](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="c9255-210">В области справа на вкладке **Spark Job View** (Просмотр заданий Spark) отображаются все приложения, запускаемые в кластере.</span><span class="sxs-lookup"><span data-stu-id="c9255-210">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="c9255-211">Выберите имя приложения, дополнительные сведения о котором вы хотите просмотреть.</span><span class="sxs-lookup"><span data-stu-id="c9255-211">Select the name of the application for which you want to see more details.</span></span>

    ![Сведения о приложении](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="c9255-213">Чтобы отобразить базовые сведения о выполняющемся задании, наведите указатель мыши на граф задания.</span><span class="sxs-lookup"><span data-stu-id="c9255-213">To display basic running job information, hover over the job graph.</span></span> <span data-ttu-id="c9255-214">Чтобы просмотреть этапы графа и сведения, создаваемые каждым заданием, выберите узел на графе задания.</span><span class="sxs-lookup"><span data-stu-id="c9255-214">To view the stages graph and information that every job generates, select a node on the job graph.</span></span>

    ![Сведения об этапе задания](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="c9255-216">Выберите вкладку **Журнал**, чтобы просмотреть часто используемые журналы, включая *Driver Stderr*, *Driver Stdout* и *Directory Info*.</span><span class="sxs-lookup"><span data-stu-id="c9255-216">To view frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select the **Log** tab.</span></span>

    ![Подробные сведения журнала](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="c9255-218">Вы также можете просмотреть пользовательский интерфейс журнала Spark и пользовательский интерфейс YARN (на уровне приложения), щелкнув ссылку в верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="c9255-218">You can also view the Spark history UI and the YARN UI (at the application level) by selecting a link at the top of the window.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="c9255-219">Доступ к серверу журнала Spark</span><span class="sxs-lookup"><span data-stu-id="c9255-219">Access the Spark history server</span></span>
1. <span data-ttu-id="c9255-220">В Azure Explorer разверните **HDInsight**, щелкните имя кластера Spark правой кнопкой мыши и выберите **Open Spark History UI** (Открыть пользовательский интерфейс журнала Spark).</span><span class="sxs-lookup"><span data-stu-id="c9255-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="c9255-221">При появлении запроса введите учетные данные администратора для кластера, указанные при настройке кластера.</span><span class="sxs-lookup"><span data-stu-id="c9255-221">When you're prompted, enter the cluster's admin credentials, which you specified when you set up the cluster.</span></span>

3. <span data-ttu-id="c9255-222">На панели мониторинга сервера журнала Spark вы сможете найти приложение, выполнение которого только что было завершено, по его имени.</span><span class="sxs-lookup"><span data-stu-id="c9255-222">On the Spark history server dashboard, you can use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="c9255-223">В приведенном выше коде имя приложения было указано с помощью `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="c9255-223">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="c9255-224">Следовательно, приложение Spark называется **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="c9255-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="c9255-225">Запуск портала Ambari</span><span class="sxs-lookup"><span data-stu-id="c9255-225">Start the Ambari portal</span></span>
1. <span data-ttu-id="c9255-226">В Azure Explorer разверните **HDInsight**, щелкните имя кластера Spark правой кнопкой мыши и выберите **Open Cluster Management Portal (Ambari)** (Открыть портал управления кластерами (Ambari)).</span><span class="sxs-lookup"><span data-stu-id="c9255-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="c9255-227">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="c9255-227">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="c9255-228">Вы указали эти учетные данные во время установки кластера.</span><span class="sxs-lookup"><span data-stu-id="c9255-228">You specified these credentials during the cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="c9255-229">Управление подписками Azure</span><span class="sxs-lookup"><span data-stu-id="c9255-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="c9255-230">По умолчанию набор средств Azure для IntelliJ содержит список кластеров Spark из всех ваших подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="c9255-230">By default, Azure Toolkit for IntelliJ lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="c9255-231">При необходимости можно указать подписки, к которым необходимо получить доступ.</span><span class="sxs-lookup"><span data-stu-id="c9255-231">If necessary, you can specify the subscriptions that you want to access.</span></span> 

1. <span data-ttu-id="c9255-232">В Azure Explorer щелкните правой кнопкой мыши корневой узел **Azure**, а затем выберите **Управление подписками**.</span><span class="sxs-lookup"><span data-stu-id="c9255-232">In Azure Explorer, right-click the **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="c9255-233">В диалоговом окне снимите флажки напротив подписок, доступ к которым вам не требуется, и выберите **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="c9255-233">In the dialog box, clear the check boxes next to the subscriptions that you don't want to access, and then select **Close**.</span></span> <span data-ttu-id="c9255-234">Если вы хотите выйти из своей подписки Azure, выберите **Выйти**.</span><span class="sxs-lookup"><span data-stu-id="c9255-234">You can also select **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="c9255-235">Запуск приложения Spark Scala на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="c9255-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="c9255-236">Набор средств Azure для IntelliJ позволяет запускать приложения Spark Scala локально на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="c9255-236">You can use Azure Toolkit for IntelliJ to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="c9255-237">Как правило, такие приложения не требуют доступа к кластерным ресурсам, таким как контейнер хранилища, и могут запускаться и тестироваться локально.</span><span class="sxs-lookup"><span data-stu-id="c9255-237">The applications usually don't need access to cluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="c9255-238">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c9255-238">Prerequisite</span></span>
<span data-ttu-id="c9255-239">При запуске локального приложения Spark Scala на компьютере с Windows может возникнуть исключение, описанное в статье о [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="c9255-239">While you're running the local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="c9255-240">Это исключение возникает, так как в Windows отсутствует файл WinUtils.exe.</span><span class="sxs-lookup"><span data-stu-id="c9255-240">The exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="c9255-241">Чтобы устранить эту ошибку, [скачайте этот исполняемый файл](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe), например в папку **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="c9255-241">To resolve this error, [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="c9255-242">После этого добавьте переменную среды **HADOOP_HOME** и присвойте ей значение **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="c9255-242">Then, add the environment variable **HADOOP_HOME**, and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="c9255-243">Запуск локального приложения Spark Scala</span><span class="sxs-lookup"><span data-stu-id="c9255-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="c9255-244">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="c9255-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="c9255-245">В диалоговом окне **Новый проект** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9255-245">In the **New Project** dialog box, do the following:</span></span>
   
    <span data-ttu-id="c9255-246">а.</span><span class="sxs-lookup"><span data-stu-id="c9255-246">a.</span></span> <span data-ttu-id="c9255-247">Выберите **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Пример локального запуска Spark в HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="c9255-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="c9255-248">b.</span><span class="sxs-lookup"><span data-stu-id="c9255-248">b.</span></span> <span data-ttu-id="c9255-249">В списке **средств сборки** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="c9255-249">In the **Build tool** list, select either of the following, according to your need:</span></span>

      * <span data-ttu-id="c9255-250">**Maven.** Для поддержки мастера создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="c9255-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="c9255-251">**SBT.** Для управления зависимостями и создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="c9255-251">**SBT**, for managing the dependencies and building for the Scala project</span></span>

    ![Диалоговое окно нового проекта](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="c9255-253">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c9255-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="c9255-254">В следующем окне сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9255-254">In the next window, do the following:</span></span>
   
    <span data-ttu-id="c9255-255">а.</span><span class="sxs-lookup"><span data-stu-id="c9255-255">a.</span></span> <span data-ttu-id="c9255-256">Введите имя и расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="c9255-256">Enter a project name and location.</span></span>

    <span data-ttu-id="c9255-257">b.</span><span class="sxs-lookup"><span data-stu-id="c9255-257">b.</span></span> <span data-ttu-id="c9255-258">В раскрывающемся списке **пакета SDK проекта** выберите версию Jav выше 1.7.</span><span class="sxs-lookup"><span data-stu-id="c9255-258">In the **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="c9255-259">c.</span><span class="sxs-lookup"><span data-stu-id="c9255-259">c.</span></span> <span data-ttu-id="c9255-260">В раскрывающемся списке **версии Spark**  выберите версию Scala, которую необходимо использовать, например Scala 2.11.x для Spark 2.0 или Scala 2.10.x для Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="c9255-260">In the **Spark Version** drop-down list, select the version of Scala that you want to use: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![Диалоговое окно нового проекта](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="c9255-262">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c9255-262">Select **Finish**.</span></span>

6. <span data-ttu-id="c9255-263">Шаблон добавляет пример кода (**LogQuery**) в папку **src**, который можно запустить локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c9255-263">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Расположение LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="c9255-265">Щелкните правой кнопкой мыши приложение **LogQuery** и выберите **Run LogQuery** (Запустить LogQuery).</span><span class="sxs-lookup"><span data-stu-id="c9255-265">Right-click the **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="c9255-266">В нижней части вкладки **запуска** появятся выходные данные, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c9255-266">On the **Run** tab at the bottom, you see an output like the following:</span></span>
   
   ![Результат локального запуска приложения Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a><span data-ttu-id="c9255-268">Преобразование имеющихся приложений IntelliJ IDEA для использования набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c9255-268">Convert existing IntelliJ IDEA applications to use Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="c9255-269">Имеющиеся приложения Spark Scala, созданные в IntelliJ IDEA, можно преобразовать и сделать совместимыми с набором средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c9255-269">You can convert the existing Spark Scala applications that you created in IntelliJ IDEA to be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="c9255-270">Затем вы сможете использовать подключаемый модуль для отправки приложений в кластер HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="c9255-270">You can then use the plug-in to submit the applications to an HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="c9255-271">Для имеющегося приложения Spark Scala, созданного с помощью IntelliJ IDEA, откройте соответствующий IML-файл.</span><span class="sxs-lookup"><span data-stu-id="c9255-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open the associated .iml file.</span></span>

2. <span data-ttu-id="c9255-272">На корневом уровне вы увидите элемент **module** следующего вида:</span><span class="sxs-lookup"><span data-stu-id="c9255-272">At the root level is a **module** element like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="c9255-273">Измените элемент, добавив `UniqueKey="HDInsightTool"` , чтобы элемент **module** выглядел следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c9255-273">Edit the element to add `UniqueKey="HDInsightTool"` so that the **module** element looks like the following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="c9255-274">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="c9255-274">Save the changes.</span></span> <span data-ttu-id="c9255-275">Ваше приложение станет совместимым с набором средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c9255-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="c9255-276">Это можно проверить, щелкнув имя проекта в обозревателе проектов правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="c9255-276">You can test it by right-clicking the project name in Project Explorer.</span></span> <span data-ttu-id="c9255-277">Во всплывающем меню должен появиться пункт **Submit Spark Application to HDInsight** (Отправить приложение Spark в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="c9255-277">The pop-up menu now has the option **Submit Spark Application to HDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c9255-278">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="c9255-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="c9255-279">Ошибка *Please use a larger heap size* (Используйте больший размер кучи) в локальной среде</span><span class="sxs-lookup"><span data-stu-id="c9255-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="c9255-280">В Spark 1.6 при использовании 32-разрядного пакета SDK для Java в локальной среде выполнения могут возникать следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="c9255-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter the following errors:</span></span>

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

<span data-ttu-id="c9255-281">Это связано с тем, что размер кучи недостаточно велик для запуска Spark.</span><span class="sxs-lookup"><span data-stu-id="c9255-281">These errors happen because the heap size is not large enough for Spark to run.</span></span> <span data-ttu-id="c9255-282">Для Spark требуется не меньше 471 МБ.</span><span class="sxs-lookup"><span data-stu-id="c9255-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="c9255-283">(Дополнительные сведения см. в статье о [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) Простое решение – это использовать 64-разрядный пакет SDK для Java.</span><span class="sxs-lookup"><span data-stu-id="c9255-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is to use a 64-bit Java SDK.</span></span> <span data-ttu-id="c9255-284">Кроме того, можно изменить параметры виртуальной машины Java в IntelliJ, добавив следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c9255-284">You can also change the JVM settings in IntelliJ by adding the following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Добавление параметров в поле VM options (Параметры виртуальной машины) в IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="c9255-286">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="c9255-286">FAQ</span></span>
<span data-ttu-id="c9255-287">Чтобы отправить приложение в Azure Data Lake Store, выберите **интерактивный** режим во время входа в Azure.</span><span class="sxs-lookup"><span data-stu-id="c9255-287">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="c9255-288">Если выбрать **автоматический** режим, может произойти ошибка.</span><span class="sxs-lookup"><span data-stu-id="c9255-288">If you select **Automated** mode, you can get an error.</span></span>

![Интерактивный вход](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="c9255-290">Теперь мы устранили ее.</span><span class="sxs-lookup"><span data-stu-id="c9255-290">Now, we resolved it.</span></span> <span data-ttu-id="c9255-291">Можно выбрать кластер Azure Data Lake для отправки приложения с помощью любого метода входа.</span><span class="sxs-lookup"><span data-stu-id="c9255-291">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="c9255-292">Отзывы и известные проблемы</span><span class="sxs-lookup"><span data-stu-id="c9255-292">Feedback and known issues</span></span>
<span data-ttu-id="c9255-293">Сейчас просмотр выходных данных Spark напрямую не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c9255-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="c9255-294">С любыми отзывами и предложениями, а также в случае возникновения проблем при работе с этим подключаемым модулем вы можете отправить сообщение по электронному адресу hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="c9255-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="c9255-295"><a name="seealso"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9255-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="c9255-296">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9255-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="c9255-297">Демонстрация</span><span class="sxs-lookup"><span data-stu-id="c9255-297">Demo</span></span>
* <span data-ttu-id="c9255-298">Создание проекта Scala (видео): [создание приложений Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c9255-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="c9255-299">Удаленная отладка (видео): [удаленная отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c9255-299">Remote debug (video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="c9255-300">Сценарии</span><span class="sxs-lookup"><span data-stu-id="c9255-300">Scenarios</span></span>
* [<span data-ttu-id="c9255-301">Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9255-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c9255-302">Создание приложений машинного обучения Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9255-302">Spark with Machine Learning: Use Spark in HDInsight to analyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c9255-303">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="c9255-303">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c9255-304">Потоковая передача Apache Spark. Обработка данных из концентраторов событий Azure с помощью кластера Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9255-304">Spark Streaming: Use Spark in HDInsight to build real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c9255-305">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9255-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="c9255-306">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="c9255-306">Creating and running applications</span></span>
* [<span data-ttu-id="c9255-307">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="c9255-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c9255-308">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="c9255-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c9255-309">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="c9255-309">Tools and extensions</span></span>
* [<span data-ttu-id="c9255-310">Удаленная отладка приложений Spark через VPN с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c9255-310">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c9255-311">Удаленная отладка приложений Spark через SSH с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c9255-311">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="c9255-312">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="c9255-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="c9255-313">Использование средств HDInsight в наборе средств Azure для Eclipse для создания приложений Spark</span><span class="sxs-lookup"><span data-stu-id="c9255-313">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="c9255-314">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9255-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c9255-315">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9255-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c9255-316">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="c9255-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c9255-317">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c9255-317">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="c9255-318">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="c9255-318">Managing resources</span></span>
* [<span data-ttu-id="c9255-319">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9255-319">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c9255-320">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="c9255-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

