---
title: "набор средств Azure для IntelliJ с песочницей Hortonworks aaaUse | Документы Microsoft"
description: "Дополнительные сведения о том, как toouse HDInsight средства в набор средств Azure для IntelliJ с Hortonworks \"песочницы\"."
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
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="1d4f7-104">Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks</span><span class="sxs-lookup"><span data-stu-id="1d4f7-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="1d4f7-105">Узнайте, как toouse средства HDInsight для приложений Apache Scala toodevelop IntelliJ и проверки hello приложений на [Hortonworks "песочницы"](http://hortonworks.com/products/sandbox/) на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="1d4f7-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) — это интегрированная среда разработки (IDE) Java для разработки программного обеспечения для компьютеров.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="1d4f7-107">После разработки и тестирования приложения в "песочнице" Hortonworks, вы можете переместить их слишком[Azure HDInsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d4f7-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1d4f7-108">Prerequisites</span></span>

<span data-ttu-id="1d4f7-109">Для работы с этим руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="1d4f7-110">Платформа данных Hortonworks Data Platform 2.4 (HDP) в песочнице Hortonworks, выполняемая в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="1d4f7-111">в разделе tooconfigure HDP, [приступить к работе в экосистеме hello Hadoop с изолированной среде Hadoop на виртуальной машине](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="1d4f7-112">Средства HDInsight для IntelliJ были протестированы только с HDP 2.4.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="1d4f7-113">Разверните tooget HDP 2.4 **Hortonworks "песочницы" архив** на hello [сайта загрузки для "песочницы" Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="1d4f7-114">[Java Developer Kit (JDK) версии 1.8 или более поздней версии](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="1d4f7-115">JDK требуется hello Azure Toolkit для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="1d4f7-116">[ИДЕЯ IntelliJ community edition](https://www.jetbrains.com/idea/download) с hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) подключаемого модуля и hello [средств Azure для IntelliJ](../azure-toolkit-for-intellij.md) подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="1d4f7-117">Средства HDInsight для IntelliJ доступен как часть средств Azure для IntelliJ hello.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="1d4f7-118">tooinstall hello подключаемые модули, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="1d4f7-119">Откройте IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="1d4f7-120">На hello **приветствия** выберите **Настройка**, а затем выберите **подключаемых модулей**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="1d4f7-121">Выберите **JetBrains установить подключаемый модуль** в левом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="1d4f7-122">Использовать hello toosearch функции поиска для **Scala**, а затем выберите **установить**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="1d4f7-123">Выберите **перезапустите ИДЕЯ IntelliJ** toocomplete hello установки.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="1d4f7-124">Повторите шаг 4 и 5 hello tooinstall **средств Azure для IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="1d4f7-125">Дополнительные сведения см. в разделе [hello установки набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="1d4f7-126">Создание приложения Spark Scala</span><span class="sxs-lookup"><span data-stu-id="1d4f7-126">Create a Spark Scala application</span></span>

<span data-ttu-id="1d4f7-127">В этом разделе с помощью IntelliJ IDEA создается пример проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="1d4f7-128">В следующем разделе hello свяжите ИДЕЯ IntelliJ toohello Hortonworks "песочницы" (эмулятора) перед отправкой hello проекта.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="1d4f7-129">Откройте IntelliJ IDEA со своей рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="1d4f7-130">В hello **новый проект** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="1d4f7-131">а.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-131">a.</span></span> <span data-ttu-id="1d4f7-132">Выберите **HDInsight** > **Spark on HDInsight (Scala)** (Spark в HDInsight (Scala)).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="1d4f7-133">b.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-133">b.</span></span> <span data-ttu-id="1d4f7-134">В hello **инструмент сборки** выберите либо hello следующие, tooyour потребность в соответствии с:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="1d4f7-135">**Maven.** Для поддержки мастера создания проекта Scala.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="1d4f7-136">**SBT**, для управления зависимостями hello и построения для проекта Scala hello</span><span class="sxs-lookup"><span data-stu-id="1d4f7-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![диалоговое окно нового проекта Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="1d4f7-138">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-138">Select **Next**.</span></span>

3. <span data-ttu-id="1d4f7-139">В hello Далее **новый проект** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![Создание свойств проекта IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="1d4f7-141">а.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-141">a.</span></span> <span data-ttu-id="1d4f7-142">В hello **имя проекта** введите имя проекта.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="1d4f7-143">b.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-143">b.</span></span> <span data-ttu-id="1d4f7-144">В hello **расположение проекта** введите расположение проекта.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="1d4f7-145">c.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-145">c.</span></span> <span data-ttu-id="1d4f7-146">Далее toohello **проекта SDK** раскрывающемся списке выберите **New**выберите **JDK**, и укажите папку hello Java JDK версии 1.7 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="1d4f7-147">Выберите **Java 1.8** для кластера 2.x Spark hello, или выберите **Java 1.7** для hello Spark 1.x кластера.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="1d4f7-148">расположение по умолчанию Hello — C:\Program Files\Java\jdk1.8.x_xxx.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="1d4f7-149">d.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-149">d.</span></span> <span data-ttu-id="1d4f7-150">В hello **версии Spark** раскрывающегося списка, мастер создания проекта Scala интегрируется hello правильной версии пакета SDK Spark и Scala SDK.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="1d4f7-151">Если версия кластера Spark hello является более ранней, чем 2.0, выберите **усилить 1.x**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="1d4f7-152">В противном случае выберите **Spark 2.x**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="1d4f7-153">В этом примере используется Spark 1.6.2 (Scala 2.10.5).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="1d4f7-154">Убедитесь, что вы используете помечен Scala репозитория hello 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="1d4f7-155">Не используйте репозиторий hello помечен Scala 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="1d4f7-156">Выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-156">Select **Finish**.</span></span>

5. <span data-ttu-id="1d4f7-157">Если hello **проекта** представление еще не открыта, нажмите клавишу **Alt + 1** tooopen его.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="1d4f7-158">В **обозревателя проектов**, разверните проект hello и выберите **src**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="1d4f7-159">Щелкните правой кнопкой мыши **src**, слишком точки**New**и выберите **Scala класса**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="1d4f7-160">В hello **имя** введите имя в hello **тип** выберите **объекта**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![Создайте новый класс Scala окна Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="1d4f7-162">В файле .scala hello вставьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-162">In hello .scala file, paste hello following code:</span></span>

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

10. <span data-ttu-id="1d4f7-163">На hello **построения** последовательно выберите пункты **построения проекта**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="1d4f7-164">Убедитесь, что успешно завершена hello компиляции.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="1d4f7-165">Связать "песочницы" Hortonworks toohello</span><span class="sxs-lookup"><span data-stu-id="1d4f7-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="1d4f7-166">Прежде чем связывать tooa Hortonworks "песочницы" (эмулятора), необходимо иметь приложение IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="1d4f7-167">Эмулятор tooan toolink, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="1d4f7-168">Привет открыть проект в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="1d4f7-169">На hello **представление** выберите пункт **средства Windows**, а затем выберите **обозреватель Azure**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="1d4f7-170">Разверните **Azure**, щелкните правой кнопкой мыши **HDInsight**, а затем выберите **Link an Emulator** (Установить связь с эмулятором).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="1d4f7-171">В hello **новый эмулятор ссылку** окно, введите пароль hello, настроенных для учетной записи корневой hello hello Hortonworks "песочницы", введите примерно toothose значения в следующий снимок экрана приветствия и выберите **ОК** .</span><span class="sxs-lookup"><span data-stu-id="1d4f7-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![окна «Связи новый эмулятор» Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="1d4f7-173">Эмулятор hello tooconfigure, выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="1d4f7-174">Если подключения эмулятора hello hello эмулятор (Hortonworks "песочницы") отображается в узел HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="1d4f7-175">Отправить toohello приложения hello Spark Scala Hortonworks "песочницы"</span><span class="sxs-lookup"><span data-stu-id="1d4f7-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="1d4f7-176">После связывания IntelliJ ИДЕЯ toohello эмулятора, вы можете отправить проекта.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="1d4f7-177">toosubmit симулятор tooan проекта hello следующие:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="1d4f7-178">В **обозревателя проектов**, щелкните правой кнопкой мыши проект hello и выберите **tooHDInsight приложения отправить Spark**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="1d4f7-179">Здравствуйте, следующие:</span><span class="sxs-lookup"><span data-stu-id="1d4f7-179">Do hello following:</span></span>

    <span data-ttu-id="1d4f7-180">а.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-180">a.</span></span> <span data-ttu-id="1d4f7-181">В hello **кластера Spark (Linux)** раскрывающегося списка выберите локальный "песочницы" Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="1d4f7-182">b.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-182">b.</span></span> <span data-ttu-id="1d4f7-183">В hello **имя класса Main** выберите или введите имя основного класса hello.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="1d4f7-184">В этом учебнике — имя hello **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="1d4f7-185">Нажмите кнопку **Submit** (Отправить).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-185">Select **Submit**.</span></span> <span data-ttu-id="1d4f7-186">журналы отправки заданий Hello отображаются в окне инструментов отправки Spark hello.</span><span class="sxs-lookup"><span data-stu-id="1d4f7-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d4f7-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d4f7-187">Next steps</span></span>

- <span data-ttu-id="1d4f7-188">как toocreate приложений Spark для HDInsight с помощью средства HDInsight для IntelliJ, перейдите в слишком toolearn[используйте средства HDInsight в набор средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="1d4f7-189">слишком go toowatch видео средства HDInsight для IntelliJ,[вводит средства HDInsight для IntelliJ для разработки Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="1d4f7-190">toolearn как toodebug Spark приложений с помощью hello toolkit удаленно на HDInsight через SSH, перейдите слишком[удаленно отлаживать приложения Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="1d4f7-191">toolearn как toodebug Spark приложений с помощью hello toolkit удаленно на HDInsight через виртуальную частную сеть, перейдите слишком[используйте средства HDInsight в набор средств Azure для приложений Spark toodebug IntelliJ удаленно в кластере HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="1d4f7-192">как toouse средства HDInsight для Eclipse toocreate приложении Spark go слишком toolearn[используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="1d4f7-193">toowatch видео средства HDInsight для Eclipse, go слишком[использовать инструмент HDInsight Spark приложений Eclipse toocreate](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="1d4f7-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
