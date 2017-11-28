---
title: "Перемещение данных из источников OData | Документация Майкрософт"
description: "Узнайте, как перемещать данные из источников OData с помощью фабрики данных Azure."
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
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="f227c-103">Перемещение данных из источника OData с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="f227c-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="f227c-104">В этой статье описывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из источника OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="f227c-105">Это продолжение статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.</span><span class="sxs-lookup"><span data-stu-id="f227c-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="f227c-106">Данные из источника OData можно скопировать в любое хранилище данных, поддерживаемое в качестве приемника.</span><span class="sxs-lookup"><span data-stu-id="f227c-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="f227c-107">Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f227c-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="f227c-108">Сейчас фабрика данных поддерживает только перемещение данных из источника OData в другие хранилища данных, но не наоборот.</span><span class="sxs-lookup"><span data-stu-id="f227c-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="f227c-109">Поддерживаемые версии и типы аутентификации</span><span class="sxs-lookup"><span data-stu-id="f227c-109">Supported versions and authentication types</span></span>
<span data-ttu-id="f227c-110">Этот соединитель OData поддерживает OData версии 3.0 и 4.0 и может копировать данные как из облачных, так и из локальных источников OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="f227c-111">Для копирования из локальных источников необходимо установить шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="f227c-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="f227c-112">Сведения о шлюзе управления данными см. в статье [Перемещение данных между локальными источниками и облаком](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="f227c-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="f227c-113">Далее приведены поддерживаемые типы аутентификации:</span><span class="sxs-lookup"><span data-stu-id="f227c-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="f227c-114">Чтобы получить доступ к **облачному** каналу OData, можно использовать анонимную, обычную (имя пользователя и пароль) аутентификацию или аутентификацию OAuth на основе Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f227c-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="f227c-115">Чтобы получить доступ к **локальному** каналу OData, можно использовать анонимную, обычную (имя пользователя и пароль) аутентификацию или аутентификацию Windows.</span><span class="sxs-lookup"><span data-stu-id="f227c-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f227c-116">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="f227c-116">Getting started</span></span>
<span data-ttu-id="f227c-117">Вы можете создать конвейер с действием копирования, который перемещает данные из источника OData, с помощью разных инструментов и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="f227c-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="f227c-118">Проще всего создать конвейер с помощью **мастера копирования**.</span><span class="sxs-lookup"><span data-stu-id="f227c-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="f227c-119">В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.</span><span class="sxs-lookup"><span data-stu-id="f227c-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="f227c-120">Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**.</span><span class="sxs-lookup"><span data-stu-id="f227c-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f227c-121">Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f227c-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f227c-122">Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="f227c-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="f227c-123">Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="f227c-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="f227c-124">Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования.</span><span class="sxs-lookup"><span data-stu-id="f227c-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="f227c-125">Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="f227c-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f227c-126">Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера).</span><span class="sxs-lookup"><span data-stu-id="f227c-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="f227c-127">При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="f227c-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="f227c-128">Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных из источника OData, доступен в разделе [Пример JSON. Копирование данных из источника OData в большой двоичный объект Azure](#json-example-copy-data-from-odata-source-to-azure-blob) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="f227c-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="f227c-129">Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к источнику OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f227c-130">Свойства связанной службы</span><span class="sxs-lookup"><span data-stu-id="f227c-130">Linked Service properties</span></span>
<span data-ttu-id="f227c-131">В приведенной далее таблице содержится описание элементов JSON, которые относятся к связанной службе OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="f227c-132">Свойство</span><span class="sxs-lookup"><span data-stu-id="f227c-132">Property</span></span> | <span data-ttu-id="f227c-133">Описание</span><span class="sxs-lookup"><span data-stu-id="f227c-133">Description</span></span> | <span data-ttu-id="f227c-134">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f227c-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f227c-135">type</span><span class="sxs-lookup"><span data-stu-id="f227c-135">type</span></span> |<span data-ttu-id="f227c-136">Для свойства type необходимо задать значение **OData**</span><span class="sxs-lookup"><span data-stu-id="f227c-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="f227c-137">Да</span><span class="sxs-lookup"><span data-stu-id="f227c-137">Yes</span></span> |
| <span data-ttu-id="f227c-138">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="f227c-138">url</span></span> |<span data-ttu-id="f227c-139">URL-адрес службы OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-139">Url of the OData service.</span></span> |<span data-ttu-id="f227c-140">Да</span><span class="sxs-lookup"><span data-stu-id="f227c-140">Yes</span></span> |
| <span data-ttu-id="f227c-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="f227c-141">authenticationType</span></span> |<span data-ttu-id="f227c-142">Тип проверки подлинности, используемый для подключения к источнику OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="f227c-143">Возможные значения для облачной службы OData: "Анонимно", "Обычная" и "OAuth" (обратите внимание, что сейчас фабрика данных Azure поддерживает только аутентификацию OAuth на основе Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f227c-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="f227c-144">Для локальной службы OData возможными значениями являются "Анонимная", "Обычная" и "Windows".</span><span class="sxs-lookup"><span data-stu-id="f227c-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="f227c-145">Да</span><span class="sxs-lookup"><span data-stu-id="f227c-145">Yes</span></span> |
| <span data-ttu-id="f227c-146">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="f227c-146">username</span></span> |<span data-ttu-id="f227c-147">При использовании обычной проверки подлинности укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="f227c-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="f227c-148">Да (только при использовании обычной проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="f227c-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="f227c-149">пароль</span><span class="sxs-lookup"><span data-stu-id="f227c-149">password</span></span> |<span data-ttu-id="f227c-150">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="f227c-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="f227c-151">Да (только при использовании обычной проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="f227c-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="f227c-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="f227c-152">authorizedCredential</span></span> |<span data-ttu-id="f227c-153">Если используется OAuth, в мастере копирования фабрики данных или редакторе нажмите кнопку **Авторизовать** и введите свои учетные данные, после чего значение этого свойства будет создано автоматически.</span><span class="sxs-lookup"><span data-stu-id="f227c-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="f227c-154">Да (только при использовании аутентификации OAuth)</span><span class="sxs-lookup"><span data-stu-id="f227c-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="f227c-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f227c-155">gatewayName</span></span> |<span data-ttu-id="f227c-156">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной службе OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="f227c-157">Его необходимо указывать только в том случае, если вы копируете данные из источника в локальной службе OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="f227c-158">Нет</span><span class="sxs-lookup"><span data-stu-id="f227c-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="f227c-159">Использовать обычную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="f227c-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="f227c-160">Использовать анонимную проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="f227c-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="f227c-161">Использование проверки подлинности Windows при получении доступа к локальному источнику OData</span><span class="sxs-lookup"><span data-stu-id="f227c-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="f227c-162">Использование аутентификации OAuth при получении доступа к облачному источнику OData</span><span class="sxs-lookup"><span data-stu-id="f227c-162">Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f227c-163">Свойства набора данных</span><span class="sxs-lookup"><span data-stu-id="f227c-163">Dataset properties</span></span>
<span data-ttu-id="f227c-164">Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f227c-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f227c-165">Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).</span><span class="sxs-lookup"><span data-stu-id="f227c-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f227c-166">Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="f227c-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f227c-167">Раздел typeProperties набора данных типа **ODataResource** (который включает в себя набор данных OData) содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="f227c-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="f227c-168">Свойство</span><span class="sxs-lookup"><span data-stu-id="f227c-168">Property</span></span> | <span data-ttu-id="f227c-169">Описание</span><span class="sxs-lookup"><span data-stu-id="f227c-169">Description</span></span> | <span data-ttu-id="f227c-170">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f227c-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f227c-171">path</span><span class="sxs-lookup"><span data-stu-id="f227c-171">path</span></span> |<span data-ttu-id="f227c-172">Путь к ресурсу OData</span><span class="sxs-lookup"><span data-stu-id="f227c-172">Path to the OData resource</span></span> |<span data-ttu-id="f227c-173">Нет</span><span class="sxs-lookup"><span data-stu-id="f227c-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f227c-174">Свойства действия копирования</span><span class="sxs-lookup"><span data-stu-id="f227c-174">Copy activity properties</span></span>
<span data-ttu-id="f227c-175">Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f227c-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f227c-176">Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="f227c-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="f227c-177">С другой стороны, свойства, доступные в разделе typeProperties действия, зависят от конкретного типа действия.</span><span class="sxs-lookup"><span data-stu-id="f227c-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="f227c-178">Для действия копирования они различаются в зависимости от типов источников и приемников.</span><span class="sxs-lookup"><span data-stu-id="f227c-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="f227c-179">Если источник относится к типу **RelationalSource** (который содержит OData), в разделе typeProperties доступны следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="f227c-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="f227c-180">Свойство</span><span class="sxs-lookup"><span data-stu-id="f227c-180">Property</span></span> | <span data-ttu-id="f227c-181">Описание</span><span class="sxs-lookup"><span data-stu-id="f227c-181">Description</span></span> | <span data-ttu-id="f227c-182">Пример</span><span class="sxs-lookup"><span data-stu-id="f227c-182">Example</span></span> | <span data-ttu-id="f227c-183">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f227c-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f227c-184">query</span><span class="sxs-lookup"><span data-stu-id="f227c-184">query</span></span> |<span data-ttu-id="f227c-185">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="f227c-185">Use the custom query to read data.</span></span> |<span data-ttu-id="f227c-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="f227c-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="f227c-187">Нет</span><span class="sxs-lookup"><span data-stu-id="f227c-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="f227c-188">Сопоставление типов для OData</span><span class="sxs-lookup"><span data-stu-id="f227c-188">Type Mapping for OData</span></span>
<span data-ttu-id="f227c-189">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="f227c-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="f227c-190">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="f227c-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f227c-191">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="f227c-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f227c-192">При перемещении данных из OData Business Warehouse для преобразования типов OData Business Warehouse в типы .NET используются следующие сопоставления.</span><span class="sxs-lookup"><span data-stu-id="f227c-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="f227c-193">Тип данных OData</span><span class="sxs-lookup"><span data-stu-id="f227c-193">OData Data Type</span></span> | <span data-ttu-id="f227c-194">Тип .NET</span><span class="sxs-lookup"><span data-stu-id="f227c-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="f227c-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="f227c-195">Edm.Binary</span></span> |<span data-ttu-id="f227c-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f227c-196">Byte[]</span></span> |
| <span data-ttu-id="f227c-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="f227c-197">Edm.Boolean</span></span> |<span data-ttu-id="f227c-198">Bool</span><span class="sxs-lookup"><span data-stu-id="f227c-198">Bool</span></span> |
| <span data-ttu-id="f227c-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="f227c-199">Edm.Byte</span></span> |<span data-ttu-id="f227c-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f227c-200">Byte[]</span></span> |
| <span data-ttu-id="f227c-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="f227c-201">Edm.DateTime</span></span> |<span data-ttu-id="f227c-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="f227c-202">DateTime</span></span> |
| <span data-ttu-id="f227c-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="f227c-203">Edm.Decimal</span></span> |<span data-ttu-id="f227c-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="f227c-204">Decimal</span></span> |
| <span data-ttu-id="f227c-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="f227c-205">Edm.Double</span></span> |<span data-ttu-id="f227c-206">Double</span><span class="sxs-lookup"><span data-stu-id="f227c-206">Double</span></span> |
| <span data-ttu-id="f227c-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="f227c-207">Edm.Single</span></span> |<span data-ttu-id="f227c-208">Single</span><span class="sxs-lookup"><span data-stu-id="f227c-208">Single</span></span> |
| <span data-ttu-id="f227c-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="f227c-209">Edm.Guid</span></span> |<span data-ttu-id="f227c-210">Guid</span><span class="sxs-lookup"><span data-stu-id="f227c-210">Guid</span></span> |
| <span data-ttu-id="f227c-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="f227c-211">Edm.Int16</span></span> |<span data-ttu-id="f227c-212">Int16</span><span class="sxs-lookup"><span data-stu-id="f227c-212">Int16</span></span> |
| <span data-ttu-id="f227c-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="f227c-213">Edm.Int32</span></span> |<span data-ttu-id="f227c-214">Int32</span><span class="sxs-lookup"><span data-stu-id="f227c-214">Int32</span></span> |
| <span data-ttu-id="f227c-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="f227c-215">Edm.Int64</span></span> |<span data-ttu-id="f227c-216">Int64</span><span class="sxs-lookup"><span data-stu-id="f227c-216">Int64</span></span> |
| <span data-ttu-id="f227c-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="f227c-217">Edm.SByte</span></span> |<span data-ttu-id="f227c-218">Int16</span><span class="sxs-lookup"><span data-stu-id="f227c-218">Int16</span></span> |
| <span data-ttu-id="f227c-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="f227c-219">Edm.String</span></span> |<span data-ttu-id="f227c-220">Строка</span><span class="sxs-lookup"><span data-stu-id="f227c-220">String</span></span> |
| <span data-ttu-id="f227c-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="f227c-221">Edm.Time</span></span> |<span data-ttu-id="f227c-222">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="f227c-222">TimeSpan</span></span> |
| <span data-ttu-id="f227c-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="f227c-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="f227c-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f227c-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="f227c-225">Сложные типы данных OData, например объекты, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="f227c-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="f227c-226">Пример JSON. Копирование данных из источника OData в большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="f227c-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="f227c-227">Ниже приведен пример с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f227c-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f227c-228">Вы узнаете, как копировать данные из источника OData в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="f227c-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="f227c-229">Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f227c-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="f227c-230">Пример содержит следующие сущности фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="f227c-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="f227c-231">Связанная служба типа [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f227c-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="f227c-232">Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f227c-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f227c-233">Входной [набор данных](data-factory-create-datasets.md) типа [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f227c-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="f227c-234">Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f227c-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f227c-235">[Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f227c-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f227c-236">В примере данные из запросов к источнику OData каждый час копируются в BLOB-объект Azure.</span><span class="sxs-lookup"><span data-stu-id="f227c-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="f227c-237">Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.</span><span class="sxs-lookup"><span data-stu-id="f227c-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f227c-238">**Связанная служба OData**. В этом примере используется анонимный доступ.</span><span class="sxs-lookup"><span data-stu-id="f227c-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="f227c-239">Сведения о различных типах проверки подлинности, которые можно использовать, см. в разделе [Свойства связанной службы OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f227c-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="f227c-240">**Связанная служба хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="f227c-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="f227c-241">**Входной набор данных OData**</span><span class="sxs-lookup"><span data-stu-id="f227c-241">**OData input dataset:**</span></span>

<span data-ttu-id="f227c-242">Если параметру external присвоить значение true, фабрика данных воспримет этот набор данных как внешний и созданный не в результате какого-либо действия в этой службе.</span><span class="sxs-lookup"><span data-stu-id="f227c-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="f227c-243">Указывать **path** в определении набора данных необязательно.</span><span class="sxs-lookup"><span data-stu-id="f227c-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="f227c-244">**Выходной набор данных BLOB-объекта Azure**</span><span class="sxs-lookup"><span data-stu-id="f227c-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f227c-245">Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f227c-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f227c-246">Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза.</span><span class="sxs-lookup"><span data-stu-id="f227c-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f227c-247">В пути к папке используется год, месяц, день и час времени начала.</span><span class="sxs-lookup"><span data-stu-id="f227c-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


<span data-ttu-id="f227c-248">**Действие копирования в конвейере с OData в качестве источника и большим двоичным объектом в качестве приемника**</span><span class="sxs-lookup"><span data-stu-id="f227c-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="f227c-249">Конвейер содержит действие копирования, которое использует входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="f227c-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f227c-250">В определении JSON конвейера для типа **source** установлено значение **RelationalSource**, а для типа **sink** — значение **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f227c-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f227c-251">SQL-запрос, заданный для свойства **query** , выбирает самые последние (новейшие) данные из источника OData.</span><span class="sxs-lookup"><span data-stu-id="f227c-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

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

<span data-ttu-id="f227c-252">Указывать **query** в определении конвейера необязательно.</span><span class="sxs-lookup"><span data-stu-id="f227c-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="f227c-253">**URL-адрес** , который служба фабрики данных использует для извлечения данных, имеет следующий вид: URL-адрес, указанный в связанной службе (обязательно) + путь, указанный в наборе данных (необязательно) + запрос в конвейере (необязательно).</span><span class="sxs-lookup"><span data-stu-id="f227c-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="f227c-254">Сопоставление типов для OData</span><span class="sxs-lookup"><span data-stu-id="f227c-254">Type mapping for OData</span></span>
<span data-ttu-id="f227c-255">Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа.</span><span class="sxs-lookup"><span data-stu-id="f227c-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="f227c-256">Преобразование собственных типов источников в тип .NET.</span><span class="sxs-lookup"><span data-stu-id="f227c-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f227c-257">Преобразование типа .NET в собственный тип приемника.</span><span class="sxs-lookup"><span data-stu-id="f227c-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f227c-258">При перемещении данных из хранилищ данных OData типы данных OData сопоставляются с типами .NET.</span><span class="sxs-lookup"><span data-stu-id="f227c-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="f227c-259">Сопоставление столбцов источника и приемника</span><span class="sxs-lookup"><span data-stu-id="f227c-259">Map source to sink columns</span></span>
<span data-ttu-id="f227c-260">Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f227c-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="f227c-261">Повторяющиеся операции чтения из реляционных источников</span><span class="sxs-lookup"><span data-stu-id="f227c-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="f227c-262">При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов.</span><span class="sxs-lookup"><span data-stu-id="f227c-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="f227c-263">В фабрике данных Azure можно вручную повторно выполнить срез.</span><span class="sxs-lookup"><span data-stu-id="f227c-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f227c-264">Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно.</span><span class="sxs-lookup"><span data-stu-id="f227c-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f227c-265">При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез.</span><span class="sxs-lookup"><span data-stu-id="f227c-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f227c-266">Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f227c-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f227c-267">Производительность и настройка</span><span class="sxs-lookup"><span data-stu-id="f227c-267">Performance and Tuning</span></span>
<span data-ttu-id="f227c-268">Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="f227c-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
