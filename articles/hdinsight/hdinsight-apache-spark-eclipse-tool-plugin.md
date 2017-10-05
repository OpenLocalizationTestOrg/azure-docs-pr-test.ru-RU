---
title: "Создание приложений Scala для HDInsight Spark с помощью набора средств Azure для Eclipse | Документация Майкрософт"
description: "Использование средств HDInsight из набора средств Azure для Eclipse для разработки приложений Spark на языке Scala и их отправки в кластер HDInsight Spark непосредственно из интегрированной среды разработки Eclipse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 4bcb1987a62c0b7f4965e6fd257315e820004238
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-eclipse-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="616f8-103">Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="616f8-103">Use Azure Toolkit for Eclipse to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="616f8-104">Использование средств HDInsight из набора средств Azure для Eclipse для разработки приложений Spark на языке Scala и их отправки в кластер Azure HDInsight Spark непосредственно из интегрированной среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="616f8-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an Azure HDInsight Spark cluster, directly from the Eclipse IDE.</span></span> <span data-ttu-id="616f8-105">Подключаемый модуль средств HDInsight можно использовать по-разному.</span><span class="sxs-lookup"><span data-stu-id="616f8-105">You can use the HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="616f8-106">Для разработки и отправки приложений Scala Spark в кластер HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="616f8-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="616f8-107">Для доступа к ресурсам кластера Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="616f8-107">To access your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="616f8-108">Для разработки и локального запуска приложений Scala Spark.</span><span class="sxs-lookup"><span data-stu-id="616f8-108">To develop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="616f8-109">Это средство позволяет создавать и отправлять приложения только в кластер HDInsight Spark на Linux.</span><span class="sxs-lookup"><span data-stu-id="616f8-109">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="616f8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="616f8-110">Prerequisites</span></span>

