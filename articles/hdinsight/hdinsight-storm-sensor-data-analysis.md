---
title: "Анализ полученных с датчиков данных с помощью Apache Storm и HBase | Документация Майкрософт"
description: "В этой статье вы узнаете, как подключить к Apache Storm к виртуальной сети. Используйте Storm с HBase для обработки данных датчиков из концентратора событий и их визуализации с помощью D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: 0d1cc959c87bd64ed728f8b56c9b9156fa492a8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="a8383-104">Анализ полученных с датчиков данных с использованием Apache Storm, концентратора событий и базы данных HBase в службе HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="a8383-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="a8383-105">Узнайте, как с помощью Apache Storm в HDInsight можно обрабатывать данные датчиков из концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="a8383-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span></span> <span data-ttu-id="a8383-106">Эти данные можно сохранить в Apache HBase в HDInsight и визуализировать с помощью D3.js.</span><span class="sxs-lookup"><span data-stu-id="a8383-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="a8383-107">С помощью шаблона Azure Resource Manager, используемого в этом документе, показывается, как создать несколько ресурсов Azure в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8383-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span></span> <span data-ttu-id="a8383-108">Этот шаблон создает виртуальную сеть Azure, два кластера HDInsight (Storm и HBase) и веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="a8383-108">The template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="a8383-109">Реализация node.js панели мониторинга в реальном времени автоматически развертывается в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="a8383-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="a8383-110">Для работы с этим документом требуется HDInsight версии 3.6.</span><span class="sxs-lookup"><span data-stu-id="a8383-110">The information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="a8383-111">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a8383-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a8383-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a8383-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8383-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8383-113">Prerequisites</span></span>

