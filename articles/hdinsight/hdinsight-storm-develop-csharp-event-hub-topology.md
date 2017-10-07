---
title: "события aaaProcess из концентраторов событий с Storm - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как tooprocess данные из концентраторов событий Azure с топологией Storm C# создаются в Visual Studio с помощью hello средства HDInsight для Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="c3b9b-103">Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="c3b9b-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="c3b9b-104">Узнайте, как toowork с концентраторов событий Azure из Apache Storm на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="c3b9b-105">В этом документе используется C# Storm топологии tooread и запись данных из концентраторов Evbent</span><span class="sxs-lookup"><span data-stu-id="c3b9b-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="c3b9b-106">Этот же проект на языке Java рассматривается в статье [Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="c3b9b-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="c3b9b-107">SCP.NET</span></span>

<span data-ttu-id="c3b9b-108">Hello в данном пошаговом руководстве используется SCP.NET пакета NuGet, который обеспечивает топологии легко toocreate C#, а также компоненты для использования с Storm на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3b9b-109">Хотя hello шагов в этом документе используют среду разработки Windows с помощью Visual Studio, hello скомпилированный проект может быть отправлено tooa Storm для кластера HDInsight, использующего Linux.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c3b9b-110">Топологии SCP.NET поддерживаются только теми кластерами под управлением Linux, которые созданы после 28 октября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="c3b9b-111">HDInsight 3.4 и больше топологии используйте моно toorun C#.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="c3b9b-112">в этом документе примере Hello работает с HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="c3b9b-113">Если планируется создание собственных решений .NET для HDInsight, проверьте hello [моно совместимости](http://www.mono-project.com/docs/about-mono/compatibility/) документа потенциальные проблемы совместимости.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="c3b9b-114">Управление версиями кластера</span><span class="sxs-lookup"><span data-stu-id="c3b9b-114">Cluster versioning</span></span>

