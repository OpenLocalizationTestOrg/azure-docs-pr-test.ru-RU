---
title: "aaaAnalyze датчиков с Apache Storm и HBase | Документы Microsoft"
description: "Узнайте, как tooconnect tooApache Storm с помощью виртуальной сети. Используйте Storm HBase tooprocess датчик данными из концентратора событий и их визуализации с D3.js."
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
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="cc5f4-104">Анализ полученных с датчиков данных с использованием Apache Storm, концентратора событий и базы данных HBase в службе HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="cc5f4-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="cc5f4-105">Дополнительные сведения о том, как Apache Storm toouse на концентратор событий Azure данных датчика tooprocess HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="cc5f4-106">Hello данных хранится в Apache HBase на HDInsight и визуализировать с помощью D3.js.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="cc5f4-107">шаблон диспетчера ресурсов Azure Hello, используемый в этом документе показано, как toocreate несколько ресурсов Azure в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="cc5f4-108">шаблон Hello создает виртуальную сеть Azure, кластерами HDInsight (Storm и HBase) и веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="cc5f4-109">Реализацию node.js на панели мониторинга реального времени является toohello автоматически развернутого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="cc5f4-110">Hello сведения в этом документе и пример в этом документе требуют HDInsight версии 3.6.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="cc5f4-111">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cc5f4-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc5f4-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cc5f4-113">Prerequisites</span></span>

