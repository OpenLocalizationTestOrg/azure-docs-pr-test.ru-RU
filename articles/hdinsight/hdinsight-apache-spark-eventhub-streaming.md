---
title: "aaaUse Apache Spark потоковой передачи с концентраторами событий в Azure HDInsight | Документы Microsoft"
description: "Постройте Apache Spark потоковой передачи потока tooAzure концентратора событий и затем получения этих событий в кластере HDInsight Spark с помощью приложения scala toosend данных."
keywords: "потоковая передача apache spark, потоковая передача spark, пример приложения spark, пример приложения потоковой передачи apache spark, пример концентратора событий azure, пример приложения spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="c360b-104">Потоковая передача Apache Spark. Обработка данных из концентраторов событий Azure с помощью кластера Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c360b-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="c360b-105">В этой статье создайте Apache Spark, образец, который включает в себя следующие шаги hello потоковой передачи:</span><span class="sxs-lookup"><span data-stu-id="c360b-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="c360b-106">Использовать автономные приложения tooingest сообщений в концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c360b-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="c360b-107">С два различных подхода получения сообщений hello из концентратора событий в режиме реального времени с помощью приложения, запущенного в кластере Spark на Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c360b-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="c360b-108">Построение потоковой передачи конвейеры аналитических систем хранения toodifferent toopersist данных или получения сведений из данных на лету hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c360b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c360b-109">Prerequisites</span></span>

* <span data-ttu-id="c360b-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="c360b-110">An Azure subscription.</span></span> <span data-ttu-id="c360b-111">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c360b-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="c360b-112">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c360b-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="c360b-113">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="c360b-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="c360b-114">Основные понятия потоковой передачи Spark</span><span class="sxs-lookup"><span data-stu-id="c360b-114">Spark Streaming concepts</span></span>