<span data-ttu-id="c3b9b-115">Hello пакет Microsoft.SCP.Net.SDK NuGet, используемого для проекта должно соответствовать hello основной номер версии Storm установлен на HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="c3b9b-116">В HDInsight версий 3.5 и 3.6 используется Storm 1.x, следовательно, для таких кластеров нужно использовать версию SCP.NET 1.0.x.x.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3b9b-117">пример Hello в этом документе ожидает HDInsight 3.5 или 3.6 кластера.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="c3b9b-118">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3b9b-119">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c3b9b-120">Топологии C# должны быть рассчитаны на использование с .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="c3b9b-121">Как toowork с концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="c3b9b-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="c3b9b-122">Корпорация Майкрософт предоставляет набор компонентов Java, которые могут быть используется toocommunicate с концентраторами событий из топологии Storm.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="c3b9b-123">Можно найти hello Java архива (JAR) файла, содержащего совместимой версии HDInsight 3.6 эти компоненты на [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3b9b-124">Хотя компоненты hello написаны на языке Java, их можно легко использовать из топологии на C#.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="c3b9b-125">в этом примере используются следующие компоненты Hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="c3b9b-126">__EventHubSpout__: считывает данные из концентраторов событий Azure;</span><span class="sxs-lookup"><span data-stu-id="c3b9b-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="c3b9b-127">__EventHubBolt__: записывает данные tooEvent концентраторов.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="c3b9b-128">__EventHubSpoutConfig__: использовать tooconfigure EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="c3b9b-129">__EventHubBoltConfig__: использовать tooconfigure EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="c3b9b-130">Пример использования объекта spout</span><span class="sxs-lookup"><span data-stu-id="c3b9b-130">Example spout usage</span></span>

<span data-ttu-id="c3b9b-131">SCP.NET предоставляет методы для добавления EventHubSpout tooyour топологии.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="c3b9b-132">Эти методы позволяют упростить tooadd spout, чем использование hello универсальные методы для добавления компонента Java.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="c3b9b-133">Hello следующем примере показано, как hello toocreate spout с помощью __SetEventHubSpout__ и **EventHubSpoutConfig** методы, предоставляемые SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="c3b9b-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="c3b9b-134">Hello предыдущего примера создается новый компонент с именем spout __EventHubSpout__и присваивает ему toocommunicate концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="c3b9b-135">Указание параллелизма Hello для компонента hello задано toohello количество разделов в концентраторе событий hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="c3b9b-136">Этот параметр позволяет Storm toocreate экземпляр компонента hello для каждой секции.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="c3b9b-137">Пример использования объекта bolt</span><span class="sxs-lookup"><span data-stu-id="c3b9b-137">Example bolt usage</span></span>

<span data-ttu-id="c3b9b-138">Используйте hello **JavaComponmentConstructor** toocreate метод экземпляра hello молнии.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="c3b9b-139">Hello следующем примере показано, как toocreate и настройте новый экземпляр hello **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="c3b9b-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="c3b9b-140">В этом примере используется выражение Clojure передан в виде строки, а не с помощью **JavaComponentConstructor** toocreate **EventHubBoltConfig**, чем spout пример hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="c3b9b-141">Работает каждый из этих методов.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-141">Either method works.</span></span> <span data-ttu-id="c3b9b-142">Используйте метод hello, который, в том числе рекомендации tooyou.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="c3b9b-143">Загрузите проект hello завершена</span><span class="sxs-lookup"><span data-stu-id="c3b9b-143">Download hello completed project</span></span>

<span data-ttu-id="c3b9b-144">Можно загрузить полную версию hello проект, созданный в этом учебнике из [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="c3b9b-145">Однако по-прежнему требуются параметры конфигурации tooprovide hello инструкциям в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c3b9b-146">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3b9b-146">Prerequisites</span></span>

* <span data-ttu-id="c3b9b-147">[Кластер Apache Storm в HDInsight версии 3.5 или 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="c3b9b-148">пример Hello, используемые в этом документе требуется Storm в HDInsight версии 3.5 или 3.6.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="c3b9b-149">Это не работает с более ранними версиями HDInsight, из-за изменения имени класса toobreaking.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="c3b9b-150">Версию этого примера, которая работает со старыми кластерами, можно найти на сайте [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="c3b9b-151">[Концентратор событий Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="c3b9b-152">Hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="c3b9b-153">Hello [средства HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="c3b9b-154">Пакет Java JDK 1.8 или более поздней версии, в зависимости от используемой среды разработки.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="c3b9b-155">Скачиваемые файлы JDK доступны на сайте [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="c3b9b-156">Hello **JAVA_HOME** среды переменной должен точки toohello каталог, содержащий Java.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="c3b9b-157">Hello **%JAVA_HOME%/bin** каталог должен находиться в пути hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="c3b9b-158">Загрузить компоненты hello концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="c3b9b-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="c3b9b-159">Загрузка hello концентраторов событий spout и винта компонента из [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="c3b9b-160">Создайте каталог с именем `eventhubspout`и сохраните файл hello в каталог hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="c3b9b-161">Настройка концентраторов событий Azure</span><span class="sxs-lookup"><span data-stu-id="c3b9b-161">Configure Event Hubs</span></span>

<span data-ttu-id="c3b9b-162">Концентраторы событий — hello источника данных для этого примера.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="c3b9b-163">Используйте hello сведения в разделе «Создание концентратора событий» hello объекта [приступить к работе с концентраторами событий](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="c3b9b-164">После создания концентратора событий hello просмотра hello **EventHub** колонки в hello Azure портала и выберите **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="c3b9b-165">Выберите **+ добавить** tooadd hello следующие политики:</span><span class="sxs-lookup"><span data-stu-id="c3b9b-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="c3b9b-166">Имя</span><span class="sxs-lookup"><span data-stu-id="c3b9b-166">Name</span></span> | <span data-ttu-id="c3b9b-167">Разрешения</span><span class="sxs-lookup"><span data-stu-id="c3b9b-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="c3b9b-168">writer</span><span class="sxs-lookup"><span data-stu-id="c3b9b-168">writer</span></span> |<span data-ttu-id="c3b9b-169">Отправка</span><span class="sxs-lookup"><span data-stu-id="c3b9b-169">Send</span></span> |
   | <span data-ttu-id="c3b9b-170">reader</span><span class="sxs-lookup"><span data-stu-id="c3b9b-170">reader</span></span> |<span data-ttu-id="c3b9b-171">Прослушивание</span><span class="sxs-lookup"><span data-stu-id="c3b9b-171">Listen</span></span> |

    ![Снимок экрана окна политик общего доступа](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="c3b9b-173">Выберите hello **чтения** и **записи** политики.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="c3b9b-174">Скопируйте и сохраните hello значение первичного ключа для обоих политик, как эти значения используются в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="c3b9b-175">Настройка hello EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="c3b9b-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="c3b9b-176">Если вы еще не установили hello последнюю версию средства HDInsight hello для Visual Studio, в разделе [приступить к работе со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="c3b9b-177">Загрузите решение hello из [eventhub-storm гибридный](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="c3b9b-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="c3b9b-178">В hello **EventHubWriter** проект, откройте hello **App.config** файла.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="c3b9b-179">Используйте сведения hello из концентратора событий hello, настроенные ранее toofill на значение hello hello следующие ключи:</span><span class="sxs-lookup"><span data-stu-id="c3b9b-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="c3b9b-180">Ключ</span><span class="sxs-lookup"><span data-stu-id="c3b9b-180">Key</span></span> | <span data-ttu-id="c3b9b-181">Значение</span><span class="sxs-lookup"><span data-stu-id="c3b9b-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="c3b9b-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="c3b9b-182">EventHubPolicyName</span></span> |<span data-ttu-id="c3b9b-183">модуль записи (Если вы использовали другое имя для политики hello с *отправки* разрешение, вместо этого используйте.)</span><span class="sxs-lookup"><span data-stu-id="c3b9b-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="c3b9b-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="c3b9b-184">EventHubPolicyKey</span></span> |<span data-ttu-id="c3b9b-185">Ключ политики записи hello Hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="c3b9b-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="c3b9b-186">EventHubNamespace</span></span> |<span data-ttu-id="c3b9b-187">Здравствуйте, пространство имен, содержащее концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="c3b9b-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="c3b9b-188">EventHubName</span></span> |<span data-ttu-id="c3b9b-189">Имя концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-189">Your event hub name.</span></span> |
   | <span data-ttu-id="c3b9b-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="c3b9b-190">EventHubPartitionCount</span></span> |<span data-ttu-id="c3b9b-191">количество секций в концентратор событий Hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="c3b9b-192">Сохраните и закройте hello **App.config** файла.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="c3b9b-193">Настройка hello EventHubReader</span><span class="sxs-lookup"><span data-stu-id="c3b9b-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="c3b9b-194">Откройте hello **EventHubReader** проекта.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="c3b9b-195">Откройте hello **App.config** файл для hello **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="c3b9b-196">Используйте сведения hello из концентратора событий hello, настроенные ранее toofill на значение hello hello следующие ключи:</span><span class="sxs-lookup"><span data-stu-id="c3b9b-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="c3b9b-197">Ключ</span><span class="sxs-lookup"><span data-stu-id="c3b9b-197">Key</span></span> | <span data-ttu-id="c3b9b-198">Значение</span><span class="sxs-lookup"><span data-stu-id="c3b9b-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="c3b9b-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="c3b9b-199">EventHubPolicyName</span></span> |<span data-ttu-id="c3b9b-200">Модуль чтения (Если вы использовали другое имя для политики hello с *прослушивания* разрешение, вместо этого используйте.)</span><span class="sxs-lookup"><span data-stu-id="c3b9b-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="c3b9b-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="c3b9b-201">EventHubPolicyKey</span></span> |<span data-ttu-id="c3b9b-202">Ключ политики чтения hello Hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="c3b9b-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="c3b9b-203">EventHubNamespace</span></span> |<span data-ttu-id="c3b9b-204">Здравствуйте, пространство имен, содержащее концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="c3b9b-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="c3b9b-205">EventHubName</span></span> |<span data-ttu-id="c3b9b-206">Имя концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-206">Your event hub name.</span></span> |
   | <span data-ttu-id="c3b9b-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="c3b9b-207">EventHubPartitionCount</span></span> |<span data-ttu-id="c3b9b-208">количество секций в концентратор событий Hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="c3b9b-209">Сохраните и закройте hello **App.config** файла.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="c3b9b-210">Hello топологии развертывания</span><span class="sxs-lookup"><span data-stu-id="c3b9b-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="c3b9b-211">Из **обозревателе решений**, щелкните правой кнопкой мыши hello **EventHubReader** проекта, а затем выберите **отправить tooStorm на HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![Снимок экрана обозревателя решений, с tooStorm отправить в выделенной HDInsight](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="c3b9b-213">На hello **отправить топологии** выберите ваш **кластер Storm**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="c3b9b-214">Разверните **дополнительных конфигураций**выберите **пути к файлам Java**выберите **...** и выберите hello каталог, содержащий hello JAR-файл, загруженный ранее.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="c3b9b-215">Теперь нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-215">Finally, click **Submit**.</span></span>

    ![Снимок экрана с диалоговым окном Submit Topology (Отправка топологии)](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="c3b9b-217">При отправке топологии hello hello **средство просмотра топологии Storm** отображается.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="c3b9b-218">tooview сведения о топологии hello, выберите hello **EventHubReader** топологии hello левой панели.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Снимок экрана средства просмотра топологий Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="c3b9b-220">Из **обозревателе решений**, щелкните правой кнопкой мыши hello **EventHubWriter** проекта, а затем выберите **отправить tooStorm на HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="c3b9b-221">На hello **отправить топологии** выберите ваш **кластер Storm**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="c3b9b-222">Разверните **дополнительных конфигураций**выберите **пути к файлам Java**выберите **...** , и выберите hello каталог, содержащий hello JAR-файл был загружен ранее.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="c3b9b-223">Теперь нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="c3b9b-224">При отправке топологии hello обновить список топологии hello в hello **средство просмотра топологии Storm** tooverify обеих топологий, на котором работают hello кластера.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="c3b9b-225">В **средство просмотра топологии Storm**выберите hello **EventHubReader** топологии.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="c3b9b-226">Сводка по молнии hello компонент hello tooopen дважды щелкните hello **LogBolt** компонент на схеме hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="c3b9b-227">В hello **исполнителей** выберите одну из ссылок hello в hello **порт** столбца.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="c3b9b-228">Отобразится информация, зарегистрированная компонентом hello.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-228">This displays information logged by hello component.</span></span> <span data-ttu-id="c3b9b-229">Hello в журнал сведения являются аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="c3b9b-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="c3b9b-230">Остановить hello топологии</span><span class="sxs-lookup"><span data-stu-id="c3b9b-230">Stop hello topologies</span></span>

<span data-ttu-id="c3b9b-231">toostop hello топологий, выберите каждой топологии в hello **средство просмотра топологии Storm**, нажмите кнопку **Kill**.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Снимок экрана средства просмотра топологии Storm с выделенной кнопкой "Прервать"](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="c3b9b-233">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="c3b9b-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="c3b9b-234">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3b9b-234">Next steps</span></span>

<span data-ttu-id="c3b9b-235">В этом документе вы узнали, как toouse концентраторов событий Java hello spout и винта из toowork топологии C# с данными в концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c3b9b-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="c3b9b-236">toolearn Дополнительные сведения о создании C# топологии, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="c3b9b-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="c3b9b-237">Разработка топологий для Apache Storm в HDInsight на C# с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3b9b-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="c3b9b-238">Руководство по программированию для SCP</span><span class="sxs-lookup"><span data-stu-id="c3b9b-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="c3b9b-239">Примеры топологий для Storm в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3b9b-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
