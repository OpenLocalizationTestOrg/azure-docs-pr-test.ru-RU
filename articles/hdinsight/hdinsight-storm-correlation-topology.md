---
title: "события aaaCorrelate со временем с Storm и HBase на HDInsight"
description: "Узнайте, как toocorrelate события, поступающие в разное время с помощью Storm и HBase на HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="d3437-103">Сопоставление событий, поступающих в разное время, с помощью Storm и HBase</span><span class="sxs-lookup"><span data-stu-id="d3437-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="d3437-104">Благодаря сохранению постоянных данных в Apache Storm можно сопоставлять данные, поступающие в разное время.</span><span class="sxs-lookup"><span data-stu-id="d3437-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="d3437-105">Например связывание события входа и выхода для toocalculate сеанса пользователя как долго сеанс hello выполнялись.</span><span class="sxs-lookup"><span data-stu-id="d3437-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="d3437-106">В этом документе вы узнаете, как toocreate базовая топология Storm C#, отслеживает события входа и выхода для сеансов пользователей, а затем вычисляет hello продолжительность сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="d3437-107">Топология Hello HBase использует в качестве хранилища постоянных данных.</span><span class="sxs-lookup"><span data-stu-id="d3437-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="d3437-108">HBase также позволяет tooperform пакетные запросы на hello исторические данные tooproduce дополнительные функции анализа.</span><span class="sxs-lookup"><span data-stu-id="d3437-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="d3437-109">Например, количество пользовательских сеансов, начатых или завершенных за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="d3437-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3437-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3437-110">Prerequisites</span></span>

