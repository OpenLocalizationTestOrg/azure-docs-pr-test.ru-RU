---
title: "Источник OData данных aaaMove | Документы Microsoft"
description: "Узнайте, как данные toomove из OData источников, с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="06b82-103">Перемещение данных из источника OData с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="06b82-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="06b82-104">В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данные из источника OData.</span><span class="sxs-lookup"><span data-stu-id="06b82-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="06b82-105">Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="06b82-106">Можно скопировать данные из хранилища данных приемник tooany поддерживается источника OData.</span><span class="sxs-lookup"><span data-stu-id="06b82-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="06b82-107">Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы.</span><span class="sxs-lookup"><span data-stu-id="06b82-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="06b82-108">Фабрика данных в настоящее время поддерживает только для перемещения данных из источника данных tooother OData хранятся, но не для перемещения данных из других данных хранит tooan источника OData.</span><span class="sxs-lookup"><span data-stu-id="06b82-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="06b82-109">Поддерживаемые версии и типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="06b82-109">Supported versions and authentication types</span></span>
<span data-ttu-id="06b82-110">Этот соединитель OData поддерживает OData версии 3.0 и 4.0 и может копировать данные как из облачных, так и из локальных источников OData.</span><span class="sxs-lookup"><span data-stu-id="06b82-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="06b82-111">На последнем hello требуется hello tooinstall шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="06b82-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="06b82-112">Сведения о шлюзе управления данными см. в статье [Перемещение данных между локальными источниками и облаком](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="06b82-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="06b82-113">Далее приведены поддерживаемые типы аутентификации:</span><span class="sxs-lookup"><span data-stu-id="06b82-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="06b82-114">tooaccess **облака** веб-канала OData, можно использовать анонимные, basic (имя пользователя и пароль) или Azure Active Directory на основе проверки подлинности OAuth.</span><span class="sxs-lookup"><span data-stu-id="06b82-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="06b82-115">tooaccess **локальной** веб-канала OData, можно использовать анонимный доступ, basic (имя пользователя и пароль), или проверку подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="06b82-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="06b82-116">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="06b82-116">Getting started</span></span>
<span data-ttu-id="06b82-117">Вы можете создать конвейер с действием копирования, который перемещает данные из источника OData, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="06b82-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="06b82-118">toocreate простым способом Hello конвейера — toouse hello **мастер копирования**.</span><span class="sxs-lookup"><span data-stu-id="06b82-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="06b82-119">В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="06b82-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="06b82-120">Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**.</span><span class="sxs-lookup"><span data-stu-id="06b82-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="06b82-121">В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.</span><span class="sxs-lookup"><span data-stu-id="06b82-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="06b82-122">Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="06b82-123">Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="06b82-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="06b82-124">Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования.</span><span class="sxs-lookup"><span data-stu-id="06b82-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="06b82-125">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="06b82-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="06b82-126">При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="06b82-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="06b82-127">При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="06b82-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="06b82-128">Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из источника OData см. в разделе [JSON пример: копирование данных из источника OData tooAzure большого двоичного объекта](#json-example-copy-data-from-odata-source-to-azure-blob) данной статьи.</span><span class="sxs-lookup"><span data-stu-id="06b82-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="06b82-129">Hello в следующих разделах содержатся сведения о свойствах JSON, которые являются источником tooOData определенных сущностей фабрики данных используется toodefine:</span><span class="sxs-lookup"><span data-stu-id="06b82-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="06b82-130">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="06b82-130">Linked Service properties</span></span>
<span data-ttu-id="06b82-131">Hello в следующей таблице приводится описание службы конкретных tooOData связанные элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="06b82-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="06b82-132">Свойство</span><span class="sxs-lookup"><span data-stu-id="06b82-132">Property</span></span> | <span data-ttu-id="06b82-133">Описание</span><span class="sxs-lookup"><span data-stu-id="06b82-133">Description</span></span> | <span data-ttu-id="06b82-134">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06b82-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06b82-135">type</span><span class="sxs-lookup"><span data-stu-id="06b82-135">type</span></span> |<span data-ttu-id="06b82-136">свойство типа Hello должно быть присвоено: **OData**</span><span class="sxs-lookup"><span data-stu-id="06b82-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="06b82-137">Да</span><span class="sxs-lookup"><span data-stu-id="06b82-137">Yes</span></span> |
| <span data-ttu-id="06b82-138">url</span><span class="sxs-lookup"><span data-stu-id="06b82-138">url</span></span> |<span data-ttu-id="06b82-139">URL-адрес службы OData hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-139">Url of hello OData service.</span></span> |<span data-ttu-id="06b82-140">Да</span><span class="sxs-lookup"><span data-stu-id="06b82-140">Yes</span></span> |
| <span data-ttu-id="06b82-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="06b82-141">authenticationType</span></span> |<span data-ttu-id="06b82-142">Тип проверки подлинности, используемый источник OData toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="06b82-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="06b82-143">Возможные значения для облачной службы OData: "Анонимно", "Обычная" и "OAuth" (обратите внимание, что сейчас фабрика данных Azure поддерживает только аутентификацию OAuth на основе Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="06b82-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="06b82-144">Для локальной службы OData возможными значениями являются "Анонимная", "Обычная" и "Windows".</span><span class="sxs-lookup"><span data-stu-id="06b82-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="06b82-145">Да</span><span class="sxs-lookup"><span data-stu-id="06b82-145">Yes</span></span> |
| <span data-ttu-id="06b82-146">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="06b82-146">username</span></span> |<span data-ttu-id="06b82-147">При использовании обычной проверки подлинности укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="06b82-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="06b82-148">Да (только при использовании обычной проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="06b82-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="06b82-149">пароль</span><span class="sxs-lookup"><span data-stu-id="06b82-149">password</span></span> |<span data-ttu-id="06b82-150">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="06b82-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="06b82-151">Да (только при использовании обычной проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="06b82-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="06b82-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="06b82-152">authorizedCredential</span></span> |<span data-ttu-id="06b82-153">Если вы используете OAuth, нажмите кнопку **авторизовать** приветствия мастера копирования фабрики данных или редактор и введите учетные данные, hello значением этого свойства будет создан.</span><span class="sxs-lookup"><span data-stu-id="06b82-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="06b82-154">Да (только при использовании аутентификации OAuth)</span><span class="sxs-lookup"><span data-stu-id="06b82-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="06b82-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="06b82-155">gatewayName</span></span> |<span data-ttu-id="06b82-156">Имя шлюза hello, hello служба фабрики данных следует использовать службы OData tooconnect toohello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="06b82-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="06b82-157">Его необходимо указывать только в том случае, если вы копируете данные из источника в локальной службе OData.</span><span class="sxs-lookup"><span data-stu-id="06b82-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="06b82-158">Нет</span><span class="sxs-lookup"><span data-stu-id="06b82-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="06b82-159">Использовать обычную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="06b82-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="06b82-160">Использовать анонимную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="06b82-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="06b82-161">Использование проверки подлинности Windows при получении доступа к локальному источнику OData</span><span class="sxs-lookup"><span data-stu-id="06b82-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="06b82-162">Использование аутентификации OAuth при получении доступа к облачному источнику OData</span><span class="sxs-lookup"><span data-stu-id="06b82-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="06b82-163">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="06b82-163">Dataset properties</span></span>
<span data-ttu-id="06b82-164">Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="06b82-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="06b82-165">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="06b82-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="06b82-166">Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="06b82-167">Hello typeProperties статьи для набора данных типа **ODataResource** (включает набор данных OData) имеет следующие свойства hello</span><span class="sxs-lookup"><span data-stu-id="06b82-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="06b82-168">Свойство</span><span class="sxs-lookup"><span data-stu-id="06b82-168">Property</span></span> | <span data-ttu-id="06b82-169">Описание</span><span class="sxs-lookup"><span data-stu-id="06b82-169">Description</span></span> | <span data-ttu-id="06b82-170">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06b82-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="06b82-171">path</span><span class="sxs-lookup"><span data-stu-id="06b82-171">path</span></span> |<span data-ttu-id="06b82-172">Путь toohello ресурс OData</span><span class="sxs-lookup"><span data-stu-id="06b82-172">Path toohello OData resource</span></span> |<span data-ttu-id="06b82-173">Нет</span><span class="sxs-lookup"><span data-stu-id="06b82-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="06b82-174">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="06b82-174">Copy activity properties</span></span>
<span data-ttu-id="06b82-175">Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="06b82-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="06b82-176">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="06b82-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="06b82-177">Свойства доступны в разделе typeProperties hello hello действий на hello другой стороны, могут различаться для каждого типа действия.</span><span class="sxs-lookup"><span data-stu-id="06b82-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="06b82-178">Для действия копирования они зависят от типов источников и приемников hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="06b82-179">Если источник имеет тип **RelationalSource** (включает OData) hello следующие свойства доступны в разделе "typeProperties":</span><span class="sxs-lookup"><span data-stu-id="06b82-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="06b82-180">Свойство</span><span class="sxs-lookup"><span data-stu-id="06b82-180">Property</span></span> | <span data-ttu-id="06b82-181">Описание</span><span class="sxs-lookup"><span data-stu-id="06b82-181">Description</span></span> | <span data-ttu-id="06b82-182">Пример</span><span class="sxs-lookup"><span data-stu-id="06b82-182">Example</span></span> | <span data-ttu-id="06b82-183">Обязательно</span><span class="sxs-lookup"><span data-stu-id="06b82-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="06b82-184">query</span><span class="sxs-lookup"><span data-stu-id="06b82-184">query</span></span> |<span data-ttu-id="06b82-185">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="06b82-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="06b82-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="06b82-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="06b82-187">Нет</span><span class="sxs-lookup"><span data-stu-id="06b82-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="06b82-188">Сопоставление типов для OData</span><span class="sxs-lookup"><span data-stu-id="06b82-188">Type Mapping for OData</span></span>
<span data-ttu-id="06b82-189">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="06b82-190">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="06b82-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="06b82-191">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="06b82-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="06b82-192">При перемещении данных из OData hello следующие сопоставления используются из типа too.NET типы OData.</span><span class="sxs-lookup"><span data-stu-id="06b82-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="06b82-193">Тип данных OData</span><span class="sxs-lookup"><span data-stu-id="06b82-193">OData Data Type</span></span> | <span data-ttu-id="06b82-194">Тип .NET</span><span class="sxs-lookup"><span data-stu-id="06b82-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="06b82-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="06b82-195">Edm.Binary</span></span> |<span data-ttu-id="06b82-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="06b82-196">Byte[]</span></span> |
| <span data-ttu-id="06b82-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="06b82-197">Edm.Boolean</span></span> |<span data-ttu-id="06b82-198">Bool</span><span class="sxs-lookup"><span data-stu-id="06b82-198">Bool</span></span> |
| <span data-ttu-id="06b82-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="06b82-199">Edm.Byte</span></span> |<span data-ttu-id="06b82-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="06b82-200">Byte[]</span></span> |
| <span data-ttu-id="06b82-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="06b82-201">Edm.DateTime</span></span> |<span data-ttu-id="06b82-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="06b82-202">DateTime</span></span> |
| <span data-ttu-id="06b82-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="06b82-203">Edm.Decimal</span></span> |<span data-ttu-id="06b82-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="06b82-204">Decimal</span></span> |
| <span data-ttu-id="06b82-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="06b82-205">Edm.Double</span></span> |<span data-ttu-id="06b82-206">Double</span><span class="sxs-lookup"><span data-stu-id="06b82-206">Double</span></span> |
| <span data-ttu-id="06b82-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="06b82-207">Edm.Single</span></span> |<span data-ttu-id="06b82-208">Single</span><span class="sxs-lookup"><span data-stu-id="06b82-208">Single</span></span> |
| <span data-ttu-id="06b82-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="06b82-209">Edm.Guid</span></span> |<span data-ttu-id="06b82-210">Guid</span><span class="sxs-lookup"><span data-stu-id="06b82-210">Guid</span></span> |
| <span data-ttu-id="06b82-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="06b82-211">Edm.Int16</span></span> |<span data-ttu-id="06b82-212">Int16</span><span class="sxs-lookup"><span data-stu-id="06b82-212">Int16</span></span> |
| <span data-ttu-id="06b82-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="06b82-213">Edm.Int32</span></span> |<span data-ttu-id="06b82-214">Int32</span><span class="sxs-lookup"><span data-stu-id="06b82-214">Int32</span></span> |
| <span data-ttu-id="06b82-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="06b82-215">Edm.Int64</span></span> |<span data-ttu-id="06b82-216">Int64</span><span class="sxs-lookup"><span data-stu-id="06b82-216">Int64</span></span> |
| <span data-ttu-id="06b82-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="06b82-217">Edm.SByte</span></span> |<span data-ttu-id="06b82-218">Int16</span><span class="sxs-lookup"><span data-stu-id="06b82-218">Int16</span></span> |
| <span data-ttu-id="06b82-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="06b82-219">Edm.String</span></span> |<span data-ttu-id="06b82-220">Строка</span><span class="sxs-lookup"><span data-stu-id="06b82-220">String</span></span> |
| <span data-ttu-id="06b82-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="06b82-221">Edm.Time</span></span> |<span data-ttu-id="06b82-222">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="06b82-222">TimeSpan</span></span> |
| <span data-ttu-id="06b82-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="06b82-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="06b82-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="06b82-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="06b82-225">Сложные типы данных OData, например объекты, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="06b82-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="06b82-226">Пример JSON: копирование данных из источника OData tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="06b82-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="06b82-227">В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="06b82-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="06b82-228">Они показывают, как toocopy из OData источника tooan хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="06b82-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="06b82-229">Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="06b82-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="06b82-230">Образец Hello имеет hello, следуя сущностей фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="06b82-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="06b82-231">Связанная служба типа [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06b82-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="06b82-232">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06b82-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="06b82-233">Входной [набор данных](data-factory-create-datasets.md) типа [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06b82-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="06b82-234">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="06b82-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="06b82-235">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="06b82-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="06b82-236">Образец Hello копирует данные из запросов к tooan источника OData, BLOB-объектов Azure каждый час.</span><span class="sxs-lookup"><span data-stu-id="06b82-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="06b82-237">свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="06b82-238">**OData связанной службы:** в этом примере используется hello анонимную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="06b82-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="06b82-239">Сведения о различных типах проверки подлинности, которые можно использовать, см. в разделе [Свойства связанной службы OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="06b82-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="06b82-240">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="06b82-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="06b82-241">**Входной набор данных OData**</span><span class="sxs-lookup"><span data-stu-id="06b82-241">**OData input dataset:**</span></span>

<span data-ttu-id="06b82-242">Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="06b82-243">Указание **путь** в наборе данных hello определение является необязательным.</span><span class="sxs-lookup"><span data-stu-id="06b82-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="06b82-244">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="06b82-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="06b82-245">Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="06b82-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="06b82-246">путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается.</span><span class="sxs-lookup"><span data-stu-id="06b82-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="06b82-247">путь к папке Hello использует года, месяца, дня и часа части времени начала hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="06b82-248">**Действие копирования в конвейере с OData в качестве источника и большим двоичным объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="06b82-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="06b82-249">Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="06b82-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="06b82-250">В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="06b82-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="06b82-251">запрос SQL Hello, указанный для hello **запроса** свойство выбирает hello последние (новейшую) данные из источника OData hello.</span><span class="sxs-lookup"><span data-stu-id="06b82-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="06b82-252">Указание **запроса** в конвейере hello определение является необязательным.</span><span class="sxs-lookup"><span data-stu-id="06b82-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="06b82-253">Hello **URL-адрес** , служба фабрики данных hello использует tooretrieve данных является: URL-адрес указан в hello связанной службы (обязательно) + пути, указанному в наборе данных hello (необязательно) + запроса в конвейере hello (необязательно).</span><span class="sxs-lookup"><span data-stu-id="06b82-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="06b82-254">Сопоставление типов для OData</span><span class="sxs-lookup"><span data-stu-id="06b82-254">Type mapping for OData</span></span>
<span data-ttu-id="06b82-255">Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:</span><span class="sxs-lookup"><span data-stu-id="06b82-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="06b82-256">Преобразование из типа too.NET типы собственного источника</span><span class="sxs-lookup"><span data-stu-id="06b82-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="06b82-257">Преобразовываемый тип приемника toonative тип .NET</span><span class="sxs-lookup"><span data-stu-id="06b82-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="06b82-258">При перемещении данных из хранилищ данных OData, OData указаны too.NET сопоставленные типы.</span><span class="sxs-lookup"><span data-stu-id="06b82-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="06b82-259">Сопоставить исходные столбцы toosink</span><span class="sxs-lookup"><span data-stu-id="06b82-259">Map source toosink columns</span></span>
<span data-ttu-id="06b82-260">toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="06b82-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="06b82-261">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="06b82-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="06b82-262">При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="06b82-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="06b82-263">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="06b82-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="06b82-264">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="06b82-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="06b82-265">При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез.</span><span class="sxs-lookup"><span data-stu-id="06b82-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="06b82-266">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="06b82-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="06b82-267">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="06b82-267">Performance and Tuning</span></span>
<span data-ttu-id="06b82-268">В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.</span><span class="sxs-lookup"><span data-stu-id="06b82-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
