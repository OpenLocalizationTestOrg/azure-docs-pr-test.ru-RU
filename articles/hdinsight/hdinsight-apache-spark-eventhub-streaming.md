---
title: "Потоковая передача данных Apache Spark из концентраторов событий в Azure HDInsight | Документация Майкрософт"
description: "Сведения о разработке примера приложения потоковой передачи Apache Spark для отправки потока данных в концентратор событий Azure и последующего получения этих событий в кластере HDInsight Spark с помощью приложения Scala."
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
ms.openlocfilehash: 175a2ad70b1f554d05846eb62fb685d4f259af7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="0403f-104">Потоковая передача Apache Spark. Обработка данных из концентраторов событий Azure с помощью кластера Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0403f-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="0403f-105">В этой статье вы создадите пример приложения потоковой передачи Apache Spark, выполняющий следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0403f-105">In this article, you create an Apache Spark streaming sample that involves the following steps:</span></span>

1. <span data-ttu-id="0403f-106">Автономное приложение принимает сообщения в концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="0403f-106">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="0403f-107">С помощью двух разных подходов сообщения извлекаются из концентратора событий в режиме реального времени с помощью приложения, работающего в кластере Spark в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0403f-107">With two different approaches, you retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="0403f-108">Вы создаете конвейеры потоковой передачи данных аналитики для сохранения данных в разных системах хранения или анализируете данные оперативно.</span><span class="sxs-lookup"><span data-stu-id="0403f-108">You build streaming analytic pipelines to persist data to different storage systems, or get insights from data on the fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0403f-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0403f-109">Prerequisites</span></span>

* <span data-ttu-id="0403f-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="0403f-110">An Azure subscription.</span></span> <span data-ttu-id="0403f-111">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0403f-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="0403f-112">Кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0403f-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="0403f-113">Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="0403f-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="0403f-114">Основные понятия потоковой передачи Spark</span><span class="sxs-lookup"><span data-stu-id="0403f-114">Spark Streaming concepts</span></span>