<span data-ttu-id="c360b-115">Подробное описание потоковой передачи Spark см. в [этом разделе](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="c360b-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="c360b-116">HDInsight переводит hello кластера же потоковой передачи tooa функции Spark на Azure.</span><span class="sxs-lookup"><span data-stu-id="c360b-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="c360b-117">Каково предназначение этого решения?</span><span class="sxs-lookup"><span data-stu-id="c360b-117">What does this solution do?</span></span>

<span data-ttu-id="c360b-118">В этой статье toocreate пример для потоковой передачи Spark выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="c360b-119">Создание концентратора событий Azure, который будет принимать поток событий.</span><span class="sxs-lookup"><span data-stu-id="c360b-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="c360b-120">Запуск локального автономное приложение, приводит к возникновению события и помещает его toohello концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c360b-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="c360b-121">Пример приложения Hello, делает это опубликованы по адресу [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="c360b-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="c360b-122">Удаленно запустите в кластере Spark приложение потоковой передачи, которое считывает потоковые события из концентратора событий Azure и выполняет различные задачи обработки и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="c360b-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="c360b-123">Создание концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="c360b-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="c360b-124">Войдите на toohello [портала Azure](https://ms.portal.azure.com)и нажмите кнопку **New** на hello верхнего левого угла экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="c360b-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="c360b-125">Последовательно выберите **Интернет вещей** и **Концентраторы событий**.</span><span class="sxs-lookup"><span data-stu-id="c360b-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="c360b-126">![Создание концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Создание концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="c360b-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="c360b-127">В hello **создать пространство имен** колонки, введите имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="c360b-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="c360b-128">Выберите hello ценовой категории (Basic или Standard).</span><span class="sxs-lookup"><span data-stu-id="c360b-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="c360b-129">Кроме того, в какой ресурс hello toocreate выберите подписки Azure, группа ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="c360b-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="c360b-130">Нажмите кнопку **создать** toocreate приветствия имен.</span><span class="sxs-lookup"><span data-stu-id="c360b-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="c360b-131">![Указание имени концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Указание имени концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="c360b-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="c360b-132">Вы должны выбрать hello же **расположение** как кластера Apache Spark в HDInsight tooreduce задержки и затраты.</span><span class="sxs-lookup"><span data-stu-id="c360b-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="c360b-133">В списке имен hello концентраторов событий выберите пространство имен созданного hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="c360b-134">В колонке hello пространства имен, щелкните **концентраторов событий**, а затем нажмите кнопку **+ концентратора событий** toocreate новый концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="c360b-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="c360b-135">![Создание концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Создание концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="c360b-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="c360b-136">Введите имя для концентратора событий, набор hello секции count too10 и too1 хранения сообщений.</span><span class="sxs-lookup"><span data-stu-id="c360b-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="c360b-137">Мы не архивация выполняется сообщений hello в этом решении, оставьте hello rest по умолчанию и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="c360b-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="c360b-138">![Указание сведений о концентраторе событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Указание сведений о концентраторе событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="c360b-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="c360b-139">в колонке hello концентратора событий перечислены Hello вновь созданные концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c360b-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="c360b-140">![Просмотр концентратор событий для потоковой передачи пример hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "представление концентратор событий для hello Поместите здесь пример потоковой передачи")</span><span class="sxs-lookup"><span data-stu-id="c360b-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="c360b-141">В колонке hello пространства имен (не hello конкретного концентратора событий колонку), нажмите кнопку **политики общего доступа**, а затем нажмите кнопку **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="c360b-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="c360b-142">![Установка политики концентратора событий для потоковой передачи пример hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "концентратора событий набор политик для hello Поместите здесь пример потоковой передачи")</span><span class="sxs-lookup"><span data-stu-id="c360b-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="c360b-143">Нажмите кнопку toocopy hello копирования hello **RootManageSharedAccessKey** первичный ключ и соединения строки toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="c360b-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="c360b-144">Сохраните эти toouse далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="c360b-145">![Просмотр ключей политики концентратора событий для потоковой передачи пример hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "ключей политики концентратора событий представления для hello Поместите здесь пример потоковой передачи")</span><span class="sxs-lookup"><span data-stu-id="c360b-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="c360b-146">Отправка сообщений tooAzure концентратора событий с помощью Scala примера приложения</span><span class="sxs-lookup"><span data-stu-id="c360b-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="c360b-147">В этом разделе используется изолированный локальное Scala приложение, приводит к возникновению ошибки потока событий и отправляет его tooAzure концентратора событий, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="c360b-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="c360b-148">Это приложение доступно на сайте GitHub по адресу [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="c360b-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="c360b-149">Hello здесь предполагается, что уже разделенными этот репозиторий GitHub.</span><span class="sxs-lookup"><span data-stu-id="c360b-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="c360b-150">Убедитесь, что у вас есть hello установлены следующие компоненты на компьютере hello, где выполняется это приложение.</span><span class="sxs-lookup"><span data-stu-id="c360b-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="c360b-151">Комплект разработчика Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="c360b-151">Oracle Java Development kit.</span></span> <span data-ttu-id="c360b-152">Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="c360b-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="c360b-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="c360b-153">Apache Maven.</span></span> <span data-ttu-id="c360b-154">Скачать эту версию можно [здесь](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="c360b-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="c360b-155">Доступные инструкции tooinstall Maven [здесь](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="c360b-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="c360b-156">Откройте командную строку и перейдите toohello расположение клонировать hello в репозитории GitHub для приложения Scala образец hello и запустите следующие команды toobuild hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="c360b-157">Hello jar выходных данных для приложения hello **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, будет создан в разделе **/target-** каталога.</span><span class="sxs-lookup"><span data-stu-id="c360b-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="c360b-158">Далее в этой статье tootest hello полнофункциональную этот JAR-ФАЙЛ используется.</span><span class="sxs-lookup"><span data-stu-id="c360b-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="c360b-159">Создания приложения tooreceive сообщений из концентратора событий в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="c360b-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="c360b-160">Имеется два подхода tooconnect, потоковая передача Spark и концентраторов событий Azure, подключение на основе приемника и Direct DStream-подключения на основе.</span><span class="sxs-lookup"><span data-stu-id="c360b-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="c360b-161">Direct DStream на основе появился на января 2017 года, в выпуске hello 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="c360b-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="c360b-162">Он должен tooreplace hello исходного получателя подключения на основе как он обеспечивает более высокую производительность и эффективность ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c360b-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="c360b-163">Дополнительные сведения см. на странице [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="c360b-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="c360b-164">Direct DStream поддерживает только Spark 2.0 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="c360b-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="c360b-165">Создание приложений с помощью соединителя toospark eventhubs hello зависимостей</span><span class="sxs-lookup"><span data-stu-id="c360b-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="c360b-166">Также мы опубликуем hello, промежуточные версии Spark EventHubs в GitHub.</span><span class="sxs-lookup"><span data-stu-id="c360b-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="c360b-167">toouse hello промежуточной версии Spark EventHubs, hello первым шагом является tooindicate GitHub как hello источник репозитория, добавив следующие записи toopom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="c360b-168">Затем можно добавить следующие предварительные выпуски версия зависимости tooyour проекта tootake hello hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="c360b-169">Зависимость Maven</span><span class="sxs-lookup"><span data-stu-id="c360b-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="c360b-170">Зависимость SBT</span><span class="sxs-lookup"><span data-stu-id="c360b-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="c360b-171">Подключение Direct DStream</span><span class="sxs-lookup"><span data-stu-id="c360b-171">Direct DStream Connection</span></span>

<span data-ttu-id="c360b-172">Предварительно собранный JAR-файл, содержащий примеры использования Direct DStream, можно скачать по адресу [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="c360b-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="c360b-173">Hello jar-файл содержит три примера, исходный код можно найти по адресу [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="c360b-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="c360b-174">Рассмотрим [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c360b-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="c360b-175">В hello в приведенном выше примере `eventhubParameters` один экземпляр EventHubs hello параметры конкретного tooa и у вас toopass его toohello `createDirectStreams` API, который создает имен прямой DStream объекта сопоставления tooa концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="c360b-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="c360b-176">Над объектом прямой DStream hello можно вызвать любой DStream API, предоставляемые платформой Spark потоковый API-Интерфейс.</span><span class="sxs-lookup"><span data-stu-id="c360b-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="c360b-177">В этом примере вычислять hello частоту каждого слова hello последнего пакета 3 micro интервалами.</span><span class="sxs-lookup"><span data-stu-id="c360b-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="c360b-178">Подключение на основе получателя</span><span class="sxs-lookup"><span data-stu-id="c360b-178">Receiver-based Connection</span></span>

<span data-ttu-id="c360b-179">Spark, пример приложения, написанного на Scala, который получает события и назначения toodifferent hello маршрутов, потоковая передача доступна на [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="c360b-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="c360b-180">Выполните действия hello ниже приложения hello tooupdate конфигурации концентратора событий и создайте jar hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c360b-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="c360b-181">Запустите IntelliJ ИДЕЯ и из hello Выбор экрана запуска **извлечь из системы управления версиями** и нажмите кнопку **Git**.</span><span class="sxs-lookup"><span data-stu-id="c360b-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="c360b-182">![Пример приложения потоковой передачи Apache Spark. Получение источников из Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Пример приложения потоковой передачи Apache Spark. Получение источников из Git")</span><span class="sxs-lookup"><span data-stu-id="c360b-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="c360b-183">В hello **клона репозитория** диалоговом предоставляют hello URL-адрес toohello Git из репозитория tooclone, укажите tooclone directory hello для и нажмите кнопку **клон**.</span><span class="sxs-lookup"><span data-stu-id="c360b-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="c360b-184">![Пример приложения потоковой передачи Apache Spark. Клонирование из Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Пример приложения потоковой передачи Apache Spark. Клонирование из Git")</span><span class="sxs-lookup"><span data-stu-id="c360b-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="c360b-185">Следуйте инструкциям hello, пока проект hello полностью клонируется.</span><span class="sxs-lookup"><span data-stu-id="c360b-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="c360b-186">Нажмите клавишу **Alt + 1** tooopen hello **представления проекта**.</span><span class="sxs-lookup"><span data-stu-id="c360b-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="c360b-187">Она должна иметь вид hello следующее.</span><span class="sxs-lookup"><span data-stu-id="c360b-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="c360b-188">![Пример приложения потоковой передачи Apache Spark. Представление проекта](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Пример приложения потоковой передачи Apache Spark. Представление проекта")</span><span class="sxs-lookup"><span data-stu-id="c360b-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="c360b-189">Убедитесь, что код приложения hello компилируется с помощью Java8.</span><span class="sxs-lookup"><span data-stu-id="c360b-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="c360b-190">tooensure, нажмите кнопку **файл**, нажмите кнопку **структура проекта**и на hello **проекта** , убедитесь, что уровень языка проекта задано слишком**8 - лямбда-выражения, тип заметки, т. д.**.</span><span class="sxs-lookup"><span data-stu-id="c360b-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="c360b-191">![Пример приложения потоковой передачи Apache Spark. Настройка компилятора](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Пример приложения потоковой передачи Apache Spark. Настройка компилятора")</span><span class="sxs-lookup"><span data-stu-id="c360b-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="c360b-192">Откройте hello **pom.xml** и убедитесь, что выбрана правильная версия Spark hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="c360b-193">В разделе `<properties>` узел, найдите следующий фрагмент кода hello и проверить версию Spark hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="c360b-194">приложение Hello требует зависимостей JAR-файл называется **JAR-файл драйвера JDBC**.</span><span class="sxs-lookup"><span data-stu-id="c360b-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="c360b-195">Это обязательный toowrite сообщений hello, полученные от концентратора событий в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c360b-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="c360b-196">Этот JAR-файл (версии 4.1 или более поздней) можно скачать [здесь](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="c360b-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="c360b-197">Добавьте jar toothis ссылку в библиотеке проектов hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="c360b-198">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="c360b-199">Щелкните в окне IntelliJ ИДЕЯ при наличии приложения hello откройте **файл**, нажмите кнопку **структура проекта**и нажмите кнопку **библиотеки**.</span><span class="sxs-lookup"><span data-stu-id="c360b-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="c360b-200">Щелкните hello значок добавления (![значок добавления](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), нажмите кнопку **Java**, а затем переходить toohello расположение, куда вы загрузили JAR-файл драйвера JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="c360b-201">Выполните запросы hello tooadd hello jar файла toohello проекта библиотеки.</span><span class="sxs-lookup"><span data-stu-id="c360b-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="c360b-202">![добавление отсутствующих зависимостей](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Добавление отсутствующих JAR-файлов зависимостей")</span><span class="sxs-lookup"><span data-stu-id="c360b-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="c360b-203">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="c360b-203">Click **Apply**.</span></span>

7. <span data-ttu-id="c360b-204">Создайте выходной hello jar-файл.</span><span class="sxs-lookup"><span data-stu-id="c360b-204">Create hello output jar file.</span></span> <span data-ttu-id="c360b-205">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="c360b-206">В hello **структура проекта** диалоговое окно, нажмите кнопку **артефакты** и нажмите кнопку hello, а также символ.</span><span class="sxs-lookup"><span data-stu-id="c360b-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="c360b-207">Hello всплывающее диалоговое окно, щелкните **JAR**, а затем нажмите кнопку **из модулей с зависимостями**.</span><span class="sxs-lookup"><span data-stu-id="c360b-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="c360b-208">![Пример приложения потоковой передачи Apache Spark. Создание JAR-файла](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Пример приложения потоковой передачи Apache Spark. Создание JAR-файла")</span><span class="sxs-lookup"><span data-stu-id="c360b-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="c360b-209">В hello **создать JAR из модулей** диалоговое окно, нажмите кнопку с многоточием hello (![многоточие](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) от hello **класс Main**.</span><span class="sxs-lookup"><span data-stu-id="c360b-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="c360b-210">В hello **выберите класс Main** диалоговое окно, выберите любой из доступных классов hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c360b-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="c360b-211">![Пример приложения потоковой передачи Apache Spark. Выбор класса JAR-файла](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Пример приложения потоковой передачи Apache Spark. Выбор класса JAR-файла")</span><span class="sxs-lookup"><span data-stu-id="c360b-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="c360b-212">В hello **создать JAR из модулей** диалогового окна поле, убедитесь, что этот параметр hello слишком**извлечения целевого toohello JAR** выбран и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c360b-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="c360b-213">В результате будет создан один JAR-файл, содержащий все зависимости.</span><span class="sxs-lookup"><span data-stu-id="c360b-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="c360b-214">![Пример приложения потоковой передачи Apache Spark. Создание JAR-файла на основе модулей](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Пример приложения потоковой передачи Apache Spark. Создание JAR-файла на основе модулей")</span><span class="sxs-lookup"><span data-stu-id="c360b-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="c360b-215">Hello **макета вывода** вкладке перечисляются все hello файлов, которые включены в состав проекта Maven hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="c360b-216">Можно выбрать и удалить hello, на которой другие hello Scala приложения имеет нет прямой зависимости.</span><span class="sxs-lookup"><span data-stu-id="c360b-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="c360b-217">Для приложения hello, мы создаем здесь, можно удалить все, кроме hello последним (**spark-потоковой передачи--сохраняемости примеры данных компиляции выходной**).</span><span class="sxs-lookup"><span data-stu-id="c360b-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="c360b-218">Выберите toodelete hello JAR-файлов и нажмите кнопку hello **удаление** значок (![значок удаления](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="c360b-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="c360b-219">![Пример приложения потоковой передачи Apache Spark. Удаление извлеченных JAR-файлов](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Пример приложения потоковой передачи Apache Spark. Удаление извлеченных JAR-файлов")</span><span class="sxs-lookup"><span data-stu-id="c360b-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="c360b-220">Убедитесь, что **сборки в проверьте** флажок, который гарантирует, что jar hello создаются каждый раз, hello проекта будут созданы или обновлены.</span><span class="sxs-lookup"><span data-stu-id="c360b-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="c360b-221">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="c360b-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="c360b-222">В hello **макета вывода** вкладки справа внизу hello hello **доступные элементы** поле, у вас есть jar SQL JDBC hello, добавленные ранее toohello проекта библиотеки.</span><span class="sxs-lookup"><span data-stu-id="c360b-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="c360b-223">Необходимо добавить этот toohello **макета вывода** вкладки. Щелкните правой кнопкой мыши hello jar-файл и нажмите кнопку **извлечения в выходных данных корневой**.</span><span class="sxs-lookup"><span data-stu-id="c360b-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="c360b-224">![Пример приложения потоковой передачи Apache Spark. Извлечение JAR-файла зависимостей](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Пример приложения потоковой передачи Apache Spark. Извлечение JAR-файла зависимостей")</span><span class="sxs-lookup"><span data-stu-id="c360b-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="c360b-225">Hello **макета вывода** вкладка теперь должна выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c360b-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="c360b-226">![Пример приложения потоковой передачи Apache Spark. Вкладка окончательных выходных данных](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Пример приложения потоковой передачи Apache Spark. Вкладка окончательных выходных данных")</span><span class="sxs-lookup"><span data-stu-id="c360b-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="c360b-227">В hello **структура проекта** диалоговое окно, нажмите кнопку **применить** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c360b-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="c360b-228">На панели меню hello, нажмите кнопку **построения**и нажмите кнопку **сделать проект**.</span><span class="sxs-lookup"><span data-stu-id="c360b-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="c360b-229">Можно также щелкнуть **артефакты сборки** toocreate hello jar.</span><span class="sxs-lookup"><span data-stu-id="c360b-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="c360b-230">Hello JAR-выходной файл будет создан в разделе **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="c360b-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="c360b-231">![Пример приложения потоковой передачи Apache Spark. Выходной JAR-файл](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Пример приложения потоковой передачи Apache Spark. Выходной JAR-файл")</span><span class="sxs-lookup"><span data-stu-id="c360b-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="c360b-232">Удаленно запускать приложения hello на кластере Spark, с помощью Livy</span><span class="sxs-lookup"><span data-stu-id="c360b-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="c360b-233">В этой статье используется потоковой передачи приложения hello toorun Apache Spark Livy удаленно на кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="c360b-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="c360b-234">Подробные сведения об как кластера toouse Livy с HDInsight Spark. в разделе [отправки заданий удаленно tooan Apache Spark кластера в Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="c360b-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="c360b-235">Перед запуском приложение hello Spark потоковой передачи, существует несколько факторов, которые нужно выполнить.</span><span class="sxs-lookup"><span data-stu-id="c360b-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="c360b-236">Запуск событий toogenerate hello локального автономного приложения и отправляются tooEvent концентратора.</span><span class="sxs-lookup"><span data-stu-id="c360b-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="c360b-237">Используйте hello следующая команда toodo так:</span><span class="sxs-lookup"><span data-stu-id="c360b-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="c360b-238">Потоковая передача jar hello копирования (**spark-потоковой передачи данные сохраняемости examples.jar,**) toohello хранилище больших двоичных объектов Azure, связанном с hello кластера.</span><span class="sxs-lookup"><span data-stu-id="c360b-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="c360b-239">Это делает tooLivy доступен jar hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="c360b-240">Можно использовать [ **AzCopy**](../storage/common/storage-use-azcopy.md), Командная строка программы, toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="c360b-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="c360b-241">Существует много других клиентов можно использовать tooupload данных.</span><span class="sxs-lookup"><span data-stu-id="c360b-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="c360b-242">Дополнительные сведения о них см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="c360b-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="c360b-243">Установите ПЕРЕЛИСТЫВАНИЕ на компьютере hello, где выполняются эти приложения с.</span><span class="sxs-lookup"><span data-stu-id="c360b-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="c360b-244">Мы используем hello tooinvoke ПЕРЕЛИСТЫВАНИЕ hello toorun Livy конечных точек удаленного задания.</span><span class="sxs-lookup"><span data-stu-id="c360b-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="c360b-245">Запуска hello события hello Spark потоковой передачи приложения tooreceive в BLOB-объект хранилища Azure в виде текста</span><span class="sxs-lookup"><span data-stu-id="c360b-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="c360b-246">Откройте командную строку, перейдите в каталог toohello, где установлены ПЕРЕЛИСТЫВАНИЕ и запустите следующую команду (замените имя пользователя и пароль и кластера имя) hello:</span><span class="sxs-lookup"><span data-stu-id="c360b-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="c360b-247">Здравствуйте, параметры в файле hello **inputBlob.txt** определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c360b-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="c360b-248">Сообщите нам понять, каковы параметры hello во входном файле hello:</span><span class="sxs-lookup"><span data-stu-id="c360b-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="c360b-249">**файл** является hello путь toohello приложения jar-файл в учетной записи хранилища Azure hello, связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="c360b-250">**className** — hello имя класса hello в банке hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="c360b-251">**args** — список hello аргументы, необходимые для класса hello</span><span class="sxs-lookup"><span data-stu-id="c360b-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="c360b-252">**numExecutors** — hello количество ядер, используемых потоковой передачи приложения hello toorun Spark.</span><span class="sxs-lookup"><span data-stu-id="c360b-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="c360b-253">Всегда должно быть по крайней мере дважды hello количество секций концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c360b-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="c360b-254">**executorMemory**, **executorCores**, **driverMemory** — это ресурсы tooassign необходимые параметры, используемые toohello потоковой передачи приложения.</span><span class="sxs-lookup"><span data-stu-id="c360b-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="c360b-255">Не обязательно toocreate hello выходные папки (EventCheckpoint, EventCount или EventCount10), используемые в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="c360b-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="c360b-256">Потоковая передача приложения Hello создает их.</span><span class="sxs-lookup"><span data-stu-id="c360b-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="c360b-257">При выполнении команды hello, вы увидите, что выход hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c360b-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="c360b-258">Запишите идентификатор пакета hello в последней строке hello hello выходных данных (в этом примере это "1").</span><span class="sxs-lookup"><span data-stu-id="c360b-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="c360b-259">tooverify, hello приложения выполняется успешно, можно взглянуть на вашей учетной записи хранилища Azure, связанные с кластером hello и вы увидите hello **/EventCount/EventCount10** папки там создается.</span><span class="sxs-lookup"><span data-stu-id="c360b-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="c360b-260">Эта папка должна содержать большие двоичные объекты, которые перехватывает hello количество событий, обработанных в hello периода времени, заданного для параметра hello **пакета интервал в секундах**.</span><span class="sxs-lookup"><span data-stu-id="c360b-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="c360b-261">Hello Spark потоковой передачи приложения будет продолжено toorun, пока не удалите его.</span><span class="sxs-lookup"><span data-stu-id="c360b-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="c360b-262">Таким образом, toodo используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c360b-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="c360b-263">Приложения hello tooreceive hello события выполнения в BLOB-объект хранилища Azure как JSON</span><span class="sxs-lookup"><span data-stu-id="c360b-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="c360b-264">Откройте командную строку, перейдите в каталог toohello, где установлены ПЕРЕЛИСТЫВАНИЕ и запустите следующую команду (замените имя пользователя и пароль и кластера имя) hello:</span><span class="sxs-lookup"><span data-stu-id="c360b-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="c360b-265">Здравствуйте, параметры в файле hello **inputJSON.txt** определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c360b-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="c360b-266">Hello параметры, аналогичные toowhat, указанное для hello текстовый вывод в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="c360b-267">Опять же необязательно toocreate hello выходные папки (EventCheckpoint, EventCount или EventCount10), используемые в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="c360b-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="c360b-268">Потоковая передача приложения Hello создает их.</span><span class="sxs-lookup"><span data-stu-id="c360b-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="c360b-269">После выполнения команды hello, вы можете воспользоваться вашей учетной записи хранилища Azure, связанные с кластером hello и вы увидите hello **/EventStore10** папки там создается.</span><span class="sxs-lookup"><span data-stu-id="c360b-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="c360b-270">Откройте любой файл с префиксом **часть -** и вы увидите hello событий, обработанных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="c360b-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="c360b-271">Запускать приложения hello tooreceive hello события в таблицу Hive</span><span class="sxs-lookup"><span data-stu-id="c360b-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="c360b-272">Некоторые дополнительные компоненты, необходимые toorun hello Spark потоковой передачи приложений, который потоки событий в куст таблицу вы.</span><span class="sxs-lookup"><span data-stu-id="c360b-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="c360b-273">а именно:</span><span class="sxs-lookup"><span data-stu-id="c360b-273">These are:</span></span>

* <span data-ttu-id="c360b-274">datanucleus-api-jdo-3.2.6.jar;</span><span class="sxs-lookup"><span data-stu-id="c360b-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="c360b-275">datanucleus-rdbms-3.2.9.jar;</span><span class="sxs-lookup"><span data-stu-id="c360b-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="c360b-276">datanucleus-core-3.2.10.jar;</span><span class="sxs-lookup"><span data-stu-id="c360b-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="c360b-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="c360b-277">hive-site.xml</span></span>

<span data-ttu-id="c360b-278">Hello **.jar** файлы доступны в кластере HDInsight Spark на `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="c360b-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="c360b-279">Hello **hive-site.xml** доступен на `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="c360b-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="c360b-280">Можно использовать [WinScp](http://winscp.net/eng/download.php) toocopy эти файлы с локального компьютера hello кластера tooyour.</span><span class="sxs-lookup"><span data-stu-id="c360b-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="c360b-281">Затем можно использовать средства toocopy эти файлы по tooyour учетной записи хранения, связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="c360b-282">Дополнительные сведения о как tooupload файлы toohello учетной записи хранения см. в разделе [передать данные для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="c360b-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="c360b-283">После копирования через tooyour файлы hello учетной записи хранилища Azure, откройте командную строку, перейдите toohello каталог, где установлены ПЕРЕЛИСТЫВАНИЕ и выполните следующую команду (замените имя пользователя и пароль и кластера имя) hello:</span><span class="sxs-lookup"><span data-stu-id="c360b-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="c360b-284">Здравствуйте, параметры в файле hello **inputHive.txt** определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c360b-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="c360b-285">Hello параметры, аналогичные toowhat, указанное для hello текстовый вывод в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="c360b-286">Еще раз, нет необходимости toocreate hello выходной папки (EventCheckpoint, EventCount или EventCount10) или hello вывод таблицу Hive (EventHiveTable10), которые используются в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="c360b-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="c360b-287">Потоковая передача приложения Hello создает их.</span><span class="sxs-lookup"><span data-stu-id="c360b-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="c360b-288">Обратите внимание, что hello **JAR-файлов** и **файлы** параметр включает в себя файлы .jar toohello пути и hello hive-site.xml, скопированными с перекрытием toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c360b-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="c360b-289">tooverify, таблица hive hello успешно создан, можно SSH в кластере hello и выполнения запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="c360b-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="c360b-290">Инструкции см. в статье [Использование Hive с Hadoop в HDInsight с применением протокола SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="c360b-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="c360b-291">После установления соединения с помощью SSH можно запустить следующие команды tooverify hello таблицу Hive hello и **EventHiveTable10**, создается.</span><span class="sxs-lookup"><span data-stu-id="c360b-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="c360b-292">Вы должны увидеть следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="c360b-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="c360b-293">Можно также запустите запрос SELECT tooview hello содержимое таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="c360b-294">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c360b-294">You should see an output like hello following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="c360b-295">Запускать приложения hello tooreceive hello события в таблицу базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="c360b-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="c360b-296">Прежде чем выполнять этот шаг, убедитесь, что у вас есть созданная база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c360b-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="c360b-297">Инструкции см. в статье [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c360b-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="c360b-298">toocomplete в этом разделе, требуются значения для имени базы данных, имя сервера базы данных и учетные данные администратора hello базы данных в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="c360b-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="c360b-299">Не требуется таблица базы данных hello toocreate хотя.</span><span class="sxs-lookup"><span data-stu-id="c360b-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="c360b-300">Hello приложения потоковой Spark, будет создан.</span><span class="sxs-lookup"><span data-stu-id="c360b-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="c360b-301">Откройте командную строку, перейдите в каталог toohello, где установлены ПЕРЕЛИСТЫВАНИЕ и выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c360b-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="c360b-302">Здравствуйте, параметры в файле hello **inputSQL.txt** определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c360b-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="c360b-303">tooverify, приложение hello выполняется успешно, можно подключить toohello базы данных Azure SQL с помощью SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="c360b-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="c360b-304">Дополнительные сведения о toodo, в разделе [подключения tooSQL базы данных с SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="c360b-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="c360b-305">После toohello подключенной базы данных, можно переходить toohello **EventContent** таблицы, созданные потоковой передачи приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="c360b-306">Можно запустить tooget hello быстрого запроса данных из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="c360b-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="c360b-307">Выполните приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="c360b-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="c360b-308">Вы увидите примерно toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c360b-308">You should see output similar toohello following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="c360b-309"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c360b-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="c360b-310">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c360b-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="c360b-311">Проектирование подключения на основе приемника и Direct DStream</span><span class="sxs-lookup"><span data-stu-id="c360b-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="c360b-312">Сценарии</span><span class="sxs-lookup"><span data-stu-id="c360b-312">Scenarios</span></span>
* [<span data-ttu-id="c360b-313">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="c360b-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c360b-314">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="c360b-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c360b-315">Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов</span><span class="sxs-lookup"><span data-stu-id="c360b-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c360b-316">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c360b-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c360b-317">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="c360b-317">Create and run applications</span></span>
* [<span data-ttu-id="c360b-318">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="c360b-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c360b-319">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="c360b-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c360b-320">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="c360b-320">Tools and extensions</span></span>
* [<span data-ttu-id="c360b-321">Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений</span><span class="sxs-lookup"><span data-stu-id="c360b-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c360b-322">Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c360b-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c360b-323">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c360b-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c360b-324">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c360b-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c360b-325">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="c360b-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c360b-326">Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="c360b-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c360b-327">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="c360b-327">Manage resources</span></span>
* [<span data-ttu-id="c360b-328">Управление ресурсами кластера hello Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c360b-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c360b-329">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="c360b-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
