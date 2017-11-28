---
title: "Перемещение данных из SAP HANA с помощью фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как перемещать данные из SAP HANA с использованием фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 2ab488d82d24999a6231e40cb719715463c51d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="3b6bc-103">Перемещение данных из SAP HANA с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="3b6bc-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="3b6bc-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из локального экземпляра SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="3b6bc-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="3b6bc-106">Вы можете скопировать данные из локального хранилища данных SAP HANA в любой поддерживаемый приемник данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="3b6bc-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3b6bc-108">Сейчас фабрика данных поддерживает перемещение данных из SAP HANA в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="3b6bc-109">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="3b6bc-109">Supported versions and installation</span></span>
<span data-ttu-id="3b6bc-110">Этот соединитель поддерживает все версии базы данных SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="3b6bc-111">Он поддерживает копирование данных из информационных моделей HANA (например, представлений Analytic и Calculation) и таблиц со строками и столбцами с помощью SQL-запросов.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="3b6bc-112">Чтобы обеспечить возможность подключения к экземпляру SAP HANA, установите следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="3b6bc-113">**Шлюз управления данными**. Служба фабрики данных поддерживает подключение к локальным хранилищам данным (включая SAP HANA) с помощью компонента, который называется шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="3b6bc-114">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="3b6bc-115">Шлюз является обязательным, даже если SAP HANA размещается на виртуальной машине IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="3b6bc-116">Шлюз можно установить на той же ВМ, на которой размещается хранилище данных, или на другой ВМ. Важно, чтобы шлюз мог подключиться к базе данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="3b6bc-117">**Драйвер ODBC для SAP HANA** на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="3b6bc-118">Драйвер ODBC для SAP HANA можно скачать на странице [SAP Software Download Center](https://support.sap.com/swdc) (Центр загрузки программного обеспечения SAP).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="3b6bc-119">Выполните поиск по ключевой фразе **SAP HANA CLIENT for Windows**.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="3b6bc-120">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="3b6bc-120">Getting started</span></span>
<span data-ttu-id="3b6bc-121">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="3b6bc-122">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="3b6bc-123">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="3b6bc-124">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3b6bc-125">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3b6bc-126">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="3b6bc-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="3b6bc-127">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="3b6bc-128">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="3b6bc-129">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3b6bc-130">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="3b6bc-131">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="3b6bc-132">Пример определения JSON для сущностей фабрики данных, которые используются для копирования данных из локального хранилища данных SAP HANA, вы найдете в разделе [Пример JSON. Копирование данных из SAP HANA в большой двоичный объект Azure](#json-example-copy-data-from-sap-hana-to-azure-blob) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3b6bc-133">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для хранилища данных SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3b6bc-134">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="3b6bc-134">Linked service properties</span></span>
<span data-ttu-id="3b6bc-135">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="3b6bc-136">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b6bc-136">Property</span></span> | <span data-ttu-id="3b6bc-137">Описание</span><span class="sxs-lookup"><span data-stu-id="3b6bc-137">Description</span></span> | <span data-ttu-id="3b6bc-138">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3b6bc-138">Allowed values</span></span> | <span data-ttu-id="3b6bc-139">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3b6bc-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="3b6bc-140">server</span><span class="sxs-lookup"><span data-stu-id="3b6bc-140">server</span></span> | <span data-ttu-id="3b6bc-141">Имя сервера, на котором размещен экземпляр SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="3b6bc-142">Если ваш сервер использует настроенный порт, укажите `server:port`.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="3b6bc-143">строка</span><span class="sxs-lookup"><span data-stu-id="3b6bc-143">string</span></span> | <span data-ttu-id="3b6bc-144">Да</span><span class="sxs-lookup"><span data-stu-id="3b6bc-144">Yes</span></span>
<span data-ttu-id="3b6bc-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b6bc-145">authenticationType</span></span> | <span data-ttu-id="3b6bc-146">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-146">Type of authentication.</span></span> | <span data-ttu-id="3b6bc-147">string.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-147">string.</span></span> <span data-ttu-id="3b6bc-148">Basic или Windows.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="3b6bc-149">Да</span><span class="sxs-lookup"><span data-stu-id="3b6bc-149">Yes</span></span> 
<span data-ttu-id="3b6bc-150">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="3b6bc-150">username</span></span> | <span data-ttu-id="3b6bc-151">Имя пользователя, имеющего доступ к серверу SAP.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="3b6bc-152">строка</span><span class="sxs-lookup"><span data-stu-id="3b6bc-152">string</span></span> | <span data-ttu-id="3b6bc-153">Да</span><span class="sxs-lookup"><span data-stu-id="3b6bc-153">Yes</span></span>
<span data-ttu-id="3b6bc-154">пароль</span><span class="sxs-lookup"><span data-stu-id="3b6bc-154">password</span></span> | <span data-ttu-id="3b6bc-155">Пароль для пользователя</span><span class="sxs-lookup"><span data-stu-id="3b6bc-155">Password for the user.</span></span> | <span data-ttu-id="3b6bc-156">string</span><span class="sxs-lookup"><span data-stu-id="3b6bc-156">string</span></span> | <span data-ttu-id="3b6bc-157">Да</span><span class="sxs-lookup"><span data-stu-id="3b6bc-157">Yes</span></span>
<span data-ttu-id="3b6bc-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b6bc-158">gatewayName</span></span> | <span data-ttu-id="3b6bc-159">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальному экземпляру SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="3b6bc-160">строка</span><span class="sxs-lookup"><span data-stu-id="3b6bc-160">string</span></span> | <span data-ttu-id="3b6bc-161">Да</span><span class="sxs-lookup"><span data-stu-id="3b6bc-161">Yes</span></span>
<span data-ttu-id="3b6bc-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b6bc-162">encryptedCredential</span></span> | <span data-ttu-id="3b6bc-163">Строка зашифрованных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-163">The encrypted credential string.</span></span> | <span data-ttu-id="3b6bc-164">string</span><span class="sxs-lookup"><span data-stu-id="3b6bc-164">string</span></span> | <span data-ttu-id="3b6bc-165">Нет</span><span class="sxs-lookup"><span data-stu-id="3b6bc-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="3b6bc-166">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="3b6bc-166">Dataset properties</span></span>
<span data-ttu-id="3b6bc-167">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3b6bc-168">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3b6bc-169">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="3b6bc-170">Для набора данных SAP HANA типа **RelationalTable** не поддерживаются какие-либо свойства типа.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="3b6bc-171">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="3b6bc-171">Copy activity properties</span></span>
<span data-ttu-id="3b6bc-172">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3b6bc-173">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="3b6bc-174">В свою очередь свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="3b6bc-175">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="3b6bc-176">Если источник действия копирования относится к типу **RelationalSource** (к которому относится SAP HANA), в разделе typeProperties доступны следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="3b6bc-177">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b6bc-177">Property</span></span> | <span data-ttu-id="3b6bc-178">Описание</span><span class="sxs-lookup"><span data-stu-id="3b6bc-178">Description</span></span> | <span data-ttu-id="3b6bc-179">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="3b6bc-179">Allowed values</span></span> | <span data-ttu-id="3b6bc-180">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3b6bc-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b6bc-181">query</span><span class="sxs-lookup"><span data-stu-id="3b6bc-181">query</span></span> | <span data-ttu-id="3b6bc-182">Указывает SQL-запрос для чтения данных из экземпляра SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="3b6bc-183">SQL-запрос.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-183">SQL query.</span></span> | <span data-ttu-id="3b6bc-184">Да</span><span class="sxs-lookup"><span data-stu-id="3b6bc-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="3b6bc-185">Пример JSON. Копирование данных из SAP HANA в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="3b6bc-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="3b6bc-186">Ниже приведен пример с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3b6bc-187">В этом примере показано, как скопировать данные из локального экземпляра SAP HANA в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="3b6bc-188">Тем не менее данные можно копировать **непосредственно** в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3b6bc-189">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="3b6bc-190">Он не включает в себя пошаговые инструкции по созданию фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="3b6bc-191">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="3b6bc-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="3b6bc-192">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="3b6bc-193">Связанная служба типа [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="3b6bc-194">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3b6bc-195">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="3b6bc-196">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3b6bc-197">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3b6bc-198">Пример копирует данные из экземпляра SAP HANA в большой двоичный объект Azure раз в час.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="3b6bc-199">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="3b6bc-200">Сначала настройте шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="3b6bc-201">Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="3b6bc-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="3b6bc-202">Связанная служба SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3b6bc-202">SAP HANA linked service</span></span>
<span data-ttu-id="3b6bc-203">Это связанная служба связывает экземпляр SAP HANA с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="3b6bc-204">Свойству type присваивается значение **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="3b6bc-205">Раздел typeProperties содержит сведения о подключении для экземпляра SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="3b6bc-206">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="3b6bc-206">Azure Storage linked service</span></span>
<span data-ttu-id="3b6bc-207">Связанная служба связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="3b6bc-208">Для свойства type задано значение **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="3b6bc-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="3b6bc-209">Раздел typeProperties содержит сведения о подключении для учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="3b6bc-210">Входной набор данных SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3b6bc-210">SAP HANA input dataset</span></span>

<span data-ttu-id="3b6bc-211">Этот набор данных определяет набор данных SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="3b6bc-212">Для набора данных фабрики данных задается тип **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="3b6bc-213">В настоящее время какие-либо свойства типа для набора данных SAP HANA не указываются пользователем.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="3b6bc-214">Запрос в определении действия копирования указывает, какие данные следует считывать из экземпляра SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="3b6bc-215">Если для свойства external задать значение true, то фабрика данных воспримет эту таблицу как внешнюю, которая создана не в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="3b6bc-216">Свойства frequency и interval определяют расписание.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="3b6bc-217">В этом случае данные считываются из экземпляра SAP HANA раз в час.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="3b6bc-218">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="3b6bc-218">Azure Blob output dataset</span></span>
<span data-ttu-id="3b6bc-219">Этот набор данных определяет выходной набор данных больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="3b6bc-220">Для свойства type задано значение AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="3b6bc-221">В разделе typeProperties указывается, где сохраняются данные, скопированные из экземпляра SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="3b6bc-222">Данные записываются в новый большой двоичный объект раз в час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3b6bc-223">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3b6bc-224">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="3b6bc-225">Конвейер с действием копирования</span><span class="sxs-lookup"><span data-stu-id="3b6bc-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="3b6bc-226">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="3b6bc-227">В определении JSON конвейера для типа **source** установлено значение **RelationalSource** (для источника SAP HANA), а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="3b6bc-228">SQL-запрос, указанный для свойства **query** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="3b6bc-229">Сопоставление типов для SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3b6bc-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="3b6bc-230">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="3b6bc-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="3b6bc-231">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="3b6bc-232">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="3b6bc-233">При перемещении данных из SAP HANA для преобразования типов SAP HANA в типы .NET используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="3b6bc-234">Тип SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3b6bc-234">SAP HANA Type</span></span> | <span data-ttu-id="3b6bc-235">Тип данных на основе .NET</span><span class="sxs-lookup"><span data-stu-id="3b6bc-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="3b6bc-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="3b6bc-236">TINYINT</span></span> | <span data-ttu-id="3b6bc-237">Byte</span><span class="sxs-lookup"><span data-stu-id="3b6bc-237">Byte</span></span>
<span data-ttu-id="3b6bc-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="3b6bc-238">SMALLINT</span></span> | <span data-ttu-id="3b6bc-239">Int16</span><span class="sxs-lookup"><span data-stu-id="3b6bc-239">Int16</span></span>
<span data-ttu-id="3b6bc-240">INT</span><span class="sxs-lookup"><span data-stu-id="3b6bc-240">INT</span></span> | <span data-ttu-id="3b6bc-241">Int32</span><span class="sxs-lookup"><span data-stu-id="3b6bc-241">Int32</span></span>
<span data-ttu-id="3b6bc-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="3b6bc-242">BIGINT</span></span> | <span data-ttu-id="3b6bc-243">Int64</span><span class="sxs-lookup"><span data-stu-id="3b6bc-243">Int64</span></span>
<span data-ttu-id="3b6bc-244">REAL</span><span class="sxs-lookup"><span data-stu-id="3b6bc-244">REAL</span></span> | <span data-ttu-id="3b6bc-245">Single</span><span class="sxs-lookup"><span data-stu-id="3b6bc-245">Single</span></span>
<span data-ttu-id="3b6bc-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="3b6bc-246">DOUBLE</span></span> | <span data-ttu-id="3b6bc-247">Single</span><span class="sxs-lookup"><span data-stu-id="3b6bc-247">Single</span></span>
<span data-ttu-id="3b6bc-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="3b6bc-248">DECIMAL</span></span> | <span data-ttu-id="3b6bc-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="3b6bc-249">Decimal</span></span>
<span data-ttu-id="3b6bc-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="3b6bc-250">BOOLEAN</span></span> | <span data-ttu-id="3b6bc-251">Byte</span><span class="sxs-lookup"><span data-stu-id="3b6bc-251">Byte</span></span>
<span data-ttu-id="3b6bc-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="3b6bc-252">VARCHAR</span></span> | <span data-ttu-id="3b6bc-253">string</span><span class="sxs-lookup"><span data-stu-id="3b6bc-253">String</span></span>
<span data-ttu-id="3b6bc-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="3b6bc-254">NVARCHAR</span></span> | <span data-ttu-id="3b6bc-255">Строка</span><span class="sxs-lookup"><span data-stu-id="3b6bc-255">String</span></span>
<span data-ttu-id="3b6bc-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="3b6bc-256">CLOB</span></span> | <span data-ttu-id="3b6bc-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="3b6bc-257">Byte[]</span></span>
<span data-ttu-id="3b6bc-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="3b6bc-258">ALPHANUM</span></span> | <span data-ttu-id="3b6bc-259">string</span><span class="sxs-lookup"><span data-stu-id="3b6bc-259">String</span></span>
<span data-ttu-id="3b6bc-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="3b6bc-260">BLOB</span></span> | <span data-ttu-id="3b6bc-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="3b6bc-261">Byte[]</span></span>
<span data-ttu-id="3b6bc-262">DATE</span><span class="sxs-lookup"><span data-stu-id="3b6bc-262">DATE</span></span> | <span data-ttu-id="3b6bc-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="3b6bc-263">DateTime</span></span>
<span data-ttu-id="3b6bc-264">TIME</span><span class="sxs-lookup"><span data-stu-id="3b6bc-264">TIME</span></span> | <span data-ttu-id="3b6bc-265">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="3b6bc-265">TimeSpan</span></span>
<span data-ttu-id="3b6bc-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="3b6bc-266">TIMESTAMP</span></span> | <span data-ttu-id="3b6bc-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="3b6bc-267">DateTime</span></span>
<span data-ttu-id="3b6bc-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="3b6bc-268">SECONDDATE</span></span> | <span data-ttu-id="3b6bc-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="3b6bc-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="3b6bc-270">Известные ограничения</span><span class="sxs-lookup"><span data-stu-id="3b6bc-270">Known limitations</span></span>
<span data-ttu-id="3b6bc-271">Существует несколько известных ограничений, действующих при копировании данных из SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="3b6bc-272">Строки NVARCHAR усекаются до 4000 знаков Юникода.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="3b6bc-273">SMALLDECIMAL не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="3b6bc-274">VARBINARY не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="3b6bc-275">Допустимый диапазон дат: 30.12.1899–31.12.9999.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="3b6bc-276">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="3b6bc-276">Map source to sink columns</span></span>
<span data-ttu-id="3b6bc-277">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3b6bc-278">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="3b6bc-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="3b6bc-279">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="3b6bc-280">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3b6bc-281">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3b6bc-282">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3b6bc-283">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="3b6bc-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3b6bc-284">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="3b6bc-284">Performance and Tuning</span></span>
<span data-ttu-id="3b6bc-285">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="3b6bc-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