* <span data-ttu-id="cc5f4-114">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-114">An Azure subscription.</span></span>
* <span data-ttu-id="cc5f4-115">[Node.js](http://nodejs.org/): панель мониторинга web hello используется toopreview локально в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="cc5f4-116">[Java и hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): использовать toodevelop hello Storm топологии.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="cc5f4-117">[Maven](http://maven.apache.org/what-is-maven.html): hello toobuild и компиляции использованных проектов.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="cc5f4-118">[Git](http://git-scm.com/): проект hello используется toodownload из GitHub.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="cc5f4-119">**SSH** клиента: использовать кластеры HDInsight под управлением Linux toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="cc5f4-120">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="cc5f4-121">Вам не нужен существующий кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="cc5f4-122">Hello в данном пошаговом руководстве создайте hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="cc5f4-123">виртуальная сеть Azure;</span><span class="sxs-lookup"><span data-stu-id="cc5f4-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="cc5f4-124">кластер Storm в HDInsight (под управлением Linux, с двумя рабочими узлами);</span><span class="sxs-lookup"><span data-stu-id="cc5f4-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="cc5f4-125">кластер HBase в HDInsight (под управлением Linux, с двумя рабочими узлами);</span><span class="sxs-lookup"><span data-stu-id="cc5f4-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="cc5f4-126">Веб-приложение Azure, на котором размещена панель мониторинга web hello</span><span class="sxs-lookup"><span data-stu-id="cc5f4-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="cc5f4-127">Архитектура</span><span class="sxs-lookup"><span data-stu-id="cc5f4-127">Architecture</span></span>

![схема архитектуры](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="cc5f4-129">В этом примере состоит из следующих компонентов hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="cc5f4-130">**Концентраторы событий Azure**: содержат собираемые с датчиков данные.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="cc5f4-131">**Storm в HDInsight**: в реальном времени обрабатывает данные, получаемые из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="cc5f4-132">**HBase в HDInsight.**Обеспечивает постоянное хранилище данных NoSQL для данных, обработанных Storm.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="cc5f4-133">**Служба виртуальной сети Azure**: включает безопасного взаимодействия между hello Storm на HDInsight и HBase на HDInsight кластеров.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cc5f4-134">При использовании API клиента hello Java HBase требуется виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="cc5f4-135">Она не предоставляется через шлюз открытый hello для кластеров HBase.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="cc5f4-136">Установка HBase и Storm кластеров в одной виртуальной сети позволяет hello hello ураган кластера (или любую другую систему hello виртуальной сети) toodirectly доступ к HBase с помощью API клиента.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="cc5f4-137">**Веб-сайт панели мониторинга**: пример панели мониторинга, на которой в режиме реального времени строятся диаграммы на основе полученных данных.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="cc5f4-138">веб-сайт Hello реализуется в Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="cc5f4-139">[Socket.IO](http://socket.io/) используются для взаимодействия в режиме реального времени между топологии Storm hello и hello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cc5f4-140">Использование Socket.io для связи относится к тонкостям реализации.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="cc5f4-141">На практике можно использовать любую платформу, например сокеты прямого доступа WebSocket или SignalR.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="cc5f4-142">[D3.js](http://d3js.org/) — используется toograph hello данные, отправленные toohello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc5f4-143">Два кластера не требуются, как не поддерживаемый метод toocreate один кластер HDInsight для Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="cc5f4-144">Hello топологии считывает данные из концентратора событий с помощью hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) класс и записи данных в HBase с помощью hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) класс.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="cc5f4-145">Связь с веб-сайта hello осуществляется с помощью [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="cc5f4-146">Следующая схема Hello объясняется макета hello hello топологии:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-146">hello following diagram explains hello layout of hello topology:</span></span>

![схема топологии](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="cc5f4-148">Эта диаграмма представляет упрощенное представление топологии hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="cc5f4-149">Для каждого раздела концентратора событий создается экземпляр каждого компонента.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="cc5f4-150">Эти экземпляры будут распределены по hello узлов в кластере hello и данные передаются между ними, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="cc5f4-151">Данные из средства синтаксического анализа toohello spout hello переводится подсистемой балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="cc5f4-152">Данные из toohello средство синтаксического анализа hello панели мониторинга и HBase группируются по Идентификатору устройства, чтобы сообщения от hello одного устройства всегда потока toohello того же компонента.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="cc5f4-153">Компоненты топологии</span><span class="sxs-lookup"><span data-stu-id="cc5f4-153">Topology components</span></span>

* <span data-ttu-id="cc5f4-154">**Spout концентратора событий**: hello spout входит Apache Storm версии 0.10.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cc5f4-155">Hello spout концентратора событий, используемых в этом примере требуется Storm на версия кластера HDInsight, 3.5 или 3.6.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="cc5f4-156">**ParserBolt.java**: hello данные, генерируемой hello spout необработанные JSON и иногда несколько вызывается событие за раз.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="cc5f4-157">Это молнии считывает данные hello, генерируемой hello spout и анализ приветственное сообщение JSON.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="cc5f4-158">Hello молнии затем передает данные hello как кортеж, содержащий несколько полей.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="cc5f4-159">**DashboardBolt.java**: этот компонент показано, как toouse hello Socket.io клиентская библиотека для данных toosend Java в режиме реального времени toohello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="cc5f4-160">**Нет hbase.yaml**: hello определения топологии, используемые при работе в локальном режиме.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="cc5f4-161">Компоненты HBase при этом не используются.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-161">It does not use HBase components.</span></span>
* <span data-ttu-id="cc5f4-162">**с hbase.yaml**: hello определения топологии, используемые при работе в кластере hello hello топологии.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="cc5f4-163">Компоненты HBase при этом используются.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-163">It does use HBase components.</span></span>
* <span data-ttu-id="cc5f4-164">**dev.Properties**: hello сведения о конфигурации для концентратора событий spout hello, HBase молнии и компоненты панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="cc5f4-165">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="cc5f4-165">Prepare your environment</span></span>

<span data-ttu-id="cc5f4-166">Прежде чем использовать этот пример, необходимо создать концентратор событий Azure, какая топология Storm hello считывает из.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="cc5f4-167">Настройка концентраторов Event Hub</span><span class="sxs-lookup"><span data-stu-id="cc5f4-167">Configure Event Hub</span></span>

<span data-ttu-id="cc5f4-168">Концентратор событий является hello источника данных для этого примера.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="cc5f4-169">Используйте следующие шаги toocreate концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="cc5f4-170">Из hello [портал Azure](https://portal.azure.com)выберите **+ создать** -> **Интернета вещей** -> **концентраторов событий**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="cc5f4-171">В hello **создать пространство имен** выполните hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="cc5f4-172">Введите **имя** для hello пространства имен.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="cc5f4-173">Выберите ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-173">Select a pricing tier.</span></span> <span data-ttu-id="cc5f4-174">**Базовый** подойдет для этого примера.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="cc5f4-175">Выберите hello Azure **подписки** toouse.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="cc5f4-176">Создайте группу ресурсов или выберите имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="cc5f4-177">Выберите hello **расположение** для hello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="cc5f4-178">Выберите **toodashboard ПИН-код**, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="cc5f4-179">После завершения процесса создания hello отображается hello сведения концентраторов событий для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="cc5f4-180">В этой колонке выберите **+ Add Event Hub**(+ Добавить концентратор событий).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="cc5f4-181">В hello **создать концентратор событий** статьи, введите имя **sensordata**, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="cc5f4-182">Оставьте остальные поля в значения по умолчанию hello hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="cc5f4-183">Из концентраторов событий hello просмотра пространства имен, выберите **концентраторов событий**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="cc5f4-184">Выберите hello **sensordata** входа.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="cc5f4-185">Hello sensordata концентратора событий, выберите **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="cc5f4-186">Используйте hello **+ добавить** следующими политиками hello tooadd ссылку:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="cc5f4-187">Имя политики</span><span class="sxs-lookup"><span data-stu-id="cc5f4-187">Policy name</span></span> | <span data-ttu-id="cc5f4-188">Claims</span><span class="sxs-lookup"><span data-stu-id="cc5f4-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="cc5f4-189">устройства</span><span class="sxs-lookup"><span data-stu-id="cc5f4-189">devices</span></span> | <span data-ttu-id="cc5f4-190">Отправка</span><span class="sxs-lookup"><span data-stu-id="cc5f4-190">Send</span></span> |
    | <span data-ttu-id="cc5f4-191">storm</span><span class="sxs-lookup"><span data-stu-id="cc5f4-191">storm</span></span> | <span data-ttu-id="cc5f4-192">Прослушивание</span><span class="sxs-lookup"><span data-stu-id="cc5f4-192">Listen</span></span> |

1. <span data-ttu-id="cc5f4-193">Выберите обе политики и запишите hello **ПЕРВИЧНОГО ключа** значение.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="cc5f4-194">Необходимо получить значение hello для обеих политик на следующих этапах.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="cc5f4-195">Загрузить и настроить проект hello</span><span class="sxs-lookup"><span data-stu-id="cc5f4-195">Download and configure hello project</span></span>

<span data-ttu-id="cc5f4-196">Используйте следующую toodownload hello проекта из GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="cc5f4-197">После выполнения команды hello имеется hello следующая структура каталогов:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="cc5f4-198">В этом документе не рассматривается в сведениях о toofull включены в этом примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="cc5f4-199">Тем не менее полностью закомментирована кода hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="cc5f4-200">tooread проекта hello tooconfigure из концентратора событий, откройте hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` и добавьте ваш toohello сведения концентратора событий, следующие строки:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="cc5f4-201">Локальная компиляция и тестирование</span><span class="sxs-lookup"><span data-stu-id="cc5f4-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc5f4-202">Использование топологии hello локально требует рабочий Storm среды разработки.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="cc5f4-203">См. дополнительные сведения о [настройке среды разработки Storm](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) на сайте Apache.org.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="cc5f4-204">При использовании среды разработки Windows может появиться `java.io.IOException` при выполнении топологии hello локально.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="cc5f4-205">В этом случае перемещение по топологии hello toorunning на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="cc5f4-206">Перед началом тестирования, необходимо запустить hello мониторинга tooview hello выходные данные топологии hello и создать toostore данные в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc5f4-207">При тестировании локально компонент HBase Hello этой топологии не активен.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="cc5f4-208">Hello API-интерфейса Java для hello HBase кластера нельзя получить доступ из внешней hello виртуальной сети Azure, содержащей hello кластеров.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="cc5f4-209">Запуск веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="cc5f4-209">Start hello web application</span></span>

1. <span data-ttu-id="cc5f4-210">Откройте командную строку и перейдите в каталог слишком`hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="cc5f4-211">Используйте следующие команды tooinstall hello зависимости, необходимые веб-приложением hello hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="cc5f4-212">Используйте следующие команды toostart hello веб-приложение hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="cc5f4-213">Вы видите toohello аналогичные сообщения после текста:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="cc5f4-214">Откройте веб-браузер и введите `http://localhost:3000/` в качестве адреса hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="cc5f4-215">Отображается примерно toohello страницы, после изображения.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-215">A page similar toohello following image is displayed:</span></span>
   
    ![веб-панель мониторинга](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="cc5f4-217">Не закрывайте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-217">Leave this command prompt open.</span></span> <span data-ttu-id="cc5f4-218">После тестирования, используйте сочетание клавиш Ctrl-C toostop hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="cc5f4-219">Создание данных</span><span class="sxs-lookup"><span data-stu-id="cc5f4-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="cc5f4-220">Hello действия, описанные в этом разделе используют Node.js, чтобы их можно использовать на любой платформе.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="cc5f4-221">Другие примеры языка в разделе hello `SendEvents` каталога.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="cc5f4-222">Открыть новую строку, оболочки или терминала и перейдите слишком`hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="cc5f4-223">tooinstall hello зависимости, необходимые для приложения hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="cc5f4-224">Привет открыть `app.js` в текстовом редакторе и добавьте hello полученного ранее сведения концентратора событий:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
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
   > <span data-ttu-id="cc5f4-225">В этом примере предполагается, что используется `sensordata` имени hello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="cc5f4-226">И что `devices` имени hello hello политика, имеющая `Send` утверждения.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="cc5f4-227">Используйте hello следующая команда tooinsert новых записей в концентратор событий:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="cc5f4-228">Вы увидите, что несколько строк выходных данных, содержащих данные hello отправлено tooEvent концентратора:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
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

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="cc5f4-229">Построения и запуска топологии hello</span><span class="sxs-lookup"><span data-stu-id="cc5f4-229">Build and start hello topology</span></span>

1. <span data-ttu-id="cc5f4-230">Откройте новую командную строку и перейдите в каталог слишком`hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="cc5f4-231">toobuild и пакета hello топологии, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="cc5f4-232">Топология toostart hello в локальном режиме hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="cc5f4-233">`--local`запускает топологии hello в локальном режиме.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="cc5f4-234">`--filter`использует hello `dev.properties` файл toopopulate параметров в определении топологии hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="cc5f4-235">`resources/no-hbase.yaml`использует hello `no-hbase.yaml` определения топологии.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="cc5f4-236">После запуска топологии hello считывает записи из концентратора событий и отправляет их toohello панели мониторинга, запущенного на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="cc5f4-237">Вы увидите строки отображаются в hello панели мониторинга, аналогичную toohello после изображения:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![панель мониторинга с данными](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="cc5f4-239">Во время hello панели мониторинга с помощью hello `node app.js` команда из предыдущего hello шаги toosend новых данных tooEvent концентраторов.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="cc5f4-240">Поскольку значения температуры hello случайным образом создаются, граф hello следует обновить tooshow значительные изменения в температуры.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cc5f4-241">Вы должны находиться в hello **hdinsight-eventhub пример/SendEvents/Nodejs** каталог при использовании hello `node app.js` команды.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="cc5f4-242">После проверки этой панели мониторинга hello обновляет топологии hello stop, с помощью клавиш Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="cc5f4-243">Также можно использовать сочетание клавиш Ctrl + C toostop hello локальный веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="cc5f4-244">Создание кластеров Storm и HBase</span><span class="sxs-lookup"><span data-stu-id="cc5f4-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="cc5f4-245">Hello шаги этого раздела используется [шаблона Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate виртуальной сети Azure и Storm и HBase кластера hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="cc5f4-246">шаблон Hello также создает веб-приложение Azure и развертывает копию hello панели мониторинга в него.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="cc5f4-247">Виртуальная сеть используется, чтобы топологии hello, работающих в кластере Storm hello может напрямую взаимодействовать с hello HBase кластера с помощью API-интерфейса Java HBase hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="cc5f4-248">Hello шаблона диспетчера ресурсов, используемых в данном документе, расположенные в контейнере большой двоичный объект открытого в **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="cc5f4-249">Щелкните hello toosign кнопки в tooAzure и откройте hello шаблона диспетчера ресурсов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="cc5f4-250">Из hello **развертывания пользовательского** введите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![Параметры HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="cc5f4-252">**Базовые имена кластеров**: это значение используется как базовое имя hello для кластеров hello Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="cc5f4-253">Например, если ввести **abc**, будут созданы кластер Storm **storm-abc** и кластер HBase **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="cc5f4-254">**Имя входа пользователя кластера**: hello имя пользователя администратора для кластеров hello Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="cc5f4-255">**Имя входа пароль кластера**: hello пароль пользователя администратора для кластеров Storm и HBase hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="cc5f4-256">**Имя пользователя SSH**: hello toocreate пользователя SSH для кластеров hello Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="cc5f4-257">**Пароль SSH**: hello пароль пользователя SSH hello для кластеров hello Storm и HBase.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="cc5f4-258">**Расположение**: hello области создания кластеров hello в.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="cc5f4-259">Нажмите кнопку **ОК** toosave hello параметров.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="cc5f4-260">Используйте hello **основы** статьи toocreate группу ресурсов или выберите существующий.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="cc5f4-261">В hello **расположение группы ресурсов** раскрывающееся меню, выберите hello местоположения, которые вы выбрали для hello **расположение** параметр в hello **параметры** раздела.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="cc5f4-262">Прочитайте hello положения и условия, а затем выберите **я принимаю условия, указанных выше, toohello**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="cc5f4-263">Наконец, проверьте **toodashboard ПИН-код** , а затем выберите **покупки**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="cc5f4-264">Занимает около 20 минут toocreate hello кластеров.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="cc5f4-265">После создания ресурсов hello отображается информация о группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Группа ресурсов для виртуальной сети hello и кластеров](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="cc5f4-267">Обратите внимание, что имена hello hello кластеров HDInsight **базовым ИМЕНЕМ storm** и **базовое имя hbase**, где базовое имя — имя hello указано toohello шаблона.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="cc5f4-268">Эти имена на более позднем этапе используется при подключении toohello кластеров.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="cc5f4-269">Также Обратите внимание, что hello имя узла мониторинга hello — **мониторинга базовым именем**.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="cc5f4-270">Это значение используется ниже в этом документе.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="cc5f4-271">Настройка мониторинга молнии hello</span><span class="sxs-lookup"><span data-stu-id="cc5f4-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="cc5f4-272">мониторинга данных toohello toosend развернуто как веб-приложения, необходимо изменить hello, следующей строкой в hello `dev.properties`файла:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="cc5f4-273">Изменение `http://localhost:3000` слишком`http://BASENAME-dashboard.azurewebsites.net` и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="cc5f4-274">Замените **базовым ИМЕНЕМ** с базовым именем hello, указанное в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="cc5f4-275">Можно также использовать hello группы ресурсов, созданные ранее tooselect hello панели мониторинга и представления hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="cc5f4-276">Создайте таблицу HBase hello</span><span class="sxs-lookup"><span data-stu-id="cc5f4-276">Create hello HBase table</span></span>

<span data-ttu-id="cc5f4-277">toostore данных в HBase, необходимо сначала создать таблицу.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="cc5f4-278">Предварительно создать ресурсы, необходимые для Storm toowrite для, как идет ресурсы toocreate внутри топологии Storm может привести к попытке несколько экземпляров toocreate hello того же ресурса.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="cc5f4-279">Создать hello ресурсам за пределами топологии hello и использовать Storm для чтения/записи и аналитики.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="cc5f4-280">Используйте SSH tooconnect toohello HBase кластера с помощью hello SSH пользователя и пароль, указанный шаблон toohello во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="cc5f4-281">Например, при соединении с помощью hello `ssh` используется hello, используя синтаксис команды:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="cc5f4-282">Замените `sshuser` с имя пользователя SSH hello заданы при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="cc5f4-283">Замените `clustername` с именем кластера HBase hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="cc5f4-284">Из сеанса SSH hello запустите оболочку HBase hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="cc5f4-285">После загрузки оболочки hello, вы видите `hbase(main):001:0>` строки.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="cc5f4-286">Введите следующая команда toocreate датчиков таблицы toostore hello hello hello оболочки HBase:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="cc5f4-287">Убедитесь, что для этой таблицы hello был создан с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="cc5f4-288">Возвращает сведения аналогичные toohello следующий пример, об отсутствии 0 строк в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="cc5f4-289">Введите `exit` tooexit hello оболочки HBase:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="cc5f4-290">Настройка молнии HBase hello</span><span class="sxs-lookup"><span data-stu-id="cc5f4-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="cc5f4-291">tooHBase toowrite из кластера Storm hello, необходимо предоставить hello HBase молнии hello сведения о конфигурации кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="cc5f4-292">Используйте один из следующих примеров tooretrieve hello Zookeeper кворума для кластера HBase hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="cc5f4-293">Замените `your_HDInsight_cluster_name` с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="cc5f4-294">Дополнительные сведения об установке hello `jq` программы, в разделе [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="cc5f4-295">При появлении запроса введите пароль hello для входа администратора HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="cc5f4-296">Замените "your_HDInsight_cluster_name с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="cc5f4-297">При появлении запроса введите пароль hello для входа администратора HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="cc5f4-298">Для этого примера требуется Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="cc5f4-299">См. дополнительные сведения об [установке Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="cc5f4-300">Hello информацию, возвращаемую эти примеры — примерно toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="cc5f4-301">Эта информация используется toocommunicate Storm с кластером HBase hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="cc5f4-302">Изменение hello `dev.properties` и добавьте hello Zookeeper кворума сведения toohello следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="cc5f4-303">Построение пакета и разверните решение tooHDInsight hello</span><span class="sxs-lookup"><span data-stu-id="cc5f4-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="cc5f4-304">В среде разработки используйте следующие шаги toodeploy hello Storm топологии toohello storm кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="cc5f4-305">Из hello `TemperatureMonitor` каталога, используйте hello следующую команду tooperform новую сборку и создать пакет JAR-ФАЙЛ из проекта:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="cc5f4-306">Эта команда создает файл с именем `TemperatureMonitor-1.0-SNAPSHOT.jar in hello ` в целевом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="cc5f4-307">Использование scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` и `dev.properties` кластер Storm tooyour файлов.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="cc5f4-308">Следующий пример, замените в hello `sshuser` с пользователем SSH hello, указанный при создании кластера hello и `clustername` с именем hello Storm кластера.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="cc5f4-309">При появлении запроса введите пароль hello для hello пользователя SSH.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="cc5f4-310">Он может занять несколько минут tooupload hello файлы.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="cc5f4-311">Дополнительные сведения об использовании hello `scp` и `ssh` команд с HDInsight, в разделе [использование SSH с HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="cc5f4-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="cc5f4-312">После загрузки файла hello подключите кластер Storm toohello, с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="cc5f4-313">Замените `sshuser` с именем пользователя SSH hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="cc5f4-314">Замените `clustername` с имя_кластера Storm hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="cc5f4-315">toostart hello топологии, выполните следующую команду из сеанса SSH hello hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="cc5f4-316">`--remote`отправляет toohello топологии hello Nimbus службу, которая распространяет его toohello начальника узлы кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="cc5f4-317">`--filter`использует hello `dev.properties` файл toopopulate параметров в определении топологии hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="cc5f4-318">`-R /with-hbase.yaml`использует hello `with-hbase.yaml` топологии, включенный в пакет hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="cc5f4-319">После запуска топологии hello, откройте веб-сайт toohello браузера, опубликованных в Azure, а затем используйте hello `node app.js` команда toosend данных tooEvent концентратора.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="cc5f4-320">Вы увидите информацию о hello toodisplay обновление в панели мониторинга веб hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    !["Веб-транзакции"](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="cc5f4-322">Просмотр данных HBase</span><span class="sxs-lookup"><span data-stu-id="cc5f4-322">View HBase data</span></span>

<span data-ttu-id="cc5f4-323">Используйте следующие шаги tooconnect tooHBase hello и убедитесь, что hello записи данных toohello таблицы:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="cc5f4-324">Использование SSH tooconnect toohello HBase кластера.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="cc5f4-325">Замените `sshuser` с именем пользователя SSH hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="cc5f4-326">Замените `clustername` с именем кластера HBase hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="cc5f4-327">Из сеанса SSH hello запустите оболочку HBase hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="cc5f4-328">После загрузки оболочки hello, вы видите `hbase(main):001:0>` строки.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="cc5f4-329">Представление строк из таблицы hello:</span><span class="sxs-lookup"><span data-stu-id="cc5f4-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="cc5f4-330">Эта команда возвращает сведения аналогичные toohello после текста, указывающее на данные в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
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
   > <span data-ttu-id="cc5f4-331">Эта операция сканирования возвращает максимум 10 строк из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="cc5f4-332">Удаление кластеров</span><span class="sxs-lookup"><span data-stu-id="cc5f4-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="cc5f4-333">toodelete hello кластеров, хранения и веб-приложения за один раз удаления группы ресурсов hello, содержащий их.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc5f4-334">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc5f4-334">Next steps</span></span>

<span data-ttu-id="cc5f4-335">Другие примеры топологий Storm с HDInsight приведены в статье [Примеры топологий и компонентов Storm для Apache Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="cc5f4-336">Дополнительные сведения о Apache Storm см. в разделе hello [Apache Storm](https://storm.incubator.apache.org/) сайта.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="cc5f4-337">Дополнительные сведения о HBase на HDInsight см. в разделе hello [HBase с HDInsight Обзор](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="cc5f4-338">Дополнительные сведения о Socket.io см. в разделе hello [socket.io](http://socket.io/) сайта.</span><span class="sxs-lookup"><span data-stu-id="cc5f4-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="cc5f4-339">Дополнительные сведения о D3.js см. на странице [D3.js - Data Driven Documents](http://d3js.org/) (D3.js. Документы, управляемые данными).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="cc5f4-340">Сведения о создании топологий на языке Java см. в статье [Разработка топологий на основе Java для базовых приложений подсчета слов с помощью Apache Storm и Maven в HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="cc5f4-341">Сведения о создании топологий на .NET см. в статье [Разработка топологий для Apache Storm в HDInsight на C# с помощью средств Hadoop для Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cc5f4-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
