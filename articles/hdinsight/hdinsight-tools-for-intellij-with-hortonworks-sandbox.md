---
title: "Использование набора средств Azure для IntelliJ с песочницей Hortonworks | Документация Майкрософт"
description: "Узнайте, как использовать инструменты HDInsight в наборе средств Azure для IntelliJ с песочницей Hortonworks."
keywords: "инструменты hadoop,запрос hive,intellij,песочница hortonworks,набор средств azure для intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c49f185db5a035f70a711bf309b973182d94a2b0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="b9634-104">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="b9634-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="b9634-105">Узнайте, как использовать инструменты HDInsight для IntelliJ при разработке приложений Apache Scala и их тестировании в [песочнице Hortonworks](http://hortonworks.com/products/sandbox/), запущенной на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="b9634-105">Learn how to use HDInsight Tools for IntelliJ to develop Apache Scala applications and then test the applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="b9634-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) — это интегрированная среда разработки (IDE) Java для разработки программного обеспечения для компьютеров.</span><span class="sxs-lookup"><span data-stu-id="b9634-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="b9634-107">После разработки и тестирования приложений в песочнице Hortonworks их можно переместить в [Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9634-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them to [Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9634-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b9634-108">Prerequisites</span></span>

<span data-ttu-id="b9634-109">Для работы с этим руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b9634-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="b9634-110">Платформа данных Hortonworks Data Platform 2.4 (HDP) в песочнице Hortonworks, выполняемая в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="b9634-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="b9634-111">Сведения о настройке см. в статье [Начало работы с песочницей Hadoop, эмулятором на виртуальной машине](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9634-111">To configure HDP, see [Get started in the Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="b9634-112">Средства HDInsight для IntelliJ были протестированы только с HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="b9634-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="b9634-113">Чтобы получить HDP 2.4, разверните **архив песочницы Hortonworks** на [сайте скачивания песочницы Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="b9634-113">To get HDP 2.4, expand **Hortonworks Sandbox Archive** on the [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="b9634-114">[Java Developer Kit (JDK) версии 1.8 или более поздней версии](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="b9634-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="b9634-115">JDK необходим для набора средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b9634-115">JDK is required by the Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="b9634-116">[Выпуск IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download) с подключаемым модулем [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) и подключаемым модулем [Набор средств Azure для IntelliJ](../azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="b9634-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with the [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and the [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="b9634-117">Средства HDInsight для IntelliJ доступны в составе набора средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b9634-117">HDInsight Tools for IntelliJ is available as a part of the Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="b9634-118">Чтобы установить подключаемые модули, выполните такие действия:</span><span class="sxs-lookup"><span data-stu-id="b9634-118">To install the plug-ins, do the following:</span></span>

  1. <span data-ttu-id="b9634-119">Откройте IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b9634-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="b9634-120">На экране **Welcome** (Добро пожаловать) выберите **Configure** (Настройка), а затем **Plugins** (Подключаемые модули).</span><span class="sxs-lookup"><span data-stu-id="b9634-120">On the **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="b9634-121">Выберите **Install JetBrains plugin** (Установить подключаемый модуль JetBrains) в левом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="b9634-121">Select **Install JetBrains plugin** in the lower-left corner.</span></span>
  4. <span data-ttu-id="b9634-122">Используйте функцию поиска, чтобы найти **Scala**, а затем выберите **Install** (Установить).</span><span class="sxs-lookup"><span data-stu-id="b9634-122">Use the search function to search for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="b9634-123">Чтобы завершить установку, щелкните **Restart IntelliJ IDEA** (Перезапустить IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="b9634-123">Select **Restart IntelliJ IDEA** to complete the installation.</span></span>
  6. <span data-ttu-id="b9634-124">Чтобы установить **набор средств Azure для IntelliJ**, повторите шаги 4 и 5.</span><span class="sxs-lookup"><span data-stu-id="b9634-124">Repeat step 4 and 5 to install the **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="b9634-125">Дополнительные сведения см. в статье [Установка набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="b9634-125">For more information, see [Install the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="b9634-126">Создание приложения Spark Scala</span><span class="sxs-lookup"><span data-stu-id="b9634-126">Create a Spark Scala application</span></span>

<span data-ttu-id="b9634-127">В этом разделе с помощью IntelliJ IDEA создается пример проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="b9634-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="b9634-128">В следующем разделе IntelliJ IDEA связывается с песочницей Hortonworks (эмулятором) до отправки проекта.</span><span class="sxs-lookup"><span data-stu-id="b9634-128">In the next section, you link IntelliJ IDEA to the Hortonworks Sandbox (emulator) before you submit the project.</span></span>

1. <span data-ttu-id="b9634-129">Откройте IntelliJ IDEA со своей рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="b9634-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="b9634-130">В диалоговом окне **Новый проект** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b9634-130">In the **New Project** dialog box, do the following:</span></span>

   <span data-ttu-id="b9634-131">а.</span><span class="sxs-lookup"><span data-stu-id="b9634-131">a.</span></span> <span data-ttu-id="b9634-132">Выберите **HDInsight** > **Spark on HDInsight (Scala)** (Spark в HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="b9634-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="b9634-133">b.</span><span class="sxs-lookup"><span data-stu-id="b9634-133">b.</span></span> <span data-ttu-id="b9634-134">В списке **средств сборки** выберите один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="b9634-134">In the **Build tool** list, select either of the following, according to your need:</span></span>

    * <span data-ttu-id="b9634-135">**Maven.** Для поддержки мастера создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="b9634-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="b9634-136">**SBT.** Для управления зависимостями и создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="b9634-136">**SBT**, for managing the dependencies and building for the Scala project</span></span>

   ![Диалоговое окно нового проекта](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="b9634-138">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b9634-138">Select **Next**.</span></span>

3. <span data-ttu-id="b9634-139">В диалоговом окне **New Project** (Новый проект) сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b9634-139">In the next **New Project** dialog box, do the following:</span></span>

    ![Создание свойств проекта IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="b9634-141">а.</span><span class="sxs-lookup"><span data-stu-id="b9634-141">a.</span></span> <span data-ttu-id="b9634-142">В поле **Project name** (Имя проекта) введите имя проекта.</span><span class="sxs-lookup"><span data-stu-id="b9634-142">In the **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="b9634-143">b.</span><span class="sxs-lookup"><span data-stu-id="b9634-143">b.</span></span> <span data-ttu-id="b9634-144">В поле **Project location** (Расположение проекта) введите расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="b9634-144">In the **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="b9634-145">c.</span><span class="sxs-lookup"><span data-stu-id="b9634-145">c.</span></span> <span data-ttu-id="b9634-146">Рядом с раскрывающимся списком **Project SDK** (Пакет SDK проекта) выберите **New** (Создать), а затем **JDK** и укажите папку пакета Java JDK версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="b9634-146">Next to the **Project SDK** drop-down list, select **New**, select **JDK**, and then specify the folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="b9634-147">Выберите **Java 1.8** для кластера Spark 2.x или **Java 1.7** для кластера Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="b9634-147">Select **Java 1.8** for the Spark 2.x cluster, or select **Java 1.7** for the Spark 1.x cluster.</span></span> <span data-ttu-id="b9634-148">Расположение по умолчанию: C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="b9634-148">The default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="b9634-149">d.</span><span class="sxs-lookup"><span data-stu-id="b9634-149">d.</span></span> <span data-ttu-id="b9634-150">В раскрывающемся списке для параметра **Spark version** (Версия Spark) мастер создания проекта Scala интегрирует правильную версию пакета SDK для Spark и пакета SDK для Scala.</span><span class="sxs-lookup"><span data-stu-id="b9634-150">In the **Spark version** drop-down list, Scala project creation wizard integrates the proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="b9634-151">Если версия кластера Spark ниже 2.0, выберите **Spark 1.x**.</span><span class="sxs-lookup"><span data-stu-id="b9634-151">If the Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="b9634-152">В противном случае выберите **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="b9634-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="b9634-153">В этом примере используется Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="b9634-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="b9634-154">Убедитесь, что используется репозиторий, помеченный Scala 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="b9634-154">Make sure that you are using the repository marked Scala 2.10.x.</span></span> <span data-ttu-id="b9634-155">Не используйте репозиторий, помеченный Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="b9634-155">Do not use the repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="b9634-156">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b9634-156">Select **Finish**.</span></span>

5. <span data-ttu-id="b9634-157">Если представление **Project** (Проект) еще не открыто, нажмите клавиши **ALT+1**, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="b9634-157">If the **Project** view is not already open, press **Alt+1** to open it.</span></span>

6. <span data-ttu-id="b9634-158">В **обозревателе проектов** разверните проект и выберите **src**.</span><span class="sxs-lookup"><span data-stu-id="b9634-158">In **Project Explorer**, expand the project, and then select **src**.</span></span>

7. <span data-ttu-id="b9634-159">Щелкните правой кнопкой мыши **src**, наведите указатель мыши на пункт **New** (Создать), а затем щелкните **Scala Class** (Класс Scala).</span><span class="sxs-lookup"><span data-stu-id="b9634-159">Right-click **src**, point to **New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="b9634-160">В поле **Name** (Имя) введите имя, а в поле **Kind** (Тип) выберите **Object** (Объект), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b9634-160">In the **Name** box, enter a name, in the **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![Окно создания нового класса Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="b9634-162">Скопируйте приведенный ниже код и вставьте его в файл с расширением SCALA.</span><span class="sxs-lookup"><span data-stu-id="b9634-162">In the .scala file, paste the following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="b9634-163">В меню **Build** (Сборка) выберите **Build project** (Собрать проект).</span><span class="sxs-lookup"><span data-stu-id="b9634-163">On the **Build** menu, select **Build project**.</span></span> <span data-ttu-id="b9634-164">Убедитесь, что компиляция завершилась успешно.</span><span class="sxs-lookup"><span data-stu-id="b9634-164">Make sure that the compilation has been completed successfully.</span></span>


## <a name="link-to-the-hortonworks-sandbox"></a><span data-ttu-id="b9634-165">Связь с песочницей HortonWorks</span><span class="sxs-lookup"><span data-stu-id="b9634-165">Link to the Hortonworks Sandbox</span></span>

<span data-ttu-id="b9634-166">Прежде чем устанавливать связь с песочницей Hortonworks (эмулятором), необходимо иметь приложение IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b9634-166">Before you can link to a Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="b9634-167">Чтобы установить связь с эмулятором, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="b9634-167">To link to an emulator, do the following:</span></span>

1. <span data-ttu-id="b9634-168">Откройте проект в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b9634-168">Open the project in IntelliJ.</span></span>

2. <span data-ttu-id="b9634-169">В меню **View** (Вид) выберите **Tool Windows** (Окна инструментов) и выберите **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b9634-169">On the **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="b9634-170">Разверните **Azure**, щелкните правой кнопкой мыши **HDInsight**, а затем выберите **Link an Emulator** (Установить связь с эмулятором).</span><span class="sxs-lookup"><span data-stu-id="b9634-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="b9634-171">В окне **Link A New Emulator** (Установить связь с новым эмулятором) введите пароль, который был настроен для учетной записи привилегированного пользователя песочницы Hortonworks, введите значения, аналогичные приведенным на следующем снимке экрана, а затем нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9634-171">In the **Link A New Emulator** window, enter the password that you've configured for the root account of the Hortonworks Sandbox, enter values similar to those in the following screenshot, and then select **OK**.</span></span> 

   ![Окно Link a New Emulator (Установить связь с новым эмулятором)](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="b9634-173">Чтобы настроить эмулятор, выберите **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="b9634-173">To configure the emulator, select **Yes**.</span></span>

<span data-ttu-id="b9634-174">При успешном подключении эмулятор (песочница Hortonworks) будет внесен в узел HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9634-174">When the emulator is connected successfully, the emulator (Hortonworks Sandbox) is listed in the HDInsight node.</span></span>

## <a name="submit-the-spark-scala-application-to-the-hortonworks-sandbox"></a><span data-ttu-id="b9634-175">Отправка приложения Spark Scala в песочницу Hortonworks</span><span class="sxs-lookup"><span data-stu-id="b9634-175">Submit the Spark Scala application to the Hortonworks Sandbox</span></span>

<span data-ttu-id="b9634-176">Когда среда IntelliJ IDEA связана с эмулятором, можно отправить проект.</span><span class="sxs-lookup"><span data-stu-id="b9634-176">After you have linked IntelliJ IDEA to the emulator, you can submit your project.</span></span>

<span data-ttu-id="b9634-177">Чтобы отправить проект на эмулятор, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="b9634-177">To submit a project to an emulator, do the following:</span></span>

1. <span data-ttu-id="b9634-178">В **обозревателе проектов** щелкните проект правой кнопкой мыши и выберите **Submit Spark Application to HDInsight** (Отправить приложение Spark в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="b9634-178">In **Project Explorer**, right-click the project, and then select **Submit Spark application to HDInsight**.</span></span>

2. <span data-ttu-id="b9634-179">Выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="b9634-179">Do the following:</span></span>

    <span data-ttu-id="b9634-180">а.</span><span class="sxs-lookup"><span data-stu-id="b9634-180">a.</span></span> <span data-ttu-id="b9634-181">В раскрывающемся списке **Spark cluster (Linux only)** (Кластер Spark (только для Linux)) выберите локальную песочницу Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="b9634-181">In the **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="b9634-182">b.</span><span class="sxs-lookup"><span data-stu-id="b9634-182">b.</span></span> <span data-ttu-id="b9634-183">В поле **Main class name** (Имя класса Main) введите имя класса Main.</span><span class="sxs-lookup"><span data-stu-id="b9634-183">In the **Main class name** box, choose or enter the main class name.</span></span> <span data-ttu-id="b9634-184">В этом руководстве имя — **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="b9634-184">For this tutorial, the name is **GroupByTest**.</span></span>

3. <span data-ttu-id="b9634-185">Нажмите кнопку **Submit** (Отправить).</span><span class="sxs-lookup"><span data-stu-id="b9634-185">Select **Submit**.</span></span> <span data-ttu-id="b9634-186">Журналы отправки заданий отображаются в окне инструмента отправки Spark.</span><span class="sxs-lookup"><span data-stu-id="b9634-186">The job submission logs are shown in the Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9634-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9634-187">Next steps</span></span>

- <span data-ttu-id="b9634-188">Сведения о создании приложений Spark для HDInsight с помощью инструментов HDInsight для IntelliJ см. в статье [Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="b9634-188">To learn how to create Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to create Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="b9634-189">Просмотрите видеоролик [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c) (Вводные сведения об инструментах HDInsight для IntelliJ для разработки Spark).</span><span class="sxs-lookup"><span data-stu-id="b9634-189">To watch a video of HDInsight Tools for IntelliJ, go to [Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="b9634-190">Сведения об удаленной отладке приложений Spark в HDInsight по протоколу SSH см. в статье [Удаленная отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="b9634-190">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through SSH, go to [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="b9634-191">Сведения об удаленной отладке приложений Spark через VPN с помощью набора средств в HDInsight см. в статье [Удаленная отладка приложений в HDInsight Spark через VPN с помощью набора средств Azure для IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="b9634-191">To learn how to debug Spark applications by using the toolkit remotely on HDInsight through VPN, go to [Use HDInsight Tools in Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="b9634-192">Сведения об использовании средств HDInsight для Eclipse для создания приложений Spark см. в статье [Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="b9634-192">To learn how to use HDInsight Tools for Eclipse to create a Spark application, go to [Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="b9634-193">Просмотрите видеоролик [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha) (Использование средств HDInsight для Eclipse для создания приложений Spark).</span><span class="sxs-lookup"><span data-stu-id="b9634-193">To watch a video of HDInsight Tools for Eclipse, go to [Use HDInsight Tool for Eclipse to create Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