* <span data-ttu-id="a8383-114">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a8383-114">An Azure subscription.</span></span>
* <span data-ttu-id="a8383-115">[Node.js](http://nodejs.org/): используется для локального предварительного просмотра веб-панели мониторинга в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="a8383-115">[Node.js](http://nodejs.org/): Used to preview the web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="a8383-116">[Java и пакет JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): используется для разработки топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="a8383-116">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span></span>
* <span data-ttu-id="a8383-117">[Maven](http://maven.apache.org/what-is-maven.html): используется для создания и компиляции проекта.</span><span class="sxs-lookup"><span data-stu-id="a8383-117">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span></span>
* <span data-ttu-id="a8383-118">[Git](http://git-scm.com/): используется для скачивания проекта с сайта GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8383-118">[Git](http://git-scm.com/): Used to download the project from GitHub.</span></span>
* <span data-ttu-id="a8383-119">Клиент **SSH**: используется для подключения к кластерам HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="a8383-119">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="a8383-120">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a8383-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="a8383-121">Вам не нужен существующий кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="a8383-122">В этом документе описаны действия по созданию следующие ресурсов:</span><span class="sxs-lookup"><span data-stu-id="a8383-122">The steps in this document create the following resources:</span></span>
> 
> * <span data-ttu-id="a8383-123">виртуальная сеть Azure;</span><span class="sxs-lookup"><span data-stu-id="a8383-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="a8383-124">кластер Storm в HDInsight (под управлением Linux, с двумя рабочими узлами);</span><span class="sxs-lookup"><span data-stu-id="a8383-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="a8383-125">кластер HBase в HDInsight (под управлением Linux, с двумя рабочими узлами);</span><span class="sxs-lookup"><span data-stu-id="a8383-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="a8383-126">веб-приложение Azure, в котором размещается панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a8383-126">An Azure Web App that hosts the web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="a8383-127">Архитектура</span><span class="sxs-lookup"><span data-stu-id="a8383-127">Architecture</span></span>

![схема архитектуры](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="a8383-129">В этом примере используются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="a8383-129">This example consists of the following components:</span></span>

* <span data-ttu-id="a8383-130">**Концентраторы событий Azure**: содержат собираемые с датчиков данные.</span><span class="sxs-lookup"><span data-stu-id="a8383-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="a8383-131">**Storm в HDInsight**: в реальном времени обрабатывает данные, получаемые из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="a8383-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="a8383-132">**HBase в HDInsight.**Обеспечивает постоянное хранилище данных NoSQL для данных, обработанных Storm.</span><span class="sxs-lookup"><span data-stu-id="a8383-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="a8383-133">**Служба виртуальной сети Azure**: обеспечивает безопасный обмен данными между кластерами Storm в HDInsight и HBase в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-133">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a8383-134">Виртуальная сеть требуется при использовании клиентского API Java для HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-134">A virtual network is required when using the Java HBase client API.</span></span> <span data-ttu-id="a8383-135">Она не предоставляется через общедоступный шлюз для кластеров HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-135">It is not exposed over the public gateway for HBase clusters.</span></span> <span data-ttu-id="a8383-136">Установка кластеров HBase и Storm в одной виртуальной сети позволяет кластеру Storm (или любой другой системе в виртуальной сети) обращаться непосредственно к кластеру HBase с помощью клиентского API.</span><span class="sxs-lookup"><span data-stu-id="a8383-136">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span></span>

* <span data-ttu-id="a8383-137">**Веб-сайт панели мониторинга**: пример панели мониторинга, на которой в режиме реального времени строятся диаграммы на основе полученных данных.</span><span class="sxs-lookup"><span data-stu-id="a8383-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="a8383-138">Веб-сайт реализован в Node.js.</span><span class="sxs-lookup"><span data-stu-id="a8383-138">The website is implemented in Node.js.</span></span>
  * <span data-ttu-id="a8383-139">[Socket.io](http://socket.io/) .</span><span class="sxs-lookup"><span data-stu-id="a8383-139">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a8383-140">Использование Socket.io для связи относится к тонкостям реализации.</span><span class="sxs-lookup"><span data-stu-id="a8383-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="a8383-141">На практике можно использовать любую платформу, например сокеты прямого доступа WebSocket или SignalR.</span><span class="sxs-lookup"><span data-stu-id="a8383-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="a8383-142">[D3.js](http://d3js.org/) .</span><span class="sxs-lookup"><span data-stu-id="a8383-142">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8383-143">Требуются два кластера, так как метода для создания одного кластера HDInsight для Storm и для HBase не существует.</span><span class="sxs-lookup"><span data-stu-id="a8383-143">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="a8383-144">Топология считывает данные из концентратора событий с помощью класса [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) и записывает их в HBase с помощью класса [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html).</span><span class="sxs-lookup"><span data-stu-id="a8383-144">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="a8383-145">Связь с веб-сайтом реализована с использованием библиотеки [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="a8383-145">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="a8383-146">На следующей схеме поясняется структура топологии.</span><span class="sxs-lookup"><span data-stu-id="a8383-146">The following diagram explains the layout of the topology:</span></span>

![схема топологии](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="a8383-148">Это упрощенное представление топологии.</span><span class="sxs-lookup"><span data-stu-id="a8383-148">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="a8383-149">Для каждого раздела концентратора событий создается экземпляр каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="a8383-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="a8383-150">Экземпляры распределяются между узлами в кластере. Обмен данными между ними выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a8383-150">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="a8383-151">Данные из «воронки» равномерно передаются в средство синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="a8383-151">Data from the spout to the parser is load balanced.</span></span>
> * <span data-ttu-id="a8383-152">Данные из средства синтаксического анализа передаются в панель мониторинга и базу данных HBase. Данные группируются по идентификатору устройства, чтобы сообщения с одного устройства всегда перенаправлялись в один и тот же компонент.</span><span class="sxs-lookup"><span data-stu-id="a8383-152">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="a8383-153">Компоненты топологии</span><span class="sxs-lookup"><span data-stu-id="a8383-153">Topology components</span></span>

* <span data-ttu-id="a8383-154">**Компонент концентратора событий spout**: входит в состав Apache Storm версии 0.10.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="a8383-154">**Event Hub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a8383-155">Для работы этого компонента, используемого в нашем примере, требуется кластер Storm в HDInsight версии 3.5 или 3.6.</span><span class="sxs-lookup"><span data-stu-id="a8383-155">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="a8383-156">**ParserBolt.java**: из воронки отправляются необработанные данные JSON. Иногда за один раз может отправляться сразу несколько событий.</span><span class="sxs-lookup"><span data-stu-id="a8383-156">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="a8383-157">Этот компонент bolt считывает данные, генерируемые компонентом spout, и выполняет синтаксический анализ сообщения JSON.</span><span class="sxs-lookup"><span data-stu-id="a8383-157">This bolt reads the data emitted by the spout and parses the JSON message.</span></span> <span data-ttu-id="a8383-158">Затем компонент bolt передает данные как кортеж, содержащий несколько полей.</span><span class="sxs-lookup"><span data-stu-id="a8383-158">The bolt then emits the data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="a8383-159">**DashboardBolt.java**: этот компонент показывает, как использовать клиентскую библиотеку Socket.io для Java для отправки данных в реальном времени в веб-панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a8383-159">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span></span>
* <span data-ttu-id="a8383-160">**no-hbase.yaml**: определение топологии, используемое во время выполнения в локальном режиме.</span><span class="sxs-lookup"><span data-stu-id="a8383-160">**no-hbase.yaml**: The topology definition used when running in local mode.</span></span> <span data-ttu-id="a8383-161">Компоненты HBase при этом не используются.</span><span class="sxs-lookup"><span data-stu-id="a8383-161">It does not use HBase components.</span></span>
* <span data-ttu-id="a8383-162">**with-hbase.yaml**: определение топологии, используемое во время выполнения топологии в кластере.</span><span class="sxs-lookup"><span data-stu-id="a8383-162">**with-hbase.yaml**: The topology definition used when running the topology on the cluster.</span></span> <span data-ttu-id="a8383-163">Компоненты HBase при этом используются.</span><span class="sxs-lookup"><span data-stu-id="a8383-163">It does use HBase components.</span></span>
* <span data-ttu-id="a8383-164">**dev.properties**: сведения о конфигурации для компонента spout концентратора событий, компонента bolt HBase и компонентов панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a8383-164">**dev.properties**: The configuration information for the Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="a8383-165">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="a8383-165">Prepare your environment</span></span>

<span data-ttu-id="a8383-166">Прежде чем использовать этот пример, необходимо создать концентратор событий Azure, из которого топология Storm будет считывать данные.</span><span class="sxs-lookup"><span data-stu-id="a8383-166">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="a8383-167">Настройка концентраторов Event Hub</span><span class="sxs-lookup"><span data-stu-id="a8383-167">Configure Event Hub</span></span>

<span data-ttu-id="a8383-168">В этом примере концентратор событий выступает в роли источника данных.</span><span class="sxs-lookup"><span data-stu-id="a8383-168">Event Hub is the data source for this example.</span></span> <span data-ttu-id="a8383-169">Чтобы создать концентратор событий, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a8383-169">Use the following steps to create an Event Hub.</span></span>

1. <span data-ttu-id="a8383-170">На [портале Azure](https://portal.azure.com) выберите **+ Создать** -> **Интернет вещей** -> **Концентраторы событий**.</span><span class="sxs-lookup"><span data-stu-id="a8383-170">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="a8383-171">В колонке **Создание пространства имен** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a8383-171">In the **Create Namespace** section, perform the following tasks:</span></span>
   
   1. <span data-ttu-id="a8383-172">В поле **Имя** введите имя для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="a8383-172">Enter a **Name** for the namespace.</span></span>
   2. <span data-ttu-id="a8383-173">Выберите ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="a8383-173">Select a pricing tier.</span></span> <span data-ttu-id="a8383-174">**Базовый** подойдет для этого примера.</span><span class="sxs-lookup"><span data-stu-id="a8383-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="a8383-175">В поле **Подписка** выберите подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="a8383-175">Select the Azure **Subscription** to use.</span></span>
   4. <span data-ttu-id="a8383-176">Создайте группу ресурсов или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="a8383-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="a8383-177">В поле **Расположение** выберите расположение для концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="a8383-177">Select the **Location** for the Event Hub.</span></span>
   6. <span data-ttu-id="a8383-178">Выберите **Закрепить на панели мониторинга** и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8383-178">Select **Pin to dashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="a8383-179">По завершении создания отобразятся сведения о концентраторах событий для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="a8383-179">When the creation process completes, the Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="a8383-180">В этой колонке выберите **+ Add Event Hub**(+ Добавить концентратор событий).</span><span class="sxs-lookup"><span data-stu-id="a8383-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="a8383-181">В разделе **Создание концентратора событий** введите имя **sensordata**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8383-181">In the **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="a8383-182">Оставьте в остальных полях значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8383-182">Leave the other fields at the default values.</span></span>
4. <span data-ttu-id="a8383-183">В представлении "Концентраторы событий" для пространства имен выберите **Концентраторы событий**.</span><span class="sxs-lookup"><span data-stu-id="a8383-183">From the Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="a8383-184">Выберите запись **sensordata** .</span><span class="sxs-lookup"><span data-stu-id="a8383-184">Select the **sensordata** entry.</span></span>
5. <span data-ttu-id="a8383-185">В представлении для sensordata концентратора событий выберите **Политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="a8383-185">From the sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="a8383-186">Воспользуйтесь ссылкой **+ Добавить** , чтобы добавить следующие политики.</span><span class="sxs-lookup"><span data-stu-id="a8383-186">Use the **+ Add** link to add the following policies:</span></span>

    | <span data-ttu-id="a8383-187">Имя политики</span><span class="sxs-lookup"><span data-stu-id="a8383-187">Policy name</span></span> | <span data-ttu-id="a8383-188">Claims</span><span class="sxs-lookup"><span data-stu-id="a8383-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="a8383-189">устройства</span><span class="sxs-lookup"><span data-stu-id="a8383-189">devices</span></span> | <span data-ttu-id="a8383-190">Отправка</span><span class="sxs-lookup"><span data-stu-id="a8383-190">Send</span></span> |
    | <span data-ttu-id="a8383-191">storm</span><span class="sxs-lookup"><span data-stu-id="a8383-191">storm</span></span> | <span data-ttu-id="a8383-192">Прослушивание</span><span class="sxs-lookup"><span data-stu-id="a8383-192">Listen</span></span> |

1. <span data-ttu-id="a8383-193">Выберите обе политики и запишите значение параметра **Первичный ключ** .</span><span class="sxs-lookup"><span data-stu-id="a8383-193">Select both policies and make a note of the **PRIMARY KEY** value.</span></span> <span data-ttu-id="a8383-194">При выполнении следующих шагов понадобятся значения обеих политик.</span><span class="sxs-lookup"><span data-stu-id="a8383-194">You need the value for both policies in future steps.</span></span>

## <a name="download-and-configure-the-project"></a><span data-ttu-id="a8383-195">Скачивание и настройка проекта</span><span class="sxs-lookup"><span data-stu-id="a8383-195">Download and configure the project</span></span>

<span data-ttu-id="a8383-196">Для скачивания проекта с GitHub выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a8383-196">Use the following to download the project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="a8383-197">После выполнения команды структура каталогов будет следующей:</span><span class="sxs-lookup"><span data-stu-id="a8383-197">After the command completes, you have the following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains the topology
            resources/
                log4j2.xml - set logging to minimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO to the web dashboard.
        dashboard/nodejs/ - this is the node.js web dashboard.
        SendEvents/ - utilities to send fake sensor data.

> [!NOTE]
> <span data-ttu-id="a8383-198">В этом документе не приводятся подробные сведения о коде примера.</span><span class="sxs-lookup"><span data-stu-id="a8383-198">This document does not go in to full details of the code included in this example.</span></span> <span data-ttu-id="a8383-199">Тем не менее, код содержит полные комментарии.</span><span class="sxs-lookup"><span data-stu-id="a8383-199">However, the code is fully commented.</span></span>

<span data-ttu-id="a8383-200">Чтобы настроить проект для чтения из концентратора событий, откройте файл `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` и добавьте сведения о концентраторе событий в следующие строки:</span><span class="sxs-lookup"><span data-stu-id="a8383-200">To configure the project to read from Event Hub, open the `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information to the following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="a8383-201">Локальная компиляция и тестирование</span><span class="sxs-lookup"><span data-stu-id="a8383-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8383-202">Для локального использования топологии требуется рабочая среда разработки Storm.</span><span class="sxs-lookup"><span data-stu-id="a8383-202">Using the topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="a8383-203">См. дополнительные сведения о [настройке среды разработки Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) на сайте Apache.org.</span><span class="sxs-lookup"><span data-stu-id="a8383-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="a8383-204">Если вы используете среду разработки Windows, при локальном выполнении топологии может возникнуть исключение `java.io.IOException`.</span><span class="sxs-lookup"><span data-stu-id="a8383-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running the topology locally.</span></span> <span data-ttu-id="a8383-205">В таком случае переключитесь на выполнение в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-205">If so, move on to running the topology on HDInsight.</span></span>

<span data-ttu-id="a8383-206">Перед началом тестирования вам необходимо запустить панель мониторинга, чтобы просмотреть выходные данные топологии и создать данные для хранения в концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="a8383-206">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8383-207">При локальном тестировании компонент HBase этой топологии неактивен.</span><span class="sxs-lookup"><span data-stu-id="a8383-207">The HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="a8383-208">Доступ к API Java для кластера HBase нельзя получить за пределами виртуальной сети Azure, содержащей кластеры.</span><span class="sxs-lookup"><span data-stu-id="a8383-208">The Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span></span>

### <a name="start-the-web-application"></a><span data-ttu-id="a8383-209">Запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a8383-209">Start the web application</span></span>

1. <span data-ttu-id="a8383-210">В командной строке измените каталог на `hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="a8383-210">Open a command prompt and change directories to `hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="a8383-211">Чтобы установить зависимости, необходимые для веб-приложения, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a8383-211">Use the following command to install the dependencies needed by the web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="a8383-212">Запустите веб-приложение с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="a8383-212">Use the following command to start the web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="a8383-213">Должно появиться сообщение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="a8383-213">You see a message similar to the following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="a8383-214">Откройте веб-браузер и введите `http://localhost:3000/` как адрес.</span><span class="sxs-lookup"><span data-stu-id="a8383-214">Open a web browser and enter `http://localhost:3000/` as the address.</span></span> <span data-ttu-id="a8383-215">Откроется страница, аналогичная следующей:</span><span class="sxs-lookup"><span data-stu-id="a8383-215">A page similar to the following image is displayed:</span></span>
   
    ![веб-панель мониторинга](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="a8383-217">Не закрывайте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="a8383-217">Leave this command prompt open.</span></span> <span data-ttu-id="a8383-218">После завершения тестирования остановите веб-сервер с помощью клавиш CTRL+C.</span><span class="sxs-lookup"><span data-stu-id="a8383-218">After testing, use Ctrl-C to stop the web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="a8383-219">Создание данных</span><span class="sxs-lookup"><span data-stu-id="a8383-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="a8383-220">Для описанных в этом разделе действий используется Node.js, поэтому эти действия могут выполняться на любой платформе.</span><span class="sxs-lookup"><span data-stu-id="a8383-220">The steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="a8383-221">Примеры для других языков см. в каталоге `SendEvents`.</span><span class="sxs-lookup"><span data-stu-id="a8383-221">For other language examples, see the `SendEvents` directory.</span></span>

1. <span data-ttu-id="a8383-222">Откройте новую строку, оболочку или окно терминала и измените каталог на `hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="a8383-222">Open a new prompt, shell, or terminal, and change directories to `hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="a8383-223">Чтобы установить зависимости, необходимые для веб-приложения, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a8383-223">To install the dependencies needed by the application, use the following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="a8383-224">Откройте файл `app.js` в текстовом редакторе и добавьте полученные ранее сведения о концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="a8383-224">Open the `app.js` file in a text editor and add the Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a8383-225">В этом примере предполагается, что вы использовали `sensordata` как имя концентратора событий</span><span class="sxs-lookup"><span data-stu-id="a8383-225">This example assumes that you have used `sensordata` as the name of your Event Hub.</span></span> <span data-ttu-id="a8383-226">и `devices` как имя политики с утверждением `Send`.</span><span class="sxs-lookup"><span data-stu-id="a8383-226">And that `devices` as the name of the policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="a8383-227">Для добавления новых записей в концентратор событий используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a8383-227">Use the following command to insert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="a8383-228">Вы должны увидеть несколько строк выходных данных, среди которых будет информация, отправленная в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="a8383-228">You see several lines of output that contain the data sent to Event Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-the-topology"></a><span data-ttu-id="a8383-229">Создание и запуск топологии</span><span class="sxs-lookup"><span data-stu-id="a8383-229">Build and start the topology</span></span>

1. <span data-ttu-id="a8383-230">В новой командной строке измените каталог на `hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="a8383-230">Open a new command prompt and change directories to `hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="a8383-231">Для сборки и создания пакета топологии выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8383-231">To build and package the topology, use the following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="a8383-232">Запустите топологию в локальном режиме с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="a8383-232">To start the topology in local mode, use the following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="a8383-233">Команда `--local` запускает топологию в локальном режиме.</span><span class="sxs-lookup"><span data-stu-id="a8383-233">`--local` starts the topology in local mode.</span></span>
    * <span data-ttu-id="a8383-234">Команда `--filter` использует файл `dev.properties` для указания значений параметров в определении топологии.</span><span class="sxs-lookup"><span data-stu-id="a8383-234">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="a8383-235">Команда `resources/no-hbase.yaml` использует определение топологии `no-hbase.yaml`.</span><span class="sxs-lookup"><span data-stu-id="a8383-235">`resources/no-hbase.yaml` uses the `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="a8383-236">После запуска топология считывает записи из концентратора событий и отправляет их на панель мониторинга, работающую на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8383-236">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span></span> <span data-ttu-id="a8383-237">На веб-панели мониторинга должны появиться линии, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="a8383-237">You should see lines appear in the web dashboard, similar to the following image:</span></span>
   
    ![панель мониторинга с данными](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="a8383-239">Не закрывая панель мониторинга, отправьте новые данные в концентраторы событий с помощью команды `node app.js` (использовалась на предыдущих шагах).</span><span class="sxs-lookup"><span data-stu-id="a8383-239">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span></span> <span data-ttu-id="a8383-240">Так как значения температуры генерируются случайным образом, граф будет изменяться, отображая значительные изменения температуры.</span><span class="sxs-lookup"><span data-stu-id="a8383-240">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a8383-241">Выполнять команду `node app.js` необходимо из каталога **hdinsight-eventhub-example/SendEvents/Nodejs**.</span><span class="sxs-lookup"><span data-stu-id="a8383-241">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span></span>

3. <span data-ttu-id="a8383-242">Убедившись, что панель мониторинга обновляется, остановите топологию, нажав клавиши CTRL+C.</span><span class="sxs-lookup"><span data-stu-id="a8383-242">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span></span> <span data-ttu-id="a8383-243">С помощью клавиш Ctrl+C можно также остановить локальный веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="a8383-243">You can use Ctrl+C to stop the local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="a8383-244">Создание кластеров Storm и HBase</span><span class="sxs-lookup"><span data-stu-id="a8383-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="a8383-245">В действиях, описанных в этом разделе, используется [шаблон Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) для создания виртуальной сети Azure, содержащей кластеры Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-245">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create an Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span></span> <span data-ttu-id="a8383-246">Шаблон также создает веб-приложение Azure и развертывает в нем копию панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="a8383-246">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="a8383-247">Виртуальная сеть используется для того, чтобы топология, запущенная на кластере Storm, могла непосредственно обмениваться данными с кластером HBase с помощью API Java для HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-247">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span></span>

<span data-ttu-id="a8383-248">Шаблон Resource Manager, используемый в этом документе, расположен в общедоступном контейнере BLOB-объектов по адресу **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="a8383-248">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="a8383-249">Нажмите следующую кнопку, чтобы войти в Azure и открыть шаблон Resource Manager на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a8383-249">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="a8383-250">В колонке **Настраиваемое развертывание** укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a8383-250">From the **Custom deployment** section, enter the following values:</span></span>
   
    ![Параметры HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="a8383-252">**Base Cluster Name** (Базовое имя кластера). Это значение будет использоваться в качестве базового имени для кластеров Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-252">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span></span> <span data-ttu-id="a8383-253">Например, если ввести **abc**, будут созданы кластер Storm **storm-abc** и кластер HBase **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="a8383-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="a8383-254">**Cluster Login User Name** (Имя пользователя для входа в кластер). Имя администратора для кластеров Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-254">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="a8383-255">**Cluster Login User Password** (Пароль пользователя для входа в кластер). Имя администратора для кластеров Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-255">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="a8383-256">**Имя пользователя SSH**. Создаваемый пользователь SSH для кластеров Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-256">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="a8383-257">**Пароль SSH**. Пароль пользователя SSH для кластеров Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-257">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="a8383-258">**Расположение.** Регион, в котором создаются кластеры.</span><span class="sxs-lookup"><span data-stu-id="a8383-258">**Location**: The region that the clusters are created in.</span></span>
     
     <span data-ttu-id="a8383-259">Нажмите кнопку **ОК** , чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="a8383-259">Click **OK** to save the parameters.</span></span>

3. <span data-ttu-id="a8383-260">В разделе **Основные** создайте новую группу ресурсов или выберите существующую.</span><span class="sxs-lookup"><span data-stu-id="a8383-260">Use the **Basics** section to create a resource group or select an existing one.</span></span>
4. <span data-ttu-id="a8383-261">Из раскрывающегося меню **Расположение группы ресурсов** выберите расположение, указанное в параметре **Расположение** в разделе **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="a8383-261">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span></span>
5. <span data-ttu-id="a8383-262">Прочтите условия использования и установите флажок **Я принимаю указанные выше условия**.</span><span class="sxs-lookup"><span data-stu-id="a8383-262">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span></span>
6. <span data-ttu-id="a8383-263">Установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="a8383-263">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="a8383-264">Процесс создания кластеров занимает около 20 минут.</span><span class="sxs-lookup"><span data-stu-id="a8383-264">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="a8383-265">Когда ресурсы будут созданы, отобразится колонка со сведениями о группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a8383-265">Once the resources have been created, information about the resource group is displayed.</span></span>

![Группа ресурсов для виртуальной сети и кластеров](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="a8383-267">Обратите внимание, что кластерам HDInsight присвоены имена **storm-BASENAME** и **hbase-BASENAME**, где BASENAME — имя, указанное в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="a8383-267">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="a8383-268">Эти имена будут использоваться позже при подключении к кластерам.</span><span class="sxs-lookup"><span data-stu-id="a8383-268">You use these names in a later step when connecting to the clusters.</span></span> <span data-ttu-id="a8383-269">Кроме того, обратите внимание, что имя сайта панели мониторинга — **basename-dashboard**.</span><span class="sxs-lookup"><span data-stu-id="a8383-269">Also note that the name of the dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="a8383-270">Это значение используется ниже в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a8383-270">This value is used later in this document.</span></span>

## <a name="configure-the-dashboard-bolt"></a><span data-ttu-id="a8383-271">Настройка сита панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="a8383-271">Configure the Dashboard bolt</span></span>

<span data-ttu-id="a8383-272">Для отправки данных в панель мониторинга, развернутую в виде веб-приложения, необходимо изменить в файле `dev.properties` следующую строку:</span><span class="sxs-lookup"><span data-stu-id="a8383-272">To send data to the dashboard deployed as a web app, you must modify the following line in the `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="a8383-273">Измените `http://localhost:3000` на `http://BASENAME-dashboard.azurewebsites.net` и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="a8383-273">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span></span> <span data-ttu-id="a8383-274">Замените **BASENAME** базовым именем, введенным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="a8383-274">Replace **BASENAME** with the base name you provided in the previous step.</span></span> <span data-ttu-id="a8383-275">Можно также использовать созданную ранее группу ресурсов, чтобы выбрать панель мониторинга и просмотреть URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a8383-275">You can also use the resource group created previously to select the dashboard and view the URL.</span></span>

## <a name="create-the-hbase-table"></a><span data-ttu-id="a8383-276">Создание таблицы HBase</span><span class="sxs-lookup"><span data-stu-id="a8383-276">Create the HBase table</span></span>

<span data-ttu-id="a8383-277">Чтобы хранить данные в HBase, необходимо сначала создать таблицу.</span><span class="sxs-lookup"><span data-stu-id="a8383-277">To store data in HBase, we must first create a table.</span></span> <span data-ttu-id="a8383-278">Заранее создайте ресурсы, в которые Storm будет записывать данные, так как попытка создать ресурсы изнутри топологии Storm может привести к тому, что несколько экземпляров попытаются создать один и тот же ресурс.</span><span class="sxs-lookup"><span data-stu-id="a8383-278">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span></span> <span data-ttu-id="a8383-279">Создайте эти ресурсы вне топологии и используйте Storm для чтения, записи и анализа данных.</span><span class="sxs-lookup"><span data-stu-id="a8383-279">Create the resources outside the topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="a8383-280">Используйте протокол SSH для подключения к кластеру с помощью пользователя SSH и его пароля, указанных в шаблоне при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="a8383-280">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span></span> <span data-ttu-id="a8383-281">Например, для подключения с помощью команды `ssh` необходимо использовать следующий синтаксис.</span><span class="sxs-lookup"><span data-stu-id="a8383-281">For example, if connecting using the `ssh` command, you would use the following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="a8383-282">Замените `sshuser` именем пользователя SSH, которое использовалось при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="a8383-282">Replace `sshuser` with the SSH user name you provided when creating the cluster.</span></span> <span data-ttu-id="a8383-283">Замените `clustername` именем кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-283">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="a8383-284">Из сеанса SSH запустите оболочку HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-284">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="a8383-285">После загрузки оболочки вы увидите запрос `hbase(main):001:0>`.</span><span class="sxs-lookup"><span data-stu-id="a8383-285">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="a8383-286">В оболочке HBase введите следующую команду, чтобы создать таблицу, в которой будут храниться данные с датчиков.</span><span class="sxs-lookup"><span data-stu-id="a8383-286">From the HBase shell, enter the following command to create a table to store the sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="a8383-287">Используйте следующую команду, чтобы проверить, создана ли таблица.</span><span class="sxs-lookup"><span data-stu-id="a8383-287">Verify that the table has been created by using the following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="a8383-288">Она вернет информацию, которая указывает на то, что в таблице 0 строк и выглядит примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="a8383-288">This returns information similar to the following example, indicating that there are 0 rows in the table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="a8383-289">Введите `exit` для выхода из оболочки HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-289">Enter `exit` to exit the HBase shell:</span></span>

## <a name="configure-the-hbase-bolt"></a><span data-ttu-id="a8383-290">Настройка сита HBase</span><span class="sxs-lookup"><span data-stu-id="a8383-290">Configure the HBase bolt</span></span>

<span data-ttu-id="a8383-291">Для записи данных в HBase из кластера Storm ситу HBase необходимо предоставить сведения о конфигурации кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-291">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="a8383-292">Чтобы получить кворум Zookeeper для кластера HBase, используйте один из следующих примеров:</span><span class="sxs-lookup"><span data-stu-id="a8383-292">Use one of the following examples to retrieve the Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="a8383-293">Замените `your_HDInsight_cluster_name` на имя вашего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-293">Replace `your_HDInsight_cluster_name` with the name of your HDInsight cluster.</span></span> <span data-ttu-id="a8383-294">См. дополнительные сведения об установке служебной программы `jq`: [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="a8383-294">For more information on installing the `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="a8383-295">При появлении запроса введите пароль администратора HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-295">When prompted, enter the password for the HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="a8383-296">Замените your_HDInsight_cluster_name именем своего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-296">Replace \`your_HDInsight_cluster_name with the name of your HDInsight cluster.</span></span> <span data-ttu-id="a8383-297">При появлении запроса введите пароль администратора HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a8383-297">When prompted, enter the password for the HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="a8383-298">Для этого примера требуется Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a8383-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="a8383-299">См. дополнительные сведения об [установке Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="a8383-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="a8383-300">Возвращаемая информация выглядит приблизительно так:</span><span class="sxs-lookup"><span data-stu-id="a8383-300">The information returned by these examples is similar to the following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="a8383-301">Эта информация используется Storm для обмена данными с кластером HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-301">This information is used by Storm to communicate with the HBase cluster.</span></span>

2. <span data-ttu-id="a8383-302">Измените файл `dev.properties` и добавьте сведения о кворуме Zookeeper в следующую строку:</span><span class="sxs-lookup"><span data-stu-id="a8383-302">Modify the `dev.properties` file and add the Zookeeper quorum information to the following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-the-solution-to-hdinsight"></a><span data-ttu-id="a8383-303">Выполнение сборки, упаковка и развертывание решения в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a8383-303">Build, package, and deploy the solution to HDInsight</span></span>

<span data-ttu-id="a8383-304">Выполните приведенные действия в своей среде разработки, чтобы развернуть топологию Storm в кластере Storm.</span><span class="sxs-lookup"><span data-stu-id="a8383-304">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span></span>

1. <span data-ttu-id="a8383-305">Из каталога `TemperatureMonitor` выполните следующую команду, чтобы создать пакет JAR из своего проекта:</span><span class="sxs-lookup"><span data-stu-id="a8383-305">From the `TemperatureMonitor` directory, use the following command to perform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="a8383-306">Эта команда создает файл с именем `TemperatureMonitor-1.0-SNAPSHOT.jar in the ` в целевом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="a8383-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in the `target\` directory of your project.</span></span>

2. <span data-ttu-id="a8383-307">Используйте SCP, чтобы отправить файлы `TemperatureMonitor-1.0-SNAPSHOT.jar` и `dev.properties` в кластер Storm.</span><span class="sxs-lookup"><span data-stu-id="a8383-307">Use scp to upload the `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files to your Storm cluster.</span></span> <span data-ttu-id="a8383-308">В следующем примере замените `sshuser` именем пользователя SSH, указанным при создании кластера, а `clustername` — именем кластера Storm.</span><span class="sxs-lookup"><span data-stu-id="a8383-308">In the following example, replace `sshuser` with the SSH user you provided when creating the cluster, and `clustername` with the name of your Storm cluster.</span></span> <span data-ttu-id="a8383-309">При появлении запроса введите пароль пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="a8383-309">When prompted, enter the password for the SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="a8383-310">Передача файла может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a8383-310">It may take several minutes to upload the files.</span></span>

    <span data-ttu-id="a8383-311">Дополнительные сведения об использовании команд `scp` и `ssh` с HDInsight см. в статье [Подключение к HDInsight (Hadoop) с помощью SSH](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a8383-311">For more information on using the `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="a8383-312">Когда файл будет передан, подключитесь к кластеру Storm с помощью протокола SSH.</span><span class="sxs-lookup"><span data-stu-id="a8383-312">Once the file has been uploaded, connect to the Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a8383-313">Замените `sshuser` именем пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="a8383-313">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="a8383-314">Замените `clustername` именем пользователя кластера Storm.</span><span class="sxs-lookup"><span data-stu-id="a8383-314">Replace `clustername` with the Storm cluster name.</span></span>

4. <span data-ttu-id="a8383-315">Чтобы запустить топологию, в сеансе SSH выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="a8383-315">To start the topology, use the following command from the SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="a8383-316">Команда `--remote` отправляет топологию в службу Nimbus, которая распределяет ее между узлами супервизора в кластере.</span><span class="sxs-lookup"><span data-stu-id="a8383-316">`--remote` submits the topology to the Nimbus service, which distributes it to the supervisor nodes in the cluster.</span></span>
    * <span data-ttu-id="a8383-317">Команда `--filter` использует файл `dev.properties` для указания значений параметров в определении топологии.</span><span class="sxs-lookup"><span data-stu-id="a8383-317">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="a8383-318">Команда `-R /with-hbase.yaml` использует топологию `with-hbase.yaml`, включенную в пакет.</span><span class="sxs-lookup"><span data-stu-id="a8383-318">`-R /with-hbase.yaml` uses the `with-hbase.yaml` topology included in the package.</span></span>

5. <span data-ttu-id="a8383-319">После запуска топологии откройте в браузере опубликованный в Azure веб-сайт и с помощью команды `node app.js` отправьте данные в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="a8383-319">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span></span> <span data-ttu-id="a8383-320">Веб-панель мониторинга должна начать обновлять данные.</span><span class="sxs-lookup"><span data-stu-id="a8383-320">You should see the web dashboard update to display the information.</span></span>
   
    !["Веб-транзакции"](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="a8383-322">Просмотр данных HBase</span><span class="sxs-lookup"><span data-stu-id="a8383-322">View HBase data</span></span>

<span data-ttu-id="a8383-323">Выполните приведенные ниже инструкции, чтобы подключиться к HBase и проверить, записаны ли данные в таблицу.</span><span class="sxs-lookup"><span data-stu-id="a8383-323">Use the following steps to connect to HBase and verify that the data has been written to the table:</span></span>

1. <span data-ttu-id="a8383-324">Используйте SSH, чтобы подключиться к кластеру HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-324">Use SSH to connect to the HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a8383-325">Замените `sshuser` именем пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="a8383-325">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="a8383-326">Замените `clustername` именем кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-326">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="a8383-327">Из сеанса SSH запустите оболочку HBase.</span><span class="sxs-lookup"><span data-stu-id="a8383-327">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="a8383-328">После загрузки оболочки вы увидите запрос `hbase(main):001:0>`.</span><span class="sxs-lookup"><span data-stu-id="a8383-328">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="a8383-329">Просмотрите строки из таблицы с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="a8383-329">View rows from the table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="a8383-330">Эта команда возвращает информацию, которая указывает на то, что в таблице имеются данные. Эта информация имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="a8383-330">This command returns information similar to the following text, indicating that there is data in the table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="a8383-331">Эта операция проверки возвращает не более 10 строк из таблицы.</span><span class="sxs-lookup"><span data-stu-id="a8383-331">This scan operation returns a maximum of 10 rows from the table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="a8383-332">Удаление кластеров</span><span class="sxs-lookup"><span data-stu-id="a8383-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="a8383-333">Чтобы одновременно удалить кластеры, хранилище и веб-приложение, удалите группу ресурсов, которая их содержит.</span><span class="sxs-lookup"><span data-stu-id="a8383-333">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8383-334">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8383-334">Next steps</span></span>

<span data-ttu-id="a8383-335">Другие примеры топологий Storm с HDInsight приведены в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a8383-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="a8383-336">Дополнительные сведения об Apache Storm см. на сайте [Apache Storm](https://storm.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="a8383-336">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="a8383-337">Дополнительные сведения о базе данных HBase в HDInsight см. в статье [Что такое HBase в HDInsight: база данных NoSQL, которая предоставляет возможности, схожие с BigTable, для Hadoop](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8383-337">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="a8383-338">Дополнительные сведения о библиотеке Socket.io см. на сайте [socket.io](http://socket.io/).</span><span class="sxs-lookup"><span data-stu-id="a8383-338">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="a8383-339">Дополнительные сведения о D3.js см. на странице [D3.js - Data Driven Documents](http://d3js.org/) (D3.js. Документы, управляемые данными).</span><span class="sxs-lookup"><span data-stu-id="a8383-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="a8383-340">Сведения о создании топологий на языке Java см. в статье [Разработка топологий на основе Java для базовых приложений подсчета слов с помощью Apache Storm и Maven в HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a8383-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="a8383-341">Сведения о создании топологий на .NET см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a8383-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
