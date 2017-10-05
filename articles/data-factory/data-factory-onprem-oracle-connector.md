---
title: "Копирование данных в базу данных Oracle и из нее с помощью фабрики данных | Документация Майкрософт"
description: "Узнайте, как копировать данные в локальную базу данных Oracle или из нее с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="db6f4-103">Копирование данных в локальную базу данных Oracle и обратно с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="db6f4-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="db6f4-104">В этой статье рассказывается, как с помощью действия копирования в фабрике данных Azure перемещать данные в локальную базу данных Oracle и обратно.</span><span class="sxs-lookup"><span data-stu-id="db6f4-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="db6f4-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="db6f4-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="db6f4-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="db6f4-106">Supported scenarios</span></span>
<span data-ttu-id="db6f4-107">Данные можно скопировать **из базы данных Oracle** в следующие хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="db6f4-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="db6f4-108">Данные можно скопировать **в базу данных Oracle** из следующих хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="db6f4-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="db6f4-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="db6f4-109">Prerequisites</span></span>
<span data-ttu-id="db6f4-110">Фабрика данных поддерживает подключение к локальным источникам Oracle с помощью шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="db6f4-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="db6f4-111">Сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md), а пошаговые инструкции по настройке шлюза для перемещения данных с использованием конвейера — в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="db6f4-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="db6f4-112">Шлюз является обязательным, даже если база данных Oracle размещается на виртуальной машине Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="db6f4-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="db6f4-113">Шлюз можно установить на той же ВМ IaaS, на которой размещается хранилище данных, или на другой ВМ. Важно, чтобы шлюз мог подключиться к базе данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="db6f4-114">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="db6f4-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="db6f4-115">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="db6f4-115">Supported versions and installation</span></span>
<span data-ttu-id="db6f4-116">Этот соединитель Oracle поддерживает две версии драйверов.</span><span class="sxs-lookup"><span data-stu-id="db6f4-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="db6f4-117">**Драйвер Майкрософт для Oracle (рекомендуется)**. Начиная со шлюза управления данными версии 2.7, драйвер Майкрософт для Oracle устанавливается автоматически вместе со шлюзом. Поэтому нет необходимости дополнительно устанавливать драйвер для подключения к Oracle. Кроме того, производительность копирования при использовании этого драйвера может увеличиться.</span><span class="sxs-lookup"><span data-stu-id="db6f4-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="db6f4-118">Ниже перечислены поддерживаемые версии баз данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="db6f4-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="db6f4-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="db6f4-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="db6f4-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="db6f4-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="db6f4-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="db6f4-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="db6f4-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="db6f4-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="db6f4-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db6f4-124">В настоящее время драйвер Майкрософт для Oracle поддерживает копирование данных из базы данных Oracle, но не поддерживает запись к базу данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="db6f4-125">Обратите внимание, что этот драйвер не поддерживает возможность тестирования подключения на вкладке "Диагностика" в шлюзе управления данными.</span><span class="sxs-lookup"><span data-stu-id="db6f4-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="db6f4-126">Кроме того, для проверки подключения можно воспользоваться мастером копирования.</span><span class="sxs-lookup"><span data-stu-id="db6f4-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="db6f4-127">**Поставщик данных Oracle для .NET**: для копирования данных в базу данных Oracle и из нее также можно использовать поставщик данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="db6f4-128">Входит в состав [компонентов доступа к данным Oracle для Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="db6f4-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="db6f4-129">Установите соответствующую версию (32- или 64- разрядную) на компьютере, на котором установлен шлюз.</span><span class="sxs-lookup"><span data-stu-id="db6f4-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="db6f4-130">[Поставщик данных Oracle для .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) может обращаться к Oracle Database 10g версии 2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="db6f4-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="db6f4-131">Если вы выбрали "XCopy Installation" (Установка XCopy), то следуйте инструкциям в файле readme.htm.</span><span class="sxs-lookup"><span data-stu-id="db6f4-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="db6f4-132">Мы советуем выбрать установщик через пользовательский интерфейс (а не через XCopy).</span><span class="sxs-lookup"><span data-stu-id="db6f4-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="db6f4-133">После установки поставщика **перезапустите** на компьютере службу узла шлюза управления данными, используя приложение "Службы" или диспетчер конфигурации шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="db6f4-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="db6f4-134">При использовании мастера копирования для создания конвейера копирования тип драйвера будет определен автоматически.</span><span class="sxs-lookup"><span data-stu-id="db6f4-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="db6f4-135">Драйвер Майкрософт будет использоваться по умолчанию, если только вы не используете версию шлюза ниже 2.7 или выбрали Oracle в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="db6f4-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="db6f4-136">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="db6f4-136">Getting started</span></span>
<span data-ttu-id="db6f4-137">Создать конвейер с действием копирования, который перемещает данные из локальной базы данных Oracle или в нее, можно с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="db6f4-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="db6f4-138">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="db6f4-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="db6f4-139">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="db6f4-140">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="db6f4-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="db6f4-141">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="db6f4-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="db6f4-142">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="db6f4-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="db6f4-143">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="db6f4-143">Create a **data factory**.</span></span> <span data-ttu-id="db6f4-144">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="db6f4-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="db6f4-145">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="db6f4-146">Например, при копировании данных из базы данных Oralce в хранилище BLOB-объектов Azure создайте две связанные службы, чтобы связать базу данных Oralce и учетную запись хранения Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="db6f4-147">Сведения о свойствах связанной службы, относящихся к Oralce, см. в разделе [Свойства связанной службы](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="db6f4-148">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="db6f4-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="db6f4-149">В примере, упомянутом на последнем шаге, создайте набор данных, чтобы указать таблицу в базе данных Oracle, содержащую входные данные.</span><span class="sxs-lookup"><span data-stu-id="db6f4-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="db6f4-150">И создайте другой набор данных, чтобы указать контейнер BLOB-объектов и папку, содержащую данные, скопированные из базы данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="db6f4-151">Сведения о свойствах набора данных, относящихся к Oracle, см. в разделе [Свойства набора данных](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="db6f4-152">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="db6f4-153">В примере выше OracleSource используется как источник, а BlobSink — как приемник для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="db6f4-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="db6f4-154">Аналогично, при копировании из хранилища BLOB-объектов Azure в базу данных Oracle в действии копирования используются BlobSource и OracleSink.</span><span class="sxs-lookup"><span data-stu-id="db6f4-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="db6f4-155">Сведения о свойствах действия копирования, относящихся к базе данных Oracle, см. в разделе [Свойства действия копирования](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="db6f4-156">Для получения сведений о том, как использовать хранилище данных в качестве источника или приемника, щелкните ссылку в предыдущем разделе об источнике данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="db6f4-157">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="db6f4-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="db6f4-158">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="db6f4-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="db6f4-159">Примеры с определениями JSON для сущностей фабрики данных, которые используются для копирования данных в локальную базу данных Oracle и обратно, см. в разделе [Примеры JSON](#json-examples-for-copying-data-to-and-from-oracle-database) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="db6f4-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="db6f4-160">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="db6f4-161">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="db6f4-161">Linked service properties</span></span>
<span data-ttu-id="db6f4-162">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="db6f4-163">Свойство</span><span class="sxs-lookup"><span data-stu-id="db6f4-163">Property</span></span> | <span data-ttu-id="db6f4-164">Описание</span><span class="sxs-lookup"><span data-stu-id="db6f4-164">Description</span></span> | <span data-ttu-id="db6f4-165">Обязательно</span><span class="sxs-lookup"><span data-stu-id="db6f4-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db6f4-166">type</span><span class="sxs-lookup"><span data-stu-id="db6f4-166">type</span></span> |<span data-ttu-id="db6f4-167">Для свойства type необходимо задать значение **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="db6f4-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="db6f4-168">Да</span><span class="sxs-lookup"><span data-stu-id="db6f4-168">Yes</span></span> |
| <span data-ttu-id="db6f4-169">driverType</span><span class="sxs-lookup"><span data-stu-id="db6f4-169">driverType</span></span> | <span data-ttu-id="db6f4-170">Укажите, какой драйвер следует использовать для копирования данных в базу данных Oracle и из нее.</span><span class="sxs-lookup"><span data-stu-id="db6f4-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="db6f4-171">Допустимые значения: **Майкрософт** или **ODP** (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="db6f4-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="db6f4-172">Дополнительные сведения о драйверах см. в разделе [Поддерживаемые версии и установка](#supported-versions-and-installation).</span><span class="sxs-lookup"><span data-stu-id="db6f4-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="db6f4-173">Нет</span><span class="sxs-lookup"><span data-stu-id="db6f4-173">No</span></span> |
| <span data-ttu-id="db6f4-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="db6f4-174">connectionString</span></span> | <span data-ttu-id="db6f4-175">В свойстве connectionString указываются сведения, необходимые для подключения к экземпляру базы данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="db6f4-176">Да</span><span class="sxs-lookup"><span data-stu-id="db6f4-176">Yes</span></span> |
| <span data-ttu-id="db6f4-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="db6f4-177">gatewayName</span></span> | <span data-ttu-id="db6f4-178">Имя шлюза, который будет использоваться для подключения к локальному серверу Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="db6f4-179">Да</span><span class="sxs-lookup"><span data-stu-id="db6f4-179">Yes</span></span> |

<span data-ttu-id="db6f4-180">**Пример: использование драйвера Майкрософт**</span><span class="sxs-lookup"><span data-stu-id="db6f4-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="db6f4-181">**Пример: использование драйвера ODP**</span><span class="sxs-lookup"><span data-stu-id="db6f4-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="db6f4-182">Допустимые форматы приведены на [этом сайте](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/).</span><span class="sxs-lookup"><span data-stu-id="db6f4-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="db6f4-183">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="db6f4-183">Dataset properties</span></span>
<span data-ttu-id="db6f4-184">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="db6f4-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="db6f4-185">Такие разделы, как структура, доступность и политика набора данных JSON, одинаковы для всех видов наборов данных (Oracle, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="db6f4-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="db6f4-186">Раздел typeProperties во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="db6f4-187">Раздел typeProperties набора данных с типом OracleTable обладает следующими свойствами.</span><span class="sxs-lookup"><span data-stu-id="db6f4-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="db6f4-188">Свойство</span><span class="sxs-lookup"><span data-stu-id="db6f4-188">Property</span></span> | <span data-ttu-id="db6f4-189">Описание</span><span class="sxs-lookup"><span data-stu-id="db6f4-189">Description</span></span> | <span data-ttu-id="db6f4-190">Обязательно</span><span class="sxs-lookup"><span data-stu-id="db6f4-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db6f4-191">tableName</span><span class="sxs-lookup"><span data-stu-id="db6f4-191">tableName</span></span> |<span data-ttu-id="db6f4-192">Имя таблицы в базе данных Oracle, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="db6f4-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="db6f4-193">Нет (если указан параметр **oracleReaderQuery** объекта **OracleSource**)</span><span class="sxs-lookup"><span data-stu-id="db6f4-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="db6f4-194">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="db6f4-194">Copy activity properties</span></span>
<span data-ttu-id="db6f4-195">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="db6f4-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="db6f4-196">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="db6f4-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="db6f4-197">Действие копирования принимает только один набор входных данных и возвращает только один набор выходных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="db6f4-198">В свою очередь свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="db6f4-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="db6f4-199">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="db6f4-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="db6f4-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="db6f4-200">OracleSource</span></span>
<span data-ttu-id="db6f4-201">Если источник относится к типу **OracleSource**, в разделе **typeProperties** для действия копирования доступны следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="db6f4-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="db6f4-202">Свойство</span><span class="sxs-lookup"><span data-stu-id="db6f4-202">Property</span></span> | <span data-ttu-id="db6f4-203">Описание</span><span class="sxs-lookup"><span data-stu-id="db6f4-203">Description</span></span> | <span data-ttu-id="db6f4-204">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="db6f4-204">Allowed values</span></span> | <span data-ttu-id="db6f4-205">Обязательно</span><span class="sxs-lookup"><span data-stu-id="db6f4-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db6f4-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="db6f4-206">oracleReaderQuery</span></span> |<span data-ttu-id="db6f4-207">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-207">Use the custom query to read data.</span></span> |<span data-ttu-id="db6f4-208">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="db6f4-208">SQL query string.</span></span> <span data-ttu-id="db6f4-209">Например, select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="db6f4-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="db6f4-210">Если не указано другое, то выполняется следующая инструкция SQL: select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="db6f4-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="db6f4-211">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="db6f4-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="db6f4-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="db6f4-212">OracleSink</span></span>
<span data-ttu-id="db6f4-213">**OracleSink** поддерживает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="db6f4-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="db6f4-214">Свойство</span><span class="sxs-lookup"><span data-stu-id="db6f4-214">Property</span></span> | <span data-ttu-id="db6f4-215">Описание</span><span class="sxs-lookup"><span data-stu-id="db6f4-215">Description</span></span> | <span data-ttu-id="db6f4-216">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="db6f4-216">Allowed values</span></span> | <span data-ttu-id="db6f4-217">Обязательно</span><span class="sxs-lookup"><span data-stu-id="db6f4-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db6f4-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="db6f4-218">writeBatchTimeout</span></span> |<span data-ttu-id="db6f4-219">Время ожидания до выполнения операции пакетной вставки, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="db6f4-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="db6f4-220">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="db6f4-220">timespan</span></span><br/><br/> <span data-ttu-id="db6f4-221">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="db6f4-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="db6f4-222">Нет</span><span class="sxs-lookup"><span data-stu-id="db6f4-222">No</span></span> |
| <span data-ttu-id="db6f4-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="db6f4-223">writeBatchSize</span></span> |<span data-ttu-id="db6f4-224">Вставляет данные в таблицу SQL, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="db6f4-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="db6f4-225">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="db6f4-225">Integer (number of rows)</span></span> |<span data-ttu-id="db6f4-226">Нет (значение по умолчанию — 100)</span><span class="sxs-lookup"><span data-stu-id="db6f4-226">No (default: 100)</span></span> |
| <span data-ttu-id="db6f4-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="db6f4-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="db6f4-228">Укажите запрос на выполнение действия копирования, позволяющий убедиться в том, что данные конкретного среза очищены.</span><span class="sxs-lookup"><span data-stu-id="db6f4-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="db6f4-229">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="db6f4-229">A query statement.</span></span> |<span data-ttu-id="db6f4-230">Нет</span><span class="sxs-lookup"><span data-stu-id="db6f4-230">No</span></span> |
| <span data-ttu-id="db6f4-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="db6f4-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="db6f4-232">Укажите имя столбца, в которое действие копирования добавляет автоматически созданный идентификатор среза. Этот идентификатор используется для очистки данных конкретного среза при повторном запуске.</span><span class="sxs-lookup"><span data-stu-id="db6f4-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="db6f4-233">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="db6f4-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="db6f4-234">Нет</span><span class="sxs-lookup"><span data-stu-id="db6f4-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="db6f4-235">Примеры JSON для копирования данных в базу данных Oracle и обратно</span><span class="sxs-lookup"><span data-stu-id="db6f4-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="db6f4-236">Ниже приведены примеры с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="db6f4-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="db6f4-237">Вы узнаете, как копировать данные между базой данных Oracle и хранилищем BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="db6f4-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="db6f4-238">Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="db6f4-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="db6f4-239">Пример копирования данных из Oracle в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="db6f4-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="db6f4-240">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="db6f4-241">Связанная служба типа [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="db6f4-242">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="db6f4-243">Входной [набор данных](data-factory-create-datasets.md) типа [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="db6f4-244">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="db6f4-245">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) в качестве источника и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="db6f4-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="db6f4-246">В примере данные из локальной таблицы Oracle ежечасно копируются в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="db6f4-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="db6f4-247">Дополнительные сведения о различных свойствах, используемых в примере, см. в документации, ссылки на которую приведены в разделах после примеров.</span><span class="sxs-lookup"><span data-stu-id="db6f4-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="db6f4-248">**Связанная служба Oracle**</span><span class="sxs-lookup"><span data-stu-id="db6f4-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="db6f4-249">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="db6f4-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="db6f4-250">**Входной набор данных Oracle**</span><span class="sxs-lookup"><span data-stu-id="db6f4-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="db6f4-251">В примере предполагается, что таблица MyTable уже создана в Oracle и содержит столбец с именем timestampcolumn для данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="db6f4-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="db6f4-252">Если параметру external присвоить значение true, фабрика данных воспримет этот набор данных как внешний и созданный не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="db6f4-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {     
            "externalData": {        
                "retryInterval": "00:01:00",    
                "retryTimeout": "00:10:00",       
                "maximumRetry": 3       
            }     
        }
    }
}
```

<span data-ttu-id="db6f4-253">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="db6f4-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="db6f4-254">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="db6f4-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="db6f4-255">Путь к папке с BLOB-объектом и имя файла вычисляются динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="db6f4-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="db6f4-256">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="db6f4-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="db6f4-257">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="db6f4-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="db6f4-258">Конвейер содержит действие копирования, которое использует входные и выходные наборы данных и выполняется ежечасно.</span><span class="sxs-lookup"><span data-stu-id="db6f4-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="db6f4-259">В определении JSON конвейера для типа **source** устанавливается значение **OracleSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="db6f4-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="db6f4-260">SQL-запрос, указанный для свойства **oracleReaderQuery** , выбирает для копирования данные за последний час.</span><span class="sxs-lookup"><span data-stu-id="db6f4-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 0,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="db6f4-261">Пример копирования данных из большого двоичного объекта Azure в Oracle</span><span class="sxs-lookup"><span data-stu-id="db6f4-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="db6f4-262">В этом примере показано, как скопировать данные из хранилища BLOB-объектов Azure в локальную базу данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="db6f4-263">Однако данные можно **напрямую** копировать из любого указанного [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) источника, используя действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="db6f4-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="db6f4-264">Образец состоит из следующих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="db6f4-265">Связанная служба типа [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="db6f4-266">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="db6f4-267">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="db6f4-268">Выходной [набор данных](data-factory-create-datasets.md) типа [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="db6f4-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="db6f4-269">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) в качестве источника и [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="db6f4-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="db6f4-270">В примере данные из хранилища BLOB-объектов каждый час копируются в таблицу в локальной базе данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="db6f4-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="db6f4-271">Дополнительные сведения о различных свойствах, используемых в примере, см. в документации, ссылки на которую приведены в разделах после примеров.</span><span class="sxs-lookup"><span data-stu-id="db6f4-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="db6f4-272">**Связанная служба Oracle**</span><span class="sxs-lookup"><span data-stu-id="db6f4-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="db6f4-273">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="db6f4-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="db6f4-274">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="db6f4-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="db6f4-275">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="db6f4-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="db6f4-276">Путь к папке с BLOB-объектом и имя файла вычисляются динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="db6f4-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="db6f4-277">В пути к папке используется год, месяц и день начала, а в имени файла — час начала.</span><span class="sxs-lookup"><span data-stu-id="db6f4-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="db6f4-278">Когда для параметра external задано значение true, служба фабрики данных считает эту таблицу внешней и созданной не в результате какого-либо действия в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="db6f4-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="db6f4-279">**Выходной набор данных Oracle**</span><span class="sxs-lookup"><span data-stu-id="db6f4-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="db6f4-280">В примере предполагается, что вы создали в Oracle таблицу MyTable.</span><span class="sxs-lookup"><span data-stu-id="db6f4-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="db6f4-281">Таблицу в Oracle нужно создать с таким же количеством столбцов, которое должно быть в CSV-файле большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="db6f4-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="db6f4-282">Новые строки добавляются в таблицу каждый час.</span><span class="sxs-lookup"><span data-stu-id="db6f4-282">New rows are added to the table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="db6f4-283">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="db6f4-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="db6f4-284">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="db6f4-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="db6f4-285">В определении JSON конвейера для типа **source** устанавливается значение **BlobSource**, а для типа **sink** — значение **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="db6f4-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 0,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```


## <a name="troubleshooting-tips"></a><span data-ttu-id="db6f4-286">Советы по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="db6f4-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="db6f4-287">Проблема 1: поставщик данных .NET Framework</span><span class="sxs-lookup"><span data-stu-id="db6f4-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="db6f4-288">Отображается следующее **сообщение об ошибке**:</span><span class="sxs-lookup"><span data-stu-id="db6f4-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="db6f4-289">**Возможные причины:**</span><span class="sxs-lookup"><span data-stu-id="db6f4-289">**Possible causes:**</span></span>

1. <span data-ttu-id="db6f4-290">Поставщик данных .NET Framework для Oracle не был установлен.</span><span class="sxs-lookup"><span data-stu-id="db6f4-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="db6f4-291">Поставщик данных .NET Framework для Oracle был установлен в .NET Framework 2.0 и не найден в папках .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="db6f4-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="db6f4-292">**Решение:**</span><span class="sxs-lookup"><span data-stu-id="db6f4-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="db6f4-293">Если поставщик данных .NET для Oracle не установлен, [установите его](http://www.oracle.com/technetwork/topics/dotnet/downloads/) и повторите сценарий.</span><span class="sxs-lookup"><span data-stu-id="db6f4-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="db6f4-294">Если сообщение об ошибке появляется даже после установки поставщика, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="db6f4-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="db6f4-295">Откройте файл конфигурации .NET 2.0 из папки: <system disk> \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="db6f4-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="db6f4-296">Найдите **поставщик данных Oracle для .NET** и вы сможете найти запись, как показано в следующем примере, в разделе **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Поставщик данных Oracle для .NET</span><span class="sxs-lookup"><span data-stu-id="db6f4-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="db6f4-297">”</span><span class="sxs-lookup"><span data-stu-id="db6f4-297">”</span></span>
3. <span data-ttu-id="db6f4-298">Скопируйте эту запись в файл конфигурации компьютера в следующей папке v4.0: <system disk>\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, измените версию на 4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="db6f4-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="db6f4-299">Установите файл <путь установки ODP.NET>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll в глобальный кэш сборок (GAC), выполнив команду `gacutil /i [provider path]`.## Советы по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="db6f4-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="db6f4-300">Проблема 2: формат даты и времени</span><span class="sxs-lookup"><span data-stu-id="db6f4-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="db6f4-301">Отображается следующее **сообщение об ошибке**:</span><span class="sxs-lookup"><span data-stu-id="db6f4-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="db6f4-302">**Решение:**</span><span class="sxs-lookup"><span data-stu-id="db6f4-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="db6f4-303">Необходимо настроить строку запроса в действии копирования в зависимости от настроек дат в базе данных Oracle, как показано в следующем примере (используя функцию to_date):</span><span class="sxs-lookup"><span data-stu-id="db6f4-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="db6f4-304">Сопоставление типов для Oracle</span><span class="sxs-lookup"><span data-stu-id="db6f4-304">Type mapping for Oracle</span></span>
<span data-ttu-id="db6f4-305">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="db6f4-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="db6f4-306">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="db6f4-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="db6f4-307">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="db6f4-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="db6f4-308">Когда данные перемещаются из Oracle, для преобразования типа данных Oracle в тип .NET и наоборот используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="db6f4-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="db6f4-309">Тип данных Oracle</span><span class="sxs-lookup"><span data-stu-id="db6f4-309">Oracle data type</span></span> | <span data-ttu-id="db6f4-310">Тип данных платформы .NET</span><span class="sxs-lookup"><span data-stu-id="db6f4-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="db6f4-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="db6f4-311">BFILE</span></span> |<span data-ttu-id="db6f4-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="db6f4-312">Byte[]</span></span> |
| <span data-ttu-id="db6f4-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="db6f4-313">BLOB</span></span> |<span data-ttu-id="db6f4-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="db6f4-314">Byte[]</span></span> |
| <span data-ttu-id="db6f4-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="db6f4-315">CHAR</span></span> |<span data-ttu-id="db6f4-316">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-316">String</span></span> |
| <span data-ttu-id="db6f4-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="db6f4-317">CLOB</span></span> |<span data-ttu-id="db6f4-318">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-318">String</span></span> |
| <span data-ttu-id="db6f4-319">DATE</span><span class="sxs-lookup"><span data-stu-id="db6f4-319">DATE</span></span> |<span data-ttu-id="db6f4-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="db6f4-320">DateTime</span></span> |
| <span data-ttu-id="db6f4-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="db6f4-321">FLOAT</span></span> |<span data-ttu-id="db6f4-322">десятичное число, строка (если точность больше 28)</span><span class="sxs-lookup"><span data-stu-id="db6f4-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="db6f4-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="db6f4-323">INTEGER</span></span> |<span data-ttu-id="db6f4-324">десятичное число, строка (если точность больше 28)</span><span class="sxs-lookup"><span data-stu-id="db6f4-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="db6f4-325">INTERVAL YEAR TO MONTH</span><span class="sxs-lookup"><span data-stu-id="db6f4-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="db6f4-326">Int32</span><span class="sxs-lookup"><span data-stu-id="db6f4-326">Int32</span></span> |
| <span data-ttu-id="db6f4-327">INTERVAL DAY TO SECOND</span><span class="sxs-lookup"><span data-stu-id="db6f4-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="db6f4-328">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="db6f4-328">TimeSpan</span></span> |
| <span data-ttu-id="db6f4-329">LONG</span><span class="sxs-lookup"><span data-stu-id="db6f4-329">LONG</span></span> |<span data-ttu-id="db6f4-330">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-330">String</span></span> |
| <span data-ttu-id="db6f4-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="db6f4-331">LONG RAW</span></span> |<span data-ttu-id="db6f4-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="db6f4-332">Byte[]</span></span> |
| <span data-ttu-id="db6f4-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="db6f4-333">NCHAR</span></span> |<span data-ttu-id="db6f4-334">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-334">String</span></span> |
| <span data-ttu-id="db6f4-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="db6f4-335">NCLOB</span></span> |<span data-ttu-id="db6f4-336">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-336">String</span></span> |
| <span data-ttu-id="db6f4-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="db6f4-337">NUMBER</span></span> |<span data-ttu-id="db6f4-338">десятичное число, строка (если точность больше 28)</span><span class="sxs-lookup"><span data-stu-id="db6f4-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="db6f4-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="db6f4-339">NVARCHAR2</span></span> |<span data-ttu-id="db6f4-340">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-340">String</span></span> |
| <span data-ttu-id="db6f4-341">RAW</span><span class="sxs-lookup"><span data-stu-id="db6f4-341">RAW</span></span> |<span data-ttu-id="db6f4-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="db6f4-342">Byte[]</span></span> |
| <span data-ttu-id="db6f4-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="db6f4-343">ROWID</span></span> |<span data-ttu-id="db6f4-344">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-344">String</span></span> |
| <span data-ttu-id="db6f4-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="db6f4-345">TIMESTAMP</span></span> |<span data-ttu-id="db6f4-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="db6f4-346">DateTime</span></span> |
| <span data-ttu-id="db6f4-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="db6f4-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="db6f4-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="db6f4-348">DateTime</span></span> |
| <span data-ttu-id="db6f4-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="db6f4-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="db6f4-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="db6f4-350">DateTime</span></span> |
| <span data-ttu-id="db6f4-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="db6f4-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="db6f4-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="db6f4-352">Number</span></span> |
| <span data-ttu-id="db6f4-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="db6f4-353">VARCHAR2</span></span> |<span data-ttu-id="db6f4-354">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-354">String</span></span> |
| <span data-ttu-id="db6f4-355">XML</span><span class="sxs-lookup"><span data-stu-id="db6f4-355">XML</span></span> |<span data-ttu-id="db6f4-356">Строка</span><span class="sxs-lookup"><span data-stu-id="db6f4-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="db6f4-357">При использовании драйвера Майкрософт типы данных **INTERVAL YEAR TO MONTH** и **INTERVAL DAY TO SECOND** не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="db6f4-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="db6f4-358">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="db6f4-358">Map source to sink columns</span></span>
<span data-ttu-id="db6f4-359">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="db6f4-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="db6f4-360">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="db6f4-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="db6f4-361">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="db6f4-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="db6f4-362">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="db6f4-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="db6f4-363">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="db6f4-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="db6f4-364">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="db6f4-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="db6f4-365">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="db6f4-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="db6f4-366">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="db6f4-366">Performance and Tuning</span></span>
<span data-ttu-id="db6f4-367">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="db6f4-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
