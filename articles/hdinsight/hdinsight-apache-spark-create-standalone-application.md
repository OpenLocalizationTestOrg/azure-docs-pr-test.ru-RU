---
title: "toorun приложения Scala aaaCreate в кластерах Spark - Azure HDInsight | Документы Microsoft"
description: "Создайте приложение Spark языке Scala с помощью Apache Maven как hello построения системы и существующие архетипа Maven для Scala, предоставляемые IntelliJ ИДЕЯ."
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
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="21f71-103">Создание приложения Scala Maven toorun на кластере Apache Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="21f71-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="21f71-104">Узнайте, как toocreate Spark приложения, написанного на Scala использование Maven с IntelliJ ИДЕЯ.</span><span class="sxs-lookup"><span data-stu-id="21f71-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="21f71-105">статья Hello использует Apache Maven как hello системы сборки и начинается с существующие архетипа Maven для Scala, предоставляемые IntelliJ ИДЕЯ.</span><span class="sxs-lookup"><span data-stu-id="21f71-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="21f71-106">Создание приложения Scala в IntelliJ ИДЕЯ состоит hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="21f71-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="21f71-107">Используйте Maven как система сборки hello.</span><span class="sxs-lookup"><span data-stu-id="21f71-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="21f71-108">Обновление зависимостей модуля Spark tooresolve файла модели объекта проекта (POM).</span><span class="sxs-lookup"><span data-stu-id="21f71-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="21f71-109">написание приложения на языке Scala;</span><span class="sxs-lookup"><span data-stu-id="21f71-109">Write your application in Scala.</span></span>
* <span data-ttu-id="21f71-110">Создания файла JAR-файл, который может быть отправленной tooHDInsight Spark кластеров.</span><span class="sxs-lookup"><span data-stu-id="21f71-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="21f71-111">Запустите приложение hello на кластере Spark с помощью Livy.</span><span class="sxs-lookup"><span data-stu-id="21f71-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="21f71-112">HDInsight также предоставляет IntelliJ ИДЕЯ подключаемого модуля средства tooease hello процесс создания и отправки приложения tooan кластера Spark на HDInsight в Linux.</span><span class="sxs-lookup"><span data-stu-id="21f71-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="21f71-113">Дополнительные сведения см. в разделе [использование подключаемого модуля средства HDInsight для toocreate IntelliJ ИДЕЯ и отправки приложения Spark](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="21f71-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="21f71-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="21f71-114">Prerequisites</span></span>

