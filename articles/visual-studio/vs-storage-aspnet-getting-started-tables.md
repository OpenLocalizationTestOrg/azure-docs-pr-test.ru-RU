---
title: "aaaGet к работе с хранилищем таблиц Azure и Visual Studio подключения службы (ASP.NET) | Документы Microsoft"
description: "Как tooget запущена с помощью табличного хранилища Azure в проект ASP.NET в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraigb
ms.openlocfilehash: 04f79db7aad60ca51c3c866da1f4b01d9e11ac52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="476ae-103">Начало работы с хранилищем таблиц Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="476ae-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="476ae-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="476ae-104">Overview</span></span>

<span data-ttu-id="476ae-105">Хранилище таблиц Azure позволяет toostore больших объемов структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="476ae-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="476ae-106">Hello служба находится в хранилище данных NoSQL, принимающий вызовам c аутентификацией внутри и вне hello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="476ae-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="476ae-107">Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="476ae-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="476ae-108">В этом учебнике показано, как toowrite ASP.NET кода в некоторых распространенных сценариях, использование сущностей в хранилище таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="476ae-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="476ae-109">К этим сценариям относится создание таблицы, а также добавление, запрос и удаление сущностей таблиц.</span><span class="sxs-lookup"><span data-stu-id="476ae-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="476ae-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="476ae-110">Prerequisites</span></span>

