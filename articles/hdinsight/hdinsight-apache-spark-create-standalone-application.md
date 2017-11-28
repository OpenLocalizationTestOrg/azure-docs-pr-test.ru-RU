---
title: "Создание приложения Scala для работы в кластерах Spark — Azure HDInsight | Документы Майкрософт"
description: "Создайте приложение Spark, написанное на Scala, используя Apache Maven в качестве системы сборки и существующий архетип Maven для Scala, который предоставляется IntelliJ IDEA."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 95dba08744357f8800b05e3d4b892e3a363d5985
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-scala-maven-application-to-run-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="360c7-103">Создание приложения Scala в Maven для работы в кластере Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="360c7-103">Create a Scala Maven application to run on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="360c7-104">Узнайте, как создать приложение Spark на языке Scala в Maven с помощью IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="360c7-104">Learn how to create a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="360c7-105">В качестве системы сборки в этой статье используется Apache Maven и изначально применяется существующий архетип Maven для Scala, который обеспечивает IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="360c7-105">The article uses Apache Maven as the build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="360c7-106">Создание приложения Scala в IntelliJ IDEA включает в себя следующие этапы:</span><span class="sxs-lookup"><span data-stu-id="360c7-106">Creating a Scala application in IntelliJ IDEA involves the following steps:</span></span>

