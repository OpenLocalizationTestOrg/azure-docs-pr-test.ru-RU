---
title: "Разработка с помощью API таблицы базы данных Azure Cosmos DB на языке .NET | Документация Майкрософт"
description: "Сведения о разработке с помощью API таблицы базы данных Azure Cosmos DB на языке .NET."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 52cb5f2569b6c3a5301752b1e8bfb6cea13ff7f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="005d3-103">Разработка с помощью API таблицы базы данных Azure Cosmos DB на языке .NET</span><span class="sxs-lookup"><span data-stu-id="005d3-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="005d3-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="005d3-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="005d3-105">Вы можете быстро создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="005d3-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="005d3-106">В рамках этого руководства рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="005d3-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="005d3-107">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="005d3-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="005d3-108">включение возможностей в файле app.config;</span><span class="sxs-lookup"><span data-stu-id="005d3-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="005d3-109">создание таблицы с помощью [API таблицы](table-introduction.md) (предварительная версия);</span><span class="sxs-lookup"><span data-stu-id="005d3-109">Create a table using the [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="005d3-110">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="005d3-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="005d3-111">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="005d3-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="005d3-112">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="005d3-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="005d3-113">запрос сущностей с использованием автоматического вторичного индексирования;</span><span class="sxs-lookup"><span data-stu-id="005d3-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="005d3-114">Замена сущности</span><span class="sxs-lookup"><span data-stu-id="005d3-114">Replace an entity</span></span> 
> * <span data-ttu-id="005d3-115">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="005d3-115">Delete an entity</span></span> 
> * <span data-ttu-id="005d3-116">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="005d3-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="005d3-117">Таблицы в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="005d3-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="005d3-118">База данных Azure Cosmos DB предоставляет [API таблицы](table-introduction.md) (предварительная версия) для приложений, которым требуется хранилище пар "ключ — значение", не имеющее схемы.</span><span class="sxs-lookup"><span data-stu-id="005d3-118">Azure Cosmos DB provides the [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="005d3-119">Для работы с этой базой данных можно использовать пакеты SDK для [Хранилища таблиц Azure](../storage/common/storage-introduction.md) и интерфейсы REST API.</span><span class="sxs-lookup"><span data-stu-id="005d3-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used to work with Azure Cosmos DB.</span></span> <span data-ttu-id="005d3-120">Azure Cosmos DB позволяет создавать таблицы с высокими требованиями к пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="005d3-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span> <span data-ttu-id="005d3-121">Кроме того, она поддерживает оптимизированные для пропускной способности таблицы, которые неофициально называются таблицами класса "Премиум" и сейчас доступны в общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="005d3-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="005d3-122">Хранилище таблиц Azure можно по-прежнему использовать для таблиц, требующих более низкой пропускной способности и большой емкости хранилища.</span><span class="sxs-lookup"><span data-stu-id="005d3-122">You can continue to use Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="005d3-123">В будущем обновлении мы планируем реализовать в базе данных Azure Cosmos DB поддержку оптимизированных для хранилища таблиц, а имеющиеся и новые учетные записи Хранилища таблиц Azure будут обновлены до учетных записей базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="005d3-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded to Azure Cosmos DB.</span></span>

<span data-ttu-id="005d3-124">Если вы сейчас используете Хранилище таблиц Azure, таблицы класса "Премиум", доступные в предварительной версии, предоставят следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="005d3-124">If you currently use Azure Table storage, you gain the following benefits with the "premium table" preview:</span></span>

- <span data-ttu-id="005d3-125">поддержка готового к использованию [глобального распределения](distribute-data-globally.md) со множественной адресацией, а также с [ручной и автоматической отработкой отказа](regional-failover.md);</span><span class="sxs-lookup"><span data-stu-id="005d3-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="005d3-126">поддержка автоматического схемонезависимого индексирования данных для всех свойств ("вторичные индексы") и быстрого выполнения запросов;</span><span class="sxs-lookup"><span data-stu-id="005d3-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="005d3-127">поддержка [независимого масштабирования хранилища и пропускной способности](partition-data.md) в любом количестве регионов;</span><span class="sxs-lookup"><span data-stu-id="005d3-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="005d3-128">поддержка [выделения пропускной способности на таблицу](request-units.md) с возможностью масштабирования числа запросов в секунду от нескольких сотен до миллионов;</span><span class="sxs-lookup"><span data-stu-id="005d3-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="005d3-129">поддержка [пяти настраиваемых уровней согласованности](consistency-levels.md) с возможностью изменять показатели доступности, задержки и согласованности в соответствии с требованиями приложений;</span><span class="sxs-lookup"><span data-stu-id="005d3-129">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="005d3-130">доступность уровня 99,99 % в отдельном регионе и возможность добавлять дополнительные регионы для более высокого уровня доступности, а также [ведущие в отрасли исчерпывающие Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/cosmos-db/) в общедоступной версии;</span><span class="sxs-lookup"><span data-stu-id="005d3-130">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="005d3-131">поддержка имеющегося пакета SDK .NET для службы хранилища Azure и устранение необходимости изменять код приложения.</span><span class="sxs-lookup"><span data-stu-id="005d3-131">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="005d3-132">В предварительной версии поддержка API таблицы в базе данных Azure Cosmos DB реализуется за счет пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="005d3-132">During the preview, Azure Cosmos DB supports the Table API using the .NET SDK.</span></span> <span data-ttu-id="005d3-133">Вы можете скачать [пакет SDK предварительной версии для службы хранилища Azure](https://aka.ms/premiumtablenuget) на сайте NuGet. Он имеет те же классы и подписи метода, что и [пакет SDK для службы хранилища Azure](https://www.nuget.org/packages/WindowsAzure.Storage), но также может подключаться к учетным записям базы данных Azure Cosmos DB через API таблицы.</span><span class="sxs-lookup"><span data-stu-id="005d3-133">You can download the [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has the same classes and method signatures as the [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="005d3-134">Дополнительные сведения о сложных задачах Хранилища таблиц Azure см. здесь:</span><span class="sxs-lookup"><span data-stu-id="005d3-134">To learn more about complex Azure Table storage tasks, see:</span></span>

* <span data-ttu-id="005d3-135">[Introduction to Azure Cosmos DB: Table API](table-introduction.md) (Общие сведения об API таблицы в базе данных Azure Cosmos DB)</span><span class="sxs-lookup"><span data-stu-id="005d3-135">[Introduction to Azure Cosmos DB: Table API](table-introduction.md)</span></span>
* <span data-ttu-id="005d3-136">Справочная документация по службе таблиц с полными сведениями о доступных API-интерфейсах [клиентской библиотеки службы хранилища для .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="005d3-136">The Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="005d3-137">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="005d3-137">About this tutorial</span></span>
<span data-ttu-id="005d3-138">Это руководство предназначено для разработчиков, которые уже работали с пакетом SDK для Хранилища таблиц Azure и хотели бы использовать функции уровня "Премиум", доступные в базе данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="005d3-138">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="005d3-139">Оно основано на сведениях из статьи [Приступая к работе с хранилищем таблиц Azure с помощью .NET](table-storage-how-to-use-dotnet.md) и содержит информацию о том, как воспользоваться преимуществами дополнительных возможностей, таких как вторичное индексирование, подготовка пропускной способности и множественная адресация.</span><span class="sxs-lookup"><span data-stu-id="005d3-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="005d3-140">Мы рассмотрим, как создать учетную запись базы данных Azure Cosmos DB, а затем создать и развернуть приложение "Таблица" на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="005d3-140">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="005d3-141">В этом руководстве также представлены примеры .NET для создания и удаления таблиц, а также для вставки, обновления, удаления и запроса данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="005d3-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="005d3-142">Если вы еще не установили Visual Studio 2017, вы можете скачать и использовать **бесплатный** [выпуск Visual Studio Community 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="005d3-142">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="005d3-143">При установке Visual Studio необходимо включить возможность **разработки для Azure**.</span><span class="sxs-lookup"><span data-stu-id="005d3-143">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="005d3-144">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="005d3-144">Create a database account</span></span>

<span data-ttu-id="005d3-145">Сначала создадим учетную запись базы данных Azure Cosmos DB на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="005d3-145">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="005d3-146">Уже есть учетная запись Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="005d3-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="005d3-147">перейдите к [настройке решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="005d3-147">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="005d3-148">У вас была учетная запись Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="005d3-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="005d3-149">Если да, ваша учетная запись теперь является учетной записью Azure Cosmos DB, поэтому вы можете сразу перейти к [настройке решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="005d3-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="005d3-150">Если вы используете эмулятор Azure Cosmos DB, выполните действия, описанные в статье об [эмуляторе Azure Cosmos DB](local-emulator.md), чтобы настроить эмулятор и сразу перейти к [настройке решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="005d3-150">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting to any location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="005d3-151">Клонирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="005d3-151">Clone the sample application</span></span>

<span data-ttu-id="005d3-152">Теперь необходимо клонировать приложение "Таблица" из GitHub. Задайте строку подключения и выполните ее.</span><span class="sxs-lookup"><span data-stu-id="005d3-152">Now let's clone a Table app from github, set the connection string, and run it.</span></span>

1. <span data-ttu-id="005d3-153">Откройте окно терминала Git, например Git Bash, и выполните команду `cd`, чтобы перейти в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="005d3-153">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="005d3-154">Выполните команду ниже, чтобы клонировать репозиторий с примером.</span><span class="sxs-lookup"><span data-stu-id="005d3-154">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="005d3-155">Затем откройте файл решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="005d3-155">Then open the solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="005d3-156">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="005d3-156">Update your connection string</span></span>

<span data-ttu-id="005d3-157">Теперь вернитесь на портал Azure, чтобы получить данные строки подключения. Скопируйте эти данные в приложение.</span><span class="sxs-lookup"><span data-stu-id="005d3-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="005d3-158">На [портале Azure](http://portal.azure.com/) перейдите к учетной записи базы данных Azure Cosmos DB и на левой панели навигации щелкните **Ключи**, а затем выберите **Ключи записи-чтения**.</span><span class="sxs-lookup"><span data-stu-id="005d3-158">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="005d3-159">На следующем шаге используйте кнопку копирования в правой части экрана, чтобы скопировать строку подключения в файл app.config.</span><span class="sxs-lookup"><span data-stu-id="005d3-159">You'll use the copy buttons on the right side of the screen to copy the connection string into the app.config file in the next step.</span></span>

2. <span data-ttu-id="005d3-160">В Visual Studio откройте файл app.config.</span><span class="sxs-lookup"><span data-stu-id="005d3-160">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="005d3-161">Скопируйте значение универсального кода ресурса (URI) на портале (с помощью кнопки копирования) и добавьте его в качестве значения параметра account-key в файле app.config. В файле app.config в качестве значения параметра account-name задайте имя созданной ранее учетной записи.</span><span class="sxs-lookup"><span data-stu-id="005d3-161">Copy your URI value from the portal (using the copy button) and make it the value of the account-key in app.config. Use the account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="005d3-162">Чтобы использовать это приложение с Хранилищем таблиц Azure класса "Стандартный", необходимо изменить строку подключения в файле `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="005d3-162">To use this app with standard Azure Table Storage, you need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="005d3-163">В качестве значения параметра AccountName используйте имя учетной записи таблицы, а в качестве параметра AccountKey — первичный ключ службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="005d3-163">Use the account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="005d3-164">Создание и развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="005d3-164">Build and deploy the app</span></span>
1. <span data-ttu-id="005d3-165">В Visual Studio в **обозревателе решений** щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="005d3-165">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="005d3-166">В поле **Обзор** введите ***WindowsAzure.Storage-PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="005d3-166">In the NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="005d3-167">Установите флажок **Включить предварительные выпуски**.</span><span class="sxs-lookup"><span data-stu-id="005d3-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="005d3-168">В результатах поиска найдите **WindowsAzure.Storage-PremiumTable** и установите ее. Затем выберите предварительную сборку `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="005d3-168">From the results, install the **WindowsAzure.Storage-PremiumTable** and choose the preview build `0.0.1-preview`.</span></span> <span data-ttu-id="005d3-169">После этого начнется установка пакета Хранилища таблиц Azure и всех зависимостей.</span><span class="sxs-lookup"><span data-stu-id="005d3-169">This action installs the Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="005d3-170">Нажмите клавиши CTRL+F5 для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="005d3-170">Click CTRL + F5 to run the application.</span></span> 

<span data-ttu-id="005d3-171">Вернитесь в обозреватель данных, где вы можете просматривать, запрашивать и изменять данные этой таблицы, а также работать с ними.</span><span class="sxs-lookup"><span data-stu-id="005d3-171">You can now go back to Data Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="005d3-172">Чтобы использовать это приложение с эмулятором базы данных Azure Cosmos DB, необходимо просто изменить строку подключения в файле `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="005d3-172">To use this app with an Azure Cosmos DB Emulator, you just need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="005d3-173">Для эмулятора используйте указанные ниже значения.</span><span class="sxs-lookup"><span data-stu-id="005d3-173">Use the below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="005d3-174">Возможности базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="005d3-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="005d3-175">База данных Azure Cosmos DB поддерживает ряд возможностей, которые недоступны в API Хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="005d3-175">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> <span data-ttu-id="005d3-176">Эти новые возможности можно включить, используя приведенные ниже значения конфигурации `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="005d3-176">The new functionality can be enabled via the following `appSettings` configuration values.</span></span> <span data-ttu-id="005d3-177">В предварительную версию пакета SDK для службы хранилища Azure мы не включали новые подписи или перегрузки.</span><span class="sxs-lookup"><span data-stu-id="005d3-177">We did not introduce any new signatures or overloads to the preview Azure Storage SDK.</span></span> <span data-ttu-id="005d3-178">Таким образом, вы можете подключиться к таблицам класса "Стандартный" и "Премиум", а также работать с другими службами в службе хранилища Azure, такими как большие двоичные объекты и очереди.</span><span class="sxs-lookup"><span data-stu-id="005d3-178">This allows you to connect to both standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="005d3-179">Ключ</span><span class="sxs-lookup"><span data-stu-id="005d3-179">Key</span></span> | <span data-ttu-id="005d3-180">Описание</span><span class="sxs-lookup"><span data-stu-id="005d3-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="005d3-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="005d3-181">TableConnectionMode</span></span>  | <span data-ttu-id="005d3-182">База данных Azure Cosmos DB поддерживает два режима подключения.</span><span class="sxs-lookup"><span data-stu-id="005d3-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="005d3-183">В режиме `Gateway` запросы всегда направляются к шлюзу базы данных Azure Cosmos DB, а затем перенаправляются в соответствующие секции данных.</span><span class="sxs-lookup"><span data-stu-id="005d3-183">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="005d3-184">В режиме подключения `Direct` клиент получает сведения о сопоставлении таблиц с секциями, а запросы выполняются непосредственно к секциям данных.</span><span class="sxs-lookup"><span data-stu-id="005d3-184">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="005d3-185">Мы советуем использовать метод по умолчанию `Direct`.</span><span class="sxs-lookup"><span data-stu-id="005d3-185">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="005d3-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="005d3-186">TableConnectionProtocol</span></span> | <span data-ttu-id="005d3-187">База данных Azure Cosmos DB поддерживает два протокола подключения: `Https` и `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="005d3-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="005d3-188">По умолчанию используется протокол `Tcp`. Мы рекомендуем использовать его, так как он более легкий.</span><span class="sxs-lookup"><span data-stu-id="005d3-188">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="005d3-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="005d3-189">TablePreferredLocations</span></span> | <span data-ttu-id="005d3-190">Разделенный запятыми список предпочтительных расположений (множественная адресация) для операций чтения.</span><span class="sxs-lookup"><span data-stu-id="005d3-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="005d3-191">Каждую учетную запись базы данных Azure Cosmos DB можно связать з разным числом регионов (от одного до более тридцати).</span><span class="sxs-lookup"><span data-stu-id="005d3-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="005d3-192">Каждый экземпляр клиента может указать подмножество этих регионов в порядке предпочтения, чтобы обеспечить низкую задержку операций чтения.</span><span class="sxs-lookup"><span data-stu-id="005d3-192">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="005d3-193">Регионам необходимо присвоить их [отображаемые имена](https://msdn.microsoft.com/library/azure/gg441293.aspx), например `West US`.</span><span class="sxs-lookup"><span data-stu-id="005d3-193">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="005d3-194">Дополнительные сведения см. в статье [How to setup Azure Cosmos DB global distribution using the Table API](tutorial-global-distribution-table.md) (Как настроить глобальное распределение Azure Cosmos DB с помощью API таблицы).</span><span class="sxs-lookup"><span data-stu-id="005d3-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="005d3-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="005d3-195">TableConsistencyLevel</span></span> | <span data-ttu-id="005d3-196">Вы можете изменить показатели доступности, задержки и согласованности, выбрав один из пяти следующих четко определенных уровней согласованности: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` и `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="005d3-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="005d3-197">Значение по умолчанию — `Session`.</span><span class="sxs-lookup"><span data-stu-id="005d3-197">Default is `Session`.</span></span> <span data-ttu-id="005d3-198">От выбранного уровня согласованности существенно зависит производительность в конфигурациях с несколькими регионами.</span><span class="sxs-lookup"><span data-stu-id="005d3-198">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="005d3-199">Дополнительные сведения см. в статье [Настраиваемые уровни согласованности данных в DocumentDB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="005d3-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="005d3-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="005d3-200">TableThroughput</span></span> | <span data-ttu-id="005d3-201">Зарезервированная пропускная способность таблицы, выраженная в единицах запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="005d3-201">Reserved throughput for the table expressed in request units (RU) per second.</span></span> <span data-ttu-id="005d3-202">Каждая таблица может поддерживать сотни миллионов единиц запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="005d3-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="005d3-203">Дополнительные сведения см. в статье [Единицы запросов в DocumentDB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="005d3-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="005d3-204">Значение по умолчанию — `400`.</span><span class="sxs-lookup"><span data-stu-id="005d3-204">Default is `400`</span></span> |
| <span data-ttu-id="005d3-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="005d3-205">TableIndexingPolicy</span></span> | <span data-ttu-id="005d3-206">Согласованное и автоматическое вторичное индексирование всех столбцов в таблицах.</span><span class="sxs-lookup"><span data-stu-id="005d3-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="005d3-207">Строка JSON соответствует спецификации политики индексации.</span><span class="sxs-lookup"><span data-stu-id="005d3-207">JSON string conforming to the indexing policy specification.</span></span> <span data-ttu-id="005d3-208">Сведения о добавлении или удалении определенных столбцов из политики индексации см. в [этой статье](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="005d3-208">See [Indexing Policy](indexing-policies.md) to see how you can change indexing policy to include/exclude specific columns.</span></span> | <span data-ttu-id="005d3-209">Автоматическое индексирование всех свойств (хэш-индексация для строк и диапазонная индексация для чисел).</span><span class="sxs-lookup"><span data-stu-id="005d3-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="005d3-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="005d3-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="005d3-211">Задайте максимальное количество элементов, возвращаемых в запросе таблицы в рамках одного цикла обхода.</span><span class="sxs-lookup"><span data-stu-id="005d3-211">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="005d3-212">Значение по умолчанию — `-1`. Оно позволяет базе данных Azure Cosmos DB динамически определять значение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="005d3-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="005d3-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="005d3-213">TableQueryEnableScan</span></span> | <span data-ttu-id="005d3-214">Если запрос не может использовать индекс для какого-либо фильтра, все равно выполните его через сканирование.</span><span class="sxs-lookup"><span data-stu-id="005d3-214">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="005d3-215">Значение по умолчанию — `false`.</span><span class="sxs-lookup"><span data-stu-id="005d3-215">Default is `false`.</span></span>|
| <span data-ttu-id="005d3-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="005d3-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="005d3-217">Степень параллелизма для выполнения запроса между секциями.</span><span class="sxs-lookup"><span data-stu-id="005d3-217">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="005d3-218">`0` — порядковое выполнение запросов без предварительной выборки. `1` — порядковое выполнение запросов с предварительной выборкой. Более высокие значения приводят к повышению степени параллелизма.</span><span class="sxs-lookup"><span data-stu-id="005d3-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="005d3-219">Значение по умолчанию — `-1`. Оно позволяет базе данных Azure Cosmos DB динамически определять значение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="005d3-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="005d3-220">Чтобы изменить значение по умолчанию, откройте файл `app.config` в обозревателе решений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="005d3-220">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="005d3-221">Добавьте содержимое элемента `<appSettings>` , показанное ниже.</span><span class="sxs-lookup"><span data-stu-id="005d3-221">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="005d3-222">Замените `account-name` именем своей учетной записи хранения, а `account-key` — ключом доступа своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="005d3-222">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="005d3-223">Сделаем краткий обзор того, что происходит в приложении.</span><span class="sxs-lookup"><span data-stu-id="005d3-223">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="005d3-224">Откройте файл `Program.cs`, и вы увидите, что эти строки кода создают ресурсы таблиц.</span><span class="sxs-lookup"><span data-stu-id="005d3-224">Open the `Program.cs` file and you find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="005d3-225">Создание клиента таблицы</span><span class="sxs-lookup"><span data-stu-id="005d3-225">Create the table client</span></span>
<span data-ttu-id="005d3-226">Сначала необходимо инициализировать `CloudTableClient`, чтобы подключиться к учетной записи таблицы.</span><span class="sxs-lookup"><span data-stu-id="005d3-226">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="005d3-227">Инициализация клиента осуществляется на основе значений конфигурации `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel` и `TablePreferredLocations`, если они указаны в параметрах приложения.</span><span class="sxs-lookup"><span data-stu-id="005d3-227">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="005d3-228">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="005d3-228">Create a table</span></span>
<span data-ttu-id="005d3-229">Затем создайте таблицу, используя `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="005d3-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="005d3-230">Таблицы в базе данных Azure Cosmos DB можно масштабировать независимо друг от друга в контексте хранилища и пропускной способности. Служба выполняет секционирование автоматически.</span><span class="sxs-lookup"><span data-stu-id="005d3-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="005d3-231">База данных Azure Cosmos DB поддерживает таблицы с фиксированным и неограниченным размером.</span><span class="sxs-lookup"><span data-stu-id="005d3-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="005d3-232">Дополнительные сведения см. в статье [Секционирование и масштабирование в базе данных Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="005d3-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="005d3-233">Создание таблиц существенно отличается.</span><span class="sxs-lookup"><span data-stu-id="005d3-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="005d3-234">База данных Azure Cosmos DB резервирует пропускную способность, а в службе хранилища Azure к транзакциям применяется модель с оплатой по мере использования.</span><span class="sxs-lookup"><span data-stu-id="005d3-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="005d3-235">Модель резервирования имеет два основных преимущества:</span><span class="sxs-lookup"><span data-stu-id="005d3-235">The reservation model has two key benefits:</span></span>

* <span data-ttu-id="005d3-236">Пропускная способность выделяется или резервируется, поэтому вам не нужно выполнять регулирование, если частота запросов на уровне или ниже подготовленной пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="005d3-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="005d3-237">Модель резервирования дает [экономическую выгоду при наличии рабочих нагрузок с высокими требованиями к пропускной способности](key-value-store-cost.md).</span><span class="sxs-lookup"><span data-stu-id="005d3-237">The reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="005d3-238">Вы можете указать пропускную способность по умолчанию, задав параметр `TableThroughput`. Пропускная способность выражается в единицах запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="005d3-238">You can configure the default throughput by configuring the setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="005d3-239">Для считывания сущности размером 1 КБ требуется 1 единица запроса. В других операциях это значение также фиксировано и зависит от потребления ресурсов ЦП, памяти и числа операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="005d3-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="005d3-240">Дополнительные сведения о [единицах запроса в Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="005d3-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="005d3-241">Сейчас пакет SDK для Хранилища таблиц не поддерживает изменение пропускной способности, но вы можете сделать это в любое время на портале Azure или с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="005d3-241">While Table storage SDK does not currently support modifying throughput, you can change the throughput instantaneously at any time using the Azure portal or Azure CLI.</span></span>

<span data-ttu-id="005d3-242">Далее мы рассмотрим простые операции чтения и записи (CRUD) с использованием пакета SDK для Хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="005d3-242">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="005d3-243">В этом руководстве показаны такие преимущества базы данных Azure Cosmos DB, как прогнозируемые задержки операций, длительностью менее 10 секунд, и быстрое выполнение запросов.</span><span class="sxs-lookup"><span data-stu-id="005d3-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="005d3-244">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="005d3-244">Add an entity to a table</span></span>
<span data-ttu-id="005d3-245">Сущности в Хранилище таблиц Azure расширены с помощью класса `TableEntity` и должны иметь свойства `PartitionKey` и `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="005d3-245">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="005d3-246">Ниже приведен пример определения сущности клиента.</span><span class="sxs-lookup"><span data-stu-id="005d3-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="005d3-247">В приведенном ниже фрагменте кода показано, как вставить сущность с помощью пакета SDK для службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="005d3-247">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="005d3-248">База данных Azure Cosmos DB обеспечивает низкую задержку при любом масштабе и в любом регионе.</span><span class="sxs-lookup"><span data-stu-id="005d3-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="005d3-249">Эта база данных гарантирует выполнение операций записи с менее 15 мс задержки при уровне P99 и примерно 6 мс при уровне P50 для приложения, запущенного в том же расположении, что и учетная запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="005d3-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="005d3-250">Это время рассчитано с учетом того, что операции записи подтверждаются клиентом только после их синхронной репликации, надежной фиксации и индексирования всего содержимого.</span><span class="sxs-lookup"><span data-stu-id="005d3-250">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="005d3-251">API таблицы базы данных Azure Cosmos DB предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="005d3-251">The Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="005d3-252">В общедоступной версии гарантии низкой задержки на уровне P99 обеспечиваются Соглашениями об уровне обслуживания, как и для других API-интерфейсов базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="005d3-252">At general availability, the p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="005d3-253">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="005d3-253">Insert a batch of entities</span></span>
<span data-ttu-id="005d3-254">Хранилище таблиц Azure поддерживает API пакетных операций, который позволяет выполнять обновление, удаление и вставку в одной пакетной операции.</span><span class="sxs-lookup"><span data-stu-id="005d3-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same single batch operation.</span></span> <span data-ttu-id="005d3-255">В отличие от Хранилища таблиц Azure база данных Azure Cosmos DB не имеет ограничений на использование API пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="005d3-255">Azure Cosmos DB does not have some of the limitations on the batch API as Azure Table storage.</span></span> <span data-ttu-id="005d3-256">Например, в одном пакете вы можете выполнить несколько операций чтения и несколько операций записи в ту же сущность без ограничения в 100 операций на пакет.</span><span class="sxs-lookup"><span data-stu-id="005d3-256">For example, you can perform multiple reads within a batch, you can perform multiple writes to the same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="005d3-257">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="005d3-257">Retrieve a single entity</span></span>
<span data-ttu-id="005d3-258">Операции извлечения (GET) в базе данных Azure Cosmos DB выполняются с менее 10 мс задержки при уровне P99 и примерно 1 мс при уровне P50 в том же регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="005d3-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="005d3-259">Вы можете добавить в учетную запись нужное число регионов для низкой задержки операций чтения и развернуть приложения для чтения из локального региона (множественная адресация), задав параметр `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="005d3-259">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="005d3-260">Следующий фрагмент кода позволяет извлечь одну сущность:</span><span class="sxs-lookup"><span data-stu-id="005d3-260">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="005d3-261">Дополнительные сведения об API-интерфейсах множественной адресации см. в статье [How to setup Azure Cosmos DB global distribution using the Table API](tutorial-global-distribution-table.md) (Как настроить глобальное распределение Azure Cosmos DB с помощью API таблицы).</span><span class="sxs-lookup"><span data-stu-id="005d3-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="005d3-262">Запрос сущностей с использованием автоматического вторичного индексирования</span><span class="sxs-lookup"><span data-stu-id="005d3-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="005d3-263">Таблицы можно запрашивать с помощью класса `TableQuery`.</span><span class="sxs-lookup"><span data-stu-id="005d3-263">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="005d3-264">База данных Azure Cosmos DB содержит ядро СУБД, оптимизированное для операций записи, которое автоматически индексирует все столбцы в таблице.</span><span class="sxs-lookup"><span data-stu-id="005d3-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="005d3-265">Индексирование в базе данных Azure Cosmos DB не зависит от схемы.</span><span class="sxs-lookup"><span data-stu-id="005d3-265">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="005d3-266">Поэтому, даже если схема отличается между строками или меняется с течением времени, она автоматически индексируется.</span><span class="sxs-lookup"><span data-stu-id="005d3-266">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="005d3-267">Так как база данных Azure Cosmos DB поддерживает автоматическое вторичное индексирование, запросы к любому свойству могут использовать индекс и эффективно обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="005d3-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="005d3-268">В предварительной версии база данных Azure Cosmos DB поддерживает те же функции обработки запросов, что и Хранилище таблиц Azure для API таблицы.</span><span class="sxs-lookup"><span data-stu-id="005d3-268">In preview, Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="005d3-269">Кроме того, эта база данных поддерживает сортировку, выполнение статистических вычислений, геопространственные запросы, иерархию и множество встроенных функций.</span><span class="sxs-lookup"><span data-stu-id="005d3-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="005d3-270">Дополнительные возможности API таблицы будут добавлены в будущем обновлении.</span><span class="sxs-lookup"><span data-stu-id="005d3-270">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="005d3-271">Общие сведения об этих возможностях см. в статье [SQL-запросы и синтаксис SQL в DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="005d3-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="005d3-272">Замена сущности</span><span class="sxs-lookup"><span data-stu-id="005d3-272">Replace an entity</span></span>
<span data-ttu-id="005d3-273">Чтобы обновить сущность, извлеките ее из службы таблиц, измените объект сущности и сохраните изменения в службе таблиц.</span><span class="sxs-lookup"><span data-stu-id="005d3-273">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="005d3-274">Следующий код изменяет существующий номер телефона клиента.</span><span class="sxs-lookup"><span data-stu-id="005d3-274">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="005d3-275">Аналогичным образом можно выполнить операцию `InsertOrMerge` или `Merge`.</span><span class="sxs-lookup"><span data-stu-id="005d3-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="005d3-276">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="005d3-276">Delete an entity</span></span>
<span data-ttu-id="005d3-277">Сущность можно легко удалить после ее получения с использованием того же шаблона, что и для обновления сущностей.</span><span class="sxs-lookup"><span data-stu-id="005d3-277">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="005d3-278">Следующий код извлекает и удаляет сущность клиента.</span><span class="sxs-lookup"><span data-stu-id="005d3-278">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="005d3-279">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="005d3-279">Delete a table</span></span>
<span data-ttu-id="005d3-280">Наконец, следующий пример кода удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="005d3-280">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="005d3-281">Вы можете удалить и воссоздать таблицу с помощью базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="005d3-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="005d3-282">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="005d3-282">Clean up resources</span></span> 

<span data-ttu-id="005d3-283">Если вы не собираетесь использовать это приложение дальше, удалите все ресурсы, созданные в ходе работы с этим руководством, на портале Azure, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="005d3-283">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>   

1. <span data-ttu-id="005d3-284">В меню слева на портале Azure щелкните **Группы ресурсов**, а затем выберите имя созданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="005d3-284">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span>  
2. <span data-ttu-id="005d3-285">На странице группы ресурсов щелкните **Удалить**, в текстовом поле введите имя ресурса для удаления и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="005d3-285">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="005d3-286">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="005d3-286">Next steps</span></span>

<span data-ttu-id="005d3-287">В этом руководстве мы рассмотрели, как начать работу с API таблицы в базе данных Azure Cosmos DB, и сделали следующее:</span><span class="sxs-lookup"><span data-stu-id="005d3-287">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="005d3-288">создали учетную запись Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="005d3-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="005d3-289">включили возможности в файле app.config;</span><span class="sxs-lookup"><span data-stu-id="005d3-289">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="005d3-290">создали таблицу;</span><span class="sxs-lookup"><span data-stu-id="005d3-290">Created a table</span></span> 
> * <span data-ttu-id="005d3-291">добавили сущность в таблицу;</span><span class="sxs-lookup"><span data-stu-id="005d3-291">Added an entity to a table</span></span> 
> * <span data-ttu-id="005d3-292">вставили пакет сущностей;</span><span class="sxs-lookup"><span data-stu-id="005d3-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="005d3-293">извлекли одну сущность;</span><span class="sxs-lookup"><span data-stu-id="005d3-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="005d3-294">запросили сущности в процессе автоматического вторичного индексирования;</span><span class="sxs-lookup"><span data-stu-id="005d3-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="005d3-295">заменили сущность;</span><span class="sxs-lookup"><span data-stu-id="005d3-295">Replaced an entity</span></span> 
> * <span data-ttu-id="005d3-296">удалили сущность;</span><span class="sxs-lookup"><span data-stu-id="005d3-296">Deleted an entity</span></span> 
> * <span data-ttu-id="005d3-297">удалили таблицу.</span><span class="sxs-lookup"><span data-stu-id="005d3-297">Deleted a table</span></span>  

<span data-ttu-id="005d3-298">Теперь вы можете перейти к следующему руководству и более детально рассмотреть запрос данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="005d3-298">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="005d3-299">Запрос данных с помощью API таблицы</span><span class="sxs-lookup"><span data-stu-id="005d3-299">Query with the Table API</span></span>](tutorial-query-table.md)
