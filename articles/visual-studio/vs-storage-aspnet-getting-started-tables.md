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
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Начало работы с хранилищем таблиц Azure и подключенными службами Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Обзор

Хранилище таблиц Azure позволяет toostore больших объемов структурированных данных. Hello служба находится в хранилище данных NoSQL, принимающий вызовам c аутентификацией внутри и вне hello облако Azure. Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.

В этом учебнике показано, как toowrite ASP.NET кода в некоторых распространенных сценариях, использование сущностей в хранилище таблиц Azure. К этим сценариям относится создание таблицы, а также добавление, запрос и удаление сущностей таблиц. 

##<a name="prerequisites"></a>Предварительные требования

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Учетная запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Создание контроллера MVC 

1. В hello **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров**и в контекстном меню hello, выберите **Добавить -> контроллер**.

    ![Добавление контроллера tooan приложение ASP.NET MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. На hello **Добавление формирования шаблонов** диалогового окна выберите **контроллер MVC 5 - пустой**и выберите **добавить**.

    ![Выбор типа контроллера MVC](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. На hello **добавления контроллера** диалогового окна, имя контроллера hello *TablesController*и выберите **добавить**.

    ![Имя контроллера MVC hello](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Добавьте следующее hello *с помощью* toohello директивы `TablesController.cs` файла:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Создание класса модели

Многие примеры hello в этой статье используется **TableEntity**-производный класс с именем **CustomerEntity**. следующие шаги Hello проводит пользователя через объявление этот класс как класс модели:

1. В hello **обозревателе решений**, щелкните правой кнопкой мыши **моделей**и в контекстном меню hello, выберите **Добавить -> класс**.

1. На hello **Добавление нового элемента** диалогового окна, имя класса hello, **CustomerEntity**.

1. Откройте hello `CustomerEntity.cs` файл и добавьте следующее hello **с помощью** директиву:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Измените класс hello, таким образом, чтобы по завершении hello класс объявляется как hello, следующий код. Класс Hello объявляет класс сущности с именем **CustomerEntity** , использует hello имени клиента в качестве ключа строку hello и фамилию в качестве ключа секции hello.

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

## <a name="create-a-table"></a>Создание таблицы

Hello ниже показано, как toocreate таблицы:

> [!NOTE]
> 
> В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `TablesController.cs` файла.

1. Добавьте метод **CreateTable**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. В пределах hello **CreateTable** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Получите объект **CloudTableClient**, представляющий клиент службы таблиц.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Получить **CloudTable** , представляющий ссылку toohello необходимое имя таблицы. Hello **CloudTableClient.GetTableReference** метод не выполняет запрос к хранилищу таблиц. независимо от того, имеется ли hello таблица существует, возвращается ссылка Hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Вызовите hello **CloudTable.CreateIfNotExists** метод toocreate hello таблицы, если он еще не существует. Hello **CloudTable.CreateIfNotExists** возвращает **true** Если hello таблица не существует и успешно создан. В противном случае возвращается значение **false**.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Обновление hello **ViewBag** с именем hello hello таблицы.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **CreateTable** hello имя представления, а также выберите **добавить**.

1. Откройте `CreateTable.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Запустите приложение hello и выберите **создать таблицу** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Создать таблицу](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Как упоминалось ранее, hello **CloudTable.CreateIfNotExists** возвращает **true** только когда hello таблица не существует и создается. Таким образом, если при запуске приложение hello hello таблица существует, метод hello возвращает **false**. приложение hello toorun несколько раз, необходимо удалить таблицу hello перед повторным запуском приложения hello. Удаление таблицы hello можно сделать с помощью hello **CloudTable.Delete** метод. Также можно удалить таблицы hello, с помощью hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) или hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности

*Сущности* сопоставить tooC\# объектов с помощью пользовательских классов, производных от **TableEntity**. tooadd таблицу tooa сущности, создайте класс, определяющий hello свойства сущности. В этом разделе вы увидите, как класс сущностей, который использует toodefine hello имени клиента в качестве ключа строку hello и фамилию в качестве ключа секции hello. Вместе секции и ключом строки идентификации сущности hello hello таблицы. Сущности с одинаковым ключом раздела можно запрашивать быстрее, чем с разными ключами раздела, но использование различных ключей разделов обеспечивает более высокую масштабируемость параллельных операций. Для любого свойства, который должен храниться в службе таблиц hello hello свойство должно быть открытое свойство, предоставляющую установке и извлечение значений поддерживаемого типа.
Здравствуйте, класс сущностей *должен* объявить открытый конструктор без параметров.

> [!NOTE]
> 
> В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment).

1. Откройте hello `TablesController.cs` файла.

1. Добавить hello, следующий за директивой так, hello кода в hello `TablesController.cs` файла можно получить доступ к hello **CustomerEntity** класса:

    ```csharp
    using StorageAspnet.Models;
    ```

1. Добавьте метод **AddEntity**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. В пределах hello **AddEntity** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Получите объект **CloudTableClient**, представляющий клиент службы таблиц.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Получить **CloudTable** , представляющий таблицу toowhich toohello ссылку, ты tooadd hello новой сущности. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Создайте и инициализируйте hello **CustomerEntity** класса.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Создание **TableOperation** объекта, который вставляет сущность customer hello.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Выполнять операции вставки hello, вызывающему Привет **CloudTable.Execute** метод. Можно проверить hello результат операции hello, проверяя hello **TableResult.HttpStatusCode** свойство. Код состояния 2xx указывает, что запрошенное клиентом hello действие hello был успешно обработан. Например успешной вставки новых сущностей приводит код состояния HTTP 204, то есть операции hello успешно обработана и hello сервер не возвратил содержимого.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Обновление hello **ViewBag** с именем таблицы hello и hello результаты операции вставки hello.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **AddEntity** hello имя представления, а также выберите **добавить**.

1. Откройте `AddEntity.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Запустите приложение hello и выберите **добавить сущность** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Добавление сущности](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    Убедитесь, что hello сущность добавлена hello выполните действия в разделе "hello" [получить одну сущность](#get-a-single-entity). Можно также использовать hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview все hello сущностей для таблицы.

## <a name="add-a-batch-of-entities-tooa-table"></a>Добавление пакета сущностей tooa таблицы

В дополнение toobeing может слишком[одновременно добавить таблицу tooa сущности](#add-an-entity-to-a-table), также можно добавить объекты в пакете. Добавление сущностей в пакете уменьшает hello количество циклов приема-передачи между кодом и hello службы таблицы Azure. Привет, следующие шаги иллюстрируют, как tooadd несколько сущностей tooa таблицу с собой операцию вставки одной:

> [!NOTE]
> 
> В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment).

1. Откройте hello `TablesController.cs` файла.

1. Добавьте метод **AddEntities**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. В пределах hello **AddEntities** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Получите объект **CloudTableClient**, представляющий клиент службы таблиц.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Получить **CloudTable** , представляющий таблицу toowhich toohello ссылку, являются постоянной tooadd hello новых сущностей. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Создать некоторые объекты клиента на основании hello **CustomerEntity** класс, представленный в разделе hello модели [добавьте таблицу tooa сущности](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Получите объект **TableBatchOperation**.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Добавьте объект сущности toohello пакетной вставки операции.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Выполните операции пакетной вставки hello, вызывающему Привет **CloudTable.ExecuteBatch** метод.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Hello **CloudTable.ExecuteBatch** метод возвращает список **TableResult** объектов где каждого **TableResult** объект может быть проверенных toodetermine hello успешности для каждой отдельной операции. В этом примере передать tooa список hello и позвольте hello вид отображения hello результаты каждой операции. 
 
    ```csharp
    return View(results);
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **AddEntities** hello имя представления, а также выберите **добавить**.

1. Откройте `AddEntities.cshtml`и измените его, чтобы он выглядел hello следующим образом.

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

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Запустите приложение hello и выберите **добавьте сущности** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Добавление сущностей](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    Убедитесь, что hello сущность добавлена hello выполните действия в разделе "hello" [получить одну сущность](#get-a-single-entity). Можно также использовать hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview все hello сущностей для таблицы.

## <a name="get-a-single-entity"></a>Получение одной сущности

В этом разделе показано, как tooget одной сущности из таблицы с помощью hello строк и ключ секционирования сущности. 

> [!NOTE]
> 
> В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment)и использует данные из [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table). 

1. Откройте hello `TablesController.cs` файла.

1. Добавьте метод **GetSingle**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. В пределах hello **GetSingle** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Получите объект **CloudTableClient**, представляющий клиент службы таблиц.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Получить **CloudTable** , представляющий ссылочной таблицы toohello, из которого происходит извлечение сущности hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Создайте объект операции извлечения, который принимает объект сущности, производный от **TableEntity**. Первый параметр Hello — hello *partitionKey*, и второй параметр hello — hello *rowKey*. С помощью hello **CustomerEntity** класса и данные, представленные в разделе "hello" [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table), hello следующие таблицы hello запросы фрагмент кода для **CustomerEntity** сущность с *partitionKey* значение «Smith» и *rowKey* значение «Вен»:

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Выполняет операцию получения hello.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Передайте представление toohello hello результатов для отображения.

    ```csharp
    return View(result);
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **GetSingle** hello имя представления, а также выберите **добавить**.

1. Откройте `GetSingle.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

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

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Запустите приложение hello и выберите **получить один** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Получение одной сущности](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Получение всех сущностей в разделе

Как упоминалось в разделе hello [добавьте таблицу tooa сущности](#add-an-entity-to-a-table), сочетание hello секции и ключ строки однозначно определяют сущность в таблице. Сущности с одним ключом раздела можно запрашивать быстрее, чем сущности с разными ключами раздела. В этом разделе показано, как tooquery таблицы для всех hello сущностей из указанной секции.  

> [!NOTE]
> 
> В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment)и использует данные из [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table). 

1. Откройте hello `TablesController.cs` файла.

1. Добавьте метод **GetPartition**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. В пределах hello **GetPartition** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Получите объект **CloudTableClient**, представляющий клиент службы таблиц.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Получить **CloudTable** , представляющий ссылочной таблицы toohello, из которого происходит извлечение сущности hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Создать экземпляр **TableQuery** указание запроса hello в hello объекта **где** предложения. С помощью hello **CustomerEntity** класса и данные, представленные в разделе "hello" [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table), кода hello ниже фрагмент таблицы hello запросы для всех сущностей, где hello  **PartitionKey** (фамилии клиента) имеет значение «Smith»:

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. В цикле, вызовите hello **CloudTable.ExecuteQuerySegmented** метод передачи hello объекта запроса, экземпляр которого создан в предыдущем шаге hello.  Hello **CloudTable.ExecuteQuerySegmented** возвращает **TableContinuationToken** объекта, - при **null** -указывает, что нет несколько сущностей tooretrieve. В цикле hello используйте другой tooiterate цикл через hello возвращаются сущности. В следующем примере кода hello каждой возвращенной сущности добавляется tooa списка. Один раз Здравствуйте, цикл завершается, список hello передается tooa представление для отображения: 

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

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **GetPartition** hello имя представления, а также выберите **добавить**.

1. Откройте `GetPartition.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

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

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Запустите приложение hello и выберите **получить секции** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Получение раздела](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Удаление сущности

В этом разделе показано, как toodelete сущности из таблицы.

> [!NOTE]
> 
> В этом разделе предполагается шаги hello в [настроить среду разработки hello](#set-up-the-development-environment)и использует данные из [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table). 

1. Откройте hello `TablesController.cs` файла.

1. Добавьте метод **DeleteEntity**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. В пределах hello **DeleteEntity** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Получите объект **CloudTableClient**, представляющий клиент службы таблиц.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Получить **CloudTable** , представляющий ссылочной таблицы toohello, из которого нужно удалить сущности hello. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Создайте объект операции удаления, который принимает объект сущности, производный от **TableEntity**. В этом случае мы используем hello **CustomerEntity** класса и данные, представленные в разделе "hello" [Добавление пакета сущностей таблицы tooa](#add-a-batch-of-entities-to-a-table). Здравствуйте сущности **ETag** необходимо задать допустимое значение tooa.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Выполнение операции удаления hello.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Передайте представление toohello hello результатов для отображения.

    ```csharp
    return View(result);
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **таблиц**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **DeleteEntity** hello имя представления, а также выберите **добавить**.

1. Откройте `DeleteEntity.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

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

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Запустите приложение hello и выберите **удалить сущность** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Получение одной сущности](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.

  * [Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Начало работы с хранилищем очередей Azure и подключенными службами Visual Studio](../storage/vs-storage-aspnet-getting-started-queues.md)
