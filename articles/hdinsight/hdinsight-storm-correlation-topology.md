---
title: "Сопоставление событий в динамике по времени с помощью Storm и HBase в HDInsight"
description: "Узнайте, как сопоставлять события, поступающие в разное время, с помощью Storm и HBase в HDInsight."
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
ms.openlocfilehash: 06630096383601e48e8f69f8553314cee42f5f3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="4944e-103">Сопоставление событий, поступающих в разное время, с помощью Storm и HBase</span><span class="sxs-lookup"><span data-stu-id="4944e-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="4944e-104">Благодаря сохранению постоянных данных в Apache Storm можно сопоставлять данные, поступающие в разное время.</span><span class="sxs-lookup"><span data-stu-id="4944e-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="4944e-105">Например, связывание событий входа и выхода в пользовательском сеансе для расчета продолжительности сеанса.</span><span class="sxs-lookup"><span data-stu-id="4944e-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span></span>

<span data-ttu-id="4944e-106">В этом документе рассматривается создание базовой топологии Storm C#, которая отслеживает события входа и выхода в пользовательских сеансах и рассчитывает продолжительность сеанса.</span><span class="sxs-lookup"><span data-stu-id="4944e-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span></span> <span data-ttu-id="4944e-107">Топология использует HBase как хранилище постоянных данных.</span><span class="sxs-lookup"><span data-stu-id="4944e-107">The topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="4944e-108">HBase также позволяет выполнять пакетные запросы к историческим данным для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="4944e-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span></span> <span data-ttu-id="4944e-109">Например, количество пользовательских сеансов, начатых или завершенных за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="4944e-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4944e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4944e-110">Prerequisites</span></span>

