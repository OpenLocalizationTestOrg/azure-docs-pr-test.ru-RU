---
title: "Azure Cosmos DB: Разработку с использованием hello API таблиц в .NET | Документы Microsoft"
description: "Узнайте, как toodevelop с API Azure Cosmos DB таблицы, с помощью .NET"
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
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="19e71-103">Azure Cosmos DB: Разработку с использованием hello API таблиц в .NET</span><span class="sxs-lookup"><span data-stu-id="19e71-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="19e71-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="19e71-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="19e71-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="19e71-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="19e71-106">В этом учебнике hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="19e71-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="19e71-107">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="19e71-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="19e71-108">Включить функции в файле app.config hello</span><span class="sxs-lookup"><span data-stu-id="19e71-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="19e71-109">Создание таблицы с помощью hello [API таблиц](table-introduction.md) (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="19e71-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="19e71-110">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="19e71-111">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="19e71-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="19e71-112">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="19e71-113">запрос сущностей с использованием автоматического вторичного индексирования;</span><span class="sxs-lookup"><span data-stu-id="19e71-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="19e71-114">Замена сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-114">Replace an entity</span></span> 
> * <span data-ttu-id="19e71-115">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-115">Delete an entity</span></span> 
> * <span data-ttu-id="19e71-116">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="19e71-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="19e71-117">Таблицы в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="19e71-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="19e71-118">Azure Cosmos DB предоставляет hello [API таблиц](table-introduction.md) (Предварительный просмотр) для приложений, требующих хранилищу ключей и значений с помощью конструктора без схемы.</span><span class="sxs-lookup"><span data-stu-id="19e71-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="19e71-119">[Хранилище таблиц Azure](../storage/common/storage-introduction.md) пакеты SDK и API-интерфейс REST может быть используется toowork с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="19e71-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="19e71-120">Можно использовать таблицы Azure Cosmos DB toocreate с высокой пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="19e71-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="19e71-121">Кроме того, она поддерживает оптимизированные для пропускной способности таблицы, которые неофициально называются таблицами класса "Премиум" и сейчас доступны в общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="19e71-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="19e71-122">Вы можете продолжить toouse хранилища Azure Table для таблиц с высокой хранилища и более низкие требования к пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="19e71-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="19e71-123">Azure Cosmos DB будет внедрить поддержку в будущем обновлении таблицами, оптимизированными для хранения данных и существующих и новых таблиц Azure, учетные записи хранения будут легко обновляется tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="19e71-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="19e71-124">При использовании хранилища таблиц Azure в настоящее время можно получить следующие преимущества со Предварительный просмотр «premium таблицы» hello hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="19e71-125">поддержка готового к использованию [глобального распределения](distribute-data-globally.md) со множественной адресацией, а также с [ручной и автоматической отработкой отказа](regional-failover.md);</span><span class="sxs-lookup"><span data-stu-id="19e71-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="19e71-126">поддержка автоматического схемонезависимого индексирования данных для всех свойств ("вторичные индексы") и быстрого выполнения запросов;</span><span class="sxs-lookup"><span data-stu-id="19e71-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="19e71-127">поддержка [независимого масштабирования хранилища и пропускной способности](partition-data.md) в любом количестве регионов;</span><span class="sxs-lookup"><span data-stu-id="19e71-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="19e71-128">Поддержка [выделенной пропускной способности на таблицу](request-units.md) может масштабироваться от сотен toomillions запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="19e71-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="19e71-129">Поддержка [пять уровней пройтись согласованности](consistency-levels.md) tootrade выключения доступность, задержка и согласованности в зависимости от потребностей приложения</span><span class="sxs-lookup"><span data-stu-id="19e71-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="19e71-130">99,99% доступности в пределах одного региона и возможность tooadd дополнительные области для повышения доступности и [отрасли комплексное соглашений об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/cosmos-db/) на общей доступности</span><span class="sxs-lookup"><span data-stu-id="19e71-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="19e71-131">Работа с hello существующего хранилища Azure .NET SDK и ни одно приложение tooyour изменения кода</span><span class="sxs-lookup"><span data-stu-id="19e71-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="19e71-132">Во время предварительного просмотра hello Azure Cosmos DB поддерживает hello таблицы API, с помощью hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="19e71-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="19e71-133">Вы можете загрузить hello [предварительной версии хранилища Azure SDK](https://aka.ms/premiumtablenuget) из NuGet, который имеет hello же классах и подписях методов как hello [пакет SDK хранилища Azure](https://www.nuget.org/packages/WindowsAzure.Storage), но также можно подключить Cosmos DB tooAzure учетные записи, используя hello Таблица API.</span><span class="sxs-lookup"><span data-stu-id="19e71-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="19e71-134">toolearn Дополнительные сведения о сложных задач хранилища таблиц Azure, см.:</span><span class="sxs-lookup"><span data-stu-id="19e71-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="19e71-135">Введение tooAzure Cosmos DB: API таблиц</span><span class="sxs-lookup"><span data-stu-id="19e71-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="19e71-136">Здравствуйте, таблица службы справочной документации для получения подробной информации о доступных API-интерфейсы [клиентская библиотека хранилища для Справочник по .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="19e71-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="19e71-137">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="19e71-137">About this tutorial</span></span>
<span data-ttu-id="19e71-138">Этот учебник для разработчиков, знакомых с hello пакета SDK службы хранилища таблиц Azure и хотел toouse hello расширенные функции доступны использует базу данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="19e71-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="19e71-139">Он основан на [Приступая к работе с хранилищем таблиц Azure, с помощью .NET](table-storage-how-to-use-dotnet.md) и показано, как tootake преимущества дополнительных возможностей, таких как вторичные индексы, пропускная способность и многоадресными.</span><span class="sxs-lookup"><span data-stu-id="19e71-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="19e71-140">Мы рассмотрим, как toouse hello Azure toocreate портала учетной записи Azure Cosmos DB и затем постройте и разверните приложение таблицы.</span><span class="sxs-lookup"><span data-stu-id="19e71-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="19e71-141">В этом руководстве также представлены примеры .NET для создания и удаления таблиц, а также для вставки, обновления, удаления и запроса данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="19e71-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="19e71-142">Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="19e71-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="19e71-143">Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="19e71-144">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="19e71-144">Create a database account</span></span>

<span data-ttu-id="19e71-145">Давайте начнем с создания учетной записи Azure Cosmos DB в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="19e71-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="19e71-146">Уже есть учетная запись Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="19e71-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="19e71-147">Если Да, пропустить слишком[Настройка решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="19e71-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="19e71-148">У вас была учетная запись Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="19e71-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="19e71-149">Если таким образом, учетной записи теперь учетную запись Azure Cosmos DB и можно сразу перейти слишком[Настройка решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="19e71-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="19e71-150">Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить решение Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="19e71-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="19e71-151">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="19e71-151">Clone hello sample application</span></span>

<span data-ttu-id="19e71-152">Теперь давайте клонировать приложении таблицы из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="19e71-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="19e71-153">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="19e71-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="19e71-154">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="19e71-155">Затем откройте файл решения hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19e71-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="19e71-156">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="19e71-156">Update your connection string</span></span>

<span data-ttu-id="19e71-157">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="19e71-158">В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**.</span><span class="sxs-lookup"><span data-stu-id="19e71-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="19e71-159">Вы используете кнопки копия hello hello правой части экрана toocopy hello hello-строка подключения в файл app.config hello в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="19e71-160">В Visual Studio откройте файл app.config hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="19e71-161">Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение hello ключа учетной записи-в файле app.config. Используйте имя учетной записи hello, созданного ранее для имени учетной записи в файл app.config.</span><span class="sxs-lookup"><span data-stu-id="19e71-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="19e71-162">toouse приложение, используя стандартные табличного хранилища Azure, требуется строка подключения toochange hello в `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="19e71-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="19e71-163">Имя учетной записи используйте hello как имя учетной записи таблицы и ключ как хранилище Azure в первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="19e71-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="19e71-164">Построение и развертывание приложения hello</span><span class="sxs-lookup"><span data-stu-id="19e71-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="19e71-165">В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="19e71-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="19e71-166">В hello NuGet **Обзор** введите ***WindowsAzure.Storage PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="19e71-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="19e71-167">Установите флажок **Включить предварительные выпуски**.</span><span class="sxs-lookup"><span data-stu-id="19e71-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="19e71-168">На основе результатов hello установить hello **WindowsAzure.Storage PremiumTable** и выберите "сборка" Предварительный просмотр hello `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="19e71-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="19e71-169">Это действие устанавливает пакет хранилища таблиц Azure hello и все зависимости.</span><span class="sxs-lookup"><span data-stu-id="19e71-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="19e71-170">Нажмите сочетание клавиш CTRL + F5 toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="19e71-171">Теперь можно вернуться tooData обозревателя и разделе запроса, изменения и работать с данными таблицы.</span><span class="sxs-lookup"><span data-stu-id="19e71-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="19e71-172">toouse это приложение с эмулятором DB Cosmos Azure, вы просто требуется строка подключения toochange hello в `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="19e71-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="19e71-173">Используйте hello ниже значения для эмулятора.</span><span class="sxs-lookup"><span data-stu-id="19e71-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="19e71-174">Возможности базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="19e71-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="19e71-175">Azure Cosmos DB поддерживает ряд возможностей, которые не доступны в API-Интерфейс хранилища Azure Table hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="19e71-176">Hello новые функциональные возможности можно включить, используя следующие hello `appSettings` значения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="19e71-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="19e71-177">Не удалось ввести любые новые подписи или перегрузки toohello просмотра пакет SDK хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="19e71-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="19e71-178">Это позволяет tooconnect tooboth standard и premium таблиц и работа с другими службами хранилища Azure, такими как большие двоичные объекты и очереди.</span><span class="sxs-lookup"><span data-stu-id="19e71-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="19e71-179">Ключ</span><span class="sxs-lookup"><span data-stu-id="19e71-179">Key</span></span> | <span data-ttu-id="19e71-180">Описание</span><span class="sxs-lookup"><span data-stu-id="19e71-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19e71-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="19e71-181">TableConnectionMode</span></span>  | <span data-ttu-id="19e71-182">База данных Azure Cosmos DB поддерживает два режима подключения.</span><span class="sxs-lookup"><span data-stu-id="19e71-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="19e71-183">В `Gateway` режиме, запросы всегда осуществляются toohello Azure Cosmos DB шлюз, который перенаправляет его toohello соответствующие секции данных.</span><span class="sxs-lookup"><span data-stu-id="19e71-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="19e71-184">В `Direct` режим подключения hello клиент выберет hello сопоставление toopartitions таблиц и запросов, выполненных непосредственно для секции данных.</span><span class="sxs-lookup"><span data-stu-id="19e71-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="19e71-185">Мы рекомендуем `Direct`, по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="19e71-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="19e71-186">TableConnectionProtocol</span></span> | <span data-ttu-id="19e71-187">База данных Azure Cosmos DB поддерживает два протокола подключения: `Https` и `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="19e71-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="19e71-188">`Tcp`по умолчанию hello и рекомендуется, так как он является облегченной.</span><span class="sxs-lookup"><span data-stu-id="19e71-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="19e71-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="19e71-189">TablePreferredLocations</span></span> | <span data-ttu-id="19e71-190">Разделенный запятыми список предпочтительных расположений (множественная адресация) для операций чтения.</span><span class="sxs-lookup"><span data-stu-id="19e71-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="19e71-191">Каждую учетную запись базы данных Azure Cosmos DB можно связать з разным числом регионов (от одного до более тридцати).</span><span class="sxs-lookup"><span data-stu-id="19e71-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="19e71-192">Каждый экземпляр клиента можно указать подмножество этих областей в порядке hello предпочтительный для операций чтения с небольшой задержкой.</span><span class="sxs-lookup"><span data-stu-id="19e71-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="19e71-193">Hello областей должны иметь имена с помощью их [отображаемые имена](https://msdn.microsoft.com/library/azure/gg441293.aspx), например `West US`.</span><span class="sxs-lookup"><span data-stu-id="19e71-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="19e71-194">Дополнительные сведения см. в статье [How to setup Azure Cosmos DB global distribution using the Table API](tutorial-global-distribution-table.md) (Как настроить глобальное распределение Azure Cosmos DB с помощью API таблицы).</span><span class="sxs-lookup"><span data-stu-id="19e71-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="19e71-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="19e71-195">TableConsistencyLevel</span></span> | <span data-ttu-id="19e71-196">Вы можете изменить показатели доступности, задержки и согласованности, выбрав один из пяти следующих четко определенных уровней согласованности: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` и `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="19e71-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="19e71-197">Значение по умолчанию — `Session`.</span><span class="sxs-lookup"><span data-stu-id="19e71-197">Default is `Session`.</span></span> <span data-ttu-id="19e71-198">Выбор уровня согласованности Hello оказывает влияние значительного увеличения производительности в нескольких регионах настроек.</span><span class="sxs-lookup"><span data-stu-id="19e71-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="19e71-199">Дополнительные сведения см. в статье [Настраиваемые уровни согласованности данных в DocumentDB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="19e71-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="19e71-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="19e71-200">TableThroughput</span></span> | <span data-ttu-id="19e71-201">Зарезервированную полосу пропускания для таблицы hello, выраженный в единицах запроса (RU) в секунду.</span><span class="sxs-lookup"><span data-stu-id="19e71-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="19e71-202">Каждая таблица может поддерживать сотни миллионов единиц запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="19e71-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="19e71-203">Дополнительные сведения см. в статье [Единицы запросов в DocumentDB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="19e71-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="19e71-204">Значение по умолчанию — `400`.</span><span class="sxs-lookup"><span data-stu-id="19e71-204">Default is `400`</span></span> |
| <span data-ttu-id="19e71-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="19e71-205">TableIndexingPolicy</span></span> | <span data-ttu-id="19e71-206">Согласованное и автоматическое вторичное индексирование всех столбцов в таблицах.</span><span class="sxs-lookup"><span data-stu-id="19e71-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="19e71-207">JSON строки соответствующих toohello спецификация политики индексирования.</span><span class="sxs-lookup"><span data-stu-id="19e71-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="19e71-208">В разделе [политики индексирования](indexing-policies.md) toosee изменение индексирования политики tooinclude и исключения определенных столбцов.</span><span class="sxs-lookup"><span data-stu-id="19e71-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="19e71-209">Автоматическое индексирование всех свойств (хэш-индексация для строк и диапазонная индексация для чисел).</span><span class="sxs-lookup"><span data-stu-id="19e71-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="19e71-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="19e71-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="19e71-211">Настройте hello максимальное количество возвращаемых элементов для запроса таблицы в рамках одного цикла обработки.</span><span class="sxs-lookup"><span data-stu-id="19e71-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="19e71-212">Значение по умолчанию — `-1`, что позволяет динамически определять значение hello во время выполнения DB Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="19e71-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="19e71-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="19e71-213">TableQueryEnableScan</span></span> | <span data-ttu-id="19e71-214">Если запрос hello невозможно использовать индекс hello любой фильтр, запустите его все равно посредством проверки.</span><span class="sxs-lookup"><span data-stu-id="19e71-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="19e71-215">Значение по умолчанию — `false`.</span><span class="sxs-lookup"><span data-stu-id="19e71-215">Default is `false`.</span></span>|
| <span data-ttu-id="19e71-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="19e71-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="19e71-217">степень параллелизма для выполнения запроса между разделами Hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="19e71-218">`0`не выполняется параллельно с без предварительной загрузки, `1` последовательный с предварительное и выше значениями hello коэффициент увеличения параллелизма.</span><span class="sxs-lookup"><span data-stu-id="19e71-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="19e71-219">Значение по умолчанию — `-1`, что позволяет динамически определять значение hello во время выполнения DB Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="19e71-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="19e71-220">значение по умолчанию hello toochange, откройте hello `app.config` файл из обозревателя решений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19e71-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="19e71-221">Добавить содержимое hello hello `<appSettings>` элемент, показанный ниже.</span><span class="sxs-lookup"><span data-stu-id="19e71-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="19e71-222">Замените `account-name` с именем hello вашей учетной записи хранилища и `account-key` с помощью ключа доступа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="19e71-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="19e71-223">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="19e71-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="19e71-224">Откройте hello `Program.cs` файла и найдите следующие строки кода создать hello ресурсами таблиц.</span><span class="sxs-lookup"><span data-stu-id="19e71-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="19e71-225">Создание клиента hello таблиц</span><span class="sxs-lookup"><span data-stu-id="19e71-225">Create hello table client</span></span>
<span data-ttu-id="19e71-226">Можно инициализировать `CloudTableClient` tooconnect toohello таблицы, учетной записи.</span><span class="sxs-lookup"><span data-stu-id="19e71-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="19e71-227">Этот клиент инициализируется с помощью hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, и `TablePreferredLocations` значений конфигурации, если указан в параметрах приложения hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="19e71-228">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="19e71-228">Create a table</span></span>
<span data-ttu-id="19e71-229">Затем создайте таблицу, используя `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="19e71-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="19e71-230">Таблицы в базе данных Azure Cosmos можно масштабировать независимо друг от друга с точки зрения хранилища и пропускной способности и секционирование обрабатывается автоматически службой hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="19e71-231">База данных Azure Cosmos DB поддерживает таблицы с фиксированным и неограниченным размером.</span><span class="sxs-lookup"><span data-stu-id="19e71-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="19e71-232">Дополнительные сведения см. в статье [Секционирование и масштабирование в базе данных Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="19e71-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="19e71-233">Создание таблиц существенно отличается.</span><span class="sxs-lookup"><span data-stu-id="19e71-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="19e71-234">База данных Azure Cosmos DB резервирует пропускную способность, а в службе хранилища Azure к транзакциям применяется модель с оплатой по мере использования.</span><span class="sxs-lookup"><span data-stu-id="19e71-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="19e71-235">Hello резервирования модель имеет два основных преимущества:</span><span class="sxs-lookup"><span data-stu-id="19e71-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="19e71-236">Пропускная способность выделяется или резервируется, поэтому вам не нужно выполнять регулирование, если частота запросов на уровне или ниже подготовленной пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="19e71-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="19e71-237">Дополнительные модели резервирования Hello [экономически эффективные для нагрузок пропускной способности](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="19e71-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="19e71-238">Можно настроить пропускную способность по умолчанию hello, настроив параметр hello для `TableThroughput` с точки зрения RU (запроса ед.) в секунду.</span><span class="sxs-lookup"><span data-stu-id="19e71-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="19e71-239">Чтение сущности 1 КБ нормализуется как 1 RU и других операций, нормализованное tooa фиксированное значение единиц Запросов в зависимости от их потребления ЦП, памяти и операций ввода-ВЫВОДА.</span><span class="sxs-lookup"><span data-stu-id="19e71-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="19e71-240">Дополнительные сведения о [единицах запроса в Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="19e71-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="19e71-241">Хранилище таблиц SDK в настоящее время не поддерживает изменение пропускной способности, можно изменить пропускной способности hello мгновенно в любой момент, с помощью hello портал Azure или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="19e71-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="19e71-242">Далее мы Пройдите hello простой чтения и записи (CRUD) с помощью пакета SDK службы хранилища Azure Table hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="19e71-243">В этом руководстве показаны такие преимущества базы данных Azure Cosmos DB, как прогнозируемые задержки операций, длительностью менее 10 секунд, и быстрое выполнение запросов.</span><span class="sxs-lookup"><span data-stu-id="19e71-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="19e71-244">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-244">Add an entity tooa table</span></span>
<span data-ttu-id="19e71-245">Сущности в хранилище таблиц Azure расширять hello `TableEntity` класса и должен иметь `PartitionKey` и `RowKey` свойства.</span><span class="sxs-lookup"><span data-stu-id="19e71-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="19e71-246">Ниже приведен пример определения сущности клиента.</span><span class="sxs-lookup"><span data-stu-id="19e71-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="19e71-247">Hello, следующий фрагмент кода показывает, как tooinsert сущность с hello хранилища Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="19e71-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="19e71-248">Azure Cosmos DB предназначен для высокоскоростной любых объемов гарантированный Здравствуй, мир!.</span><span class="sxs-lookup"><span data-stu-id="19e71-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="19e71-249">Завершить запись < 15 мс на p99 и ms ~ 6 на p50 для приложений, работающих hello же регионе, что учетная запись Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="19e71-250">И это время учетные записи для hello фактов, которая записывает подтверждения задней toohello клиента только после их синхронно реплицируются, надежно зафиксированы, и индексируется все содержимое.</span><span class="sxs-lookup"><span data-stu-id="19e71-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="19e71-251">Hello API таблиц для Azure Cosmos DB находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="19e71-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="19e71-252">На этапе общей доступности hello p99 задержки гарантии, поддерживаемых соглашений об уровне обслуживания, как и другие API-интерфейсы DB Cosmos для Azure.</span><span class="sxs-lookup"><span data-stu-id="19e71-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="19e71-253">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="19e71-253">Insert a batch of entities</span></span>
<span data-ttu-id="19e71-254">Azure табличного хранилища поддерживаются пакетной операции API, позволяющий объединить обновления, удаления и вставки в hello одной операции в одном пакете.</span><span class="sxs-lookup"><span data-stu-id="19e71-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="19e71-255">Azure Cosmos DB имеет некоторые ограничения hello на API пакета hello как хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="19e71-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="19e71-256">Например, можно выполнять несколько операций чтения в пакете, можно выполнять несколько операций записи toohello одной сущности в пакете, и нет ограничений на 100 операций в пакете.</span><span class="sxs-lookup"><span data-stu-id="19e71-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="19e71-257">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-257">Retrieve a single entity</span></span>
<span data-ttu-id="19e71-258">Извлекает (получает) в Azure Cosmos DB полный < 10 мс на p99 и около 1 мс на p50 в hello же регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="19e71-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="19e71-259">Можно добавить столько tooyour областей учетной записи для операций чтения с небольшой задержкой, а также развернуть tooread приложений из своей локальной области («многосетевой»), задав `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="19e71-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="19e71-260">Можно получить единственную сущность, используя следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="19e71-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="19e71-261">Дополнительные сведения об API-интерфейсах множественной адресации см. в статье [How to setup Azure Cosmos DB global distribution using the Table API](tutorial-global-distribution-table.md) (Как настроить глобальное распределение Azure Cosmos DB с помощью API таблицы).</span><span class="sxs-lookup"><span data-stu-id="19e71-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="19e71-262">Запрос сущностей с использованием автоматического вторичного индексирования</span><span class="sxs-lookup"><span data-stu-id="19e71-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="19e71-263">Таблицы можно выполнять запросы hello `TableQuery` класса.</span><span class="sxs-lookup"><span data-stu-id="19e71-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="19e71-264">База данных Azure Cosmos DB содержит ядро СУБД, оптимизированное для операций записи, которое автоматически индексирует все столбцы в таблице.</span><span class="sxs-lookup"><span data-stu-id="19e71-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="19e71-265">Индексирование в базе данных Azure Cosmos — независимые tooschema.</span><span class="sxs-lookup"><span data-stu-id="19e71-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="19e71-266">Таким образом даже если схема различны строк или со временем развивается hello схемы, он автоматически индексируется.</span><span class="sxs-lookup"><span data-stu-id="19e71-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="19e71-267">Поскольку Azure Cosmos DB поддерживает автоматическое вторичные индексы, запросы к любому свойству можно использовать индекс hello и эффективно обслуживать.</span><span class="sxs-lookup"><span data-stu-id="19e71-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

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

<span data-ttu-id="19e71-268">Во время предварительного просмотра Azure Cosmos DB поддерживает hello же запрос, функциональные возможности, что хранилище таблиц Azure для hello API таблиц.</span><span class="sxs-lookup"><span data-stu-id="19e71-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="19e71-269">Кроме того, эта база данных поддерживает сортировку, выполнение статистических вычислений, геопространственные запросы, иерархию и множество встроенных функций.</span><span class="sxs-lookup"><span data-stu-id="19e71-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="19e71-270">Дополнительные функциональные возможности Hello будет предоставляться в hello таблицы API в будущих версиях.</span><span class="sxs-lookup"><span data-stu-id="19e71-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="19e71-271">Общие сведения об этих возможностях см. в статье [SQL-запросы и синтаксис SQL в DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="19e71-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="19e71-272">Замена сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-272">Replace an entity</span></span>
<span data-ttu-id="19e71-273">tooupdate сущности, получить его из службы таблиц hello, изменить объект сущности hello и сохранять изменения hello обратно toohello службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="19e71-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="19e71-274">Hello следующий код позволяет изменить номер телефона существующего клиента.</span><span class="sxs-lookup"><span data-stu-id="19e71-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="19e71-275">Аналогичным образом можно выполнить операцию `InsertOrMerge` или `Merge`.</span><span class="sxs-lookup"><span data-stu-id="19e71-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="19e71-276">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-276">Delete an entity</span></span>
<span data-ttu-id="19e71-277">Можно легко удалить сущность, после его получения с помощью hello же шаблон, показанный для обновления сущности.</span><span class="sxs-lookup"><span data-stu-id="19e71-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="19e71-278">Привет, следующий код извлекает и удаляет сущность «клиент».</span><span class="sxs-lookup"><span data-stu-id="19e71-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="19e71-279">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="19e71-279">Delete a table</span></span>
<span data-ttu-id="19e71-280">Наконец hello, следующий пример кода удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="19e71-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="19e71-281">Вы можете удалить и воссоздать таблицу с помощью базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="19e71-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="19e71-282">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="19e71-282">Clean up resources</span></span> 

<span data-ttu-id="19e71-283">Если вы не будете toocontinue toouse это приложение, используйте следующие шаги toodelete все ресурсы, созданные этого учебника в hello портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="19e71-284">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="19e71-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="19e71-285">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="19e71-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="19e71-286">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19e71-286">Next steps</span></span>

<span data-ttu-id="19e71-287">В этом учебнике мы узнали, как tooget работы с Azure Cosmos DB на hello API таблиц и вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="19e71-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="19e71-288">создали учетную запись Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="19e71-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="19e71-289">Функциональность включена в файле app.config hello</span><span class="sxs-lookup"><span data-stu-id="19e71-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="19e71-290">создали таблицу;</span><span class="sxs-lookup"><span data-stu-id="19e71-290">Created a table</span></span> 
> * <span data-ttu-id="19e71-291">Добавлена таблица tooa сущности</span><span class="sxs-lookup"><span data-stu-id="19e71-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="19e71-292">вставили пакет сущностей;</span><span class="sxs-lookup"><span data-stu-id="19e71-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="19e71-293">извлекли одну сущность;</span><span class="sxs-lookup"><span data-stu-id="19e71-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="19e71-294">запросили сущности в процессе автоматического вторичного индексирования;</span><span class="sxs-lookup"><span data-stu-id="19e71-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="19e71-295">заменили сущность;</span><span class="sxs-lookup"><span data-stu-id="19e71-295">Replaced an entity</span></span> 
> * <span data-ttu-id="19e71-296">удалили сущность;</span><span class="sxs-lookup"><span data-stu-id="19e71-296">Deleted an entity</span></span> 
> * <span data-ttu-id="19e71-297">удалили таблицу.</span><span class="sxs-lookup"><span data-stu-id="19e71-297">Deleted a table</span></span>  

<span data-ttu-id="19e71-298">Теперь можно выполнить следующее руководство toohello и Дополнительные сведения о запросах к таблице данных.</span><span class="sxs-lookup"><span data-stu-id="19e71-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="19e71-299">Запрос с hello API таблиц</span><span class="sxs-lookup"><span data-stu-id="19e71-299">Query with hello Table API</span></span>](tutorial-query-table.md)