<span data-ttu-id="0403f-115">Подробное описание потоковой передачи Spark см. в [этом разделе](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="0403f-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="0403f-116">HDInsight предоставляет аналогичные функции потоковой передачи для кластера Spark в Azure.</span><span class="sxs-lookup"><span data-stu-id="0403f-116">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="0403f-117">Каково предназначение этого решения?</span><span class="sxs-lookup"><span data-stu-id="0403f-117">What does this solution do?</span></span>

<span data-ttu-id="0403f-118">Чтобы создать пример приложения потоковой передачи Spark, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0403f-118">In this article, to create a Spark streaming example, perform the following steps:</span></span>

1. <span data-ttu-id="0403f-119">Создание концентратора событий Azure, который будет принимать поток событий.</span><span class="sxs-lookup"><span data-stu-id="0403f-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="0403f-120">Запуск локального автономного приложения, которое создает события и передает их в концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="0403f-120">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="0403f-121">Пример такого приложения опубликован по адресу [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="0403f-121">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="0403f-122">Удаленно запустите в кластере Spark приложение потоковой передачи, которое считывает потоковые события из концентратора событий Azure и выполняет различные задачи обработки и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="0403f-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="0403f-123">Создание концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="0403f-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="0403f-124">Войдите на [портал Azure](https://ms.portal.azure.com) и щелкните **Создать** вверху слева.</span><span class="sxs-lookup"><span data-stu-id="0403f-124">Log on to the [Azure Portal](https://ms.portal.azure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="0403f-125">Последовательно выберите **Интернет вещей** и **Концентраторы событий**.</span><span class="sxs-lookup"><span data-stu-id="0403f-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="0403f-126">![Создание концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Создание концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="0403f-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="0403f-127">В колонке **Создание пространства имен** укажите имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="0403f-127">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="0403f-128">выберите ценовую категорию ("Базовый" или "Стандартный").</span><span class="sxs-lookup"><span data-stu-id="0403f-128">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="0403f-129">Также выберите подписку Azure, группу ресурсов и расположение для создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="0403f-129">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="0403f-130">Щелкните **Создать** , чтобы создать пространство имен.</span><span class="sxs-lookup"><span data-stu-id="0403f-130">Click **Create** to create the namespace.</span></span>

      <span data-ttu-id="0403f-131">![Указание имени концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Указание имени концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="0403f-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="0403f-132">Для сокращения задержек и затрат в поле **Расположение** следует выбрать то же расположение, в котором находится кластер Apache Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0403f-132">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="0403f-133">В списке пространств имен концентраторов событий щелкните созданное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="0403f-133">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      


5. <span data-ttu-id="0403f-134">В колонке пространства имен щелкните **Концентраторы событий**, а затем **+Концентратор событий**, чтобы создать новый концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="0403f-134">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    <span data-ttu-id="0403f-135">![Создание концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Создание концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="0403f-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="0403f-136">Введите имя для концентратора событий; для параметра с числом разделов установите значение 10, а для хранения сообщений — 1.</span><span class="sxs-lookup"><span data-stu-id="0403f-136">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="0403f-137">Мы не будем сохранять сообщения в этом решении, поэтому остальные параметры можно не изменять. Просто нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0403f-137">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="0403f-138">![Указание сведений о концентраторе событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Указание сведений о концентраторе событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="0403f-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="0403f-139">Только что созданный концентратор событий отобразится в колонке "Концентратор событий".</span><span class="sxs-lookup"><span data-stu-id="0403f-139">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     <span data-ttu-id="0403f-140">![Просмотр концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Просмотр концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="0403f-140">![View Event Hub for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span></span>

8. <span data-ttu-id="0403f-141">В колонке пространства имен (не в конкретной колонке концентратора событий) щелкните **Политики общего доступа**, а затем нажмите щелкните **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="0403f-141">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="0403f-142">![Определение политик концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Определение политик концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="0403f-142">![Set Event Hub policies for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="0403f-143">Нажмите кнопку копирования, чтобы скопировать первичный ключ и строку подключения **RootManageSharedAccessKey** в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="0403f-143">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="0403f-144">Сохраните их, чтобы использовать на следующих этапах работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="0403f-144">Save these to use later in the tutorial.</span></span>
    
     <span data-ttu-id="0403f-145">![Просмотр ключей политик концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "Просмотр ключей политик концентратора событий для примера приложения потоковой передачи Spark")</span><span class="sxs-lookup"><span data-stu-id="0403f-145">![View Event Hub policy keys for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>

## <a name="send-messages-to-azure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="0403f-146">Отправка сообщений в концентратор событий с помощью примера приложения Scala</span><span class="sxs-lookup"><span data-stu-id="0403f-146">Send messages to Azure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="0403f-147">В этом разделе вы примените локальное автономное приложение Scala для создания потока событий и отправки его в созданный ранее концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="0403f-147">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created earlier.</span></span> <span data-ttu-id="0403f-148">Это приложение доступно на сайте GitHub по адресу [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="0403f-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="0403f-149">Здесь предполагается, что в репозитории GitHub уже созданы разветвления.</span><span class="sxs-lookup"><span data-stu-id="0403f-149">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="0403f-150">Убедитесь, что на компьютере, где выполняется это приложение, установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="0403f-150">Make sure you have the following installed on the computer where you run this application.</span></span>

    * <span data-ttu-id="0403f-151">Комплект разработчика Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="0403f-151">Oracle Java Development kit.</span></span> <span data-ttu-id="0403f-152">Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="0403f-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="0403f-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="0403f-153">Apache Maven.</span></span> <span data-ttu-id="0403f-154">Скачать эту версию можно [здесь](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="0403f-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="0403f-155">Инструкции по установке Maven доступны [здесь](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="0403f-155">Instructions to install Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="0403f-156">Откройте командную строку и перейдите к расположению, в которое вы скопировали образец приложения Scala из репозитория GitHub, а затем выполните приведенную ниже команду для сборки приложения.</span><span class="sxs-lookup"><span data-stu-id="0403f-156">Open a command prompt and navigate to the location you cloned the GitHub repo for the sample Scala application and run the following command to build the application.</span></span>

        mvn package

3. <span data-ttu-id="0403f-157">Выходной JAR-файл приложения (**com-microsoft-azure-eventhubs-client-example-0.2.0.jar**) создается в каталоге **/target**.</span><span class="sxs-lookup"><span data-stu-id="0403f-157">The output jar for the application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="0403f-158">Этот JAR-файл будет использоваться позднее в этой статье для тестирования готового решения.</span><span class="sxs-lookup"><span data-stu-id="0403f-158">You use this JAR later in this article to test the complete solution.</span></span>

## <a name="create-application-to-receive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="0403f-159">Создание приложения для получения сообщений от концентратора событий в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="0403f-159">Create application to receive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="0403f-160">Существует два подхода к установлению подключения между Spark Streaming и концентраторами событий Azure: подключение на основе приемника и подключение на основе Direct DStream.</span><span class="sxs-lookup"><span data-stu-id="0403f-160">We have two approaches to connect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="0403f-161">Подключение на основе Direct DStream появилось в январе 2017 г. в версии 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="0403f-161">Direct-DStream-based is introduced on Jan of 2017, in the 2.0.3 release.</span></span> <span data-ttu-id="0403f-162">Оно предназначено для замены прежних подключений на основе приемника, так как оно обеспечивает более высокую производительность и эффективность использования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0403f-162">It is supposed to replace the original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="0403f-163">Дополнительные сведения см. на странице [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="0403f-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="0403f-164">Direct DStream поддерживает только Spark 2.0 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="0403f-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-the-dependency-to-spark-eventhubs-connector"></a><span data-ttu-id="0403f-165">Создание приложений с зависимостью от соединителя spark-eventhubs</span><span class="sxs-lookup"><span data-stu-id="0403f-165">Build applications with the dependency to spark-eventhubs connector</span></span>

<span data-ttu-id="0403f-166">Мы также опубликуем промежуточную версию Spark-EventHubs в GitHub.</span><span class="sxs-lookup"><span data-stu-id="0403f-166">We will also publish the staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="0403f-167">Для использования промежуточной версии Spark-EventHubs сначала необходимо указать GitHub в качестве исходного репозитория, добавив в файл pom.xml следующую запись:</span><span class="sxs-lookup"><span data-stu-id="0403f-167">To use the staging version of Spark-EventHubs, the first step is to indicate GitHub as the source repo by adding the following entry to pom.xml:</span></span>

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

<span data-ttu-id="0403f-168">Далее можно добавить в проект указанную ниже зависимость для использования предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="0403f-168">You can then add the following dependency to your project to take the pre-released version.</span></span>

<span data-ttu-id="0403f-169">Зависимость Maven</span><span class="sxs-lookup"><span data-stu-id="0403f-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="0403f-170">Зависимость SBT</span><span class="sxs-lookup"><span data-stu-id="0403f-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="0403f-171">Подключение Direct DStream</span><span class="sxs-lookup"><span data-stu-id="0403f-171">Direct DStream Connection</span></span>

<span data-ttu-id="0403f-172">Предварительно собранный JAR-файл, содержащий примеры использования Direct DStream, можно скачать по адресу [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="0403f-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="0403f-173">JAR-файл содержит три примера, исходный код которых доступен на странице по адресу [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="0403f-173">The jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="0403f-174">Рассмотрим [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0403f-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

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

<span data-ttu-id="0403f-175">В приведенном выше примере `eventhubParameters` — это параметры, относящиеся к одному экземпляру EventHubs. Их необходимо передать в интерфейс API `createDirectStreams`, который создает объект Direct DStream, сопоставленный с пространством имен концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="0403f-175">In the above example, `eventhubParameters` are the parameters specific to a single EventHubs instance and you have to pass it to the `createDirectStreams` API which constructs a Direct DStream object mapping to a Event Hubs namespace.</span></span> <span data-ttu-id="0403f-176">Посредством объекта Direct DStream можно вызвать любой интерфейс API DStream, предоставляемый платформой API Spark Streaming.</span><span class="sxs-lookup"><span data-stu-id="0403f-176">Over the Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="0403f-177">В этом примере мы вычисляем частоту встречаемости каждого слова за последние 3 интервала микропакетов.</span><span class="sxs-lookup"><span data-stu-id="0403f-177">In this example, we calculate the frequency of each word within the last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="0403f-178">Подключение на основе получателя</span><span class="sxs-lookup"><span data-stu-id="0403f-178">Receiver-based Connection</span></span>

<span data-ttu-id="0403f-179">Пример приложения потоковой передачи Spark, написанного на языке Scala, которое получает события и перенаправляет их в различные расположения, доступен по адресу [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="0403f-179">A Spark streaming example application written in Scala, which receives events and route the to different destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="0403f-180">Выполните действия ниже, чтобы обновить приложение для конфигурации концентратора событий и создать выходной JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="0403f-180">Follow the steps below to update the application for your Event Hub configuration and create the output jar.</span></span>

1. <span data-ttu-id="0403f-181">Запустите IntelliJ IDEA и на экране запуска щелкните **Check out from Version Control** (Извлечь из системы управления версиями) и выберите пункт **Git**.</span><span class="sxs-lookup"><span data-stu-id="0403f-181">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="0403f-182">![Пример приложения потоковой передачи Apache Spark. Получение источников из Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Пример приложения потоковой передачи Apache Spark. Получение источников из Git")</span><span class="sxs-lookup"><span data-stu-id="0403f-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="0403f-183">В диалоговом окне **Clone Repository** (Клонирование репозитория) введите URL-адрес репозитория Git, который нужно клонировать, укажите каталог, в который будет выполняться клонирование, а затем нажмите кнопку **Clone** (Клонировать).</span><span class="sxs-lookup"><span data-stu-id="0403f-183">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="0403f-184">![Пример приложения потоковой передачи Apache Spark. Клонирование из Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Пример приложения потоковой передачи Apache Spark. Клонирование из Git")</span><span class="sxs-lookup"><span data-stu-id="0403f-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="0403f-185">Следуйте инструкциям на экране, пока проект полностью не клонируется.</span><span class="sxs-lookup"><span data-stu-id="0403f-185">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="0403f-186">Нажмите клавиши **ALT+1**, чтобы открыть **представление проекта**.</span><span class="sxs-lookup"><span data-stu-id="0403f-186">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="0403f-187">Оно должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="0403f-187">It should resemble the following.</span></span>
   
    <span data-ttu-id="0403f-188">![Пример приложения потоковой передачи Apache Spark. Представление проекта](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Пример приложения потоковой передачи Apache Spark. Представление проекта")</span><span class="sxs-lookup"><span data-stu-id="0403f-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="0403f-189">Скомпилируйте код приложения с помощью Java 8.</span><span class="sxs-lookup"><span data-stu-id="0403f-189">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="0403f-190">Чтобы сделать это, выберите **File** (Файл), **Project Structure** (Структура проекта) и на вкладке **Project** (Проект) в поле Project language level (Уровень языка проекта) установите значение **8 - Lambdas, type annotations, etc.** (8 — лямбды, аннотации типа и т. д.).</span><span class="sxs-lookup"><span data-stu-id="0403f-190">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="0403f-191">![Пример приложения потоковой передачи Apache Spark. Настройка компилятора](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Пример приложения потоковой передачи Apache Spark. Настройка компилятора")</span><span class="sxs-lookup"><span data-stu-id="0403f-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="0403f-192">Откройте узел **pom.xml** , чтобы убедиться, что используется правильная версия Spark.</span><span class="sxs-lookup"><span data-stu-id="0403f-192">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="0403f-193">В узле `<properties>` найдите фрагмент кода ниже и проверьте версию Spark.</span><span class="sxs-lookup"><span data-stu-id="0403f-193">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="0403f-194">Приложению требуется JAR-файл зависимостей, а точнее **JAR-файл драйвера JDBC**.</span><span class="sxs-lookup"><span data-stu-id="0403f-194">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="0403f-195">Этот файл необходим для записи сообщений, полученных из концентратора событий, в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0403f-195">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="0403f-196">Этот JAR-файл (версии 4.1 или более поздней) можно скачать [здесь](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="0403f-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="0403f-197">Добавьте ссылку на этот JAR-файл в библиотеке проекта.</span><span class="sxs-lookup"><span data-stu-id="0403f-197">Add reference to this jar in the project library.</span></span> <span data-ttu-id="0403f-198">Выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0403f-198">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="0403f-199">В окне IntelliJ IDEA, где открыто приложение, щелкните **File** (Файл), выберите **Project Structure** (Структура проекта) и щелкните **Libraries** (Библиотеки).</span><span class="sxs-lookup"><span data-stu-id="0403f-199">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="0403f-200">Щелкните значок "Добавить" (![добавление значка](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), выберите **Java**и перейдите в папку, куда вы скачали JAR-файл драйвера JDBC.</span><span class="sxs-lookup"><span data-stu-id="0403f-200">Click the add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="0403f-201">Следуйте инструкциям, чтобы добавить JAR-файл в библиотеку проектов.</span><span class="sxs-lookup"><span data-stu-id="0403f-201">Follow the prompts to add the jar file to the project library.</span></span>

         <span data-ttu-id="0403f-202">![добавление отсутствующих зависимостей](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Добавление отсутствующих JAR-файлов зависимостей")</span><span class="sxs-lookup"><span data-stu-id="0403f-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="0403f-203">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="0403f-203">Click **Apply**.</span></span>

7. <span data-ttu-id="0403f-204">Создайте выходной JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="0403f-204">Create the output jar file.</span></span> <span data-ttu-id="0403f-205">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0403f-205">Perform the following steps.</span></span>

   1. <span data-ttu-id="0403f-206">В диалоговом окне **Project Structure** (Структура проекта) выберите **Artifacts** (Артефакты) и щелкните знак плюса.</span><span class="sxs-lookup"><span data-stu-id="0403f-206">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="0403f-207">Во всплывающем диалоговом окне щелкните **JAR**, а затем выберите **From modules with dependencies** (На основе модулей с зависимостями).</span><span class="sxs-lookup"><span data-stu-id="0403f-207">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="0403f-208">![Пример приложения потоковой передачи Apache Spark. Создание JAR-файла](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Пример приложения потоковой передачи Apache Spark. Создание JAR-файла")</span><span class="sxs-lookup"><span data-stu-id="0403f-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="0403f-209">В диалоговом окне **Create JAR from Modules** (Создание JAR-файла на основе модулей) нажмите кнопку с многоточием (![многоточие](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) возле пункта **Main Class** (Основной класс).</span><span class="sxs-lookup"><span data-stu-id="0403f-209">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="0403f-210">В диалоговом окне **Select Main Class** (Выбор основного класса) выберите любой из доступных классов и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0403f-210">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="0403f-211">![Пример приложения потоковой передачи Apache Spark. Выбор класса JAR-файла](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Пример приложения потоковой передачи Apache Spark. Выбор класса JAR-файла")</span><span class="sxs-lookup"><span data-stu-id="0403f-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="0403f-212">В диалоговом окне **Create JAR from Modules** (Создание JAR-файла на основе модулей) установите переключатель **extract to the target JAR** (Извлечь в целевой JAR-файл) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0403f-212">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="0403f-213">В результате будет создан один JAR-файл, содержащий все зависимости.</span><span class="sxs-lookup"><span data-stu-id="0403f-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="0403f-214">![Пример приложения потоковой передачи Apache Spark. Создание JAR-файла на основе модулей](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Пример приложения потоковой передачи Apache Spark. Создание JAR-файла на основе модулей")</span><span class="sxs-lookup"><span data-stu-id="0403f-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="0403f-215">На вкладке **Макет выходных данных** содержится список всех JAR-файлов, которые включены в проект Maven.</span><span class="sxs-lookup"><span data-stu-id="0403f-215">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="0403f-216">Здесь можно выбрать и удалить файлы, от которых не зависит работа приложения Scala.</span><span class="sxs-lookup"><span data-stu-id="0403f-216">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="0403f-217">Для создаваемого приложения можно удалить все файлы, кроме последнего (**spark-streaming-data-persistence-examples compile output**).</span><span class="sxs-lookup"><span data-stu-id="0403f-217">For the application we are creating here, you can remove all but the last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="0403f-218">Выберите JAR-файлы, которые нужно удалить, и щелкните значок **удаления** (![значок удаления](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="0403f-218">Select the jars to delete and then click the **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="0403f-219">![Пример приложения потоковой передачи Apache Spark. Удаление извлеченных JAR-файлов](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Пример приложения потоковой передачи Apache Spark. Удаление извлеченных JAR-файлов")</span><span class="sxs-lookup"><span data-stu-id="0403f-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="0403f-220">Установите флажок **Build on make** («Сборка на основе созданного»), чтобы JAR-файл создавался при каждом создании и обновлении проекта.</span><span class="sxs-lookup"><span data-stu-id="0403f-220">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="0403f-221">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="0403f-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="0403f-222">На вкладке **Output Layout** (Макет выходных данных) под полем **Available Elements** (Доступные элементы) отображается JAR-файл SQL JDBC, ранее добавленный в библиотеку проекта.</span><span class="sxs-lookup"><span data-stu-id="0403f-222">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="0403f-223">Его необходимо добавить на вкладку **Output Layout** (Макет выходных данных). Щелкните JAR-файл правой кнопкой мыши и выберите пункт **Extract Into Output Root**(Извлечь в корень выходных данных).</span><span class="sxs-lookup"><span data-stu-id="0403f-223">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="0403f-224">![Пример приложения потоковой передачи Apache Spark. Извлечение JAR-файла зависимостей](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Пример приложения потоковой передачи Apache Spark. Извлечение JAR-файла зависимостей")</span><span class="sxs-lookup"><span data-stu-id="0403f-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="0403f-225">Вкладка **макета выходных данных** теперь должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0403f-225">The **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="0403f-226">![Пример приложения потоковой передачи Apache Spark. Вкладка окончательных выходных данных](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Пример приложения потоковой передачи Apache Spark. Вкладка окончательных выходных данных")</span><span class="sxs-lookup"><span data-stu-id="0403f-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="0403f-227">В диалоговом окне **Project Structure** (Структура проекта) нажмите кнопку **Применить**, а затем — **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0403f-227">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="0403f-228">В строке меню щелкните **Build** (Сборка) и выберите **Make Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="0403f-228">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="0403f-229">Кроме того, можно щелкнуть **Build Artifacts** («Сборка артефактов»), чтобы создать JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="0403f-229">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="0403f-230">Выходной JAR-файл создается в разделе **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="0403f-230">The output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="0403f-231">![Пример приложения потоковой передачи Apache Spark. Выходной JAR-файл](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Пример приложения потоковой передачи Apache Spark. Выходной JAR-файл")</span><span class="sxs-lookup"><span data-stu-id="0403f-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-the-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="0403f-232">Удаленный запуск приложений с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="0403f-232">Run the application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="0403f-233">В этой статье для удаленного запуска приложения потоковой передачи Apache Spark на кластере Spark используется Livy.</span><span class="sxs-lookup"><span data-stu-id="0403f-233">In this article you use Livy to run the Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="0403f-234">Подробное описание использования Livy с кластером HDInsight Spark см. в статье [Удаленная отправка заданий Spark в кластер Apache Spark в HDInsight на платформе Linux с помощью Livy](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="0403f-234">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="0403f-235">Перед запуском приложения потоковой передачи Apache Spark сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0403f-235">Before you can start running the Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="0403f-236">Запустите локальное автономное приложение для создания и отправки событий в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="0403f-236">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="0403f-237">Используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0403f-237">Use the following command to do so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="0403f-238">Скопируйте JAR-файл потоковой передачи (**spark-streaming-data-persistence-examples.jar**) в хранилище BLOB-объектов Azure, связанное с кластером.</span><span class="sxs-lookup"><span data-stu-id="0403f-238">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="0403f-239">Таким образом JAR-файл станет доступным для Livy.</span><span class="sxs-lookup"><span data-stu-id="0403f-239">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="0403f-240">Вы можете использовать для этого служебную программу командной строки [**AzCopy**](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="0403f-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="0403f-241">Кроме того, для отправки данных вы можете использовать множество других клиентов.</span><span class="sxs-lookup"><span data-stu-id="0403f-241">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="0403f-242">Дополнительные сведения о них см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="0403f-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="0403f-243">Установите служебную программу cURL на компьютере, где выполняются эти приложения.</span><span class="sxs-lookup"><span data-stu-id="0403f-243">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="0403f-244">Эта программа понадобится нам, чтобы вызывать конечные точки Livy для удаленного выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="0403f-244">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-spark-streaming-application-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="0403f-245">Запуск приложения потоковой передачи Spark для отправки событий в Azure Storage Blob в виде текста</span><span class="sxs-lookup"><span data-stu-id="0403f-245">Run the Spark streaming application to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="0403f-246">Откройте командную строку, перейдите в каталог, где установлена программа cURL, и выполните следующую команду (введите соответствующие имя пользователя, пароль и имя кластера):</span><span class="sxs-lookup"><span data-stu-id="0403f-246">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="0403f-247">Параметры в файле **inputBlob.txt** определяются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0403f-247">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="0403f-248">Ниже приведено описание параметров во входном файле.</span><span class="sxs-lookup"><span data-stu-id="0403f-248">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="0403f-249">**file** — путь к JAR-файлу приложения в учетной записи хранения Azure, связанной с кластером.</span><span class="sxs-lookup"><span data-stu-id="0403f-249">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="0403f-250">**className** — имя класса в JAR-файле.</span><span class="sxs-lookup"><span data-stu-id="0403f-250">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="0403f-251">**args** — список аргументов, требуемых для класса.</span><span class="sxs-lookup"><span data-stu-id="0403f-251">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="0403f-252">**numExecutors** — количество ядер, используемых Spark для запуска приложения потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="0403f-252">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="0403f-253">Это количество должно быть по крайней мере в два раза больше числа разделов в концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="0403f-253">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="0403f-254">**executorMemory**, **executorCores**, **driverMemory** — параметры, используемые для назначения необходимых ресурсов приложению потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="0403f-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="0403f-255">Вам не нужно создавать выходные папки (EventCheckpoint, EventCount или EventCount10), используемые в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="0403f-255">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="0403f-256">Приложение потоковой передачи создаст их самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="0403f-256">The streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="0403f-257">После выполнения команды вы должны увидеть следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0403f-257">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="0403f-258">Запишите идентификатор пакетной службы, указанный в последней строке выходных данных (в данном примере — 1).</span><span class="sxs-lookup"><span data-stu-id="0403f-258">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="0403f-259">Чтобы убедиться, что приложение выполняется успешно, зайдите в учетную запись хранения Azure, связанную с кластером. Там должна быть создана папка **/EventCount/EventCount10**.</span><span class="sxs-lookup"><span data-stu-id="0403f-259">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="0403f-260">В этой папке должны содержаться большие двоичные объекты, которые записывают число событий, обработанных в течение периода времени, заданного для параметра **batch-interval-in-seconds**.</span><span class="sxs-lookup"><span data-stu-id="0403f-260">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="0403f-261">Приложение потоковой передачи Spark будет продолжать работу, пока вы не остановите его.</span><span class="sxs-lookup"><span data-stu-id="0403f-261">The Spark streaming application will continue to run until you kill it.</span></span> <span data-ttu-id="0403f-262">Используйте для этого следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0403f-262">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="0403f-263">Запуск приложений для отправки событий в большой двоичный объект службы хранилища Azure в виде JSON-файла</span><span class="sxs-lookup"><span data-stu-id="0403f-263">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="0403f-264">Откройте командную строку, перейдите в каталог, где установлена программа cURL, и выполните следующую команду (введите соответствующие имя пользователя, пароль и имя кластера):</span><span class="sxs-lookup"><span data-stu-id="0403f-264">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="0403f-265">Параметры в файле **inputJSON.txt** определяются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0403f-265">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="0403f-266">Параметры аналогичны тем, которые вы указали для выходного текстового файла на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="0403f-266">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="0403f-267">Опять же, вам не нужно создавать выходные папки (EventCheckpoint, EventCount или EventCount10), используемые в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="0403f-267">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="0403f-268">Приложение потоковой передачи создаст их самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="0403f-268">The streaming application creates them for you.</span></span>

 <span data-ttu-id="0403f-269">После выполнения команды зайдите в учетную запись хранения Azure, связанную с кластером. Там должна быть создана папка **EventStore10**.</span><span class="sxs-lookup"><span data-stu-id="0403f-269">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="0403f-270">Откройте любой файл с префиксом **part-**. Там будут содержаться события, обработанные в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="0403f-270">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="0403f-271">Запуск приложений для отправки событий в таблицу Hive</span><span class="sxs-lookup"><span data-stu-id="0403f-271">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="0403f-272">Для запуска приложения потоковой передачи Spark, которое передает события потоком в таблицу Hive, требуются некоторые дополнительные компоненты,</span><span class="sxs-lookup"><span data-stu-id="0403f-272">To run the Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="0403f-273">а именно:</span><span class="sxs-lookup"><span data-stu-id="0403f-273">These are:</span></span>

* <span data-ttu-id="0403f-274">datanucleus-api-jdo-3.2.6.jar;</span><span class="sxs-lookup"><span data-stu-id="0403f-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="0403f-275">datanucleus-rdbms-3.2.9.jar;</span><span class="sxs-lookup"><span data-stu-id="0403f-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="0403f-276">datanucleus-core-3.2.10.jar;</span><span class="sxs-lookup"><span data-stu-id="0403f-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="0403f-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="0403f-277">hive-site.xml</span></span>

<span data-ttu-id="0403f-278">**JAR**-файлы доступны в кластере HDInsight Spark в каталоге `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="0403f-278">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="0403f-279">Файл **hive-site.xml** доступен в каталоге `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="0403f-279">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="0403f-280">С помощью клиента [WinScp](http://winscp.net/eng/download.php) можно копировать эти файлы из кластера на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="0403f-280">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="0403f-281">Затем их можно копировать в учетную запись хранения, связанную с кластером, используя соответствующие инструменты.</span><span class="sxs-lookup"><span data-stu-id="0403f-281">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="0403f-282">Дополнительные сведения об отправке файлов в учетную запись хранения см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="0403f-282">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="0403f-283">Скопировав файлы в учетную запись хранения Azure, откройте командную строку, перейдите в каталог, где установлена программа cURL, и выполните следующую команду (введите соответствующие имя пользователя, пароль и имя кластера):</span><span class="sxs-lookup"><span data-stu-id="0403f-283">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="0403f-284">Параметры в файле **inputHive.txt** определяются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0403f-284">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="0403f-285">Параметры аналогичны тем, которые вы указали для выходного текстового файла на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="0403f-285">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="0403f-286">Опять же, вам не нужно создавать выходные папки (EventCheckpoint, EventCount или EventCount10) или выходную таблицу (Hive EventHiveTable10), используемые в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="0403f-286">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="0403f-287">Приложение потоковой передачи создаст их самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="0403f-287">The streaming application creates them for you.</span></span> <span data-ttu-id="0403f-288">Обратите внимание, что в параметрах **jars** и **files** содержатся пути к JAR-файлам и файлу hive-site.xml, скопированным в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="0403f-288">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="0403f-289">Чтобы убедиться, что таблица Hive успешно создана, подключитесь к кластеру по SSH и выполните запросы Hive.</span><span class="sxs-lookup"><span data-stu-id="0403f-289">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="0403f-290">Инструкции см. в статье [Использование Hive с Hadoop в HDInsight с применением протокола SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="0403f-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="0403f-291">Подключившись с использованием SSH, можно выполнить следующую команду, чтобы убедиться, что таблица Hive, **EventHiveTable10**, создана.</span><span class="sxs-lookup"><span data-stu-id="0403f-291">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="0403f-292">Должен отобразиться результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="0403f-292">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="0403f-293">Можно также выполнить запрос SELECT, чтобы просмотреть содержимое таблицы.</span><span class="sxs-lookup"><span data-stu-id="0403f-293">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="0403f-294">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0403f-294">You should see an output like the following:</span></span>

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


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="0403f-295">Запуск приложений для отправки событий в таблицу базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0403f-295">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="0403f-296">Прежде чем выполнять этот шаг, убедитесь, что у вас есть созданная база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0403f-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="0403f-297">Инструкции см. в статье [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0403f-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="0403f-298">Чтобы завершить работу с этим разделом, укажите в качестве параметров имя базы данных, имя сервера базы данных и учетные данные администратора базы данных.</span><span class="sxs-lookup"><span data-stu-id="0403f-298">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="0403f-299">Однако создавать таблицу базы данных не нужно.</span><span class="sxs-lookup"><span data-stu-id="0403f-299">You do not need to create the database table though.</span></span> <span data-ttu-id="0403f-300">Приложение потоковой передачи Spark создаст ее самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="0403f-300">The Spark streaming application creates that for you.</span></span>

<span data-ttu-id="0403f-301">Откройте командную строку, перейдите в каталог, где установлена программа cURL, и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0403f-301">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="0403f-302">Параметры в файле **inputSQL.txt** определяются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0403f-302">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="0403f-303">Чтобы убедиться, что приложение выполняется успешно, подключитесь к базе данных SQL Azure с помощью SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="0403f-303">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="0403f-304">Соответствующие инструкции см. в статье [Подключение к базе данных SQL с помощью SQL Server Management Studio и выполнение пробного запроса T-SQL](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="0403f-304">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="0403f-305">После подключения к базе данных можно перейти в таблицу **EventContent**, созданную с помощью приложения потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="0403f-305">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="0403f-306">Для получения данных из таблицы используется быстрый запрос.</span><span class="sxs-lookup"><span data-stu-id="0403f-306">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="0403f-307">Выполните следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="0403f-307">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="0403f-308">Вы должны увидеть результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="0403f-308">You should see output similar to the following:</span></span>

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


## <span data-ttu-id="0403f-309"><a name="seealso"></a>Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="0403f-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="0403f-310">Обзор: Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0403f-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="0403f-311">Проектирование подключения на основе приемника и Direct DStream</span><span class="sxs-lookup"><span data-stu-id="0403f-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="0403f-312">Сценарии</span><span class="sxs-lookup"><span data-stu-id="0403f-312">Scenarios</span></span>
* [<span data-ttu-id="0403f-313">Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики</span><span class="sxs-lookup"><span data-stu-id="0403f-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0403f-314">Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования</span><span class="sxs-lookup"><span data-stu-id="0403f-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0403f-315">Использование Spark с машинным обучением. Использование Spark в HDInsight для прогнозирования результатов контроля качества пищевых продуктов</span><span class="sxs-lookup"><span data-stu-id="0403f-315">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0403f-316">Анализ журнала веб-сайта с использованием Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0403f-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="0403f-317">Создание и запуск приложений</span><span class="sxs-lookup"><span data-stu-id="0403f-317">Create and run applications</span></span>
* [<span data-ttu-id="0403f-318">Создание автономного приложения с использованием Scala</span><span class="sxs-lookup"><span data-stu-id="0403f-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0403f-319">Удаленный запуск заданий с помощью Livy в кластере Spark</span><span class="sxs-lookup"><span data-stu-id="0403f-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0403f-320">Средства и расширения</span><span class="sxs-lookup"><span data-stu-id="0403f-320">Tools and extensions</span></span>
* [<span data-ttu-id="0403f-321">Использование подключаемого модуля средств HDInsight для IntelliJ IDEA для создания и отправки приложений Spark Scala</span><span class="sxs-lookup"><span data-stu-id="0403f-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0403f-322">Удаленная отладка приложений Spark в кластере HDInsight Spark Linux с помощью подключаемого модуля средств HDInsight для IntelliJ IDEA</span><span class="sxs-lookup"><span data-stu-id="0403f-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0403f-323">Использование записных книжек Zeppelin с кластером Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0403f-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0403f-324">Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0403f-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0403f-325">Использование внешних пакетов с записными книжками Jupyter</span><span class="sxs-lookup"><span data-stu-id="0403f-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0403f-326">Установка записной книжки Jupyter на компьютере и ее подключение к кластеру Apache Spark в Azure HDInsight (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="0403f-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="0403f-327">Управление ресурсами</span><span class="sxs-lookup"><span data-stu-id="0403f-327">Manage resources</span></span>
* [<span data-ttu-id="0403f-328">Управление ресурсами кластера Apache Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0403f-328">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0403f-329">Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="0403f-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