* <span data-ttu-id="360c7-107">использование Maven в качестве системы сборки;</span><span class="sxs-lookup"><span data-stu-id="360c7-107">Use Maven as the build system.</span></span>
* <span data-ttu-id="360c7-108">обновление файла объектной модели проектов для разрешения зависимостей модуля Spark;</span><span class="sxs-lookup"><span data-stu-id="360c7-108">Update Project Object Model (POM) file to resolve Spark module dependencies.</span></span>
* <span data-ttu-id="360c7-109">написание приложения на языке Scala;</span><span class="sxs-lookup"><span data-stu-id="360c7-109">Write your application in Scala.</span></span>
* <span data-ttu-id="360c7-110">создание JAR-файла, который можно отправить в кластеры HDInsight Spark;</span><span class="sxs-lookup"><span data-stu-id="360c7-110">Generate a jar file that can be submitted to HDInsight Spark clusters.</span></span>
* <span data-ttu-id="360c7-111">запуск приложений с помощью Livy в кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="360c7-111">Run the application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="360c7-112">HDInsight также предоставляет подключаемый модуль IntelliJ IDEA для упрощения процесса создания и отправки приложений в кластер HDInsight Spark на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="360c7-112">HDInsight also provides an IntelliJ IDEA plugin tool to ease the process of creating and submitting applications to an HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="360c7-113">Дополнительные сведения см. в статье [Создание приложений Spark для кластера HDInsight Spark на платформе Linux с помощью средств HDInsight в наборе средств Azure для IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="360c7-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="360c7-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="360c7-114">Prerequisites</span></span>

* <span data-ttu-id="360c7-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="360c7-115">An Azure subscription.</span></span> <span data-ttu-id="360c7-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="360c7-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="360c7-117">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="360c7-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="360c7-118">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="360c7-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="360c7-119">Комплект разработчика Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="360c7-119">Oracle Java Development kit.</span></span> <span data-ttu-id="360c7-120">Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="360c7-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="360c7-121">Java IDE.</span><span class="sxs-lookup"><span data-stu-id="360c7-121">A Java IDE.</span></span> <span data-ttu-id="360c7-122">В этой статье используется среда IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="360c7-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="360c7-123">Его можно установить [отсюда](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="360c7-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="360c7-124">Установка подключаемого модуля Scala для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="360c7-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="360c7-125">Если во время установки IntelliJ IDEA вы не получили запрос на включение подключаемого модуля Scala, запустите IntelliJ IDEA и выполните следующие действия, чтобы установить его:</span><span class="sxs-lookup"><span data-stu-id="360c7-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through the following steps to install the plugin:</span></span>

1. <span data-ttu-id="360c7-126">Запустите IntelliJ IDEA и на экране приветствия щелкните **Configure** (Настройка), а затем — **Plugins** (Подключаемые модули).</span><span class="sxs-lookup"><span data-stu-id="360c7-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Включение подключаемого модуля Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="360c7-128">На следующем экране в левом нижнем углу щелкните **Install JetBrains plugin** («Установить подключаемый модуль JetBrains»).</span><span class="sxs-lookup"><span data-stu-id="360c7-128">In the next screen, click **Install JetBrains plugin** from the lower left corner.</span></span> <span data-ttu-id="360c7-129">В открывшемся диалоговом окне **Browse JetBrains Plugins** (Обзор подключаемых модулей JetBrains) найдите модуль Scala и нажмите кнопку **Install** (Установить).</span><span class="sxs-lookup"><span data-stu-id="360c7-129">In the **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Установка подключаемого модуля Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="360c7-131">После успешной установки подключаемого модуля нажмите кнопку **Restart IntelliJ IDEA** («Перезапустить IntelliJ IDEA»), чтобы перезапустить IDE.</span><span class="sxs-lookup"><span data-stu-id="360c7-131">After the plugin installs successfully, click the **Restart IntelliJ IDEA button** to restart the IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="360c7-132">Создание автономного проекта Scala</span><span class="sxs-lookup"><span data-stu-id="360c7-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="360c7-133">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="360c7-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="360c7-134">В диалоговом окне нового проекта установите параметры, как на снимке экрана ниже, а затем нажмите кнопку **Next**(«Далее»).</span><span class="sxs-lookup"><span data-stu-id="360c7-134">In the new project dialog box, make the following choices, and then click **Next**.</span></span>
   
    ![Создание проекта Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="360c7-136">Выберите **Maven** в качестве типа проекта.</span><span class="sxs-lookup"><span data-stu-id="360c7-136">Select **Maven** as the project type.</span></span>
   * <span data-ttu-id="360c7-137">Выберите пакет в поле **Project SDK** (Пакет SDK проекта).</span><span class="sxs-lookup"><span data-stu-id="360c7-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="360c7-138">Нажмите кнопку New («Создать») и перейдите к каталогу установки Java. Обычно у него такой путь: `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="360c7-138">Click New and navigate to the Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="360c7-139">Установите флажок **Create from archetype** («Создать на основе архетипа»).</span><span class="sxs-lookup"><span data-stu-id="360c7-139">Select the **Create from archetype** option.</span></span>
   * <span data-ttu-id="360c7-140">В списке архетипов выберите **org.scala-tools.archetypes:scala-archetype-simple**.</span><span class="sxs-lookup"><span data-stu-id="360c7-140">From the list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="360c7-141">В результате будет создана структура каталога и скачаны зависимости по умолчанию, необходимые для написания программы Scala.</span><span class="sxs-lookup"><span data-stu-id="360c7-141">This will create the right directory structure and download the required default dependencies to write Scala program.</span></span>
2. <span data-ttu-id="360c7-142">Введите соответствующие значения для параметров **GroupId**, **ArtifactId** и **Version**.</span><span class="sxs-lookup"><span data-stu-id="360c7-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="360c7-143">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="360c7-143">Click **Next**.</span></span>
3. <span data-ttu-id="360c7-144">В следующем диалоговом окне, где нужно указать основной каталог Maven и другие пользовательские настройки, примите значения по умолчанию и нажмите кнопку **Next**(«Далее»).</span><span class="sxs-lookup"><span data-stu-id="360c7-144">In the next dialog box, where you specify Maven home directory and other user settings, accept the defaults and click **Next**.</span></span>
4. <span data-ttu-id="360c7-145">В последнем диалоговом окне укажите имя и расположение проекта, а затем нажмите кнопку **Finish**(«Готово»).</span><span class="sxs-lookup"><span data-stu-id="360c7-145">In the last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="360c7-146">Удалите файл **MySpec.Scala** с путем **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="360c7-146">Delete the **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="360c7-147">Его не нужно использовать для приложения.</span><span class="sxs-lookup"><span data-stu-id="360c7-147">You do not need this for the application.</span></span>
6. <span data-ttu-id="360c7-148">При необходимости переименуйте исходные файлы и файлы тестирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="360c7-148">If required, rename the default source and test files.</span></span> <span data-ttu-id="360c7-149">В левой области в IntelliJ IDEA перейдите по пути **src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="360c7-149">From the left pane in the IntelliJ IDEA, navigate to **src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="360c7-150">Щелкните правой кнопкой мыши **App.scala**, выберите пункт **Refactor** (Рефакторинг), щелкните Rename file (Переименовать файл), а затем в диалоговом окне укажите новое имя для приложения и нажмите кнопку **Refactor** (Выполнить рефакторинг).</span><span class="sxs-lookup"><span data-stu-id="360c7-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in the dialog box, provide the new name for the application and then click **Refactor**.</span></span>
   
    ![Переименование файлов](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="360c7-152">На следующих шагах описывается обновление файла pom.xml для определения зависимостей приложения Spark Scala.</span><span class="sxs-lookup"><span data-stu-id="360c7-152">In the subsequent steps, you will update the pom.xml to define the dependencies for the Spark Scala application.</span></span> <span data-ttu-id="360c7-153">Чтобы автоматически скачать эти зависимости и разрешить их, необходимо соответствующим образом настроить Maven.</span><span class="sxs-lookup"><span data-stu-id="360c7-153">For those dependencies to be downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Настройка автоматической загрузки Maven](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="360c7-155">В меню **File** (Файл) выберите пункт **Settings** (Настройки).</span><span class="sxs-lookup"><span data-stu-id="360c7-155">From the **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="360c7-156">В диалоговом окне **Settings** (Настройки) выберите **Build, Execution, Deployment**(Сборка, выполнение, развертывание) > **Build Tools**(Средства сборки) > **Maven** > **Importing** (Импорт).</span><span class="sxs-lookup"><span data-stu-id="360c7-156">In the **Settings** dialog box, navigate to **Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="360c7-157">Установите флажок **Import Maven projects automatically**(«Импортировать проекты Maven автоматически»).</span><span class="sxs-lookup"><span data-stu-id="360c7-157">Select the option to **Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="360c7-158">Нажмите кнопку **Применить**, а затем — **ОК**.</span><span class="sxs-lookup"><span data-stu-id="360c7-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="360c7-159">Обновите исходный файл Scala, чтобы включить его данные в код приложения.</span><span class="sxs-lookup"><span data-stu-id="360c7-159">Update the Scala source file to include your application code.</span></span> <span data-ttu-id="360c7-160">Откройте и замените существующий пример кода кодом ниже, а затем сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="360c7-160">Open and replace the existing sample code with the following code and save the changes.</span></span> <span data-ttu-id="360c7-161">Этот код считывает данные из файла HVAC.csv (доступного во всех кластерах HDInsight Spark), извлекает строки, которые содержат только одну цифру в шестом столбце, и записывает выходные данные в папку **/HVACOut** , которая находится в используемом по умолчанию контейнере хранилища кластера.</span><span class="sxs-lookup"><span data-stu-id="360c7-161">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the sixth column, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO to wasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows which have only one digit in the 7th column in the CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="360c7-162">Обновите файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="360c7-162">Update the pom.xml.</span></span>
   
   1. <span data-ttu-id="360c7-163">Добавьте следующий код в файл `<project>\<properties>`:</span><span class="sxs-lookup"><span data-stu-id="360c7-163">Within `<project>\<properties>` add the following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="360c7-164">Добавьте следующий код в файл `<project>\<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="360c7-164">Within `<project>\<dependencies>` add the following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="360c7-165">Сохраните изменения в файле pom.xml.</span><span class="sxs-lookup"><span data-stu-id="360c7-165">Save changes to pom.xml.</span></span>
10. <span data-ttu-id="360c7-166">Создайте JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="360c7-166">Create the .jar file.</span></span> <span data-ttu-id="360c7-167">IntelliJ IDEA позволяет создавать JAR-файлы в качестве артефактов проекта.</span><span class="sxs-lookup"><span data-stu-id="360c7-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="360c7-168">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="360c7-168">Perform the following steps.</span></span>
    
    1. <span data-ttu-id="360c7-169">В меню **File** (Файл) выберите пункт **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="360c7-169">From the **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="360c7-170">В диалоговом окне **Project Structure** (Структура проекта) выберите **Artifacts** (Артефакты) и щелкните знак плюса.</span><span class="sxs-lookup"><span data-stu-id="360c7-170">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="360c7-171">Во всплывающем диалоговом окне щелкните **JAR**, а затем выберите **From modules with dependencies** (На основе модулей с зависимостями).</span><span class="sxs-lookup"><span data-stu-id="360c7-171">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="360c7-173">В диалоговом окне **Create JAR from Modules** (Создание JAR-файла на основе модулей) нажмите кнопку с многоточием (![многоточие](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png)) возле пункта **Main Class** (Основной класс).</span><span class="sxs-lookup"><span data-stu-id="360c7-173">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against the **Main Class**.</span></span>
    4. <span data-ttu-id="360c7-174">В диалоговом окне **Select Main Class** (Выбор основного класса) выберите класс, который отображается по умолчанию, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="360c7-174">In the **Select Main Class** dialog box, select the class that appears by default and then click **OK**.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="360c7-176">В диалоговом окне **Create JAR from Modules** (Создание JAR-файла на основе модулей) установите переключатель **extract to the target JAR** (Извлечь в целевой JAR-файл) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="360c7-176">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="360c7-177">В результате будет создан один JAR-файл, содержащий все зависимости.</span><span class="sxs-lookup"><span data-stu-id="360c7-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="360c7-179">На вкладке "Макет выходных данных" содержится список всех JAR-файлов, которые включены в проект Maven.</span><span class="sxs-lookup"><span data-stu-id="360c7-179">The output layout tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="360c7-180">Здесь можно выбрать и удалить файлы, от которых не зависит работа приложения Scala.</span><span class="sxs-lookup"><span data-stu-id="360c7-180">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="360c7-181">Для создаваемого приложения можно удалить все файлы, кроме последнего (**SparkSimpleApp compile output**(«Выходные данные компиляции SparkSimpleApp»)).</span><span class="sxs-lookup"><span data-stu-id="360c7-181">For the application we are creating here, you can remove all but the last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="360c7-182">Выберите JAR-файлы, которые нужно удалить, и щелкните значок **Delete** («Удалить»).</span><span class="sxs-lookup"><span data-stu-id="360c7-182">Select the jars to delete and then click the **Delete** icon.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="360c7-184">Установите флажок **Build on make** («Сборка на основе созданного»), чтобы JAR-файл создавался при каждом создании и обновлении проекта.</span><span class="sxs-lookup"><span data-stu-id="360c7-184">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="360c7-185">Нажмите кнопку **Применить**, а затем — **ОК**.</span><span class="sxs-lookup"><span data-stu-id="360c7-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="360c7-186">В строке меню щелкните **Build** (Сборка) и выберите **Make Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="360c7-186">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="360c7-187">Кроме того, можно щелкнуть **Build Artifacts** («Сборка артефактов»), чтобы создать JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="360c7-187">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="360c7-188">Выходной JAR-файл будет создан в разделе **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="360c7-188">The output jar is created under **\out\artifacts**.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-the-application-on-the-spark-cluster"></a><span data-ttu-id="360c7-190">Запуск приложения в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="360c7-190">Run the application on the Spark cluster</span></span>
<span data-ttu-id="360c7-191">Чтобы запустить приложение в кластере, нужно выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="360c7-191">To run the application on the cluster, you must do the following:</span></span>

* <span data-ttu-id="360c7-192">**Скопируйте приложение JAR в большой двоичный объект службы хранилища Azure**, связанный с кластером.</span><span class="sxs-lookup"><span data-stu-id="360c7-192">**Copy the application jar to the Azure storage blob** associated with the cluster.</span></span> <span data-ttu-id="360c7-193">Вы можете использовать для этого служебную программу командной строки [**AzCopy**](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="360c7-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="360c7-194">Кроме того, для отправки данных можно использовать множество других клиентов.</span><span class="sxs-lookup"><span data-stu-id="360c7-194">There are a lot of other clients as well that you can use to upload data.</span></span> <span data-ttu-id="360c7-195">Дополнительные сведения о них см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="360c7-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="360c7-196">**Используйте Livy для удаленной отправки задания приложения** для кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="360c7-196">**Use Livy to submit an application job remotely** to the Spark cluster.</span></span> <span data-ttu-id="360c7-197">В кластерах HDInsight Spark есть сервер Livy, который использует конечные точки REST для удаленной отправки заданий Spark.</span><span class="sxs-lookup"><span data-stu-id="360c7-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints to remotely submit Spark jobs.</span></span> <span data-ttu-id="360c7-198">Дополнительные сведения см. в статье [Удаленная отправка заданий Spark в кластер Apache Spark в HDInsight на платформе Linux с помощью Livy](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="360c7-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="360c7-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="360c7-199">Next step</span></span>

<span data-ttu-id="360c7-200">В этой статье вы узнали, как создать приложение Spark Scala.</span><span class="sxs-lookup"><span data-stu-id="360c7-200">In this article you learned how to create a Spark scala application.</span></span> <span data-ttu-id="360c7-201">Из следующей статьи вы узнаете, как запустить это приложение на кластере HDInsight Spark, используя Livy.</span><span class="sxs-lookup"><span data-stu-id="360c7-201">Advance to the next article to learn how to run this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="360c7-202">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="360c7-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