* <span data-ttu-id="d3437-111">Visual Studio и hello HDInsight tools для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3437-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="d3437-112">Дополнительные сведения см. в разделе [приступить к работе со средствами hello HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d3437-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="d3437-113">Apache Storm в кластере HDInsight (под управлением Windows).</span><span class="sxs-lookup"><span data-stu-id="d3437-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="d3437-114">Выполняемая SCP.NET топологии в кластерах Storm под управлением Linux, созданных после 10/28/2016 hello HBase пакета SDK для .NET пакет, доступный на 10/28/2016 г. не работает на основе Linux HDInsight</span><span class="sxs-lookup"><span data-stu-id="d3437-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="d3437-115">Apache HBase в кластере HDInsight (под управлением Linux или Windows).</span><span class="sxs-lookup"><span data-stu-id="d3437-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d3437-116">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d3437-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d3437-117">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d3437-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d3437-118">[Java](https://java.com) 1.7 или более поздняя версия в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="d3437-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="d3437-119">Java — используется toopackage hello топологии при отправленной toohello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d3437-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="d3437-120">Hello **JAVA_HOME** среды переменной должен точки toohello каталог, содержащий Java.</span><span class="sxs-lookup"><span data-stu-id="d3437-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="d3437-121">Hello **%JAVA_HOME%/bin** каталог должен находиться в пути hello</span><span class="sxs-lookup"><span data-stu-id="d3437-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="d3437-122">Архитектура</span><span class="sxs-lookup"><span data-stu-id="d3437-122">Architecture</span></span>

![Схема потока данных hello через hello топологии](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="d3437-124">Сопоставление событий требуется идентификатор для источника события hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="d3437-125">Например идентификатор пользователя, идентификатор сеанса или другой частью данных это) уникальный и б) в включаются все данные, отправляемые tooStorm.</span><span class="sxs-lookup"><span data-stu-id="d3437-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="d3437-126">В этом примере используется значение GUID toorepresent идентификатор сеанса.</span><span class="sxs-lookup"><span data-stu-id="d3437-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="d3437-127">В примере есть два кластера HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d3437-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="d3437-128">HBase: хранилище постоянных данных для исторических данных;</span><span class="sxs-lookup"><span data-stu-id="d3437-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="d3437-129">Storm: использовать tooingest входящих данных</span><span class="sxs-lookup"><span data-stu-id="d3437-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="d3437-130">Hello данных формируется случайным образом топологии Storm hello и состоит из следующих элементов hello:</span><span class="sxs-lookup"><span data-stu-id="d3437-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="d3437-131">идентификатор сеанса: GUID, который однозначно определяет каждый сеанс;</span><span class="sxs-lookup"><span data-stu-id="d3437-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="d3437-132">событие: событие НАЧАЛО или КОНЕЦ,</span><span class="sxs-lookup"><span data-stu-id="d3437-132">Event: a START or END event.</span></span> <span data-ttu-id="d3437-133">в этом примере НАЧАЛО всегда раньше КОНЦА;</span><span class="sxs-lookup"><span data-stu-id="d3437-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="d3437-134">Время: hello время события hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="d3437-135">Эти данные обрабатываются и хранятся в HBase.</span><span class="sxs-lookup"><span data-stu-id="d3437-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="d3437-136">Топология Storm</span><span class="sxs-lookup"><span data-stu-id="d3437-136">Storm topology</span></span>

<span data-ttu-id="d3437-137">При запуске сеанса, **ЗАПУСК** событие полученных топологии hello и tooHBase в журнал.</span><span class="sxs-lookup"><span data-stu-id="d3437-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="d3437-138">При **окончания** полученных событий, топологии hello извлекает hello **ЗАПУСК** событие и вычисляет hello времени между событиями hello двух.</span><span class="sxs-lookup"><span data-stu-id="d3437-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="d3437-139">Это **длительность** значение сохраняется в HBase вместе с hello **окончания** сведения о событии.</span><span class="sxs-lookup"><span data-stu-id="d3437-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3437-140">Во время этой топологии демонстрирует базовый шаблон hello, решение производственного понадобится tootake конструктора для hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="d3437-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="d3437-141">события, поступающие не по порядку;</span><span class="sxs-lookup"><span data-stu-id="d3437-141">Events arriving out of order</span></span>
> * <span data-ttu-id="d3437-142">повторяющиеся события;</span><span class="sxs-lookup"><span data-stu-id="d3437-142">Duplicate events</span></span>
> * <span data-ttu-id="d3437-143">удаленные события.</span><span class="sxs-lookup"><span data-stu-id="d3437-143">Dropped events</span></span>

<span data-ttu-id="d3437-144">Пример топологии Hello состоит из hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="d3437-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="d3437-145">Session.cs: имитирует сеанса пользователя путем создания идентификатора сеанса произвольного, время сеанса hello время и сколько времени начала.</span><span class="sxs-lookup"><span data-stu-id="d3437-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="d3437-146">Spout.cs: создает 100 сеансов, создает событие НАЧАЛА, ожидает hello случайное время ожидания для каждого сеанса и затем создает событие END.</span><span class="sxs-lookup"><span data-stu-id="d3437-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="d3437-147">Затем перезапускает завершения сеансов toogenerate новые.</span><span class="sxs-lookup"><span data-stu-id="d3437-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="d3437-148">HBaseLookupBolt.cs: использует toolook идентификатор сеанса hello информации сеанса в HBase.</span><span class="sxs-lookup"><span data-stu-id="d3437-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="d3437-149">При обработке события окончания обнаруживает соответствующее событие НАЧАЛА hello и вычисляет hello продолжительность сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="d3437-150">HBaseBolt.cs: сохранение информации в HBase.</span><span class="sxs-lookup"><span data-stu-id="d3437-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="d3437-151">TypeHelper.cs: Помогает преобразования типа при чтении или записи tooHBase.</span><span class="sxs-lookup"><span data-stu-id="d3437-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="d3437-152">Схема HBase</span><span class="sxs-lookup"><span data-stu-id="d3437-152">HBase schema</span></span>

<span data-ttu-id="d3437-153">В HBase hello данные хранятся в таблице с hello следующие схемы и параметры:</span><span class="sxs-lookup"><span data-stu-id="d3437-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="d3437-154">Ключ строки: hello сеанса идентификатор используется как hello ключ для строк в этой таблице.</span><span class="sxs-lookup"><span data-stu-id="d3437-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="d3437-155">Семейство столбца: hello имя семейства — «cf».</span><span class="sxs-lookup"><span data-stu-id="d3437-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="d3437-156">В этом семействе хранятся столбцы:</span><span class="sxs-lookup"><span data-stu-id="d3437-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="d3437-157">событие: НАЧАЛО или КОНЕЦ;</span><span class="sxs-lookup"><span data-stu-id="d3437-157">event: START or END.</span></span>

  * <span data-ttu-id="d3437-158">время: hello время в миллисекундах, которое hello событие произошло.</span><span class="sxs-lookup"><span data-stu-id="d3437-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="d3437-159">длительность: hello расстояние от НАЧАЛА и окончания событий.</span><span class="sxs-lookup"><span data-stu-id="d3437-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="d3437-160">ВЕРСИИ: семейства «cf» hello, задается tooretain 5 версии каждой строки.</span><span class="sxs-lookup"><span data-stu-id="d3437-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d3437-161">Версии представляют собой запись предыдущих значений, сохраненных для конкретного ключа строки.</span><span class="sxs-lookup"><span data-stu-id="d3437-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="d3437-162">По умолчанию HBase возвращает только значение hello hello самой последней версии строки.</span><span class="sxs-lookup"><span data-stu-id="d3437-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="d3437-163">В этом случае hello одной строки используется для всех событий (начало, конец.) в каждой версии строки определяется hello значение отметки времени.</span><span class="sxs-lookup"><span data-stu-id="d3437-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="d3437-164">Версии предоставляют обзор прошлых событий, зарегистрированных для определенного идентификатора.</span><span class="sxs-lookup"><span data-stu-id="d3437-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="d3437-165">Загрузите проект hello</span><span class="sxs-lookup"><span data-stu-id="d3437-165">Download hello project</span></span>

<span data-ttu-id="d3437-166">Образец Hello проекта можно загрузить из [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="d3437-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="d3437-167">Этот загружаемый файл содержит следующие проекты C# hello:</span><span class="sxs-lookup"><span data-stu-id="d3437-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="d3437-168">CorrelationTopology: топология C# Storm, которая случайным образом генерирует события начала и конца для пользовательских сеансов.</span><span class="sxs-lookup"><span data-stu-id="d3437-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="d3437-169">Каждый сеанс продолжается от 1 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="d3437-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="d3437-170">SessionInfo: Консольное приложение C#, создающий таблицу HBase hello и предоставляются примеры запросов tooreturn сведения о данных, сохраненный сеанс.</span><span class="sxs-lookup"><span data-stu-id="d3437-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="d3437-171">Создать таблицу hello</span><span class="sxs-lookup"><span data-stu-id="d3437-171">Create hello table</span></span>

1. <span data-ttu-id="d3437-172">Откройте hello **SessionInfo** проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3437-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="d3437-173">В **обозревателе решений**, щелкните правой кнопкой мыши hello **SessionInfo** проект и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="d3437-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![Снимок экрана меню с выбранными свойствами](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="d3437-175">Выберите **параметры**, а затем набор hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d3437-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="d3437-176">HBaseClusterURL: hello URL-адрес tooyour HBase кластера.</span><span class="sxs-lookup"><span data-stu-id="d3437-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="d3437-177">Например, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="d3437-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="d3437-178">HBaseClusterUserName: учетная запись администратора/HTTP hello для кластера</span><span class="sxs-lookup"><span data-stu-id="d3437-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="d3437-179">HBaseClusterPassword: hello пароль для учетной записи пользователя admin/HTTP hello</span><span class="sxs-lookup"><span data-stu-id="d3437-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="d3437-180">HBaseTableName: имя hello hello toouse таблицы с этим примером</span><span class="sxs-lookup"><span data-stu-id="d3437-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="d3437-181">HBaseTableColumnFamily: имя семейства столбца hello</span><span class="sxs-lookup"><span data-stu-id="d3437-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![Изображение окна "Параметры"](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="d3437-183">Запустите решение hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-183">Run hello solution.</span></span> <span data-ttu-id="d3437-184">При появлении запроса выберите таблицу, hello ключа toocreate hello «c» в кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="d3437-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="d3437-185">Построение и развертывание топологии Storm hello</span><span class="sxs-lookup"><span data-stu-id="d3437-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="d3437-186">Откройте hello **CorrelationTopology** решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3437-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="d3437-187">В **обозревателе решений**, щелкните правой кнопкой мыши hello **CorrelationTopology** проекта и выберите пункт Свойства.</span><span class="sxs-lookup"><span data-stu-id="d3437-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="d3437-188">Выберите в окне свойств hello **параметры** и введите hello значения конфигурации для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="d3437-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="d3437-189">Hello первые 5 являются hello используются одинаковые значения, hello **SessionInfo** проекта:</span><span class="sxs-lookup"><span data-stu-id="d3437-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="d3437-190">HBaseClusterURL: hello URL-адрес tooyour HBase кластера.</span><span class="sxs-lookup"><span data-stu-id="d3437-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="d3437-191">Например, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="d3437-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="d3437-192">HBaseClusterUserName: hello admin/HTTP учетная запись пользователя для кластера.</span><span class="sxs-lookup"><span data-stu-id="d3437-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="d3437-193">HBaseClusterPassword: hello пароль для учетной записи пользователя admin/HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="d3437-194">HBaseTableName: имя hello hello toouse таблицы с этим примером.</span><span class="sxs-lookup"><span data-stu-id="d3437-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="d3437-195">Это значение является одинаковым hello имя таблицы, используемой в проекте SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="d3437-196">HBaseTableColumnFamily: имя семейства столбца hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="d3437-197">Это значение является одинаковым hello имя семейства столбца как используемый в проекте SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d3437-198">Не изменяйте hello HBaseTableColumnNames, так как значения по умолчанию hello: hello имена, используемые **SessionInfo** tooretrieve данных.</span><span class="sxs-lookup"><span data-stu-id="d3437-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="d3437-199">Сохранить свойства hello, а затем постройте проект hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="d3437-200">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **отправить tooStorm на HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d3437-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="d3437-201">При появлении запроса введите учетные данные hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d3437-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![Пункт меню toostorm отправить изображение hello](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="d3437-203">В hello **отправить топологии** диалоговое окно, выберите hello Storm кластер toodeploy к этой топологии.</span><span class="sxs-lookup"><span data-stu-id="d3437-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d3437-204">Hello первый раз отправить топологии, может потребоваться несколько секунд имя hello tooretrieve своими кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d3437-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="d3437-205">Здравствуйте, после топологии hello отправлять и отправленных toohello кластера, **представление топологии Storm** открывает и отображает hello под управлением топологии.</span><span class="sxs-lookup"><span data-stu-id="d3437-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="d3437-206">toorefresh hello данных, выберите hello **CorrelationTopology** и используется кнопка обновления hello в hello верхнем правом углу страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="d3437-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![Изображение представления топологии hello](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="d3437-208">С началом создания данных топологии hello hello значение в hello **Emitted** приращения столбца.</span><span class="sxs-lookup"><span data-stu-id="d3437-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d3437-209">Если hello **представление топологии Storm** не открывается автоматически, используйте hello следующие tooopen действия:</span><span class="sxs-lookup"><span data-stu-id="d3437-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="d3437-210">В **обозревателе решений** разверните **Azure**, а затем — **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d3437-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="d3437-211">Щелкните правой кнопкой мыши hello Storm кластера, hello топологии ОС, а затем выберите **представление топологии Storm**</span><span class="sxs-lookup"><span data-stu-id="d3437-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="d3437-212">Запрос данных hello</span><span class="sxs-lookup"><span data-stu-id="d3437-212">Query hello data</span></span>

<span data-ttu-id="d3437-213">После получится данных используйте следующие шаги tooquery hello данные hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="d3437-214">Вернуть toohello **SessionInfo** проекта.</span><span class="sxs-lookup"><span data-stu-id="d3437-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="d3437-215">Если он не открыт, запустите новый экземпляр.</span><span class="sxs-lookup"><span data-stu-id="d3437-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="d3437-216">При появлении запроса выберите **s** toosearch для НАЧАЛА события.</span><span class="sxs-lookup"><span data-stu-id="d3437-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="d3437-217">Являются запрашиваемые tooenter начала и окончания времени toodefine диапазон времени - возвращаются только события, между этими двумя значениями времени.</span><span class="sxs-lookup"><span data-stu-id="d3437-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="d3437-218">Используйте следующие hello форматирования при вводе hello начала времени и завершения: ЧЧ: мм ''M' или 'pm».</span><span class="sxs-lookup"><span data-stu-id="d3437-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="d3437-219">Например, 11:20 pm.</span><span class="sxs-lookup"><span data-stu-id="d3437-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="d3437-220">события в журнал tooreturn использовать время начала перед hello Storm топологии была развернута и время окончания сейчас.</span><span class="sxs-lookup"><span data-stu-id="d3437-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="d3437-221">возвращаемые данные Hello содержит аналогичные toohello записи после текста:</span><span class="sxs-lookup"><span data-stu-id="d3437-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="d3437-222">Поиск hello works события окончания таким же как НАЧАЛА события.</span><span class="sxs-lookup"><span data-stu-id="d3437-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="d3437-223">От 1 до 5 минут после НАЧАЛА события hello события окончания создаются случайным образом.</span><span class="sxs-lookup"><span data-stu-id="d3437-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="d3437-224">Может иметь несколько раз события окончания hello диапазоны toofind tootry.</span><span class="sxs-lookup"><span data-stu-id="d3437-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="d3437-225">События окончания также содержать hello продолжительность сеанса hello - hello различие между hello время события НАЧАЛА и время окончания события.</span><span class="sxs-lookup"><span data-stu-id="d3437-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="d3437-226">Ниже приведен пример данных для событий КОНЕЦ:</span><span class="sxs-lookup"><span data-stu-id="d3437-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="d3437-227">Хотя hello введенные значения времени в формате местного времени, в формате UTC — время hello, возвращаемых запросом hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="d3437-228">Остановить hello топологии</span><span class="sxs-lookup"><span data-stu-id="d3437-228">Stop hello topology</span></span>

<span data-ttu-id="d3437-229">Когда вы будете готовы toostop hello топологии, возвращают toohello **CorrelationTopology** проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3437-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="d3437-230">В hello **представление топологии Storm**выберите топологию hello и затем использовать hello **Kill** кнопку вверху hello представление топологии hello.</span><span class="sxs-lookup"><span data-stu-id="d3437-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="d3437-231">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="d3437-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d3437-232">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3437-232">Next steps</span></span>

<span data-ttu-id="d3437-233">Другие примеры топологий для Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d3437-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