* <span data-ttu-id="616f8-111">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="616f8-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="616f8-112">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="616f8-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="616f8-113">Комплект разработчика Oracle Java версии 8, который используется для среды выполнения интегрированной среды разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="616f8-113">Oracle Java Development Kit version 8, which is used for the Eclipse IDE runtime.</span></span> <span data-ttu-id="616f8-114">Его можно скачать с [веб-сайта Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="616f8-114">You can download it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="616f8-115">Интегрированная среда разработки Eclipse.</span><span class="sxs-lookup"><span data-stu-id="616f8-115">Eclipse IDE.</span></span> <span data-ttu-id="616f8-116">В этой статье используется Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="616f8-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="616f8-117">Его можно установить с [веб-сайта Eclipse](https://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="616f8-117">You can install it from the [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="616f8-118">Пакет SDK для Spark.</span><span class="sxs-lookup"><span data-stu-id="616f8-118">Spark SDK.</span></span> <span data-ttu-id="616f8-119">Скачать эту версию можно с [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="616f8-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="616f8-120">Установка средства HDInsight в набор средств Azure для Eclipse и Scala подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="616f8-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="616f8-121">Установка средств HDInsight</span><span class="sxs-lookup"><span data-stu-id="616f8-121">Install HDInsight Tools</span></span>
<span data-ttu-id="616f8-122">Средства HDInsight для Eclipse доступны в составе набора средств Azure для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="616f8-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="616f8-123">Инструкции по установке см. в статье [Установка набора средств Azure для Eclipse](../azure-toolkit-for-eclipse-installation.md).</span><span class="sxs-lookup"><span data-stu-id="616f8-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="616f8-124">Установите подключаемый модуль Scala</span><span class="sxs-lookup"><span data-stu-id="616f8-124">Install Scala Plugin</span></span>
<span data-ttu-id="616f8-125">При открытии Intellij автоматического средства HDInsight обнаруживает ли установлен подключаемый модуль Scala или нет.</span><span class="sxs-lookup"><span data-stu-id="616f8-125">When you open the Intellij, the HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="616f8-126">Нажмите кнопку **ОК** продолжить и следуйте инструкциям по установке, Eclipse Marketplace.</span><span class="sxs-lookup"><span data-stu-id="616f8-126">Click **OK** to continue and follow the instructions to install by the Eclipse Marketplace.</span></span>

 ![Подключаемый модуль Scala установки автоматически](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="616f8-128">Войдите в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="616f8-128">Sign in to your Azure subscription</span></span>
1. <span data-ttu-id="616f8-129">Запустите интегрированную среду разработки Eclipse и откройте Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="616f8-129">Start the Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="616f8-130">В меню **Window** (Окно) выберите пункт **Show View** (Показать представление) и щелкните **Other** (Другие).</span><span class="sxs-lookup"><span data-stu-id="616f8-130">On the **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="616f8-131">В открывшемся диалоговом окне разверните **Azure** и щелкните **Azure Explorer**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="616f8-131">In the dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![Диалоговое окно Show View (Показать представление)](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="616f8-133">Щелкните правой кнопкой мыши узел **Azure**, а затем выберите пункт **Sign in** (Войти).</span><span class="sxs-lookup"><span data-stu-id="616f8-133">Right-click the **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="616f8-134">В диалоговом окне **Azure Sign In** (Вход в Azure) выберите режим проверки подлинности, нажмите кнопку **Sign in** (Войти) и введите свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="616f8-134">In the **Azure Sign In** dialog box, choose the authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![Диалоговое окно входа в Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="616f8-136">После входа в диалоговом окне **Select Subscriptions** (Выбор подписок) будут перечислены все подписки Azure, связанные с указанными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="616f8-136">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span></span> <span data-ttu-id="616f8-137">Щелкните **Select** (Выбрать), чтобы закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="616f8-137">Click **Select** to close the dialog box.</span></span>

    ![Диалоговое окно выбора подписок](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="616f8-139">На вкладке **Azure Explorer** разверните **HDInsight**, чтобы просмотреть кластеры HDInsight Spark в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="616f8-139">On the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span></span>
   
    ![Кластеры HDInsight Spark в Azure Explorer](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="616f8-141">Далее можно развернуть узел имени кластера, чтобы увидеть ресурсы (например, учетные записи хранения), связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="616f8-141">You can further expand a cluster name node to see the resources (for example, storage accounts) associated with the cluster.</span></span>
   
    ![Развертывание имени кластера для просмотра ресурсов](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="616f8-143">Настройка проекта Spark Scala для кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="616f8-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="616f8-144">В рабочей области интегрированной среды разработки Eclipse щелкните **File** (Файл), **New** (Создать), **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="616f8-144">In the Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="616f8-145">В мастере New Project (Новый проект) разверните **HDInsight**, выберите **Spark on HDInsight (Scala)** (Spark в HDInsight (Scala)) и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="616f8-145">In the New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![Выбор проекта Spark в HDInsight (Scala)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="616f8-147">Мастер создания проекта Scala автоматически определяет, установлен ли подключаемый модуль Scala.</span><span class="sxs-lookup"><span data-stu-id="616f8-147">The Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="616f8-148">Нажмите кнопку **ОК** продолжать загрузку подключаемый модуль Scala, следуйте инструкциям на перезапуск Eclipse.</span><span class="sxs-lookup"><span data-stu-id="616f8-148">Click **OK** to continue downloading the Scala plugin, then follow the instructions to restart Eclipse.</span></span>

    ![Проверка Scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="616f8-150">В диалоговом окне **New HDInsight Scala Project** (Новый проект Scala HDInsight) введите следующие значения, после чего нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="616f8-150">In the **New HDInsight Scala Project** dialog box, provide the following values, and then click **Next**:</span></span>
   * <span data-ttu-id="616f8-151">Введите имя проекта.</span><span class="sxs-lookup"><span data-stu-id="616f8-151">Enter a name for the project.</span></span>
   * <span data-ttu-id="616f8-152">Убедитесь, что в поле **JRE** параметр **Use an execution environment JRE** (Использовать среду выполнения JRE) имеет значение **JavaSE-1.7** или более позднюю версию.</span><span class="sxs-lookup"><span data-stu-id="616f8-152">In the **JRE** area, make sure that **Use an execution environment JRE** is set to **JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="616f8-153">Убедитесь, что для пакета SDK для Spark задано расположение, в которое вы скачали этот пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="616f8-153">Make sure that Spark SDK is set to the location where you downloaded the SDK.</span></span> <span data-ttu-id="616f8-154">Ссылка для скачивания указана в разделе [Предварительные требования](#prerequisites) ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="616f8-154">The link to the download location is included in the [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="616f8-155">Можно также скачать пакет SDK по ссылке в этом диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="616f8-155">You can also download the SDK from the link included in the dialog box.</span></span>

    ![Диалоговое окно нового проекта Scala HDInsight](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="616f8-157">В следующем диалоговом окне щелкните вкладку **Libraries** (Библиотеки) и оставьте значения по умолчанию, а затем щелкните **Finish**  (Готово).</span><span class="sxs-lookup"><span data-stu-id="616f8-157">In the next dialog box, click the **Libraries** tab and keep the defaults, and then click **Finish**.</span></span> 
   
    ![Вкладка Libraries (Библиотеки)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="616f8-159">Создание приложения Scala для кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="616f8-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="616f8-160">В интегрированной среде разработки Eclipse в обозревателе пакетов разверните созданный ранее проект, щелкните правой кнопкой мыши **src**, выберите **New** (Создать) и щелкните **Other** (Другое).</span><span class="sxs-lookup"><span data-stu-id="616f8-160">In the Eclipse IDE, from Package Explorer, expand the project that you created earlier, right-click **src**, point to **New**, and then click **Other**.</span></span>
2. <span data-ttu-id="616f8-161">В диалоговом окне **Select a wizard** (Выбор мастера) разверните **Scala Wizards** (Мастера Scala), щелкните **Scala Object** (Объект Scala) и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="616f8-161">In the **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![Диалоговое окно выбора мастера](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="616f8-163">В диалоговом окне **Create New File** (Создание файла) введите имя объекта и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="616f8-163">In the **Create New File** dialog box, enter a name for the object, and then click **Finish**.</span></span>
   
    ![Диалоговое окно создания нового файла](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="616f8-165">Вставьте следующий код в текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="616f8-165">Paste the following code in the text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows that have only one digit in the seventh column in the CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="616f8-166">Запустите приложение в кластере HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="616f8-166">Run the application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="616f8-167">В обозревателе пакетов щелкните имя проекта правой кнопкой мыши и выберите пункт **Submit Spark Application to HDInsight** (Отправить приложение Spark в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="616f8-167">From Package Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>        
   2. <span data-ttu-id="616f8-168">В диалоговом окне **Spark Submission** (Отправка в Spark) введите следующие значения и нажмите кнопку **Submit** (Отправить).</span><span class="sxs-lookup"><span data-stu-id="616f8-168">In the **Spark Submission** dialog box, provide the following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="616f8-169">В поле **Cluster Name**(Имя кластера) выберите кластер HDInsight Spark, в котором вы хотите запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="616f8-169">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span></span>
      * <span data-ttu-id="616f8-170">Выберите артефакт из проекта Eclipse или с жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="616f8-170">Select an artifact from the Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="616f8-171">Значение по умолчанию зависит от элемента, который вы щелкнете правой кнопкой мыши в обозревателе пакетов.</span><span class="sxs-lookup"><span data-stu-id="616f8-171">The default value depends on the item you right-click from package explorer.</span></span>
      * <span data-ttu-id="616f8-172">В раскрывающемся списке **Main class name** (Имя класса main) в мастере отправки отображаются имена всех объектов из выбранного проекта.</span><span class="sxs-lookup"><span data-stu-id="616f8-172">In the **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="616f8-173">Выберите или введите имя любого из них, который требуется запустить.</span><span class="sxs-lookup"><span data-stu-id="616f8-173">Select or input one that you want to run.</span></span> <span data-ttu-id="616f8-174">При выборе артефакта с жесткого диска необходимо указать имя класса main самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="616f8-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="616f8-175">Так как для кода приложения в этом примере не требуются аргументы командной строки, справочные JAR или файлы, остальные текстовые поля можно не заполнять.</span><span class="sxs-lookup"><span data-stu-id="616f8-175">Because the application code in this example does not require any command-line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span></span>
        
       ![Диалоговое окно Spark Submission (Отправка в Spark)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="616f8-177">На вкладке **Spark Submission** (Отправка в Spark) начнет отображаться ход выполнения.</span><span class="sxs-lookup"><span data-stu-id="616f8-177">The **Spark Submission** tab should start displaying the progress.</span></span> <span data-ttu-id="616f8-178">Вы можете остановить приложение, щелкнув красную кнопку в окне **Spark Submission** (Отправка в Spark).</span><span class="sxs-lookup"><span data-stu-id="616f8-178">You can stop the application by clicking the red button in the **Spark Submission** window.</span></span> <span data-ttu-id="616f8-179">Можно также просмотреть журналы для данного запуска приложения, щелкнув значок глобуса (обозначен на рисунке синей рамкой).</span><span class="sxs-lookup"><span data-stu-id="616f8-179">You can also view the logs for this specific application run by clicking the globe icon (denoted by the blue box in the image).</span></span>
      
       ![Окно Spark Submission (Отправка в Spark)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="616f8-181">Доступ к кластерам HDInsight Spark и управление ими с помощью средств HDInsight в наборе средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="616f8-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="616f8-182">С помощью средств HDInsight можно выполнять различные операции, включая доступ к выходным данным заданий.</span><span class="sxs-lookup"><span data-stu-id="616f8-182">You can perform various operations by using HDInsight Tools, including accessing the job output.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="616f8-183">Доступ к представлению задания</span><span class="sxs-lookup"><span data-stu-id="616f8-183">Access the job view</span></span>
1. <span data-ttu-id="616f8-184">В Azure Explorer разверните **HDInsight**, а затем выберите имя кластера Spark, после чего щелкните **Задания**.</span><span class="sxs-lookup"><span data-stu-id="616f8-184">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then click **Jobs**.</span></span> 

    ![Узел представления задания](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="616f8-186">Щелкните **заданий** узла.</span><span class="sxs-lookup"><span data-stu-id="616f8-186">Click on the **Jobs** node.</span></span> <span data-ttu-id="616f8-187">Средства HDInsight автоматически обнаруживает ли установлен подключаемый модуль clipse E (fx) или нет.</span><span class="sxs-lookup"><span data-stu-id="616f8-187">The HDInsight Tools auto-detects whether you installed the E(fx)clipse plugin or not.</span></span> <span data-ttu-id="616f8-188">Нажмите кнопку **ОК** продолжить и следуйте инструкциям по установке на рынке Eclipse и перезапустите Eclipse.</span><span class="sxs-lookup"><span data-stu-id="616f8-188">Click **OK** to continue and follow the instructions to install the Eclipse Marketplace and restart Eclipse.</span></span>

    ![Установка E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="616f8-190">Откройте представление задания из узла **Задания**.</span><span class="sxs-lookup"><span data-stu-id="616f8-190">Open the Job View from the **Jobs** node.</span></span> <span data-ttu-id="616f8-191">В области справа на вкладке **Spark Job View** (Просмотр заданий Spark) отображаются все приложения, запускаемые в кластере.</span><span class="sxs-lookup"><span data-stu-id="616f8-191">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="616f8-192">Щелкните имя приложения, дополнительные сведения о котором вы хотите просмотреть.</span><span class="sxs-lookup"><span data-stu-id="616f8-192">Click the name of the application for which you want to see more details.</span></span>

    ![Сведения о приложении](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="616f8-194">При наведении указателя мыши на диаграмме задания отображается базовые сведения выполняющегося задания.</span><span class="sxs-lookup"><span data-stu-id="616f8-194">If you hover on the job graph, it displays basic running job info.</span></span> <span data-ttu-id="616f8-195">Щелкните задание graph отобразить этапы диаграммы и информация, что приводит к возникновению ошибки каждого задания.</span><span class="sxs-lookup"><span data-stu-id="616f8-195">Clicking on the job graph shows the stages graph and info that every job generates.</span></span>

    ![Сведения об этапе задания](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="616f8-197">Часто используемые журналов, включая Stderr драйвера, драйвер Stdout и сведений о каталоге, перечислены в **журнала** вкладки.</span><span class="sxs-lookup"><span data-stu-id="616f8-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in the **Log** tab.</span></span>

    ![Подробные сведения журнала](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="616f8-199">Кроме того, вы можете открыть пользовательский интерфейс журнала Spark и пользовательский интерфейс YARN (на уровне приложения), щелкнув соответствующую ссылку в верхней части окна.</span><span class="sxs-lookup"><span data-stu-id="616f8-199">You can also open the Spark history UI and the YARN UI (at the application level) by clicking the respective hyperlink at the top of the window.</span></span>

### <a name="access-the-storage-container-for-the-cluster"></a><span data-ttu-id="616f8-200">Доступ к контейнеру хранилища для кластера</span><span class="sxs-lookup"><span data-stu-id="616f8-200">Access the storage container for the cluster</span></span>
1. <span data-ttu-id="616f8-201">В Azure Explorer разверните корневой узел **HDInsight**, чтобы увидеть список доступных кластеров HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="616f8-201">In Azure Explorer, expand the **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="616f8-202">Разверните имя кластера, чтобы увидеть учетную запись хранилища и контейнер хранилища по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="616f8-202">Expand the cluster name to see the storage account and the default storage container for the cluster.</span></span>
   
    ![Учетная запись хранения и контейнер по умолчанию](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="616f8-204">Щелкните имя связанного с кластером контейнера хранилища.</span><span class="sxs-lookup"><span data-stu-id="616f8-204">Click the storage container name associated with the cluster.</span></span> <span data-ttu-id="616f8-205">В области справа дважды щелкните папку **HVACOut**.</span><span class="sxs-lookup"><span data-stu-id="616f8-205">In the right pane, double-click the **HVACOut** folder.</span></span> <span data-ttu-id="616f8-206">Откройте один из файлов **part-** для просмотра выходных данных приложения.</span><span class="sxs-lookup"><span data-stu-id="616f8-206">Open one of the **part-** files to see the output of the application.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="616f8-207">Доступ к серверу журнала Spark</span><span class="sxs-lookup"><span data-stu-id="616f8-207">Access the Spark history server</span></span>
1. <span data-ttu-id="616f8-208">В Azure Explorer щелкните имя кластера Spark правой кнопкой мыши и выберите пункт **Open Spark History UI** (Открыть пользовательский интерфейс журнала Spark).</span><span class="sxs-lookup"><span data-stu-id="616f8-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="616f8-209">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="616f8-209">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="616f8-210">Вы должны были указать их при подготовке кластера.</span><span class="sxs-lookup"><span data-stu-id="616f8-210">You must have specified these while provisioning the cluster.</span></span>
2. <span data-ttu-id="616f8-211">На панели мониторинга сервера журнала Spark вы сможете найти приложение, выполнение которого только что было завершено, по его имени.</span><span class="sxs-lookup"><span data-stu-id="616f8-211">In the Spark history server dashboard, you use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="616f8-212">В приведенном выше коде имя приложения было указано с помощью `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="616f8-212">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="616f8-213">Следовательно, приложение Spark называлось **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="616f8-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="616f8-214">Запуск портала Ambari</span><span class="sxs-lookup"><span data-stu-id="616f8-214">Start the Ambari portal</span></span>
1. <span data-ttu-id="616f8-215">В Azure Explorer щелкните имя кластера Spark правой кнопкой мыши и выберите пункт **Open Cluster Management Portal (Ambari)** (Открыть портал управления кластерами (Ambari)).</span><span class="sxs-lookup"><span data-stu-id="616f8-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="616f8-216">При появлении запроса введите учетные данные администратора для кластера.</span><span class="sxs-lookup"><span data-stu-id="616f8-216">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="616f8-217">Вы должны были указать их при подготовке кластера.</span><span class="sxs-lookup"><span data-stu-id="616f8-217">You must have specified these while provisioning the cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="616f8-218">Управление подписками Azure</span><span class="sxs-lookup"><span data-stu-id="616f8-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="616f8-219">По умолчанию средства HDInsight в наборе средств Azure для Eclipse содержат список кластеров Spark из всех ваших подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="616f8-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="616f8-220">При необходимости можно указать подписки, кластеры из которых вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="616f8-220">If necessary, you can specify the subscriptions for which you want to access the cluster.</span></span> 

1. <span data-ttu-id="616f8-221">В Azure Explorer щелкните правой кнопкой мыши корневой узел **Azure**, а затем выберите пункт **Управление подписками**.</span><span class="sxs-lookup"><span data-stu-id="616f8-221">In Azure Explorer, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="616f8-222">В диалоговом окне снимите флажки напротив подписок, доступ к которым вам не требуется, и нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="616f8-222">In the dialog box, clear the check boxes for the subscription that you don't want to access, and then click **Close**.</span></span> <span data-ttu-id="616f8-223">Если вы хотите выйти из своей подписки Azure, нажмите кнопку **Выйти**.</span><span class="sxs-lookup"><span data-stu-id="616f8-223">You can also click **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="616f8-224">Запуск приложения Spark Scala на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="616f8-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="616f8-225">Средства HDInsight в наборе средств Azure для Eclipse позволяют запускать приложения Spark Scala локально на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="616f8-225">You can use HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="616f8-226">Как правило, такие приложения не требуют доступа к ресурсам кластера, таким как контейнер хранилища, и могут запускаться и тестироваться локально.</span><span class="sxs-lookup"><span data-stu-id="616f8-226">Typically, these applications don't need access to cluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="616f8-227">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="616f8-227">Prerequisite</span></span>
<span data-ttu-id="616f8-228">При запуске локального приложения Spark Scala на компьютере с Windows может возникнуть исключение, описанное в [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="616f8-228">While you're running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="616f8-229">Это исключение возникает, так как в Windows отсутствует файл **WinUtils.exe**.</span><span class="sxs-lookup"><span data-stu-id="616f8-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="616f8-230">Чтобы устранить эту ошибку, [скачайте этот исполняемый файл](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe), например в папку **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="616f8-230">To resolve this error, you must [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="616f8-231">После этого добавьте переменную среды **HADOOP_HOME** и присвойте ей значение **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="616f8-231">You must then add the environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="616f8-232">Запуск локального приложения Spark Scala</span><span class="sxs-lookup"><span data-stu-id="616f8-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="616f8-233">Запустите Eclipse и создайте новый проект.</span><span class="sxs-lookup"><span data-stu-id="616f8-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="616f8-234">В диалоговом окне **нового проекта** установите параметры, как на снимке экрана ниже, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="616f8-234">In the **New Project** dialog box, make the following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="616f8-235">В левой области выберите **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="616f8-235">In the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="616f8-236">В правой области выберите **Spark on HDInsight Local Run Sample (Scala)** (Пример локального запуска Spark в HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="616f8-236">In the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![Диалоговое окно "Новый проект"](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="616f8-238">Чтобы предоставить сведения о проекте, выполните шаги 3–6, как описано в разделе [Настройка проекта Spark Scala для кластера HDInsight Spark](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span><span class="sxs-lookup"><span data-stu-id="616f8-238">To provide the project details, follow steps 3 through 6 from the earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="616f8-239">Шаблон добавляет пример кода (**LogQuery**) в папку **src**, который можно запустить локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="616f8-239">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![Расположение LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="616f8-241">Щелкните правой кнопкой мыши приложение **LogQuery**, выберите пункт **Run As** (Запустить от имени) и щелкните **1 Scala Application** (1. Приложение Scala).</span><span class="sxs-lookup"><span data-stu-id="616f8-241">Right-click the **LogQuery** application, point to **Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="616f8-242">В нижней части вкладки **Console** (Консоль) вы увидите выходные данные следующего вида.</span><span class="sxs-lookup"><span data-stu-id="616f8-242">You will see an output like this in the **Console** tab at the bottom:</span></span>
   
   ![Результат локального запуска приложения Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="616f8-244">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="616f8-244">FAQ</span></span>
<span data-ttu-id="616f8-245">Чтобы отправить приложение в Azure Data Lake Store, выберите **интерактивный** режим во время входа в Azure.</span><span class="sxs-lookup"><span data-stu-id="616f8-245">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="616f8-246">Если выбрать **автоматический** режим, может произойти ошибка.</span><span class="sxs-lookup"><span data-stu-id="616f8-246">If you select **Automated** mode, you can get an error.</span></span>

![Интерактивный вход](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="616f8-248">Теперь мы устранили ее.</span><span class="sxs-lookup"><span data-stu-id="616f8-248">Now, we resolved it.</span></span> <span data-ttu-id="616f8-249">Можно выбрать кластер Azure Data Lake для отправки приложения с помощью любого метода входа.</span><span class="sxs-lookup"><span data-stu-id="616f8-249">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="616f8-250">Отзывы и известные проблемы</span><span class="sxs-lookup"><span data-stu-id="616f8-250">Feedback and known issues</span></span>
<span data-ttu-id="616f8-251">Сейчас просмотр выходных данных Spark напрямую не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="616f8-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="616f8-252">С любыми отзывами и предложениями (а также в случае возникновения проблем при работе с этим инструментом) обращайтесь по электронному адресу hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="616f8-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free to send us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="616f8-253"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="616f8-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="616f8-254">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="616f8-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="616f8-255">Сценарии</span><span class="sxs-lookup"><span data-stu-id="616f8-255">Scenarios</span></span>
* [<span data-ttu-id="616f8-256">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="616f8-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="616f8-257">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="616f8-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="616f8-258">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="616f8-258">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="616f8-259">Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="616f8-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="616f8-260">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="616f8-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="616f8-261">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="616f8-261">Creating and running applications</span></span>
* [<span data-ttu-id="616f8-262">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="616f8-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="616f8-263">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="616f8-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="616f8-264">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="616f8-264">Tools and extensions</span></span>
* [<span data-ttu-id="616f8-265">Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="616f8-265">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="616f8-266">Удаленная отладка приложений Spark через VPN с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="616f8-266">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="616f8-267">Удаленная отладка приложений Spark через SSH с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="616f8-267">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="616f8-268">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="616f8-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="616f8-269">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="616f8-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="616f8-270">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="616f8-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="616f8-271">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="616f8-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="616f8-272">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="616f8-272">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="616f8-273">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="616f8-273">Managing resources</span></span>
* [<span data-ttu-id="616f8-274">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="616f8-274">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="616f8-275">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="616f8-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