* <span data-ttu-id="4944e-111">Инструменты Visual Studio и средства HDInsight для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4944e-111">Visual Studio and the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="4944e-112">Дополнительные сведения см. в статье [Начало работы со средствами HDInsight для Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4944e-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="4944e-113">Apache Storm в кластере HDInsight (под управлением Windows).</span><span class="sxs-lookup"><span data-stu-id="4944e-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="4944e-114">Топологии SCP.NET поддерживаются в кластерах Storm под управлением Linux с 28 октября 2016 года, однако пакет SDK .NET для HBase, доступный с этой же даты, некорректно работает в HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="4944e-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="4944e-115">Apache HBase в кластере HDInsight (под управлением Linux или Windows).</span><span class="sxs-lookup"><span data-stu-id="4944e-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4944e-116">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="4944e-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4944e-117">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4944e-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4944e-118">[Java](https://java.com) 1.7 или более поздняя версия в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="4944e-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="4944e-119">Java используется для упаковки топологии при отправке в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4944e-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="4944e-120">Переменная среды **JAVA_HOME** должна указывать на каталог, содержащий Java.</span><span class="sxs-lookup"><span data-stu-id="4944e-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="4944e-121">В этом каталоге должен быть вложенный каталог **%JAVA_HOME%/bin**.</span><span class="sxs-lookup"><span data-stu-id="4944e-121">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="architecture"></a><span data-ttu-id="4944e-122">Архитектура</span><span class="sxs-lookup"><span data-stu-id="4944e-122">Architecture</span></span>

![Диаграмма потока данных через топологию](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="4944e-124">Для сопоставления событий требуется стандартный идентификатор источника события.</span><span class="sxs-lookup"><span data-stu-id="4944e-124">Correlating events requires a common identifier for the event source.</span></span> <span data-ttu-id="4944e-125">Например, идентификатор пользователя, идентификатор сеанса или другой элемент данных, который является: a) уникальным и (b) включен во все данные, отправляемые в Storm.</span><span class="sxs-lookup"><span data-stu-id="4944e-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span></span> <span data-ttu-id="4944e-126">В этом примере в качестве идентификатора сеанса используется значение GUID.</span><span class="sxs-lookup"><span data-stu-id="4944e-126">This example uses a GUID value to represent a session ID.</span></span>

<span data-ttu-id="4944e-127">В примере есть два кластера HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4944e-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="4944e-128">HBase: хранилище постоянных данных для исторических данных;</span><span class="sxs-lookup"><span data-stu-id="4944e-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="4944e-129">Storm: используется для получения входящих данных.</span><span class="sxs-lookup"><span data-stu-id="4944e-129">Storm: used to ingest incoming data</span></span>

<span data-ttu-id="4944e-130">Данные генерируются топологией Storm случайным образом и включают следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="4944e-130">The data is randomly generated by the Storm topology, and consists of the following items:</span></span>

* <span data-ttu-id="4944e-131">идентификатор сеанса: GUID, который однозначно определяет каждый сеанс;</span><span class="sxs-lookup"><span data-stu-id="4944e-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="4944e-132">событие: событие НАЧАЛО или КОНЕЦ,</span><span class="sxs-lookup"><span data-stu-id="4944e-132">Event: a START or END event.</span></span> <span data-ttu-id="4944e-133">в этом примере НАЧАЛО всегда раньше КОНЦА;</span><span class="sxs-lookup"><span data-stu-id="4944e-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="4944e-134">Время: время события.</span><span class="sxs-lookup"><span data-stu-id="4944e-134">Time: the time of the event.</span></span>

<span data-ttu-id="4944e-135">Эти данные обрабатываются и хранятся в HBase.</span><span class="sxs-lookup"><span data-stu-id="4944e-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="4944e-136">Топология Storm</span><span class="sxs-lookup"><span data-stu-id="4944e-136">Storm topology</span></span>

<span data-ttu-id="4944e-137">При запуске сеанса событие **НАЧАЛО** принимается топологией и записывается в HBase.</span><span class="sxs-lookup"><span data-stu-id="4944e-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span></span> <span data-ttu-id="4944e-138">При получении события **КОНЕЦ** топология извлекает событие **НАЧАЛО** и вычисляет время между двумя этими событиями.</span><span class="sxs-lookup"><span data-stu-id="4944e-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span></span> <span data-ttu-id="4944e-139">Это значение **продолжительности** сохраняется в HBase вместе с информацией о событии **КОНЕЦ**.</span><span class="sxs-lookup"><span data-stu-id="4944e-139">This **Duration** value is then stored in HBase along with the **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4944e-140">Эта топология представляет собой базовый шаблон, но в продуктивном решении  потребуется учесть следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="4944e-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span></span>
>
> * <span data-ttu-id="4944e-141">события, поступающие не по порядку;</span><span class="sxs-lookup"><span data-stu-id="4944e-141">Events arriving out of order</span></span>
> * <span data-ttu-id="4944e-142">повторяющиеся события;</span><span class="sxs-lookup"><span data-stu-id="4944e-142">Duplicate events</span></span>
> * <span data-ttu-id="4944e-143">удаленные события.</span><span class="sxs-lookup"><span data-stu-id="4944e-143">Dropped events</span></span>

<span data-ttu-id="4944e-144">Пример топологии состоит из следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="4944e-144">The sample topology is composed of the following components:</span></span>

* <span data-ttu-id="4944e-145">Session.cs: моделирование пользовательского сеанса путем создания случайного идентификатора сеанса, времени начала и его продолжительности.</span><span class="sxs-lookup"><span data-stu-id="4944e-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span></span>

* <span data-ttu-id="4944e-146">Spout.cs: создание 100 сеансов, генерация события НАЧАЛО, ожидание случайного тайм-аута для каждого сеанса и генерация события КОНЕЦ.</span><span class="sxs-lookup"><span data-stu-id="4944e-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="4944e-147">Затем завершенные сеансы удаляются для создания новых.</span><span class="sxs-lookup"><span data-stu-id="4944e-147">Then recycles ended sessions to generate new ones.</span></span>

* <span data-ttu-id="4944e-148">HBaseLookupBolt.cs: использование идентификатора сеанса для поиска информации о сеансе из HBase.</span><span class="sxs-lookup"><span data-stu-id="4944e-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span></span> <span data-ttu-id="4944e-149">При обработке события КОНЕЦ обнаруживается соответствующее событие НАЧАЛО и рассчитывается длительность сеанса.</span><span class="sxs-lookup"><span data-stu-id="4944e-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span></span>

* <span data-ttu-id="4944e-150">HBaseBolt.cs: сохранение информации в HBase.</span><span class="sxs-lookup"><span data-stu-id="4944e-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="4944e-151">TypeHelper.cs: преобразование типа при считывании из/записи в HBase.</span><span class="sxs-lookup"><span data-stu-id="4944e-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="4944e-152">Схема HBase</span><span class="sxs-lookup"><span data-stu-id="4944e-152">HBase schema</span></span>

<span data-ttu-id="4944e-153">В HBase данные хранятся в таблице со следующей схемой и параметрами:</span><span class="sxs-lookup"><span data-stu-id="4944e-153">In HBase, the data is stored in a table with the following schema/settings:</span></span>

* <span data-ttu-id="4944e-154">Ключ строки: идентификатор сеанса используется как ключ для строк в этой таблице.</span><span class="sxs-lookup"><span data-stu-id="4944e-154">Row key: the session ID is used as the key for rows in this table.</span></span>

* <span data-ttu-id="4944e-155">Семейство столбцов: имя семейства — cf.</span><span class="sxs-lookup"><span data-stu-id="4944e-155">Column family: the family name is 'cf'.</span></span> <span data-ttu-id="4944e-156">В этом семействе хранятся столбцы:</span><span class="sxs-lookup"><span data-stu-id="4944e-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="4944e-157">событие: НАЧАЛО или КОНЕЦ;</span><span class="sxs-lookup"><span data-stu-id="4944e-157">event: START or END.</span></span>

  * <span data-ttu-id="4944e-158">время: время события в миллисекундах;</span><span class="sxs-lookup"><span data-stu-id="4944e-158">time: the time in milliseconds that the event occurred.</span></span>

  * <span data-ttu-id="4944e-159">продолжительность: интервал между событиями НАЧАЛО и КОНЕЦ.</span><span class="sxs-lookup"><span data-stu-id="4944e-159">duration: the length between START and END event.</span></span>

* <span data-ttu-id="4944e-160">версии: для семейства cf установлено сохранение 5 версий каждой строки.</span><span class="sxs-lookup"><span data-stu-id="4944e-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4944e-161">Версии представляют собой запись предыдущих значений, сохраненных для конкретного ключа строки.</span><span class="sxs-lookup"><span data-stu-id="4944e-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="4944e-162">По умолчанию HBase возвращает значение только для самой последней версии строки.</span><span class="sxs-lookup"><span data-stu-id="4944e-162">By default, HBase only returns the value for the most recent version of a row.</span></span> <span data-ttu-id="4944e-163">В этом случае та же строка используется для всех событий (НАЧАЛО, КОНЕЦ). Каждая версия строки идентифицируется по метке времени.</span><span class="sxs-lookup"><span data-stu-id="4944e-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span></span> <span data-ttu-id="4944e-164">Версии предоставляют обзор прошлых событий, зарегистрированных для определенного идентификатора.</span><span class="sxs-lookup"><span data-stu-id="4944e-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-the-project"></a><span data-ttu-id="4944e-165">Скачивание проекта</span><span class="sxs-lookup"><span data-stu-id="4944e-165">Download the project</span></span>

<span data-ttu-id="4944e-166">Пример проекта можно загрузить на странице [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="4944e-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="4944e-167">Данный файл содержит следующие проекты C#:</span><span class="sxs-lookup"><span data-stu-id="4944e-167">This download contains the following C# projects:</span></span>

* <span data-ttu-id="4944e-168">CorrelationTopology: топология C# Storm, которая случайным образом генерирует события начала и конца для пользовательских сеансов.</span><span class="sxs-lookup"><span data-stu-id="4944e-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="4944e-169">Каждый сеанс продолжается от 1 до 5 минут.</span><span class="sxs-lookup"><span data-stu-id="4944e-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="4944e-170">SessionInfo: консольное приложение C#, в котором создается таблица HBase и предоставляются примеры запросов для получения информации о хранимых данных сеанса.</span><span class="sxs-lookup"><span data-stu-id="4944e-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span></span>

## <a name="create-the-table"></a><span data-ttu-id="4944e-171">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="4944e-171">Create the table</span></span>

1. <span data-ttu-id="4944e-172">Откройте проект **SessionInfo** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4944e-172">Open the **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="4944e-173">В **обозревателе решений** щелкните правой кнопкой мыши проект **SessionInfo** и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4944e-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span></span>

    ![Снимок экрана меню с выбранными свойствами](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="4944e-175">Выберите **Параметры**и установите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="4944e-175">Select **Settings**, then set the following values:</span></span>

   * <span data-ttu-id="4944e-176">HBaseClusterURL: URL-адрес кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="4944e-176">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="4944e-177">Например, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="4944e-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="4944e-178">HBaseClusterUserName: учетная запись администратора/пользователя HTTP для кластера.</span><span class="sxs-lookup"><span data-stu-id="4944e-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="4944e-179">HBaseClusterPassword: пароль для учетной записи администратора/пользователя HTTP.</span><span class="sxs-lookup"><span data-stu-id="4944e-179">HBaseClusterPassword: the password for the admin/HTTP user account</span></span>

   * <span data-ttu-id="4944e-180">HBaseTableName: имя таблицы для использования с этим примером.</span><span class="sxs-lookup"><span data-stu-id="4944e-180">HBaseTableName: the name of the table to use with this example</span></span>

   * <span data-ttu-id="4944e-181">HBaseTableColumnFamily: имя семейства столбцов.</span><span class="sxs-lookup"><span data-stu-id="4944e-181">HBaseTableColumnFamily: The column family name</span></span>

     ![Изображение окна "Параметры"](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="4944e-183">Запустите решение.</span><span class="sxs-lookup"><span data-stu-id="4944e-183">Run the solution.</span></span> <span data-ttu-id="4944e-184">При появлении запроса нажмите клавишу C для создания таблицы в кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="4944e-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span></span>

## <a name="build-and-deploy-the-storm-topology"></a><span data-ttu-id="4944e-185">Построение и развертывание топологии Storm</span><span class="sxs-lookup"><span data-stu-id="4944e-185">Build and deploy the Storm topology</span></span>

1. <span data-ttu-id="4944e-186">Откройте решение **CorrelationTopology** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4944e-186">Open the **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="4944e-187">В **обозревателе решений** щелкните правой кнопкой мыши проект **CorrelationTopology** и выберите "Свойства".</span><span class="sxs-lookup"><span data-stu-id="4944e-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="4944e-188">В окне "Свойства" выберите **Параметры** и введите значения конфигурации для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="4944e-188">In the properties window, select **Settings** and enter the configuration values for this project.</span></span> <span data-ttu-id="4944e-189">Первые пять значений должны быть теми же значениями, которые используются в проекте **SessionInfo**.</span><span class="sxs-lookup"><span data-stu-id="4944e-189">The first 5 are the same values used by the **SessionInfo** project:</span></span>

   * <span data-ttu-id="4944e-190">HBaseClusterURL: URL-адрес кластера HBase.</span><span class="sxs-lookup"><span data-stu-id="4944e-190">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="4944e-191">Например, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="4944e-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="4944e-192">HBaseClusterUserName: учетная запись администратора или учетная запись пользователя HTTP для кластера.</span><span class="sxs-lookup"><span data-stu-id="4944e-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="4944e-193">HBaseClusterPassword: пароль для учетной записи администратора или учетной записи пользователя HTTP.</span><span class="sxs-lookup"><span data-stu-id="4944e-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span></span>

   * <span data-ttu-id="4944e-194">HBaseTableName: имя таблицы для использования с этим примером.</span><span class="sxs-lookup"><span data-stu-id="4944e-194">HBaseTableName: the name of the table to use with this example.</span></span> <span data-ttu-id="4944e-195">Это то же имя таблицы, которое используется в проекте SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="4944e-195">This value is the same table name as used in the SessionInfo project.</span></span>

   * <span data-ttu-id="4944e-196">HBaseTableColumnFamily: имя семейства столбцов.</span><span class="sxs-lookup"><span data-stu-id="4944e-196">HBaseTableColumnFamily: The column family name.</span></span> <span data-ttu-id="4944e-197">Это то же имя семейства столбцов, которое используется в проекте SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="4944e-197">This value is the same column family name as used in the SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4944e-198">Не изменяйте HBaseTableColumnNames, поскольку по умолчанию указаны имена, которые используются в проекте **SessionInfo** для получения данных.</span><span class="sxs-lookup"><span data-stu-id="4944e-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span></span>

4. <span data-ttu-id="4944e-199">Сохраните свойства и создайте проект.</span><span class="sxs-lookup"><span data-stu-id="4944e-199">Save the properties, then build the project.</span></span>

5. <span data-ttu-id="4944e-200">В **обозревателе решений** щелкните правой кнопкой мыши проект и выберите **Submit to Storm on HDInsight** (Отправить в Storm в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="4944e-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="4944e-201">При появлении запроса введите учетные данные для своей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4944e-201">If prompted, enter the credentials for your Azure subscription.</span></span>

   ![Изображение пункта меню "Отправить в Storm"](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="4944e-203">В диалоговом окне **Submit Topology** (Отправить топологию) выберите кластер Storm для развертывания этой топологии.</span><span class="sxs-lookup"><span data-stu-id="4944e-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4944e-204">Первая отправка топологии может занять несколько секунд, необходимых для получения имени кластеров HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4944e-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="4944e-205">После передачи и отправки топологии в кластер откроется окно **Storm Topology View** (Представление топологии Storm) с отображенной запущенной топологией.</span><span class="sxs-lookup"><span data-stu-id="4944e-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span></span> <span data-ttu-id="4944e-206">Чтобы обновить сведения о топологии, выберите **CorrelationTopology** и нажмите кнопку "Обновить" в верхней правой части страницы.</span><span class="sxs-lookup"><span data-stu-id="4944e-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span></span>

   ![Изображение представления топологии](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="4944e-208">Когда топология начнет создавать данные, значение в столбце **Emitted** (Сгенерированный) начнет увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="4944e-208">When the topology begins generating data, the value in the **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4944e-209">Если **представление топологии Storm** не открывается автоматически, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4944e-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span></span>
   >
   > 1. <span data-ttu-id="4944e-210">В **обозревателе решений** разверните **Azure**, а затем — **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4944e-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="4944e-211">Щелкните правой кнопкой мыши кластер Storm, в котором запущена топология, а затем выберите **Просмотреть топологии Storm**.</span><span class="sxs-lookup"><span data-stu-id="4944e-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-the-data"></a><span data-ttu-id="4944e-212">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="4944e-212">Query the data</span></span>

<span data-ttu-id="4944e-213">После генерации данных выполните следующие действия для запроса данных.</span><span class="sxs-lookup"><span data-stu-id="4944e-213">Once data has been emitted, use the following steps to query the data.</span></span>

1. <span data-ttu-id="4944e-214">Вернитесь в проект **SessionInfo** .</span><span class="sxs-lookup"><span data-stu-id="4944e-214">Return to the **SessionInfo** project.</span></span> <span data-ttu-id="4944e-215">Если он не открыт, запустите новый экземпляр.</span><span class="sxs-lookup"><span data-stu-id="4944e-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="4944e-216">При появлении запроса выберите **s** для поиска события START.</span><span class="sxs-lookup"><span data-stu-id="4944e-216">When prompted, select **s** to search for START event.</span></span> <span data-ttu-id="4944e-217">Вам будет предложено ввести время начала и окончания, чтобы определить диапазон времени. Будут возвращены только те события, которые произошли между этими двумя моментами времени.</span><span class="sxs-lookup"><span data-stu-id="4944e-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="4944e-218">При вводе значения времени начала и окончания используйте следующий формат: ЧЧ:ММ и am или pm.</span><span class="sxs-lookup"><span data-stu-id="4944e-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="4944e-219">Например, 11:20 pm.</span><span class="sxs-lookup"><span data-stu-id="4944e-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="4944e-220">Чтобы вернуть зарегистрированные события, используйте время начала до развертывания топологии Storm и актуальное время окончания.</span><span class="sxs-lookup"><span data-stu-id="4944e-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="4944e-221">Возвращенные данные содержат записи, аналогичные следующим:</span><span class="sxs-lookup"><span data-stu-id="4944e-221">The return data contains entries similar to the following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="4944e-222">Поиск событий КОНЕЦ выполняется так же, как и для событий НАЧАЛО.</span><span class="sxs-lookup"><span data-stu-id="4944e-222">Searching for END events works the same as START events.</span></span> <span data-ttu-id="4944e-223">Однако события КОНЕЦ генерируются случайным образом спустя 1–5 минут после  события НАЧАЛО.</span><span class="sxs-lookup"><span data-stu-id="4944e-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span></span> <span data-ttu-id="4944e-224">Для поиска событий КОНЕЦ может потребоваться попробовать несколько временных диапазонов.</span><span class="sxs-lookup"><span data-stu-id="4944e-224">You may have to try a few time ranges to find the END events.</span></span> <span data-ttu-id="4944e-225">События КОНЕЦ также содержат продолжительность сеанса, т. е. разницу между событием НАЧАЛО и временем окончания события КОНЕЦ.</span><span class="sxs-lookup"><span data-stu-id="4944e-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span></span> <span data-ttu-id="4944e-226">Ниже приведен пример данных для событий КОНЕЦ:</span><span class="sxs-lookup"><span data-stu-id="4944e-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="4944e-227">Хотя значения времени вводятся в местном часовом поясе, возвращаемые значения времени указываются для UTC.</span><span class="sxs-lookup"><span data-stu-id="4944e-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="4944e-228">Остановка топологии</span><span class="sxs-lookup"><span data-stu-id="4944e-228">Stop the topology</span></span>

<span data-ttu-id="4944e-229">Когда вы будете готовы остановить топологию, вернитесь в проект **CorrelationTopology** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4944e-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="4944e-230">В **представлении топологии Storm** выберите топологию и нажмите кнопку **Прервать** в верхней части представления топологии.</span><span class="sxs-lookup"><span data-stu-id="4944e-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="4944e-231">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="4944e-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="4944e-232">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4944e-232">Next steps</span></span>

<span data-ttu-id="4944e-233">Другие примеры топологий для Storm см. в разделе [Примеры топологий для Storm в HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4944e-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
