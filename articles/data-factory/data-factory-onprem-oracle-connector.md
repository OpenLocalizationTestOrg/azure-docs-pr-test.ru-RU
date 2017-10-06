---
title: "aaaCopy данных из Oracle, с помощью фабрики данных | Документы Microsoft"
description: "Узнайте, как toocopy данных из базы данных Oracle, локально с помощью фабрики данных Azure."
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
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="020ae-103">Копирование данных в локальную базу данных Oracle и обратно с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="020ae-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="020ae-104">В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данные из локальной базы данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="020ae-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="020ae-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="020ae-106">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="020ae-106">Supported scenarios</span></span>
<span data-ttu-id="020ae-107">Можно скопировать данные **из базы данных Oracle** toohello следующие хранилищ данных:</span><span class="sxs-lookup"><span data-stu-id="020ae-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="020ae-108">Можно скопировать данные из hello, следуя хранилищ данных **базы данных Oracle tooan**:</span><span class="sxs-lookup"><span data-stu-id="020ae-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="020ae-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="020ae-109">Prerequisites</span></span>
<span data-ttu-id="020ae-110">Фабрика данных поддерживает подключения Oracle tooon локальные источники, с помощью hello шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="020ae-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="020ae-111">В разделе [шлюз управления данными](data-factory-data-management-gateway.md) toolearn статьи о шлюз управления данными и [перемещения данных из локальной toocloud](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговые инструкции по настройке шлюза hello в конвейере данных toomove данные.</span><span class="sxs-lookup"><span data-stu-id="020ae-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="020ae-112">Даже если hello Oracle находится в ВМ IaaS Azure требуется шлюз.</span><span class="sxs-lookup"><span data-stu-id="020ae-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="020ae-113">Hello шлюз можно установить на hello же ВМ IaaS как данные hello хранения или в другой виртуальной Машине, при условии, что шлюз hello подключения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="020ae-114">Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="020ae-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="020ae-115">Поддерживаемые версии и установка</span><span class="sxs-lookup"><span data-stu-id="020ae-115">Supported versions and installation</span></span>
<span data-ttu-id="020ae-116">Этот соединитель Oracle поддерживает две версии драйверов.</span><span class="sxs-lookup"><span data-stu-id="020ae-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="020ae-117">**Драйвер Microsoft для Oracle (рекомендуется)**: начальной из шлюза управления данными версии 2.7, драйвер Microsoft для Oracle автоматически устанавливается вместе с hello шлюза, поэтому не требуется драйвер hello дескриптор tooadditionally в порядке tooOracle tooestablish подключения, а также могут возникать большую производительность копирования при использовании этого драйвера.</span><span class="sxs-lookup"><span data-stu-id="020ae-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="020ae-118">Ниже перечислены поддерживаемые версии баз данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="020ae-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="020ae-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="020ae-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="020ae-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="020ae-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="020ae-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="020ae-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="020ae-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="020ae-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="020ae-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="020ae-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="020ae-124">В настоящее время драйвер Microsoft для Oracle поддерживает только копирование данных из Oracle, но не запись tooOracle.</span><span class="sxs-lookup"><span data-stu-id="020ae-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="020ae-125">И обратите внимание, что hello тестированию подключения на вкладке диагностику шлюза управления данными не поддерживает этот драйвер.</span><span class="sxs-lookup"><span data-stu-id="020ae-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="020ae-126">Кроме того можно использовать hello копирования мастера toovalidate hello подключения.</span><span class="sxs-lookup"><span data-stu-id="020ae-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="020ae-127">**Поставщик данных Oracle для .NET:** можно также выбрать данные toocopy toouse поставщик данных Oracle из / tooOracle.</span><span class="sxs-lookup"><span data-stu-id="020ae-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="020ae-128">Входит в состав [компонентов доступа к данным Oracle для Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="020ae-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="020ae-129">Установите соответствующую версию hello (32 или 64-разрядная версия) на компьютере hello, где установлен шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="020ae-130">[Поставщик данных Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) можно получить доступ к tooOracle 10 g, выпуск 2 или более поздней версии базы данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="020ae-131">При выборе «XCopy Installation», выполните действия в файле readme.htm hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="020ae-132">Мы рекомендуем выбрать hello установщика с пользовательским Интерфейсом (не XCopy один).</span><span class="sxs-lookup"><span data-stu-id="020ae-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="020ae-133">После установки поставщика hello **перезапустите** hello служба узла шлюза управления данными на компьютере с помощью служб приложения (или) диспетчера конфигурации шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="020ae-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="020ae-134">При использовании копирования мастера tooauthor hello копирования конвейера тип драйвера hello будет определяется автоматически.</span><span class="sxs-lookup"><span data-stu-id="020ae-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="020ae-135">Драйвер Майкрософт будет использоваться по умолчанию, если только вы не используете версию шлюза ниже 2.7 или выбрали Oracle в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="020ae-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="020ae-136">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="020ae-136">Getting started</span></span>
<span data-ttu-id="020ae-137">Создать конвейер с действием копирования, который перемещает данные из локальной базы данных Oracle или в нее, можно с помощью различных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="020ae-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="020ae-138">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="020ae-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="020ae-139">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="020ae-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="020ae-140">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="020ae-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="020ae-141">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="020ae-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="020ae-142">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="020ae-143">Создание **фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="020ae-143">Create a **data factory**.</span></span> <span data-ttu-id="020ae-144">Фабрика данных может содержать один или несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="020ae-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="020ae-145">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="020ae-146">Например при копировании данных из tooan базы данных Oralce хранилище больших двоичных объектов создается две связанные службы toolink базы данных Oracle и фабрики данных tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="020ae-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="020ae-147">Свойства связанной службы, определенные tooOracle см [связанные свойства службы](#linked-service-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="020ae-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="020ae-148">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="020ae-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="020ae-149">В примере hello, упомянутые в последнем шаге hello создайте таблице hello toospecify набора данных в базе данных Oracle, содержащий hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="020ae-150">Создайте другой контейнер больших двоичных объектов dataset toospecify hello и hello папке, содержащей данные hello копируются hello базы данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="020ae-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="020ae-151">Свойства набора данных, которые являются определенной tooOracle, в разделе [свойства набора данных](#dataset-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="020ae-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="020ae-152">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="020ae-153">В примере hello приведенные выше используются OracleSource в BlobSink источника и в приемник для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="020ae-154">Аналогично при копировании из tooOracle хранилища больших двоичных объектов базы данных использовать BlobSource и OracleSink в действии копирования hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="020ae-155">Свойства действия копирования, определенные tooOracle базы данных, в разделе [скопировать свойства действия](#copy-activity-properties) раздела.</span><span class="sxs-lookup"><span data-stu-id="020ae-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="020ae-156">Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="020ae-157">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="020ae-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="020ae-158">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="020ae-159">Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локальной базы данных Oracle см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-oracle-database) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="020ae-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="020ae-160">Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущности:</span><span class="sxs-lookup"><span data-stu-id="020ae-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="020ae-161">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="020ae-161">Linked service properties</span></span>
<span data-ttu-id="020ae-162">Hello в следующей таблице приводится описание службы конкретных tooOracle связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="020ae-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="020ae-163">Свойство</span><span class="sxs-lookup"><span data-stu-id="020ae-163">Property</span></span> | <span data-ttu-id="020ae-164">Описание</span><span class="sxs-lookup"><span data-stu-id="020ae-164">Description</span></span> | <span data-ttu-id="020ae-165">Обязательно</span><span class="sxs-lookup"><span data-stu-id="020ae-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="020ae-166">type</span><span class="sxs-lookup"><span data-stu-id="020ae-166">type</span></span> |<span data-ttu-id="020ae-167">свойство типа Hello должно быть присвоено: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="020ae-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="020ae-168">Да</span><span class="sxs-lookup"><span data-stu-id="020ae-168">Yes</span></span> |
| <span data-ttu-id="020ae-169">driverType</span><span class="sxs-lookup"><span data-stu-id="020ae-169">driverType</span></span> | <span data-ttu-id="020ae-170">Указать, какие данные toocopy драйвер toouse из / tooOracle базы данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="020ae-171">Допустимые значения: **Майкрософт** или **ODP** (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="020ae-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="020ae-172">Дополнительные сведения о драйверах см. в разделе [Поддерживаемые версии и установка](#supported-versions-and-installation).</span><span class="sxs-lookup"><span data-stu-id="020ae-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="020ae-173">Нет</span><span class="sxs-lookup"><span data-stu-id="020ae-173">No</span></span> |
| <span data-ttu-id="020ae-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="020ae-174">connectionString</span></span> | <span data-ttu-id="020ae-175">Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных Oracle toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="020ae-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="020ae-176">Да</span><span class="sxs-lookup"><span data-stu-id="020ae-176">Yes</span></span> |
| <span data-ttu-id="020ae-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="020ae-177">gatewayName</span></span> | <span data-ttu-id="020ae-178">Имя шлюза hello, что является toohello tooconnect используется локальный сервер Oracle</span><span class="sxs-lookup"><span data-stu-id="020ae-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="020ae-179">Да</span><span class="sxs-lookup"><span data-stu-id="020ae-179">Yes</span></span> |

<span data-ttu-id="020ae-180">**Пример: использование драйвера Майкрософт**</span><span class="sxs-lookup"><span data-stu-id="020ae-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="020ae-181">**Пример: использование драйвера ODP**</span><span class="sxs-lookup"><span data-stu-id="020ae-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="020ae-182">См. слишком[этот сайт](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) для hello, разрешенные форматы.</span><span class="sxs-lookup"><span data-stu-id="020ae-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="020ae-183">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="020ae-183">Dataset properties</span></span>
<span data-ttu-id="020ae-184">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="020ae-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="020ae-185">Такие разделы, как структура, доступность и политика набора данных JSON, одинаковы для всех видов наборов данных (Oracle, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="020ae-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="020ae-186">раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="020ae-187">раздел typeProperties Hello для набора данных hello типа OracleTable имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="020ae-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="020ae-188">Свойство</span><span class="sxs-lookup"><span data-stu-id="020ae-188">Property</span></span> | <span data-ttu-id="020ae-189">Описание</span><span class="sxs-lookup"><span data-stu-id="020ae-189">Description</span></span> | <span data-ttu-id="020ae-190">Обязательно</span><span class="sxs-lookup"><span data-stu-id="020ae-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="020ae-191">tableName</span><span class="sxs-lookup"><span data-stu-id="020ae-191">tableName</span></span> |<span data-ttu-id="020ae-192">Имя таблицы hello в hello базы данных Oracle, hello связанной службы относится.</span><span class="sxs-lookup"><span data-stu-id="020ae-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="020ae-193">Нет (если указан параметр **oracleReaderQuery** объекта **OracleSource**)</span><span class="sxs-lookup"><span data-stu-id="020ae-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="020ae-194">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="020ae-194">Copy activity properties</span></span>
<span data-ttu-id="020ae-195">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="020ae-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="020ae-196">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="020ae-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="020ae-197">Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.</span><span class="sxs-lookup"><span data-stu-id="020ae-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="020ae-198">В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия.</span><span class="sxs-lookup"><span data-stu-id="020ae-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="020ae-199">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="020ae-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="020ae-200">OracleSource</span></span>
<span data-ttu-id="020ae-201">В действии копирования, когда источник hello типа **OracleSource** hello следующие свойства доступны в **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="020ae-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="020ae-202">Свойство</span><span class="sxs-lookup"><span data-stu-id="020ae-202">Property</span></span> | <span data-ttu-id="020ae-203">Описание</span><span class="sxs-lookup"><span data-stu-id="020ae-203">Description</span></span> | <span data-ttu-id="020ae-204">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="020ae-204">Allowed values</span></span> | <span data-ttu-id="020ae-205">Обязательно</span><span class="sxs-lookup"><span data-stu-id="020ae-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="020ae-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="020ae-206">oracleReaderQuery</span></span> |<span data-ttu-id="020ae-207">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="020ae-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="020ae-208">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="020ae-208">SQL query string.</span></span> <span data-ttu-id="020ae-209">Например, select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="020ae-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="020ae-210">Если не указан, hello в инструкции SQL, выполняемой: выберите * from MyTable</span><span class="sxs-lookup"><span data-stu-id="020ae-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="020ae-211">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="020ae-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="020ae-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="020ae-212">OracleSink</span></span>
<span data-ttu-id="020ae-213">**OracleSink** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="020ae-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="020ae-214">Свойство</span><span class="sxs-lookup"><span data-stu-id="020ae-214">Property</span></span> | <span data-ttu-id="020ae-215">Описание</span><span class="sxs-lookup"><span data-stu-id="020ae-215">Description</span></span> | <span data-ttu-id="020ae-216">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="020ae-216">Allowed values</span></span> | <span data-ttu-id="020ae-217">Обязательно</span><span class="sxs-lookup"><span data-stu-id="020ae-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="020ae-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="020ae-218">writeBatchTimeout</span></span> |<span data-ttu-id="020ae-219">Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="020ae-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="020ae-220">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="020ae-220">timespan</span></span><br/><br/> <span data-ttu-id="020ae-221">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="020ae-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="020ae-222">Нет</span><span class="sxs-lookup"><span data-stu-id="020ae-222">No</span></span> |
| <span data-ttu-id="020ae-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="020ae-223">writeBatchSize</span></span> |<span data-ttu-id="020ae-224">Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="020ae-225">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="020ae-225">Integer (number of rows)</span></span> |<span data-ttu-id="020ae-226">Нет (значение по умолчанию — 100)</span><span class="sxs-lookup"><span data-stu-id="020ae-226">No (default: 100)</span></span> |
| <span data-ttu-id="020ae-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="020ae-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="020ae-228">Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез.</span><span class="sxs-lookup"><span data-stu-id="020ae-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="020ae-229">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="020ae-229">A query statement.</span></span> |<span data-ttu-id="020ae-230">Нет</span><span class="sxs-lookup"><span data-stu-id="020ae-230">No</span></span> |
| <span data-ttu-id="020ae-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="020ae-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="020ae-232">Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="020ae-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="020ae-233">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="020ae-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="020ae-234">Нет</span><span class="sxs-lookup"><span data-stu-id="020ae-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="020ae-235">Примеры JSON для копирования данных tooand из базы данных Oracle</span><span class="sxs-lookup"><span data-stu-id="020ae-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="020ae-236">Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="020ae-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="020ae-237">Они показывают как toocopy данные из / tooan Oracle база данных из хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="020ae-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="020ae-238">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="020ae-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="020ae-239">Пример: Копирование данных из Oracle tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="020ae-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="020ae-240">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="020ae-241">Связанная служба типа [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="020ae-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="020ae-242">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="020ae-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="020ae-243">Входной [набор данных](data-factory-create-datasets.md) типа [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="020ae-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="020ae-244">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="020ae-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="020ae-245">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) в качестве источника и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="020ae-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="020ae-246">Образец Hello копирует данные из таблицы в локальной базы данных Oracle tooa blob каждый час.</span><span class="sxs-lookup"><span data-stu-id="020ae-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="020ae-247">Дополнительные сведения о различных свойств, используемых в образце hello см. в документации в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="020ae-248">**Связанная служба Oracle**</span><span class="sxs-lookup"><span data-stu-id="020ae-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="020ae-249">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="020ae-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="020ae-250">**Входной набор данных Oracle**</span><span class="sxs-lookup"><span data-stu-id="020ae-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="020ae-251">Образец Hello предполагается создания таблицы «MyTable» в Oracle, и она содержит столбец с именем «timestampcolumn» для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="020ae-252">Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="020ae-253">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="020ae-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="020ae-254">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="020ae-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="020ae-255">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="020ae-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="020ae-256">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="020ae-257">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="020ae-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="020ae-258">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и выполняется запланированное toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="020ae-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="020ae-259">В определении JSON конвейера hello, hello **источника** тип установлен слишком**OracleSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="020ae-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="020ae-260">запрос SQL Hello, указанный с **oracleReaderQuery** свойство выбирает данные hello в hello за час toocopy.</span><span class="sxs-lookup"><span data-stu-id="020ae-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="020ae-261">Пример: Копирование данных из tooOracle больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="020ae-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="020ae-262">В этом примере показано, как toocopy данных из хранилища больших двоичных объектов tooan в локальной базе данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="020ae-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="020ae-263">Тем не менее, данные можно скопировать **непосредственно** из любого из указанных источников hello [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="020ae-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="020ae-264">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="020ae-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="020ae-265">Связанная служба типа [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="020ae-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="020ae-266">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="020ae-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="020ae-267">Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="020ae-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="020ae-268">Выходной [набор данных](data-factory-create-datasets.md) типа [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="020ae-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="020ae-269">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) в качестве источника и [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="020ae-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="020ae-270">Образец Hello копирует данные из таблицы tooa большого двоичного объекта в базе данных Oracle в локальной каждый час.</span><span class="sxs-lookup"><span data-stu-id="020ae-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="020ae-271">Дополнительные сведения о различных свойств, используемых в образце hello см. в документации в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="020ae-272">**Связанная служба Oracle**</span><span class="sxs-lookup"><span data-stu-id="020ae-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="020ae-273">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="020ae-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="020ae-274">**Входной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="020ae-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="020ae-275">Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="020ae-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="020ae-276">Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="020ae-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="020ae-277">путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="020ae-278">«external»: параметр «true» уведомляет службу hello фабрики данных, что эта таблица является внешней toohello фабрики данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="020ae-279">**Выходной набор данных Oracle**</span><span class="sxs-lookup"><span data-stu-id="020ae-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="020ae-280">Образец Hello предполагается, что вы создали таблицу «MyTable» в Oracle.</span><span class="sxs-lookup"><span data-stu-id="020ae-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="020ae-281">Создать таблицу hello в Oracle с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="020ae-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="020ae-282">Новые строки добавляются в таблицу toohello каждый час.</span><span class="sxs-lookup"><span data-stu-id="020ae-282">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="020ae-283">**Конвейер с действием копирования**</span><span class="sxs-lookup"><span data-stu-id="020ae-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="020ae-284">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="020ae-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="020ae-285">В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и hello **приемник** тип установлен слишком**OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="020ae-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="020ae-286">Советы по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="020ae-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="020ae-287">Проблема 1: поставщик данных .NET Framework</span><span class="sxs-lookup"><span data-stu-id="020ae-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="020ae-288">Вы видите следующее hello **сообщение об ошибке**:</span><span class="sxs-lookup"><span data-stu-id="020ae-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="020ae-289">**Возможные причины:**</span><span class="sxs-lookup"><span data-stu-id="020ae-289">**Possible causes:**</span></span>

1. <span data-ttu-id="020ae-290">Hello поставщик данных .NET Framework для Oracle не установлен.</span><span class="sxs-lookup"><span data-stu-id="020ae-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="020ae-291">Hello поставщик данных .NET Framework для Oracle не установленных too.NET Framework 2.0 и не найден в папках hello .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="020ae-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="020ae-292">**Решение:**</span><span class="sxs-lookup"><span data-stu-id="020ae-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="020ae-293">Если вы не установили hello поставщика .NET для Oracle, [установить его](http://www.oracle.com/technetwork/topics/dotnet/downloads/) и повторите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="020ae-294">Если появляется сообщение об ошибке hello даже после установки поставщика hello, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="020ae-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="020ae-295">Открытие файла конфигурации компьютера .NET 2.0 папки hello: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="020ae-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="020ae-296">Поиск **поставщик данных Oracle для .NET**, и должен быть доступ toofind запись, как показано в следующий пример в разделе hello **system.data** -> **DbProviderFactories**: «<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Поставщик данных oracle для .NET</span><span class="sxs-lookup"><span data-stu-id="020ae-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="020ae-297">”</span><span class="sxs-lookup"><span data-stu-id="020ae-297">”</span></span>
3. <span data-ttu-id="020ae-298">Скопируйте этот файл machine.config toohello записи в следующие папки v4.0 hello: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config и too4.xxx.x.x версии изменение hello.</span><span class="sxs-lookup"><span data-stu-id="020ae-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="020ae-299">Установить «< путь к установленному ODP.NET > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll» в hello глобальный кэш сборок (GAC), запустив `gacutil /i [provider path]`. ## Советы по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="020ae-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="020ae-300">Проблема 2: формат даты и времени</span><span class="sxs-lookup"><span data-stu-id="020ae-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="020ae-301">Вы видите следующее hello **сообщение об ошибке**:</span><span class="sxs-lookup"><span data-stu-id="020ae-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="020ae-302">**Решение:**</span><span class="sxs-lookup"><span data-stu-id="020ae-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="020ae-303">Строка запроса hello tooadjust может потребоваться в зависимости настройки даты в базе данных Oracle, как показано в следующих hello действие копирования (используя функцию to_date hello) Пример:</span><span class="sxs-lookup"><span data-stu-id="020ae-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="020ae-304">Сопоставление типов для Oracle</span><span class="sxs-lookup"><span data-stu-id="020ae-304">Type mapping for Oracle</span></span>
<span data-ttu-id="020ae-305">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статье действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="020ae-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="020ae-306">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="020ae-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="020ae-307">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="020ae-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="020ae-308">При перемещении данных из Oracle, hello следующие сопоставления используются типа too.NET тип данных Oracle и наоборот.</span><span class="sxs-lookup"><span data-stu-id="020ae-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="020ae-309">Тип данных Oracle</span><span class="sxs-lookup"><span data-stu-id="020ae-309">Oracle data type</span></span> | <span data-ttu-id="020ae-310">Тип данных платформы .NET</span><span class="sxs-lookup"><span data-stu-id="020ae-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="020ae-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="020ae-311">BFILE</span></span> |<span data-ttu-id="020ae-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="020ae-312">Byte[]</span></span> |
| <span data-ttu-id="020ae-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="020ae-313">BLOB</span></span> |<span data-ttu-id="020ae-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="020ae-314">Byte[]</span></span> |
| <span data-ttu-id="020ae-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="020ae-315">CHAR</span></span> |<span data-ttu-id="020ae-316">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-316">String</span></span> |
| <span data-ttu-id="020ae-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="020ae-317">CLOB</span></span> |<span data-ttu-id="020ae-318">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-318">String</span></span> |
| <span data-ttu-id="020ae-319">DATE</span><span class="sxs-lookup"><span data-stu-id="020ae-319">DATE</span></span> |<span data-ttu-id="020ae-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="020ae-320">DateTime</span></span> |
| <span data-ttu-id="020ae-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="020ae-321">FLOAT</span></span> |<span data-ttu-id="020ae-322">десятичное число, строка (если точность больше 28)</span><span class="sxs-lookup"><span data-stu-id="020ae-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="020ae-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="020ae-323">INTEGER</span></span> |<span data-ttu-id="020ae-324">десятичное число, строка (если точность больше 28)</span><span class="sxs-lookup"><span data-stu-id="020ae-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="020ae-325">ИНТЕРВАЛ tooMONTH год</span><span class="sxs-lookup"><span data-stu-id="020ae-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="020ae-326">Int32</span><span class="sxs-lookup"><span data-stu-id="020ae-326">Int32</span></span> |
| <span data-ttu-id="020ae-327">ДЕНЬ tooSECOND ИНТЕРВАЛ</span><span class="sxs-lookup"><span data-stu-id="020ae-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="020ae-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="020ae-328">TimeSpan</span></span> |
| <span data-ttu-id="020ae-329">LONG</span><span class="sxs-lookup"><span data-stu-id="020ae-329">LONG</span></span> |<span data-ttu-id="020ae-330">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-330">String</span></span> |
| <span data-ttu-id="020ae-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="020ae-331">LONG RAW</span></span> |<span data-ttu-id="020ae-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="020ae-332">Byte[]</span></span> |
| <span data-ttu-id="020ae-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="020ae-333">NCHAR</span></span> |<span data-ttu-id="020ae-334">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-334">String</span></span> |
| <span data-ttu-id="020ae-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="020ae-335">NCLOB</span></span> |<span data-ttu-id="020ae-336">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-336">String</span></span> |
| <span data-ttu-id="020ae-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="020ae-337">NUMBER</span></span> |<span data-ttu-id="020ae-338">десятичное число, строка (если точность больше 28)</span><span class="sxs-lookup"><span data-stu-id="020ae-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="020ae-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="020ae-339">NVARCHAR2</span></span> |<span data-ttu-id="020ae-340">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-340">String</span></span> |
| <span data-ttu-id="020ae-341">RAW</span><span class="sxs-lookup"><span data-stu-id="020ae-341">RAW</span></span> |<span data-ttu-id="020ae-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="020ae-342">Byte[]</span></span> |
| <span data-ttu-id="020ae-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="020ae-343">ROWID</span></span> |<span data-ttu-id="020ae-344">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-344">String</span></span> |
| <span data-ttu-id="020ae-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="020ae-345">TIMESTAMP</span></span> |<span data-ttu-id="020ae-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="020ae-346">DateTime</span></span> |
| <span data-ttu-id="020ae-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="020ae-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="020ae-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="020ae-348">DateTime</span></span> |
| <span data-ttu-id="020ae-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="020ae-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="020ae-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="020ae-350">DateTime</span></span> |
| <span data-ttu-id="020ae-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="020ae-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="020ae-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="020ae-352">Number</span></span> |
| <span data-ttu-id="020ae-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="020ae-353">VARCHAR2</span></span> |<span data-ttu-id="020ae-354">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-354">String</span></span> |
| <span data-ttu-id="020ae-355">XML</span><span class="sxs-lookup"><span data-stu-id="020ae-355">XML</span></span> |<span data-ttu-id="020ae-356">Строка</span><span class="sxs-lookup"><span data-stu-id="020ae-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="020ae-357">Тип данных **tooMONTH ИНТЕРВАЛ года** и **tooSECOND ИНТЕРВАЛ день** не поддерживаются при использовании драйвера Microsoft.</span><span class="sxs-lookup"><span data-stu-id="020ae-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="020ae-358">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="020ae-358">Map source toosink columns</span></span>
<span data-ttu-id="020ae-359">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="020ae-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="020ae-360">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="020ae-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="020ae-361">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="020ae-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="020ae-362">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="020ae-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="020ae-363">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="020ae-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="020ae-364">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="020ae-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="020ae-365">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="020ae-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="020ae-366">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="020ae-366">Performance and Tuning</span></span>
<span data-ttu-id="020ae-367">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="020ae-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