* <span data-ttu-id="21f71-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="21f71-115">An Azure subscription.</span></span> <span data-ttu-id="21f71-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="21f71-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="21f71-117">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21f71-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="21f71-118">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="21f71-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="21f71-119">Комплект разработчика Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="21f71-119">Oracle Java Development kit.</span></span> <span data-ttu-id="21f71-120">Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="21f71-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="21f71-121">Java IDE.</span><span class="sxs-lookup"><span data-stu-id="21f71-121">A Java IDE.</span></span> <span data-ttu-id="21f71-122">В этой статье используется среда IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="21f71-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="21f71-123">Его можно установить [отсюда](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="21f71-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="21f71-124">Установка подключаемого модуля Scala для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="21f71-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="21f71-125">Если ПРЕДСТАВЛЕНИЕ IntelliJ установки была не запрашивает Включение Scala подключаемого модуля, запустите IntelliJ ИДЕЯ и выполните следующие шаги tooinstall hello, подключаемый модуль hello:</span><span class="sxs-lookup"><span data-stu-id="21f71-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="21f71-126">Запустите IntelliJ IDEA и на экране приветствия щелкните **Configure** (Настройка), а затем — **Plugins** (Подключаемые модули).</span><span class="sxs-lookup"><span data-stu-id="21f71-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Включение подключаемого модуля Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="21f71-128">В следующем экране приветствия щелкните **JetBrains установить подключаемый модуль** в левом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="21f71-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="21f71-129">В hello **Обзор подключаемых модулей JetBrains** диалоговым окном, которое открывается, поиск Scala и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="21f71-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Установка подключаемого модуля Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="21f71-131">После успешной установки подключаемого модуля hello щелкните hello **кнопкой перезапустить ИДЕЯ IntelliJ** toorestart hello интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="21f71-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="21f71-132">Создание автономного проекта Scala</span><span class="sxs-lookup"><span data-stu-id="21f71-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="21f71-133">Запустите IntelliJ IDEA и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="21f71-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="21f71-134">В hello нового диалогового окна, сделайте hello следующие варианты, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="21f71-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Создание проекта Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="21f71-136">Выберите **Maven** hello тип проекта.</span><span class="sxs-lookup"><span data-stu-id="21f71-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="21f71-137">Выберите пакет в поле **Project SDK** (Пакет SDK проекта).</span><span class="sxs-lookup"><span data-stu-id="21f71-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="21f71-138">Нажмите кнопку Создать и перейдите в каталог установки Java toohello, обычно `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="21f71-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="21f71-139">Выберите hello **из архетипа** параметр.</span><span class="sxs-lookup"><span data-stu-id="21f71-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="21f71-140">Список archetypes hello, выберите **org.scala tools.archetypes:scala архетипа простой**.</span><span class="sxs-lookup"><span data-stu-id="21f71-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="21f71-141">Будет создан структура каталога hello и загрузите программу Scala toowrite зависимостей по умолчанию hello требуется.</span><span class="sxs-lookup"><span data-stu-id="21f71-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="21f71-142">Введите соответствующие значения для параметров **GroupId**, **ArtifactId** и **Version**.</span><span class="sxs-lookup"><span data-stu-id="21f71-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="21f71-143">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="21f71-143">Click **Next**.</span></span>
3. <span data-ttu-id="21f71-144">В hello Далее диалоговое окно, где указываются домашний каталог Maven и другие пользовательские настройки, примите значения по умолчанию hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="21f71-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="21f71-145">В последней диалоговое окно «hello», укажите имя и расположение проекта и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="21f71-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="21f71-146">Удалить hello **MySpec.Scala** файл **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="21f71-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="21f71-147">Это не требуется для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="21f71-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="21f71-148">При необходимости переименуйте файлов исходного кода и тестирования по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="21f71-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="21f71-149">Hello левой панели hello IntelliJ ПРЕДСТАВЛЕНИЕ, перейти слишком**src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="21f71-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="21f71-150">Щелкните правой кнопкой мыши **App.scala**, нажмите кнопку **рефакторинг**, щелкните переименовать файл и в диалоговом окне приветствия предоставляют hello новое имя для приложения hello и нажмите кнопку **рефакторинг**.</span><span class="sxs-lookup"><span data-stu-id="21f71-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![Переименование файлов](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="21f71-152">В последующих шагах hello обновит hello pom.xml toodefine hello зависимости для hello Spark Scala приложения.</span><span class="sxs-lookup"><span data-stu-id="21f71-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="21f71-153">Для этих зависимостей toobe загружаются и разрешить автоматически, необходимо соответствующим образом настроить Maven.</span><span class="sxs-lookup"><span data-stu-id="21f71-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Настройка автоматической загрузки Maven](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="21f71-155">Из hello **файл** меню, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="21f71-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="21f71-156">В hello **параметры** диалоговом окне перейдите слишком**, выполнение построения, развертывания** > **средства построения** > **Maven**  >  **Импорта**.</span><span class="sxs-lookup"><span data-stu-id="21f71-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="21f71-157">Выберите параметр hello слишком**Maven импорта проектов автоматически**.</span><span class="sxs-lookup"><span data-stu-id="21f71-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="21f71-158">Нажмите кнопку **Применить**, а затем — **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21f71-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="21f71-159">Обновите исходный файл hello Scala tooinclude код вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="21f71-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="21f71-160">Откройте и замените существующий образец кода с hello после кода hello и сохранить изменения hello.</span><span class="sxs-lookup"><span data-stu-id="21f71-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="21f71-161">Этот код считывает данные hello из hello HVAC.csv (доступно на всех кластерах HDInsight Spark), извлекает hello строки, которые имеют только одну цифру шестому столбцу hello и записывает выходные данные hello слишком**/HVACOut** в группе хранения по умолчанию hello контейнер для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="21f71-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="21f71-162">Обновите hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="21f71-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="21f71-163">В пределах `<project>\<properties>` добавьте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="21f71-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="21f71-164">В пределах `<project>\<dependencies>` добавьте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="21f71-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="21f71-165">Сохраните изменения toopom.xml.</span><span class="sxs-lookup"><span data-stu-id="21f71-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="21f71-166">Создайте hello JAR-файлу.</span><span class="sxs-lookup"><span data-stu-id="21f71-166">Create hello .jar file.</span></span> <span data-ttu-id="21f71-167">IntelliJ IDEA позволяет создавать JAR-файлы в качестве артефактов проекта.</span><span class="sxs-lookup"><span data-stu-id="21f71-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="21f71-168">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="21f71-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="21f71-169">Из hello **файл** меню, нажмите кнопку **структура проекта**.</span><span class="sxs-lookup"><span data-stu-id="21f71-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="21f71-170">В hello **структура проекта** диалоговое окно, нажмите кнопку **артефакты** и нажмите кнопку hello, а также символ.</span><span class="sxs-lookup"><span data-stu-id="21f71-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="21f71-171">Hello всплывающее диалоговое окно, щелкните **JAR**, а затем нажмите кнопку **из модулей с зависимостями**.</span><span class="sxs-lookup"><span data-stu-id="21f71-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="21f71-173">В hello **создать JAR из модулей** диалоговое окно, нажмите кнопку с многоточием hello (![многоточие](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) от hello **класс Main**.</span><span class="sxs-lookup"><span data-stu-id="21f71-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="21f71-174">В hello **выберите класс Main** диалоговое окно, выберите hello класс, который отображается по умолчанию и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21f71-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="21f71-176">В hello **создать JAR из модулей** диалогового окна поле, убедитесь, что этот параметр hello слишком**извлечения целевого toohello JAR** выбран и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21f71-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="21f71-177">В результате будет создан один JAR-файл, содержащий все зависимости.</span><span class="sxs-lookup"><span data-stu-id="21f71-177">This creates a single JAR with all dependencies.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="21f71-179">Hello вывода макета вкладке перечисляются все hello файлов, которые включены в состав проекта Maven hello.</span><span class="sxs-lookup"><span data-stu-id="21f71-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="21f71-180">Можно выбрать и удалить hello, на которой другие hello Scala приложения имеет нет прямой зависимости.</span><span class="sxs-lookup"><span data-stu-id="21f71-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="21f71-181">Для приложения hello, мы создаем здесь, можно удалить все, кроме hello последним (**SparkSimpleApp компиляции выходной**).</span><span class="sxs-lookup"><span data-stu-id="21f71-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="21f71-182">Выберите toodelete hello JAR-файлов и нажмите кнопку hello **удалить** значок.</span><span class="sxs-lookup"><span data-stu-id="21f71-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="21f71-184">Убедитесь, что **сборки в проверьте** флажок, который гарантирует, что jar hello создаются каждый раз, hello проекта будут созданы или обновлены.</span><span class="sxs-lookup"><span data-stu-id="21f71-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="21f71-185">Нажмите кнопку **Применить**, а затем — **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21f71-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="21f71-186">На панели меню hello, нажмите кнопку **построения**и нажмите кнопку **сделать проект**.</span><span class="sxs-lookup"><span data-stu-id="21f71-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="21f71-187">Можно также щелкнуть **артефакты сборки** toocreate hello jar.</span><span class="sxs-lookup"><span data-stu-id="21f71-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="21f71-188">Hello JAR-выходной файл будет создан в разделе **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="21f71-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="21f71-190">Запустите приложение hello на кластере Spark hello</span><span class="sxs-lookup"><span data-stu-id="21f71-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="21f71-191">приложение hello toorun hello кластере, необходимо выполнить следующие hello:</span><span class="sxs-lookup"><span data-stu-id="21f71-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="21f71-192">**Копирования hello приложения jar toohello хранилища Azure BLOB-объекта** связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="21f71-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="21f71-193">Можно использовать [ **AzCopy**](../storage/common/storage-use-azcopy.md), Командная строка программы, toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="21f71-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="21f71-194">Существует много других клиентов также можно использовать tooupload данных.</span><span class="sxs-lookup"><span data-stu-id="21f71-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="21f71-195">Дополнительные сведения о них см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="21f71-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="21f71-196">**Удаленно использовать Livy toosubmit задание приложения** toohello кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="21f71-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="21f71-197">Кластеры Spark на HDInsight включает Livy, предоставляющую отправить tooremotely конечные точки REST Spark заданий.</span><span class="sxs-lookup"><span data-stu-id="21f71-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="21f71-198">Дополнительные сведения см. в статье [Удаленная отправка заданий Spark в кластер Apache Spark в HDInsight на платформе Linux с помощью Livy](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="21f71-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="21f71-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21f71-199">Next step</span></span>

<span data-ttu-id="21f71-200">В этой статье вы узнали, каким образом toocreate приложении scala Spark.</span><span class="sxs-lookup"><span data-stu-id="21f71-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="21f71-201">Предварительное toohello далее в статье toolearn как toorun кластера с помощью Livy этого приложения на HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="21f71-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="21f71-202">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="21f71-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

