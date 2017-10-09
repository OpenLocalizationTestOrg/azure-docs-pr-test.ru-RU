---
title: "aaaMove данных из DB2, с помощью фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как toomove данных из DB2 локальной базы данных с помощью действия копирования фабрики данных Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="fc586-103">Перемещение данных из DB2 с помощью действия копирования в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="fc586-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="fc586-104">В этой статье описывается, как можно использовать действие копирования фабрики данных Azure toocopy данных из хранилища данных tooa базы данных DB2 в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="fc586-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="fc586-105">Вы можете скопировать tooany хранилища данных, который указан как поддерживаемый приемник в hello [действия перемещения данных фабрики данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) статьи.</span><span class="sxs-lookup"><span data-stu-id="fc586-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="fc586-106">В этом разделе основан на hello фабрики данных статьи, которая предоставляет обзор перемещения данных, используя действие копирования и перечислены сочетания хранилища данных hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="fc586-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="fc586-107">Фабрика данных в настоящее время поддерживает только перемещение данных из базы данных DB2 tooa [поддерживаемых приемника хранилища данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="fc586-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="fc586-108">Перемещение данных из других данных хранит tooa DB2, база данных не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="fc586-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc586-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fc586-109">Prerequisites</span></span>
<span data-ttu-id="fc586-110">Фабрика данных поддерживает подключения базы данных DB2 tooan локально с помощью hello [шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="fc586-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="fc586-111">Пошаговые инструкции tooset hello шлюза данных конвейера toomove данные см hello [перемещения данных из локальной toocloud](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fc586-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fc586-112">Даже если hello DB2 размещается на виртуальной Машине Azure IaaS, требуется шлюз.</span><span class="sxs-lookup"><span data-stu-id="fc586-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="fc586-113">Hello шлюз можно установить на hello же IaaS виртуальную Машину в качестве хранилища данных hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="fc586-114">Если шлюз hello может подключаться toohello базы данных, hello шлюз можно установить на другой виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="fc586-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="fc586-115">Шлюз управления данными Hello предоставляет встроенные драйверы DB2, вам не нужно toomanually установить драйвер toocopy данных из DB2.</span><span class="sxs-lookup"><span data-stu-id="fc586-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="fc586-116">Советы по устранению неполадок шлюза проблем с соединением и см. в разделе hello [Устранение неполадок шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) статьи.</span><span class="sxs-lookup"><span data-stu-id="fc586-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="fc586-117">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="fc586-117">Supported versions</span></span>
<span data-ttu-id="fc586-118">Соединитель Hello DB2 фабрики данных поддерживает следующие платформы IBM DB2 и версии с версиями диспетчер доступа к реляционной базе данных DRDA (архитектуры распределенной) SQL, 9, 10 и 11 hello:</span><span class="sxs-lookup"><span data-stu-id="fc586-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="fc586-119">IBM DB2 для z/OS версии 11.1</span><span class="sxs-lookup"><span data-stu-id="fc586-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="fc586-120">IBM DB2 для z/OS версии 10.1</span><span class="sxs-lookup"><span data-stu-id="fc586-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="fc586-121">IBM DB2 для i (AS400) версии 7.2</span><span class="sxs-lookup"><span data-stu-id="fc586-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="fc586-122">IBM DB2 для i (AS400) версии 7.1</span><span class="sxs-lookup"><span data-stu-id="fc586-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="fc586-123">IBM DB2 для Linux, UNIX и Windows (LUW) версии 11</span><span class="sxs-lookup"><span data-stu-id="fc586-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="fc586-124">IBM DB2 для LUW версии 10.5</span><span class="sxs-lookup"><span data-stu-id="fc586-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="fc586-125">IBM DB2 для LUW версии 10.1</span><span class="sxs-lookup"><span data-stu-id="fc586-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="fc586-126">Если появляется сообщение об ошибке hello «hello пакета соответствующего tooan SQL инструкции выполнения запроса не найден.</span><span class="sxs-lookup"><span data-stu-id="fc586-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="fc586-127">SQLSTATE = 51002 = SQLCODE-805, «hello обусловлено необходимые пакеты для hello обычного пользователя на hello ОС не создается.</span><span class="sxs-lookup"><span data-stu-id="fc586-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="fc586-128">tooresolve эту проблему, выполните следующие действия для типа сервера DB2:</span><span class="sxs-lookup"><span data-stu-id="fc586-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="fc586-129">DB2 для i (AS400): позволяет power создания коллекции hello для hello обычного пользователя до выполнения операции копирования.</span><span class="sxs-lookup"><span data-stu-id="fc586-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="fc586-130">Коллекция hello toocreate, используйте команду hello:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="fc586-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="fc586-131">DB2 для z/OS или LUW: используйте учетную запись с высоким уровнем привилегий — опытного пользователя или администратора с центры пакета и ПРИВЯЗКА, BINDADD, ПРЕДОСТАВЬТЕ разрешения EXECUTE tooPUBLIC--toorun hello копирование один раз.</span><span class="sxs-lookup"><span data-stu-id="fc586-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="fc586-132">необходимые пакеты Hello автоматически создается во время копирования hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="fc586-133">После этого можно переключиться назад toohello обычного пользователя для копирования последующих запусков.</span><span class="sxs-lookup"><span data-stu-id="fc586-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fc586-134">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="fc586-134">Getting started</span></span>
<span data-ttu-id="fc586-135">Можно создать конвейер с копирование данных toomove действия из локального хранилища данных DB2 с помощью различных средств и API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="fc586-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="fc586-136">toocreate простым способом Hello конвейера — toouse hello мастер копирования фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fc586-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="fc586-137">Краткое Пошаговое руководство по созданию конвейера с помощью мастера копирования hello, в разделе hello [учебника: создать конвейер с помощью мастера копирования hello](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="fc586-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="fc586-138">Можно также использовать средства toocreate конвейера, включая hello портал Azure, Visual Studio, Azure PowerShell, диспетчера ресурсов Azure шаблона, hello .NET API и hello REST API.</span><span class="sxs-lookup"><span data-stu-id="fc586-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="fc586-139">Пошаговые инструкции toocreate конвейер с операции копирования, в разделе hello [действие копирования учебника](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="fc586-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="fc586-140">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="fc586-141">Создание связанных служб toolink входных и выходных данных сохраняет tooyour фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fc586-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="fc586-142">Создания наборов данных toorepresent входных и выходных данных для операции копирования hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="fc586-143">Создайте конвейер с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="fc586-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="fc586-144">При использовании приветствия мастера копирования, определения JSON для службы фабрики данных связанных hello, конвейер сущностей и наборов данных автоматически создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="fc586-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="fc586-145">При использовании средств или API-интерфейсы (за исключением hello .NET API), можно определить hello фабрики данных сущности, используя формат JSON hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="fc586-146">Hello [JSON пример: копирование данных из DB2 tooAzure хранилища больших двоичных объектов](#json-example-copy-data-from-db2-to-azure-blob) показаны определения JSON hello для hello сущностей фабрики данных, используемых toocopy данные из локального хранилища данных DB2.</span><span class="sxs-lookup"><span data-stu-id="fc586-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="fc586-147">Hello в следующих разделах содержатся сведения об hello JSON свойства, используемые toodefine hello фабрики данных сущностей, которые являются определенной tooa DB2 хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="fc586-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="fc586-148">Свойства связанной службы DB2</span><span class="sxs-lookup"><span data-stu-id="fc586-148">DB2 linked service properties</span></span>
<span data-ttu-id="fc586-149">Привет, в следующей таблице перечислены свойства JSON hello, которые зависят от конкретного tooa DB2 связанной службы.</span><span class="sxs-lookup"><span data-stu-id="fc586-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="fc586-150">Свойство</span><span class="sxs-lookup"><span data-stu-id="fc586-150">Property</span></span> | <span data-ttu-id="fc586-151">Описание</span><span class="sxs-lookup"><span data-stu-id="fc586-151">Description</span></span> | <span data-ttu-id="fc586-152">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fc586-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc586-153">**type**</span><span class="sxs-lookup"><span data-stu-id="fc586-153">**type**</span></span> |<span data-ttu-id="fc586-154">Это свойство должно быть задано слишком**OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="fc586-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="fc586-155">Да</span><span class="sxs-lookup"><span data-stu-id="fc586-155">Yes</span></span> |
| <span data-ttu-id="fc586-156">**server**</span><span class="sxs-lookup"><span data-stu-id="fc586-156">**server**</span></span> |<span data-ttu-id="fc586-157">Имя сервера hello DB2 Hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="fc586-158">Да</span><span class="sxs-lookup"><span data-stu-id="fc586-158">Yes</span></span> |
| <span data-ttu-id="fc586-159">**database**</span><span class="sxs-lookup"><span data-stu-id="fc586-159">**database**</span></span> |<span data-ttu-id="fc586-160">Имя базы данных hello DB2 Hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="fc586-161">Да</span><span class="sxs-lookup"><span data-stu-id="fc586-161">Yes</span></span> |
| <span data-ttu-id="fc586-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="fc586-162">**schema**</span></span> |<span data-ttu-id="fc586-163">Имя Hello hello схемы в базе данных hello DB2.</span><span class="sxs-lookup"><span data-stu-id="fc586-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="fc586-164">Это свойство чувствительно к регистру.</span><span class="sxs-lookup"><span data-stu-id="fc586-164">This property is case-sensitive.</span></span> |<span data-ttu-id="fc586-165">Нет</span><span class="sxs-lookup"><span data-stu-id="fc586-165">No</span></span> |
| <span data-ttu-id="fc586-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="fc586-166">**authenticationType**</span></span> |<span data-ttu-id="fc586-167">Тип проверки подлинности, которая является базой данных toohello DB2 используется tooconnect Hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="fc586-168">Возможные значения Hello: анонимный, обычная проверка подлинности и Windows.</span><span class="sxs-lookup"><span data-stu-id="fc586-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="fc586-169">Да</span><span class="sxs-lookup"><span data-stu-id="fc586-169">Yes</span></span> |
| <span data-ttu-id="fc586-170">**username**</span><span class="sxs-lookup"><span data-stu-id="fc586-170">**username**</span></span> |<span data-ttu-id="fc586-171">Имя hello учетной записи пользователя при использовании проверки подлинности Basic или Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="fc586-172">Нет</span><span class="sxs-lookup"><span data-stu-id="fc586-172">No</span></span> |
| <span data-ttu-id="fc586-173">**password**</span><span class="sxs-lookup"><span data-stu-id="fc586-173">**password**</span></span> |<span data-ttu-id="fc586-174">Hello пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-174">hello password for hello user account.</span></span> |<span data-ttu-id="fc586-175">Нет</span><span class="sxs-lookup"><span data-stu-id="fc586-175">No</span></span> |
| <span data-ttu-id="fc586-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="fc586-176">**gatewayName**</span></span> |<span data-ttu-id="fc586-177">Имя Hello шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных DB2.</span><span class="sxs-lookup"><span data-stu-id="fc586-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="fc586-178">Да</span><span class="sxs-lookup"><span data-stu-id="fc586-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="fc586-179">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="fc586-179">Dataset properties</span></span>
<span data-ttu-id="fc586-180">Список разделов hello и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fc586-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fc586-181">Разделы, таких как **структуры**, **доступности**и hello **политики** JSON набора данных, являются одинаковыми для всех типов наборов данных (SQL Azure, хранилище больших двоичных объектов Azure, таблица Azure хранилище и т. д).</span><span class="sxs-lookup"><span data-stu-id="fc586-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="fc586-182">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fc586-183">Hello **typeProperties** раздел для набора данных типа **RelationalTable**, который включает набор данных hello DB2, имеет следующие свойства hello:</span><span class="sxs-lookup"><span data-stu-id="fc586-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="fc586-184">Свойство</span><span class="sxs-lookup"><span data-stu-id="fc586-184">Property</span></span> | <span data-ttu-id="fc586-185">Описание</span><span class="sxs-lookup"><span data-stu-id="fc586-185">Description</span></span> | <span data-ttu-id="fc586-186">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fc586-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc586-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="fc586-187">**tableName**</span></span> |<span data-ttu-id="fc586-188">Имя таблицы hello в экземпляре базы данных hello DB2, hello связанной службы Hello ссылается.</span><span class="sxs-lookup"><span data-stu-id="fc586-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="fc586-189">Это свойство чувствительно к регистру.</span><span class="sxs-lookup"><span data-stu-id="fc586-189">This property is case-sensitive.</span></span> |<span data-ttu-id="fc586-190">Нет (если hello **запроса** действия копирования типа **RelationalSource** указан)</span><span class="sxs-lookup"><span data-stu-id="fc586-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fc586-191">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="fc586-191">Copy Activity properties</span></span>
<span data-ttu-id="fc586-192">Список разделов hello и свойства, доступные для определения действия копирования см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fc586-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fc586-193">Свойства действия копирования, такие как **имя**, **описание**, **входные** и **выходные** таблицы и **политика**, доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="fc586-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="fc586-194">Здравствуйте, свойств, доступных в hello **typeProperties** раздел hello действия для каждого типа действия.</span><span class="sxs-lookup"><span data-stu-id="fc586-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="fc586-195">Для действия копирования hello свойства зависят от типов источников данных и приемники hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="fc586-196">Для действия копирования, когда источник hello типа **RelationalSource** (включая DB2), доступны следующие свойства hello в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="fc586-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="fc586-197">Свойство</span><span class="sxs-lookup"><span data-stu-id="fc586-197">Property</span></span> | <span data-ttu-id="fc586-198">Описание</span><span class="sxs-lookup"><span data-stu-id="fc586-198">Description</span></span> | <span data-ttu-id="fc586-199">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="fc586-199">Allowed values</span></span> | <span data-ttu-id="fc586-200">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fc586-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fc586-201">**query**</span><span class="sxs-lookup"><span data-stu-id="fc586-201">**query**</span></span> |<span data-ttu-id="fc586-202">Используйте tooread hello hello пользовательского запроса данных.</span><span class="sxs-lookup"><span data-stu-id="fc586-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="fc586-203">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="fc586-203">SQL query string.</span></span> <span data-ttu-id="fc586-204">Например: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="fc586-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="fc586-205">Нет (если hello **tableName** указанного свойства набора данных)</span><span class="sxs-lookup"><span data-stu-id="fc586-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="fc586-206">В именах схем и таблиц учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="fc586-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="fc586-207">В инструкции запроса hello, заключите имена свойств с помощью «» (двойные кавычки).</span><span class="sxs-lookup"><span data-stu-id="fc586-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="fc586-208">Например:</span><span class="sxs-lookup"><span data-stu-id="fc586-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="fc586-209">Пример JSON: копирование данных из DB2 tooAzure хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="fc586-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="fc586-210">В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fc586-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fc586-211">Hello примере показано, как данные toocopy из DB2 базы данных хранилища tooBlob.</span><span class="sxs-lookup"><span data-stu-id="fc586-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="fc586-212">Тем не менее, данные можно скопировать слишком[все поддерживаемые данные хранить тип приемника](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью действия копирования фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="fc586-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="fc586-213">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="fc586-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="fc586-214">Связанная служба DB2 типа [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fc586-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="fc586-215">Связанная служба хранилища BLOB-объектов Azure типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fc586-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="fc586-216">Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fc586-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="fc586-217">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="fc586-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="fc586-218">Объект [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) свойства</span><span class="sxs-lookup"><span data-stu-id="fc586-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="fc586-219">Образец Hello копирует данные из результатов запроса в tooan базы данных DB2 BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="fc586-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="fc586-220">свойства Hello JSON, используемые в образце hello описаны в следующих разделах hello определений сущностей hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="fc586-221">Сначала установите и настройте шлюз данных.</span><span class="sxs-lookup"><span data-stu-id="fc586-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="fc586-222">Инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="fc586-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fc586-223">**Связанная служба DB2**</span><span class="sxs-lookup"><span data-stu-id="fc586-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="fc586-224">**Связанная служба хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="fc586-224">**Azure Blob storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="fc586-225">**Входной набор данных DB2**</span><span class="sxs-lookup"><span data-stu-id="fc586-225">**DB2 input dataset**</span></span>

<span data-ttu-id="fc586-226">Образец Hello предполагается, что вы создали таблицу в DB2, с именем «MyTable», что столбец с меткой «timestamp» для hello временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="fc586-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="fc586-227">Hello **внешних** задано слишком «true».</span><span class="sxs-lookup"><span data-stu-id="fc586-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="fc586-228">Этот параметр сообщает hello служба фабрики данных, что этот набор данных является фабрикой toohello внешних данных, а не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="fc586-229">Обратите внимание, что hello **тип** задано слишком**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="fc586-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="fc586-230">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="fc586-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="fc586-231">Записывается новый большой двоичный объект tooa каждый час параметр hello **частоты** свойство слишком «Час» и hello **интервал** too1 свойство.</span><span class="sxs-lookup"><span data-stu-id="fc586-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="fc586-232">Hello **folderPath** свойства для большого двоичного объекта hello динамически вычисляется на основе hello время начала среза hello, обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="fc586-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fc586-233">путь к папке Hello использует hello года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="fc586-234">**Конвейер для действия копирования hello**</span><span class="sxs-lookup"><span data-stu-id="fc586-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="fc586-235">конвейер Hello содержит операции копирования, настроенный toouse указанного входного и выходного наборов данных, а какой запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="fc586-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="fc586-236">В hello определения JSON для конвейера hello hello **источника** тип установлен слишком**RelationalSource** и hello **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fc586-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="fc586-237">запрос SQL Hello, указанный для hello **запроса** свойство выбирает hello данные из таблицы «Заказы» hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="fc586-238">Сопоставление типов для DB2</span><span class="sxs-lookup"><span data-stu-id="fc586-238">Type mapping for DB2</span></span>
<span data-ttu-id="fc586-239">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматический тип преобразования из типа toosink тип источника, используя двухэтапный подходе hello:</span><span class="sxs-lookup"><span data-stu-id="fc586-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="fc586-240">Преобразование из типа .NET tooa тип источника</span><span class="sxs-lookup"><span data-stu-id="fc586-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="fc586-241">Преобразование из типа собственный приемник tooa тип .NET</span><span class="sxs-lookup"><span data-stu-id="fc586-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="fc586-242">Hello следующие сопоставления используются при действии копирования преобразует данные hello из типа DB2 tooa типа .NET.</span><span class="sxs-lookup"><span data-stu-id="fc586-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="fc586-243">Тип базы данных DB2</span><span class="sxs-lookup"><span data-stu-id="fc586-243">DB2 database type</span></span> | <span data-ttu-id="fc586-244">Тип .NET Framework</span><span class="sxs-lookup"><span data-stu-id="fc586-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="fc586-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="fc586-245">SmallInt</span></span> |<span data-ttu-id="fc586-246">Int16</span><span class="sxs-lookup"><span data-stu-id="fc586-246">Int16</span></span> |
| <span data-ttu-id="fc586-247">Число</span><span class="sxs-lookup"><span data-stu-id="fc586-247">Integer</span></span> |<span data-ttu-id="fc586-248">Int32</span><span class="sxs-lookup"><span data-stu-id="fc586-248">Int32</span></span> |
| <span data-ttu-id="fc586-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="fc586-249">BigInt</span></span> |<span data-ttu-id="fc586-250">Int64</span><span class="sxs-lookup"><span data-stu-id="fc586-250">Int64</span></span> |
| <span data-ttu-id="fc586-251">Real</span><span class="sxs-lookup"><span data-stu-id="fc586-251">Real</span></span> |<span data-ttu-id="fc586-252">Single</span><span class="sxs-lookup"><span data-stu-id="fc586-252">Single</span></span> |
| <span data-ttu-id="fc586-253">Double</span><span class="sxs-lookup"><span data-stu-id="fc586-253">Double</span></span> |<span data-ttu-id="fc586-254">Double</span><span class="sxs-lookup"><span data-stu-id="fc586-254">Double</span></span> |
| <span data-ttu-id="fc586-255">Float</span><span class="sxs-lookup"><span data-stu-id="fc586-255">Float</span></span> |<span data-ttu-id="fc586-256">Double</span><span class="sxs-lookup"><span data-stu-id="fc586-256">Double</span></span> |
| <span data-ttu-id="fc586-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc586-257">Decimal</span></span> |<span data-ttu-id="fc586-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc586-258">Decimal</span></span> |
| <span data-ttu-id="fc586-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="fc586-259">DecimalFloat</span></span> |<span data-ttu-id="fc586-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc586-260">Decimal</span></span> |
| <span data-ttu-id="fc586-261">Числовой</span><span class="sxs-lookup"><span data-stu-id="fc586-261">Numeric</span></span> |<span data-ttu-id="fc586-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc586-262">Decimal</span></span> |
| <span data-ttu-id="fc586-263">Дата</span><span class="sxs-lookup"><span data-stu-id="fc586-263">Date</span></span> |<span data-ttu-id="fc586-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="fc586-264">DateTime</span></span> |
| <span data-ttu-id="fc586-265">Время</span><span class="sxs-lookup"><span data-stu-id="fc586-265">Time</span></span> |<span data-ttu-id="fc586-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc586-266">TimeSpan</span></span> |
| <span data-ttu-id="fc586-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="fc586-267">Timestamp</span></span> |<span data-ttu-id="fc586-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="fc586-268">DateTime</span></span> |
| <span data-ttu-id="fc586-269">xml</span><span class="sxs-lookup"><span data-stu-id="fc586-269">Xml</span></span> |<span data-ttu-id="fc586-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fc586-270">Byte[]</span></span> |
| <span data-ttu-id="fc586-271">Char</span><span class="sxs-lookup"><span data-stu-id="fc586-271">Char</span></span> |<span data-ttu-id="fc586-272">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-272">String</span></span> |
| <span data-ttu-id="fc586-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="fc586-273">VarChar</span></span> |<span data-ttu-id="fc586-274">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-274">String</span></span> |
| <span data-ttu-id="fc586-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="fc586-275">LongVarChar</span></span> |<span data-ttu-id="fc586-276">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-276">String</span></span> |
| <span data-ttu-id="fc586-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="fc586-277">DB2DynArray</span></span> |<span data-ttu-id="fc586-278">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-278">String</span></span> |
| <span data-ttu-id="fc586-279">Binary</span><span class="sxs-lookup"><span data-stu-id="fc586-279">Binary</span></span> |<span data-ttu-id="fc586-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fc586-280">Byte[]</span></span> |
| <span data-ttu-id="fc586-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="fc586-281">VarBinary</span></span> |<span data-ttu-id="fc586-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fc586-282">Byte[]</span></span> |
| <span data-ttu-id="fc586-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="fc586-283">LongVarBinary</span></span> |<span data-ttu-id="fc586-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fc586-284">Byte[]</span></span> |
| <span data-ttu-id="fc586-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="fc586-285">Graphic</span></span> |<span data-ttu-id="fc586-286">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-286">String</span></span> |
| <span data-ttu-id="fc586-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="fc586-287">VarGraphic</span></span> |<span data-ttu-id="fc586-288">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-288">String</span></span> |
| <span data-ttu-id="fc586-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="fc586-289">LongVarGraphic</span></span> |<span data-ttu-id="fc586-290">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-290">String</span></span> |
| <span data-ttu-id="fc586-291">Clob</span><span class="sxs-lookup"><span data-stu-id="fc586-291">Clob</span></span> |<span data-ttu-id="fc586-292">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-292">String</span></span> |
| <span data-ttu-id="fc586-293">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="fc586-293">Blob</span></span> |<span data-ttu-id="fc586-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fc586-294">Byte[]</span></span> |
| <span data-ttu-id="fc586-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="fc586-295">DbClob</span></span> |<span data-ttu-id="fc586-296">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-296">String</span></span> |
| <span data-ttu-id="fc586-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="fc586-297">SmallInt</span></span> |<span data-ttu-id="fc586-298">Int16</span><span class="sxs-lookup"><span data-stu-id="fc586-298">Int16</span></span> |
| <span data-ttu-id="fc586-299">Число</span><span class="sxs-lookup"><span data-stu-id="fc586-299">Integer</span></span> |<span data-ttu-id="fc586-300">Int32</span><span class="sxs-lookup"><span data-stu-id="fc586-300">Int32</span></span> |
| <span data-ttu-id="fc586-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="fc586-301">BigInt</span></span> |<span data-ttu-id="fc586-302">Int64</span><span class="sxs-lookup"><span data-stu-id="fc586-302">Int64</span></span> |
| <span data-ttu-id="fc586-303">Real</span><span class="sxs-lookup"><span data-stu-id="fc586-303">Real</span></span> |<span data-ttu-id="fc586-304">Single</span><span class="sxs-lookup"><span data-stu-id="fc586-304">Single</span></span> |
| <span data-ttu-id="fc586-305">Double</span><span class="sxs-lookup"><span data-stu-id="fc586-305">Double</span></span> |<span data-ttu-id="fc586-306">Double</span><span class="sxs-lookup"><span data-stu-id="fc586-306">Double</span></span> |
| <span data-ttu-id="fc586-307">Float</span><span class="sxs-lookup"><span data-stu-id="fc586-307">Float</span></span> |<span data-ttu-id="fc586-308">Double</span><span class="sxs-lookup"><span data-stu-id="fc586-308">Double</span></span> |
| <span data-ttu-id="fc586-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc586-309">Decimal</span></span> |<span data-ttu-id="fc586-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc586-310">Decimal</span></span> |
| <span data-ttu-id="fc586-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="fc586-311">DecimalFloat</span></span> |<span data-ttu-id="fc586-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc586-312">Decimal</span></span> |
| <span data-ttu-id="fc586-313">Числовой</span><span class="sxs-lookup"><span data-stu-id="fc586-313">Numeric</span></span> |<span data-ttu-id="fc586-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="fc586-314">Decimal</span></span> |
| <span data-ttu-id="fc586-315">Дата</span><span class="sxs-lookup"><span data-stu-id="fc586-315">Date</span></span> |<span data-ttu-id="fc586-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="fc586-316">DateTime</span></span> |
| <span data-ttu-id="fc586-317">Время</span><span class="sxs-lookup"><span data-stu-id="fc586-317">Time</span></span> |<span data-ttu-id="fc586-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc586-318">TimeSpan</span></span> |
| <span data-ttu-id="fc586-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="fc586-319">Timestamp</span></span> |<span data-ttu-id="fc586-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="fc586-320">DateTime</span></span> |
| <span data-ttu-id="fc586-321">xml</span><span class="sxs-lookup"><span data-stu-id="fc586-321">Xml</span></span> |<span data-ttu-id="fc586-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fc586-322">Byte[]</span></span> |
| <span data-ttu-id="fc586-323">Char</span><span class="sxs-lookup"><span data-stu-id="fc586-323">Char</span></span> |<span data-ttu-id="fc586-324">Строка</span><span class="sxs-lookup"><span data-stu-id="fc586-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="fc586-325">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="fc586-325">Map source toosink columns</span></span>
<span data-ttu-id="fc586-326">статье toomap колонкам hello исходного набора данных toocolumns в наборе данных приемник hello, toolearn [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fc586-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="fc586-327">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="fc586-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="fc586-328">При копировании данных из хранилища реляционных данных хранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="fc586-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="fc586-329">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="fc586-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fc586-330">Можно также настроить повтора hello **политики** свойства для набора данных toorerun срез, когда происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="fc586-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="fc586-331">Убедитесь, что hello и тех же данных считывается независимо от того, как много раз hello срез повторного запуска и независимо от того, как повторно запустить срез hello.</span><span class="sxs-lookup"><span data-stu-id="fc586-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="fc586-332">Дополнительные сведения см. в разделе [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fc586-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fc586-333">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="fc586-333">Performance and tuning</span></span>
<span data-ttu-id="fc586-334">Дополнительные сведения о ключевых факторов, влияющих на производительность hello действия копирования, а также способы toooptimize производительности в hello [производительности для действия копирования и руководство по настройке](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="fc586-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
