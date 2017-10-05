---
title: "Платформы аналитики: сравнение Apache Storm и Stream Analytics | Документация Майкрософт"
description: "Рекомендации по выбору облачной платформы аналитики на примере сравнения Apache Storm и Stream Analytics. Возможности и отличия."
keywords: "платформа аналитики, платформы аналитики, облачная платформа аналитики, сравнение storm"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 97044cb5d7b0b3fcb3b85328df618a265bc59b61
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="7c092-105">Выбор платформы потоковой аналитики: сравнение Apache Storm и Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7c092-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="7c092-106">Azure предоставляет несколько решений для анализа потоковой передачи данных: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) и [Apache Storm на Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="7c092-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="7c092-107">Обе эти платформы аналитики предоставляют преимущества решения PaaS.</span><span class="sxs-lookup"><span data-stu-id="7c092-107">Both analytics platforms provide the benefits of a PaaS solution.</span></span> <span data-ttu-id="7c092-108">Но платформы имеют ряд существенных отличий в своих возможностях, а также в настройке и управлении.</span><span class="sxs-lookup"><span data-stu-id="7c092-108">But the platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="7c092-109">Эта статья содержит сравнение функций, которое поможет вам выбрать между Apache Storm и Azure Stream Analytics в качестве облачной платформы аналитики.</span><span class="sxs-lookup"><span data-stu-id="7c092-109">This article provides a side-by-side comparison of features to help you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="7c092-110">Общие компоненты</span><span class="sxs-lookup"><span data-stu-id="7c092-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7c092-112">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7c092-113">
                    <strong>Apache Storm в HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-114">
                    <strong>Открытый исходный код</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-115">Нет.</span><span class="sxs-lookup"><span data-stu-id="7c092-115">No.</span></span> <span data-ttu-id="7c092-116">Служба Azure Stream Analytics принадлежит исключительно корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7c092-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-117">Да.</span><span class="sxs-lookup"><span data-stu-id="7c092-117">Yes.</span></span> <span data-ttu-id="7c092-118">Служба Apache Storm является лицензированной технологией Apache.</span><span class="sxs-lookup"><span data-stu-id="7c092-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-119">
                    <strong>Служба технической поддержки Майкрософт</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-120">Да</span><span class="sxs-lookup"><span data-stu-id="7c092-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-121">Да</span><span class="sxs-lookup"><span data-stu-id="7c092-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-122">
                    <strong>Требования к оборудованию</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-123">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="7c092-123">None.</span></span> <span data-ttu-id="7c092-124">Azure Stream Analytics является службой Azure.</span><span class="sxs-lookup"><span data-stu-id="7c092-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-125">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="7c092-125">None.</span></span> <span data-ttu-id="7c092-126">Apache Storm является службой Azure.</span><span class="sxs-lookup"><span data-stu-id="7c092-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-127">
                    <strong>Единицы верхнего уровня</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-128">Пользователи развертывают и отслеживают задания потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="7c092-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-129">Пользователи развертывают и отслеживают весь кластер, который может содержать несколько заданий Storm, а также другие рабочие нагрузки (включая пакетную службу).</span><span class="sxs-lookup"><span data-stu-id="7c092-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-130">
                    <strong>Цены</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-131">Оценивается согласно объему обработанных данных и требуемому количеству единиц потоковой передачи на каждый час выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="7c092-131">Priced by volume of data processed and the number of streaming units required per hour that the job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="7c092-132">Дополнительные сведения см. на странице <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">цен на Stream Analytics</a>.</span><span class="sxs-lookup"><span data-stu-id="7c092-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-133">Вы платите за продолжительность работы кластера, независимо от развернутых заданий.</span><span class="sxs-lookup"><span data-stu-id="7c092-133">The unit of purchase is cluster-based, and is charged based on the time the cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="7c092-134">Дополнительные сведения см. на странице <a href="http://azure.microsoft.com/pricing/details/hdinsight/">цен на HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="7c092-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="7c092-135">Разработка</span><span class="sxs-lookup"><span data-stu-id="7c092-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7c092-137">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7c092-138">
                    <strong>Apache Storm в HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-139">
                    <strong>Возможности: SQL DSL</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-140">Да.</span><span class="sxs-lookup"><span data-stu-id="7c092-140">Yes.</span></span> <span data-ttu-id="7c092-141">Stream Analytics предоставляет язык на основе SQL для создания преобразований.</span><span class="sxs-lookup"><span data-stu-id="7c092-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-142">Нет.</span><span class="sxs-lookup"><span data-stu-id="7c092-142">No.</span></span> <span data-ttu-id="7c092-143">Пользователи пишут код на Java или C# или используют API Trident.</span><span class="sxs-lookup"><span data-stu-id="7c092-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-144">
                    <strong>Возможности: временные операторы</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-145">По умолчанию поддерживаются агрегаты данных на основе периодов времени и временные соединения.</span><span class="sxs-lookup"><span data-stu-id="7c092-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-146">Пользователю необходимо самому выполнить реализацию временных операторов.</span><span class="sxs-lookup"><span data-stu-id="7c092-146">Temporal operators must be implemented by the user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-147">
                    <strong>Интерфейс разработки</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-148">Пользователи могут создавать, отлаживать и отслеживать задания через портал Azure, используя пример данных на основе потока в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="7c092-148">Users can create, debug, and monitor jobs through the Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-149">Пользователи, использующие .NET, могут разрабатывать, отлаживать и отслеживать через Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c092-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="7c092-150">Пользователи, использующие Java или другие языки, могут применять интегрированную среду разработки по своему выбору.</span><span class="sxs-lookup"><span data-stu-id="7c092-150">Users using Java or other languages can use the IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-151">
                    <strong>Поддержка отладки</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-152">Отладку можно выполнить с помощью базовых журналов состояний заданий и операций.</span><span class="sxs-lookup"><span data-stu-id="7c092-152">Basic job status and operations logs are available to help debug.</span></span> <span data-ttu-id="7c092-153">Сейчас в Stream Analytics пользователи не могут указывать содержимое или его объем для журналов (например, режим подробного протоколирования).</span><span class="sxs-lookup"><span data-stu-id="7c092-153">Stream Analytics currently does not let users specify what content or how much content is included in the logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-154">Доступны подробные журналы.</span><span class="sxs-lookup"><span data-stu-id="7c092-154">Detailed logs are available.</span></span> <span data-ttu-id="7c092-155">Пользователи могут получить доступ к журналам в Visual Studio или войти в кластер и получить доступ к журналам напрямую.</span><span class="sxs-lookup"><span data-stu-id="7c092-155">Users can access logs in Visual Studio or by logging in to the cluster and accessing the logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-156">
                    <strong>Расширяемый пользовательский код</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-157">Частичная поддержка с помощью определяемых пользователем функций JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7c092-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="7c092-158">Дополнительные сведения см. в статье <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Определяемые пользователем функции JavaScript в Azure Stream Analytics</a>.</span><span class="sxs-lookup"><span data-stu-id="7c092-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-159">Да.</span><span class="sxs-lookup"><span data-stu-id="7c092-159">Yes.</span></span> <span data-ttu-id="7c092-160">Пользователи могут писать код на C#, Java или любом другом языке, поддерживаемом Storm.</span><span class="sxs-lookup"><span data-stu-id="7c092-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="7c092-161">Источники входных и выходных данных</span><span class="sxs-lookup"><span data-stu-id="7c092-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7c092-163">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7c092-164">
                    <strong>Apache Storm в HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-165">
                 <strong>Источники входных данных</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7c092-166">Концентраторы событий Azure и хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="7c092-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-167">Соединители доступны для концентраторов событий Azure, служебной шины Azure, Kafka и многих других компонентов.</span><span class="sxs-lookup"><span data-stu-id="7c092-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="7c092-168">Пользователи могут создавать дополнительные соединители с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="7c092-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-169">
                    <strong>Форматы входных данных</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-170">Avro, JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="7c092-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-171">Пользователи могут реализовать любой формат с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="7c092-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-172">
                    <strong>Выходные данные</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-173">Задание потоковой передачи может иметь несколько выходов.</span><span class="sxs-lookup"><span data-stu-id="7c092-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="7c092-174">Поддерживаемые источники выходных данных: концентраторы событий Azure, хранилище BLOB-объектов Azure, хранилище таблиц Azure, базы данных SQL Azure и Power BI.</span><span class="sxs-lookup"><span data-stu-id="7c092-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-175">Storm поддерживает множество типов выходных данных в топологии, каждый из которых может иметь настраиваемую логику для последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="7c092-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="7c092-176">Storm включает соединители для Power BI, концентраторы событий Azure, хранилище BLOB-объектов Azure, Azure Cosmos DB, SQL и HBase.</span><span class="sxs-lookup"><span data-stu-id="7c092-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="7c092-177">Пользователи могут создавать дополнительные соединители с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="7c092-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-178">
                    <strong>Форматы кодирования данных</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-179">Данные должны быть отформатированы с использованием UTF-8.</span><span class="sxs-lookup"><span data-stu-id="7c092-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-180">Пользователи могут реализовать любой формат кодирования данных с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="7c092-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="7c092-181">Управление и использование</span><span class="sxs-lookup"><span data-stu-id="7c092-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7c092-183">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7c092-184">
                    <strong>Apache Storm в HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-185">
                    <strong>Модель развертывания задания</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-186">Портал Azure, PowerShell, API REST</span><span class="sxs-lookup"><span data-stu-id="7c092-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-187">Портал Azure, PowerShell, Visual Studio и API REST.</span><span class="sxs-lookup"><span data-stu-id="7c092-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-188">
                    <strong>Мониторинг (статистика, счетчики, и т. д.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-189">Мониторинг реализуется c помощью портала Azure и API REST.</span><span class="sxs-lookup"><span data-stu-id="7c092-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="7c092-190">Пользователи также могут настраивать оповещения Azure.</span><span class="sxs-lookup"><span data-stu-id="7c092-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-191">Мониторинг реализуется с помощью пользовательского интерфейса Storm и API REST.</span><span class="sxs-lookup"><span data-stu-id="7c092-191">Monitoring is implemented using the Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-192">
                    <strong>Масштабируемость</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-193">Масштабируемость определяется числом единиц потоковой передачи для каждого задания.</span><span class="sxs-lookup"><span data-stu-id="7c092-193">Scalability is determined by the number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="7c092-194">Каждая единица потоковой передачи обрабатывает до 1 МБ/с, максимальное число единиц — 50.</span><span class="sxs-lookup"><span data-stu-id="7c092-194">Each Streaming Unit processes up to 1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="7c092-195">Дополнительные сведения см. в статье <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных</a>.</span><span class="sxs-lookup"><span data-stu-id="7c092-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale to increase throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-196">Масштабируемость определяется количеством узлов в кластере HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="7c092-196">Scalability is determined by the number of nodes in the HDInsight Storm cluster.</span></span> <span data-ttu-id="7c092-197">Верхний предел числа узлов определяется квотой Azure пользователя.</span><span class="sxs-lookup"><span data-stu-id="7c092-197">The top limit on the number of nodes is defined by the user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-198">
                    <strong>Ограничения обработки данных</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-199">Пользователи могут увеличить объем обрабатываемых данных и оптимизировать затраты, увеличивая или уменьшая число единиц потоковой передачи. Верхний предел — 1 ГБ/с.</span><span class="sxs-lookup"><span data-stu-id="7c092-199">Users can increase data processing or optimize costs by increasing or decreasing the number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-200">Пользователи могут масштабировать размер кластера.</span><span class="sxs-lookup"><span data-stu-id="7c092-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-201">
                    <strong>Остановка и возобновление</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-202">Возможность остановки и возобновления работы с последнего места остановки.</span><span class="sxs-lookup"><span data-stu-id="7c092-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-203">Возможность остановки и возобновления работы с последнего места остановки в зависимости от значения предела.</span><span class="sxs-lookup"><span data-stu-id="7c092-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-204">
                    <strong>Обновление услуг и платформы</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-205">Автоматическое исправление без простоев.</span><span class="sxs-lookup"><span data-stu-id="7c092-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-206">Автоматическое исправление без простоев.</span><span class="sxs-lookup"><span data-stu-id="7c092-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-207">
                    <strong>Непрерывность бизнес-процессов благодаря службам высокой доступности с гарантированными соглашениями об уровне обслуживания</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="7c092-208">SLA с временем бесперебойной работы на уровне 99,9%</span><span class="sxs-lookup"><span data-stu-id="7c092-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="7c092-209">Автоматическое восстановление после сбоев</span><span class="sxs-lookup"><span data-stu-id="7c092-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="7c092-210">Встроенная функция восстановления временных операторов с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="7c092-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-211">SLA с временем бесперебойной работы на уровне 99,9% кластера Storm.</span><span class="sxs-lookup"><span data-stu-id="7c092-211">SLA of 99.9% uptime of the Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="7c092-212">Apache Storm — это отказоустойчивая платформа потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="7c092-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="7c092-213">Однако пользователь несет ответственность за обеспечение непрерывного выполнения заданий потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="7c092-213">However, it is the user's responsibility to ensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="7c092-214">Дополнительные функции</span><span class="sxs-lookup"><span data-stu-id="7c092-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="7c092-216">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="7c092-217">
                    <strong>Apache Storm в HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-218">
                    <strong>Интервал и обработка событий не по порядку</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-219">Встроенные настраиваемые политики могут изменять порядок событий, удалять события или настраивать время продолжительности события.</span><span class="sxs-lookup"><span data-stu-id="7c092-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-220">Пользователь должен реализовать логику для обработки этого сценария.</span><span class="sxs-lookup"><span data-stu-id="7c092-220">Users must implement logic to handle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-221">
                    <strong>Ссылочные данные</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-222">Ссылочные данные доступны из хранилища BLOB-объектов Azure с максимальным размером 100 МБ кэша в памяти.</span><span class="sxs-lookup"><span data-stu-id="7c092-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="7c092-223">Ссылочные данные обновляются службой.</span><span class="sxs-lookup"><span data-stu-id="7c092-223">Reference data is refreshed by the service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-224">Нет ограничений на размер данных.</span><span class="sxs-lookup"><span data-stu-id="7c092-224">No limits on data size.</span></span> <span data-ttu-id="7c092-225">Соединители доступны для HBase, Azure Cosmos DB, SQL Server и Azure.</span><span class="sxs-lookup"><span data-stu-id="7c092-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="7c092-226">Пользователи могут создавать дополнительные соединители с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="7c092-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="7c092-227">Ссылочные данные должны обновляться с помощью пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="7c092-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="7c092-228">
                    <strong>Интеграция с машинным обучением</strong>
                </span><span class="sxs-lookup"><span data-stu-id="7c092-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="7c092-229">Опубликованные модели Машинного обучения Azure можно настроить в качестве функций во время создания задания.</span><span class="sxs-lookup"><span data-stu-id="7c092-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="7c092-230">Дополнительные сведения см. в статье <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Масштабирование заданий Stream Analytics с помощью функций машинного обучения Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="7c092-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="7c092-231">Доступно с помощью компонентов «сито»(bolts) в Storm.</span><span class="sxs-lookup"><span data-stu-id="7c092-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