* [<span data-ttu-id="476ae-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="476ae-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="476ae-112">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="476ae-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="476ae-113">Создание контроллера MVC</span><span class="sxs-lookup"><span data-stu-id="476ae-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="476ae-114">В hello **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров**и в контекстном меню hello, выберите **Добавить -> контроллер**.</span><span class="sxs-lookup"><span data-stu-id="476ae-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Добавление контроллера tooan приложение ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="476ae-116">На hello **Добавление формирования шаблонов** диалогового окна выберите **контроллер MVC 5 - пустой**и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="476ae-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Выбор типа контроллера MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="476ae-118">На hello **добавления контроллера** диалогового окна, имя контроллера hello *TablesController*и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="476ae-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Имя контроллера MVC hello](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="476ae-120">Добавьте следующее hello *с помощью* toohello директивы `TablesController.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="476ae-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="476ae-121">Создание класса модели</span><span class="sxs-lookup"><span data-stu-id="476ae-121">Create a model class</span></span>

<span data-ttu-id="476ae-122">Многие примеры hello в этой статье используется **TableEntity**-производный класс с именем **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="476ae-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="476ae-123">следующие шаги Hello проводит пользователя через объявление этот класс как класс модели:</span><span class="sxs-lookup"><span data-stu-id="476ae-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="476ae-124">В hello **обозревателе решений**, щелкните правой кнопкой мыши **моделей**и в контекстном меню hello, выберите **Добавить -> класс**.</span><span class="sxs-lookup"><span data-stu-id="476ae-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="476ae-125">На hello **Добавление нового элемента** диалогового окна, имя класса hello, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="476ae-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="476ae-126">Откройте hello `CustomerEntity.cs` файл и добавьте следующее hello **с помощью** директиву:</span><span class="sxs-lookup"><span data-stu-id="476ae-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="476ae-127">Измените класс hello, таким образом, чтобы по завершении hello класс объявляется как hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="476ae-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="476ae-128">Класс Hello объявляет класс сущности с именем **CustomerEntity** , использует hello имени клиента в качестве ключа строку hello и фамилию в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="476ae-129">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="476ae-129">Create a table</span></span>

<span data-ttu-id="476ae-130">Hello ниже показано, как toocreate таблицы:</span><span class="sxs-lookup"><span data-stu-id="476ae-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="476ae-131">В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="476ae-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="476ae-132">Откройте hello `TablesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="476ae-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="476ae-133">Добавьте метод **CreateTable**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="476ae-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="476ae-134">В пределах hello **CreateTable** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="476ae-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="476ae-135">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="476ae-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="476ae-136">Получите объект **CloudTableClient**, представляющий клиент службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="476ae-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="476ae-137">Получить **CloudTable** , представляющий ссылку toohello необходимое имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="476ae-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="476ae-138">Hello **CloudTableClient.GetTableReference** метод не выполняет запрос к хранилищу таблиц.</span><span class="sxs-lookup"><span data-stu-id="476ae-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="476ae-139">независимо от того, имеется ли hello таблица существует, возвращается ссылка Hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="476ae-140">Вызовите hello **CloudTable.CreateIfNotExists** метод toocreate hello таблицы, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="476ae-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="476ae-141">Hello **CloudTable.CreateIfNotExists** возвращает **true** Если hello таблица не существует и успешно создан.</span><span class="sxs-lookup"><span data-stu-id="476ae-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="476ae-142">В противном случае возвращается значение **false**.</span><span class="sxs-lookup"><span data-stu-id="476ae-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="476ae-143">Обновление hello **ViewBag** с именем hello hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="476ae-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="476ae-144">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="476ae-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="476ae-145">На hello **добавить представление** диалоговое окно, введите **CreateTable** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="476ae-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="476ae-146">Откройте `CreateTable.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="476ae-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="476ae-147">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="476ae-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="476ae-148">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="476ae-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="476ae-149">Запустите приложение hello и выберите **создать таблицу** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="476ae-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Создать таблицу](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="476ae-151">Как упоминалось ранее, hello **CloudTable.CreateIfNotExists** возвращает **true** только когда hello таблица не существует и создается.</span><span class="sxs-lookup"><span data-stu-id="476ae-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="476ae-152">Таким образом, если при запуске приложение hello hello таблица существует, метод hello возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="476ae-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="476ae-153">приложение hello toorun несколько раз, необходимо удалить таблицу hello перед повторным запуском приложения hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="476ae-154">Удаление таблицы hello можно сделать с помощью hello **CloudTable.Delete** метод.</span><span class="sxs-lookup"><span data-stu-id="476ae-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="476ae-155">Также можно удалить таблицы hello, с помощью hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) или hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="476ae-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="476ae-156">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="476ae-156">Add an entity tooa table</span></span>

<span data-ttu-id="476ae-157">*Сущности* сопоставить tooC\# объектов с помощью пользовательских классов, производных от **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="476ae-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="476ae-158">tooadd таблицу tooa сущности, создайте класс, определяющий hello свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="476ae-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="476ae-159">В этом разделе вы увидите, как класс сущностей, который использует toodefine hello имени клиента в качестве ключа строку hello и фамилию в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="476ae-160">Вместе секции и ключом строки идентификации сущности hello hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="476ae-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="476ae-161">Сущности с одинаковым ключом раздела можно запрашивать быстрее, чем с разными ключами раздела, но использование различных ключей разделов обеспечивает более высокую масштабируемость параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="476ae-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="476ae-162">Для любого свойства, который должен храниться в службе таблиц hello hello свойство должно быть открытое свойство, предоставляющую установке и извлечение значений поддерживаемого типа.</span><span class="sxs-lookup"><span data-stu-id="476ae-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="476ae-163">Здравствуйте, класс сущностей *должен* объявить открытый конструктор без параметров.</span><span class="sxs-lookup"><span data-stu-id="476ae-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="476ae-164">В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="476ae-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="476ae-165">Откройте hello `TablesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="476ae-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="476ae-166">Добавить hello, следующий за директивой так, hello кода в hello `TablesController.cs` файла можно получить доступ к hello **CustomerEntity** класса:</span><span class="sxs-lookup"><span data-stu-id="476ae-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="476ae-167">Добавьте метод **AddEntity**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="476ae-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="476ae-168">В пределах hello **AddEntity** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="476ae-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="476ae-169">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="476ae-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="476ae-170">Получите объект **CloudTableClient**, представляющий клиент службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="476ae-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="476ae-171">Получить **CloudTable** , представляющий таблицу toowhich toohello ссылку, ты tooadd hello новой сущности.</span><span class="sxs-lookup"><span data-stu-id="476ae-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="476ae-172">Создайте и инициализируйте hello **CustomerEntity** класса.</span><span class="sxs-lookup"><span data-stu-id="476ae-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="476ae-173">Создание **TableOperation** объекта, который вставляет сущность customer hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="476ae-174">Выполнять операции вставки hello, вызывающему Привет **CloudTable.Execute** метод.</span><span class="sxs-lookup"><span data-stu-id="476ae-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="476ae-175">Можно проверить hello результат операции hello, проверяя hello **TableResult.HttpStatusCode** свойство.</span><span class="sxs-lookup"><span data-stu-id="476ae-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="476ae-176">Код состояния 2xx указывает, что запрошенное клиентом hello действие hello был успешно обработан.</span><span class="sxs-lookup"><span data-stu-id="476ae-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="476ae-177">Например успешной вставки новых сущностей приводит код состояния HTTP 204, то есть операции hello успешно обработана и hello сервер не возвратил содержимого.</span><span class="sxs-lookup"><span data-stu-id="476ae-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="476ae-178">Обновление hello **ViewBag** с именем таблицы hello и hello результаты операции вставки hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="476ae-179">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="476ae-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="476ae-180">На hello **добавить представление** диалоговое окно, введите **AddEntity** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="476ae-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="476ae-181">Откройте `AddEntity.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="476ae-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="476ae-182">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="476ae-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="476ae-183">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="476ae-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="476ae-184">Запустите приложение hello и выберите **добавить сущность** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="476ae-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Добавление сущности](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="476ae-186">Убедитесь, что hello сущность добавлена hello выполните действия в разделе "hello" [получить одну сущность](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="476ae-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="476ae-187">Можно также использовать hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview все hello сущностей для таблицы.</span><span class="sxs-lookup"><span data-stu-id="476ae-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="476ae-188">Добавление пакета сущностей tooa таблицы</span><span class="sxs-lookup"><span data-stu-id="476ae-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="476ae-189">В дополнение toobeing может слишком[одновременно добавить таблицу tooa сущности](#add-an-entity-to-a-table), также можно добавить объекты в пакете.</span><span class="sxs-lookup"><span data-stu-id="476ae-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="476ae-190">Добавление сущностей в пакете уменьшает hello количество циклов приема-передачи между кодом и hello службы таблицы Azure.</span><span class="sxs-lookup"><span data-stu-id="476ae-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="476ae-191">Привет, следующие шаги иллюстрируют, как tooadd несколько сущностей tooa таблицу с собой операцию вставки одной:</span><span class="sxs-lookup"><span data-stu-id="476ae-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="476ae-192">В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="476ae-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="476ae-193">Откройте hello `TablesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="476ae-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="476ae-194">Добавьте метод **AddEntities**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="476ae-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="476ae-195">В пределах hello **AddEntities** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="476ae-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="476ae-196">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="476ae-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="476ae-197">Получите объект **CloudTableClient**, представляющий клиент службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="476ae-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="476ae-198">Получить **CloudTable** , представляющий таблицу toowhich toohello ссылку, являются постоянной tooadd hello новых сущностей.</span><span class="sxs-lookup"><span data-stu-id="476ae-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="476ae-199">Создать некоторые объекты клиента на основании hello **CustomerEntity** класс, представленный в разделе hello модели [добавьте таблицу tooa сущности](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="476ae-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="476ae-200">Получите объект **TableBatchOperation**.</span><span class="sxs-lookup"><span data-stu-id="476ae-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="476ae-201">Добавьте объект сущности toohello пакетной вставки операции.</span><span class="sxs-lookup"><span data-stu-id="476ae-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="476ae-202">Выполните операции пакетной вставки hello, вызывающему Привет **CloudTable.ExecuteBatch** метод.</span><span class="sxs-lookup"><span data-stu-id="476ae-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="476ae-203">Hello **CloudTable.ExecuteBatch** метод возвращает список **TableResult** объектов где каждого **TableResult** объект может быть проверенных toodetermine hello успешности для каждой отдельной операции.</span><span class="sxs-lookup"><span data-stu-id="476ae-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="476ae-204">В этом примере передать tooa список hello и позвольте hello вид отображения hello результаты каждой операции.</span><span class="sxs-lookup"><span data-stu-id="476ae-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="476ae-205">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="476ae-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="476ae-206">На hello **добавить представление** диалоговое окно, введите **AddEntities** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="476ae-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="476ae-207">Откройте `AddEntities.cshtml`и измените его, чтобы он выглядел hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="476ae-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="476ae-208">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="476ae-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="476ae-209">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="476ae-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="476ae-210">Запустите приложение hello и выберите **добавьте сущности** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="476ae-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![Добавление сущностей](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="476ae-212">Убедитесь, что hello сущность добавлена hello выполните действия в разделе "hello" [получить одну сущность](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="476ae-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="476ae-213">Можно также использовать hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview все hello сущностей для таблицы.</span><span class="sxs-lookup"><span data-stu-id="476ae-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="476ae-214">Получение одной сущности</span><span class="sxs-lookup"><span data-stu-id="476ae-214">Get a single entity</span></span>

<span data-ttu-id="476ae-215">В этом разделе показано, как tooget одной сущности из таблицы с помощью hello строк и ключ секционирования сущности.</span><span class="sxs-lookup"><span data-stu-id="476ae-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="476ae-216">В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment)и использует данные из [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="476ae-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="476ae-217">Откройте hello `TablesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="476ae-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="476ae-218">Добавьте метод **GetSingle**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="476ae-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="476ae-219">В пределах hello **GetSingle** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="476ae-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="476ae-220">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="476ae-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="476ae-221">Получите объект **CloudTableClient**, представляющий клиент службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="476ae-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="476ae-222">Получить **CloudTable** , представляющий ссылочной таблицы toohello, из которого происходит извлечение сущности hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="476ae-223">Создайте объект операции извлечения, который принимает объект сущности, производный от **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="476ae-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="476ae-224">Первый параметр Hello — hello *partitionKey*, и второй параметр hello — hello *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="476ae-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="476ae-225">С помощью hello **CustomerEntity** класса и данные, представленные в разделе "hello" [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table), hello следующие таблицы hello запросы фрагмент кода для **CustomerEntity** сущность с *partitionKey* значение «Smith» и *rowKey* значение «Вен»:</span><span class="sxs-lookup"><span data-stu-id="476ae-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="476ae-226">Выполняет операцию получения hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="476ae-227">Передайте представление toohello hello результатов для отображения.</span><span class="sxs-lookup"><span data-stu-id="476ae-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="476ae-228">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="476ae-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="476ae-229">На hello **добавить представление** диалоговое окно, введите **GetSingle** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="476ae-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="476ae-230">Откройте `GetSingle.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="476ae-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="476ae-231">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="476ae-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="476ae-232">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="476ae-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="476ae-233">Запустите приложение hello и выберите **получить один** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="476ae-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![Получение одной сущности](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="476ae-235">Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="476ae-235">Get all entities in a partition</span></span>

<span data-ttu-id="476ae-236">Как упоминалось в разделе hello [добавьте таблицу tooa сущности](#add-an-entity-to-a-table), сочетание hello секции и ключ строки однозначно определяют сущность в таблице.</span><span class="sxs-lookup"><span data-stu-id="476ae-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="476ae-237">Сущности с одним ключом раздела можно запрашивать быстрее, чем сущности с разными ключами раздела.</span><span class="sxs-lookup"><span data-stu-id="476ae-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="476ae-238">В этом разделе показано, как tooquery таблицы для всех hello сущностей из указанной секции.</span><span class="sxs-lookup"><span data-stu-id="476ae-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="476ae-239">В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment)и использует данные из [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="476ae-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="476ae-240">Откройте hello `TablesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="476ae-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="476ae-241">Добавьте метод **GetPartition**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="476ae-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="476ae-242">В пределах hello **GetPartition** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="476ae-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="476ae-243">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="476ae-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="476ae-244">Получите объект **CloudTableClient**, представляющий клиент службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="476ae-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="476ae-245">Получить **CloudTable** , представляющий ссылочной таблицы toohello, из которого происходит извлечение сущности hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="476ae-246">Создать экземпляр **TableQuery** указание запроса hello в hello объекта **где** предложения.</span><span class="sxs-lookup"><span data-stu-id="476ae-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="476ae-247">С помощью hello **CustomerEntity** класса и данные, представленные в разделе "hello" [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table), кода hello ниже фрагмент таблицы hello запросы для всех сущностей, где hello  **PartitionKey** (фамилии клиента) имеет значение «Smith»:</span><span class="sxs-lookup"><span data-stu-id="476ae-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="476ae-248">В цикле, вызовите hello **CloudTable.ExecuteQuerySegmented** метод передачи hello объекта запроса, экземпляр которого создан в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="476ae-249">Hello **CloudTable.ExecuteQuerySegmented** возвращает **TableContinuationToken** объекта, - при **null** -указывает, что нет несколько сущностей tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="476ae-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="476ae-250">В цикле hello используйте другой tooiterate цикл через hello возвращаются сущности.</span><span class="sxs-lookup"><span data-stu-id="476ae-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="476ae-251">В следующем примере кода hello каждой возвращенной сущности добавляется tooa списка.</span><span class="sxs-lookup"><span data-stu-id="476ae-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="476ae-252">Один раз Здравствуйте, цикл завершается, список hello передается tooa представление для отображения:</span><span class="sxs-lookup"><span data-stu-id="476ae-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="476ae-253">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="476ae-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="476ae-254">На hello **добавить представление** диалоговое окно, введите **GetPartition** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="476ae-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="476ae-255">Откройте `GetPartition.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="476ae-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="476ae-256">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="476ae-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="476ae-257">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="476ae-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="476ae-258">Запустите приложение hello и выберите **получить секции** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="476ae-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![Получение раздела](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="476ae-260">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="476ae-260">Delete an entity</span></span>

<span data-ttu-id="476ae-261">В этом разделе показано, как toodelete сущности из таблицы.</span><span class="sxs-lookup"><span data-stu-id="476ae-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="476ae-262">В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment)и использует данные из [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="476ae-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="476ae-263">Откройте hello `TablesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="476ae-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="476ae-264">Добавьте метод **DeleteEntity**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="476ae-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="476ae-265">В пределах hello **DeleteEntity** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="476ae-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="476ae-266">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="476ae-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="476ae-267">Получите объект **CloudTableClient**, представляющий клиент службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="476ae-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="476ae-268">Получить **CloudTable** , представляющий ссылочной таблицы toohello, из которого нужно удалить сущности hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="476ae-269">Создайте объект операции удаления, который принимает объект сущности, производный от **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="476ae-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="476ae-270">В этом случае мы используем hello **CustomerEntity** класса и данные, представленные в разделе "hello" [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="476ae-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="476ae-271">Здравствуйте сущности **ETag** необходимо задать допустимое значение tooa.</span><span class="sxs-lookup"><span data-stu-id="476ae-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="476ae-272">Выполнение операции удаления hello.</span><span class="sxs-lookup"><span data-stu-id="476ae-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="476ae-273">Передайте представление toohello hello результатов для отображения.</span><span class="sxs-lookup"><span data-stu-id="476ae-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="476ae-274">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="476ae-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="476ae-275">На hello **добавить представление** диалоговое окно, введите **DeleteEntity** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="476ae-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="476ae-276">Откройте `DeleteEntity.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="476ae-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="476ae-277">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="476ae-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="476ae-278">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="476ae-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="476ae-279">Запустите приложение hello и выберите **удалить сущность** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="476ae-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Получение одной сущности](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="476ae-281">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="476ae-281">Next steps</span></span>
<span data-ttu-id="476ae-282">Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="476ae-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="476ae-283">Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="476ae-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="476ae-284">Начало работы с хранилищем очередей Azure и подключенными службами Visual Studio</span><span class="sxs-lookup"><span data-stu-id="476ae-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)
