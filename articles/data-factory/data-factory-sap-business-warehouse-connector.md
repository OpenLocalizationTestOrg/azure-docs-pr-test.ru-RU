---
title: "Перемещение данных из SAP Business Warehouse с помощью фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как перемещать данные из SAP Business Warehouse с помощью фабрики данных Azure."
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
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="c3e8f-103">Перемещение данных из SAP Business Warehouse с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="c3e8f-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="c3e8f-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из локального экземпляра SAP Business Warehouse (BW).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="c3e8f-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c3e8f-106">Вы можете скопировать данные из локального хранилища данных SAP Business Warehouse в любой поддерживаемый приемник данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="c3e8f-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c3e8f-108">Сейчас фабрика данных поддерживает перемещение данных из SAP Business Warehouse в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="c3e8f-109">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-109">Supported versions and installation</span></span>
<span data-ttu-id="c3e8f-110">Этот соединитель поддерживает SAP Business Warehouse версии 7.x.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="c3e8f-111">Он поддерживает копирование данных из InfoCube и QueryCubes (включая запросы BEx) с помощью запросов многомерных выражений.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="c3e8f-112">Чтобы обеспечить возможность подключения к экземпляру SAP Business Warehouse, установите следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="c3e8f-113">**Шлюз управления данными**. Служба фабрики данных поддерживает подключение к локальным хранилищам данным (включая SAP Business Warehouse) с помощью компонента, который называется шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="c3e8f-114">В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="c3e8f-115">Шлюз является обязательным, даже если хранилище SAP Business Warehouse размещается на виртуальной машине IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="c3e8f-116">Шлюз можно установить на той же ВМ, на которой размещается хранилище данных, или на другой ВМ. Важно, чтобы шлюз мог подключиться к базе данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="c3e8f-117">**Библиотека SAP NetWeaver** на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="c3e8f-118">Библиотеку SAP Netweaver можно получить у администратора SAP или непосредственно на странице [SAP Software Download Center](https://support.sap.com/swdc) (Центр загрузки программного обеспечения SAP).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="c3e8f-119">Найдите **примечание к SAP № 1025361**, чтобы узнать адрес для скачивания самой последней версии.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="c3e8f-120">Убедитесь, что архитектура библиотеки SAP NetWeaver (32-разрядная или 64-разрядная) соответствует установленному шлюзу.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="c3e8f-121">Установите все файлы, включенные в состав пакета SDK RFC для SAP NetWeaver, согласно примечанию к SAP.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="c3e8f-122">Библиотека SAP NetWeaver также включена в состав клиентских инструментов SAP.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="c3e8f-123">Поместите библиотеки DLL, извлеченные из пакета SDK RFC для NetWeaver, в папку system32.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c3e8f-124">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="c3e8f-124">Getting started</span></span>
<span data-ttu-id="c3e8f-125">Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="c3e8f-126">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c3e8f-127">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="c3e8f-128">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c3e8f-129">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c3e8f-130">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c3e8f-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c3e8f-131">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c3e8f-132">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c3e8f-133">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c3e8f-134">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c3e8f-135">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c3e8f-136">Пример определения JSON для сущностей фабрики данных, которые используются для копирования данных из локального хранилища данных SAP Business Warehouse, вы найдете в разделе [Пример JSON. Копирование данных из SAP Business Warehouse в большой двоичный объект Azure](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c3e8f-137">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для хранилища данных SAP BW.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c3e8f-138">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="c3e8f-138">Linked service properties</span></span>
<span data-ttu-id="c3e8f-139">В таблице ниже приведено описание элементов JSON, которые относятся к связанной службе SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="c3e8f-140">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3e8f-140">Property</span></span> | <span data-ttu-id="c3e8f-141">Описание</span><span class="sxs-lookup"><span data-stu-id="c3e8f-141">Description</span></span> | <span data-ttu-id="c3e8f-142">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="c3e8f-142">Allowed values</span></span> | <span data-ttu-id="c3e8f-143">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c3e8f-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="c3e8f-144">server</span><span class="sxs-lookup"><span data-stu-id="c3e8f-144">server</span></span> | <span data-ttu-id="c3e8f-145">Имя сервера, на котором размещен экземпляр SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="c3e8f-146">string</span><span class="sxs-lookup"><span data-stu-id="c3e8f-146">string</span></span> | <span data-ttu-id="c3e8f-147">Да</span><span class="sxs-lookup"><span data-stu-id="c3e8f-147">Yes</span></span>
<span data-ttu-id="c3e8f-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="c3e8f-148">systemNumber</span></span> | <span data-ttu-id="c3e8f-149">Номер системы SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="c3e8f-150">Двузначное десятичное число, представленное в виде строки.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="c3e8f-151">Да</span><span class="sxs-lookup"><span data-stu-id="c3e8f-151">Yes</span></span>
<span data-ttu-id="c3e8f-152">clientid</span><span class="sxs-lookup"><span data-stu-id="c3e8f-152">clientId</span></span> | <span data-ttu-id="c3e8f-153">Идентификатор клиента в системе SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="c3e8f-154">Трехзначное десятичное число, представленное в виде строки.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="c3e8f-155">Да</span><span class="sxs-lookup"><span data-stu-id="c3e8f-155">Yes</span></span>
<span data-ttu-id="c3e8f-156">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="c3e8f-156">username</span></span> | <span data-ttu-id="c3e8f-157">Имя пользователя, имеющего доступ к серверу SAP.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="c3e8f-158">строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-158">string</span></span> | <span data-ttu-id="c3e8f-159">Да</span><span class="sxs-lookup"><span data-stu-id="c3e8f-159">Yes</span></span>
<span data-ttu-id="c3e8f-160">пароль</span><span class="sxs-lookup"><span data-stu-id="c3e8f-160">password</span></span> | <span data-ttu-id="c3e8f-161">Пароль для пользователя</span><span class="sxs-lookup"><span data-stu-id="c3e8f-161">Password for the user.</span></span> | <span data-ttu-id="c3e8f-162">string</span><span class="sxs-lookup"><span data-stu-id="c3e8f-162">string</span></span> | <span data-ttu-id="c3e8f-163">Да</span><span class="sxs-lookup"><span data-stu-id="c3e8f-163">Yes</span></span>
<span data-ttu-id="c3e8f-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c3e8f-164">gatewayName</span></span> | <span data-ttu-id="c3e8f-165">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальному экземпляру SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="c3e8f-166">строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-166">string</span></span> | <span data-ttu-id="c3e8f-167">Да</span><span class="sxs-lookup"><span data-stu-id="c3e8f-167">Yes</span></span>
<span data-ttu-id="c3e8f-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c3e8f-168">encryptedCredential</span></span> | <span data-ttu-id="c3e8f-169">Строка зашифрованных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-169">The encrypted credential string.</span></span> | <span data-ttu-id="c3e8f-170">string</span><span class="sxs-lookup"><span data-stu-id="c3e8f-170">string</span></span> | <span data-ttu-id="c3e8f-171">Нет</span><span class="sxs-lookup"><span data-stu-id="c3e8f-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="c3e8f-172">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="c3e8f-172">Dataset properties</span></span>
<span data-ttu-id="c3e8f-173">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c3e8f-174">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c3e8f-175">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c3e8f-176">Для набора данных SAP Business Warehouse типа **RelationalTable** не поддерживаются какие-либо свойства типа.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="c3e8f-177">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="c3e8f-177">Copy activity properties</span></span>
<span data-ttu-id="c3e8f-178">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c3e8f-179">Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="c3e8f-180">В свою очередь свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="c3e8f-181">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c3e8f-182">Если источник действия копирования относится к типу **RelationalSource** (к которому относится SAP Business Warehouse), в разделе typeProperties доступны следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c3e8f-183">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3e8f-183">Property</span></span> | <span data-ttu-id="c3e8f-184">Описание</span><span class="sxs-lookup"><span data-stu-id="c3e8f-184">Description</span></span> | <span data-ttu-id="c3e8f-185">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="c3e8f-185">Allowed values</span></span> | <span data-ttu-id="c3e8f-186">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c3e8f-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3e8f-187">query</span><span class="sxs-lookup"><span data-stu-id="c3e8f-187">query</span></span> | <span data-ttu-id="c3e8f-188">Указывает запрос многомерных выражений для чтения данных из экземпляра SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="c3e8f-189">Запрос многомерных выражений.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-189">MDX query.</span></span> | <span data-ttu-id="c3e8f-190">Да</span><span class="sxs-lookup"><span data-stu-id="c3e8f-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="c3e8f-191">Пример JSON. Копирование данных из SAP Business Warehouse в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="c3e8f-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="c3e8f-192">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c3e8f-193">В этом примере показано, как скопировать данные из локальной системы SAP Business Warehouse в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="c3e8f-194">Тем не менее данные можно копировать **непосредственно** в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c3e8f-195">Этот пример содержит фрагменты кода JSON.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="c3e8f-196">Он не включает в себя пошаговые инструкции по созданию фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="c3e8f-197">Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="c3e8f-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="c3e8f-198">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="c3e8f-199">Связанная служба типа [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="c3e8f-200">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c3e8f-201">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="c3e8f-202">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c3e8f-203">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c3e8f-204">Пример копирует данные из экземпляра SAP Business Warehouse в большой двоичный объект Azure раз в час.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="c3e8f-205">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c3e8f-206">Сначала настройте шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="c3e8f-207">Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="c3e8f-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="c3e8f-208">Связанная служба SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="c3e8f-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="c3e8f-209">Это связанная служба связывает экземпляр SAP Business Warehouse с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="c3e8f-210">Свойству type присваивается значение **SapBw**.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="c3e8f-211">Раздел typeProperties содержит сведения о подключении для экземпляра SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="c3e8f-212">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="c3e8f-212">Azure Storage linked service</span></span>
<span data-ttu-id="c3e8f-213">Связанная служба связывает учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="c3e8f-214">Для свойства type задано значение **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="c3e8f-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="c3e8f-215">Раздел typeProperties содержит сведения о подключении для учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="c3e8f-216">Входной набор данных SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="c3e8f-216">SAP BW input dataset</span></span>
<span data-ttu-id="c3e8f-217">Этот набор данных определяет набор данных SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="c3e8f-218">Для набора данных фабрики данных задается тип **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="c3e8f-219">В настоящее время какие-либо свойства типа для набора данных SAP Business Warehouse не указываются пользователем.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="c3e8f-220">Запрос в определении действия копирования указывает, какие данные следует считывать из экземпляра SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="c3e8f-221">Если для свойства external задать значение true, то фабрика данных воспримет эту таблицу как внешнюю, которая создана не в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="c3e8f-222">Свойства frequency и interval определяют расписание.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="c3e8f-223">В этом случае данные считываются из экземпляра SAP Business Warehouse раз в час.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c3e8f-224">Выходной набор данных BLOB-объекта Azure</span><span class="sxs-lookup"><span data-stu-id="c3e8f-224">Azure Blob output dataset</span></span>
<span data-ttu-id="c3e8f-225">Этот набор данных определяет выходной набор данных больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="c3e8f-226">Для свойства type задано значение AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="c3e8f-227">В разделе typeProperties указывается, где сохраняются данные, скопированные из экземпляра SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="c3e8f-228">Данные записываются в новый большой двоичный объект раз в час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c3e8f-229">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c3e8f-230">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="c3e8f-231">Конвейер с действием копирования</span><span class="sxs-lookup"><span data-stu-id="c3e8f-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="c3e8f-232">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="c3e8f-233">В определении JSON конвейера для типа **source** установлено значение **RelationalSource** (для источника SAP Business Warehouse), а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c3e8f-234">Запрос, указанный для свойства **query**, выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="c3e8f-235">Сопоставление типов для SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="c3e8f-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="c3e8f-236">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="c3e8f-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="c3e8f-237">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="c3e8f-238">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="c3e8f-239">При перемещении данных из SAP Business Warehouse для преобразования типов SAP Business Warehouse в типы .NET используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="c3e8f-240">Тип данных в словаре ABAP</span><span class="sxs-lookup"><span data-stu-id="c3e8f-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="c3e8f-241">Тип данных .NET</span><span class="sxs-lookup"><span data-stu-id="c3e8f-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="c3e8f-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="c3e8f-242">ACCP</span></span> |  <span data-ttu-id="c3e8f-243">int</span><span class="sxs-lookup"><span data-stu-id="c3e8f-243">Int</span></span>
<span data-ttu-id="c3e8f-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="c3e8f-244">CHAR</span></span> | <span data-ttu-id="c3e8f-245">Строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-245">String</span></span>
<span data-ttu-id="c3e8f-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="c3e8f-246">CLNT</span></span> | <span data-ttu-id="c3e8f-247">Строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-247">String</span></span>
<span data-ttu-id="c3e8f-248">CURR</span><span class="sxs-lookup"><span data-stu-id="c3e8f-248">CURR</span></span> | <span data-ttu-id="c3e8f-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="c3e8f-249">Decimal</span></span>
<span data-ttu-id="c3e8f-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="c3e8f-250">CUKY</span></span> | <span data-ttu-id="c3e8f-251">Строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-251">String</span></span>
<span data-ttu-id="c3e8f-252">DEC</span><span class="sxs-lookup"><span data-stu-id="c3e8f-252">DEC</span></span> | <span data-ttu-id="c3e8f-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="c3e8f-253">Decimal</span></span>
<span data-ttu-id="c3e8f-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="c3e8f-254">FLTP</span></span> | <span data-ttu-id="c3e8f-255">Double</span><span class="sxs-lookup"><span data-stu-id="c3e8f-255">Double</span></span>
<span data-ttu-id="c3e8f-256">INT1</span><span class="sxs-lookup"><span data-stu-id="c3e8f-256">INT1</span></span> | <span data-ttu-id="c3e8f-257">Byte</span><span class="sxs-lookup"><span data-stu-id="c3e8f-257">Byte</span></span>
<span data-ttu-id="c3e8f-258">INT2</span><span class="sxs-lookup"><span data-stu-id="c3e8f-258">INT2</span></span> | <span data-ttu-id="c3e8f-259">Int16</span><span class="sxs-lookup"><span data-stu-id="c3e8f-259">Int16</span></span>
<span data-ttu-id="c3e8f-260">INT4</span><span class="sxs-lookup"><span data-stu-id="c3e8f-260">INT4</span></span> | <span data-ttu-id="c3e8f-261">int</span><span class="sxs-lookup"><span data-stu-id="c3e8f-261">Int</span></span>
<span data-ttu-id="c3e8f-262">LANG</span><span class="sxs-lookup"><span data-stu-id="c3e8f-262">LANG</span></span> | <span data-ttu-id="c3e8f-263">Строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-263">String</span></span>
<span data-ttu-id="c3e8f-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="c3e8f-264">LCHR</span></span> | <span data-ttu-id="c3e8f-265">string</span><span class="sxs-lookup"><span data-stu-id="c3e8f-265">String</span></span>
<span data-ttu-id="c3e8f-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="c3e8f-266">LRAW</span></span> | <span data-ttu-id="c3e8f-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c3e8f-267">Byte[]</span></span>
<span data-ttu-id="c3e8f-268">PREC</span><span class="sxs-lookup"><span data-stu-id="c3e8f-268">PREC</span></span> | <span data-ttu-id="c3e8f-269">Int16</span><span class="sxs-lookup"><span data-stu-id="c3e8f-269">Int16</span></span>
<span data-ttu-id="c3e8f-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="c3e8f-270">QUAN</span></span> | <span data-ttu-id="c3e8f-271">Decimal</span><span class="sxs-lookup"><span data-stu-id="c3e8f-271">Decimal</span></span>
<span data-ttu-id="c3e8f-272">RAW</span><span class="sxs-lookup"><span data-stu-id="c3e8f-272">RAW</span></span> | <span data-ttu-id="c3e8f-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c3e8f-273">Byte[]</span></span>
<span data-ttu-id="c3e8f-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="c3e8f-274">RAWSTRING</span></span> | <span data-ttu-id="c3e8f-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c3e8f-275">Byte[]</span></span>
<span data-ttu-id="c3e8f-276">STRING</span><span class="sxs-lookup"><span data-stu-id="c3e8f-276">STRING</span></span> | <span data-ttu-id="c3e8f-277">string</span><span class="sxs-lookup"><span data-stu-id="c3e8f-277">String</span></span>
<span data-ttu-id="c3e8f-278">ЕДИНИЦА ИЗМЕРЕНИЯ</span><span class="sxs-lookup"><span data-stu-id="c3e8f-278">UNIT</span></span> | <span data-ttu-id="c3e8f-279">Строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-279">String</span></span>
<span data-ttu-id="c3e8f-280">DATS</span><span class="sxs-lookup"><span data-stu-id="c3e8f-280">DATS</span></span> | <span data-ttu-id="c3e8f-281">Строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-281">String</span></span>
<span data-ttu-id="c3e8f-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="c3e8f-282">NUMC</span></span> | <span data-ttu-id="c3e8f-283">Строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-283">String</span></span>
<span data-ttu-id="c3e8f-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="c3e8f-284">TIMS</span></span> | <span data-ttu-id="c3e8f-285">Строка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="c3e8f-286">Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в разделе [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="c3e8f-287">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="c3e8f-287">Map source to sink columns</span></span>
<span data-ttu-id="c3e8f-288">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c3e8f-289">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="c3e8f-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="c3e8f-290">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c3e8f-291">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c3e8f-292">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c3e8f-293">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c3e8f-294">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="c3e8f-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c3e8f-295">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="c3e8f-295">Performance and Tuning</span></span>
<span data-ttu-id="c3e8f-296">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="c3e8f-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
