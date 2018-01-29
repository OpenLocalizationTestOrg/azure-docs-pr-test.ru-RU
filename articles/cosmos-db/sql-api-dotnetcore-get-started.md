---
title: "Azure Cosmos DB: Приступая к работе с учебником .NET Core API SQL | Документы Microsoft"
description: "Учебник, в котором создает консольное приложение на C#, с помощью Azure Cosmos DB SQL API .NET Core SDK и оперативной базы данных."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.custom: devcenter
ms.openlocfilehash: 0b19071bf871029b488b26d3f125d08d7d2a2dd4
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-sql-api-and-net-core"></a>Azure Cosmos DB: Приступая к работе с API-Интерфейсы SQL и .NET Core
> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Node.js для MongoDB](mongodb-samples.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [C++](sql-api-cpp-get-started.md)
>  
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Добро пожаловать в API SQL для Azure DB Cosmos, Приступая к работе с учебником .NET Core! После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.

Темы, рассматриваемые в этом руководстве:

* создание учетной записи Azure Cosmos DB и подключение к ней;
* настройка решения Visual Studio;
* Создание оперативной базы данных
* создание коллекции;
* создание документов JSON;
* выполнение запросов к коллекции;
* замена документа;
* удаление документа;
* удаление базы данных.

У вас нет времени? Не беспокойтесь! Полное решение доступно на [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started). Краткие инструкции см. в разделе [Получение полного решения NoSQL для этого руководства](#GetSolution).

Чтобы построить Xamarin iOS, Android или формы приложения с использованием API-Интерфейсы SQL и пакета SDK для .NET Core? См. [Создание мобильных приложений с помощью Xamarin и Azure Cosmos DB](mobile-apps-with-xamarin.md).

> [!NOTE]
> Пакет SDK .NET Core для Azure Cosmos DB, используемый в этом руководстве, не совместим с приложениями универсальной платформы Windows (UWP). Чтобы получить предварительную версию пакета SDK для .NET Core, которая поддерживает приложения UWP, отправьте сообщение по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

А теперь приступим к работе!

## <a name="prerequisites"></a>Технические условия

* Активная учетная запись Azure. Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/). 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [!INCLUDE [cosmos-db-emulator-vs](../../includes/cosmos-db-emulator-vs.md)] 
    * При работе на MacOS или Linux, можно разрабатывать приложения .NET Core из командной строки, установив [пакета SDK для .NET Core](https://www.microsoft.com/net/core#macos) для платформы по своему усмотрению. 
    * При работе в Windows, можно разрабатывать приложения .NET Core из командной строки, установив [пакета SDK для .NET Core](https://www.microsoft.com/net/core#windows). 
    * Можно использовать собственный редактор или загрузить [кода Visual Studio](https://code.visualstudio.com/), который предоставляется бесплатно и работает в Windows, Linux и MacOS. 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Шаг 1. Создание учетной записи Azure Cosmos DB
Давайте создадим учетную запись Azure Cosmos DB. Если у вас уже есть учетная запись, которую вы собираетесь использовать, можно перейти к шагу [Настройка решения Visual Studio](#SetupVS). Если вы используете эмулятор Azure Cosmos DB, следуйте указаниям в [DB эмулятор Azure Cosmos](local-emulator.md) установки эмулятора и сразу перейти к [установки решения Visual Studio](#SetupVS).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a> Шаг 2. Настройка решения Visual Studio
1. Откройте **Visual Studio 2017** у себя на компьютере.
2. В меню **Файл** выберите пункт **Создать**, а затем — **Проект**.
3. В диалоговом окне **Новый проект** выберите **Шаблоны** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)** (Консольное приложение (.NET Core)), а затем присвойте проекту имя **DocumentDBGettingStarted** и нажмите кнопку **ОК**.

   ![Снимок экрана: диалоговое окно «Новый проект»](./media/sql-api-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. В **обозревателе решений** щелкните правой кнопкой мыши **DocumentDBGettingStarted**.
5. Не выходя из меню, щелкните элемент **Управление пакетами NuGet…**.

   ![Снимок экрана: меню «Проект», вызванное щелчком правой кнопки мыши](./media/sql-api-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. На вкладке **NuGet** в верхней части окна щелкните **Обзор** и в поле поиска введите **azure documentdb**.
7. В результатах найдите **Microsoft.Azure.DocumentDB.Core** и нажмите кнопку **Установить**.
   Пакет для библиотеки имеет идентификатор [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core). Если используется версия .NET Framework (например, net461), которая не поддерживается для этого пакета .NET Core NuGet, используйте [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB), поддерживающую все версии .NET Framework, начиная с .NET Framework 4.5.
8. При появлении запросов подтвердите установку пакета NuGet и примите условия лицензионного соглашения.

Отлично! Теперь, когда Настройка завершена, давайте начнем написания кода. Вы можете найти проект готового кода для этого руководства в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).

## <a id="Connect"></a>Шаг 3. Подключение к учетной записи Azure Cosmos DB
Во-первых, добавьте эти ссылки в начало приложения C# в файле Program.cs:

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> Чтобы завершить работу с этим руководством, добавьте приведенные выше зависимости.

Теперь добавьте эти две константы и переменную *client* в открытый класс *Program*.

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

Затем войдите на [портал Azure](https://portal.azure.com), чтобы получить URI и первичный ключ. URI и первичный ключ Azure Cosmos DB позволяют приложению предоставлять данные о расположении, в котором будет устанавливаться подключение, делая подключение вашего приложения доверенным для Azure Cosmos DB.

На портале Azure перейдите к учетной записи Azure Cosmos DB, а затем щелкните **Ключи**.

Скопируйте универсальный код ресурса (URI) с портала и вставьте его в параметр `<your endpoint URI>` в файле program.cs. Затем скопируйте на портале значение поля "Первичный ключ" и вставьте его в параметр `<your key>`. Если вы используете эмулятор Azure Cosmos DB, укажите `https://localhost:8081` как конечную точку, а также примените четко определенный ключ авторизации, описанный в статье об [использовании эмулятора Azure Cosmos DB для разработки](local-emulator.md). Не забудьте удалить символы "<" и ">", но оставьте двойные кавычки, в которые заключены конечная точка и ключ.

![Снимок экрана портала Azure в ходе работы с руководством по NoSQL при создании консольного приложения C#. Показывает учетную запись Azure Cosmos DB, с общаются выделен, кнопка ключи, выделенная на странице учетной записи Azure Cosmos DB и значений URI, первичный ключ и ВТОРИЧНЫЙ ключ, выделенная на странице «ключи»][keys]

Мы запустим ознакомительное приложение, создав экземпляр **DocumentClient**.

В методе **Main** добавьте эту новую асинхронную задачу с именем **GetStartedDemo**, которая создает экземпляр **DocumentClient**.

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

Добавьте указанный далее код, чтобы запустить асинхронную задачу из метода **Main** . **Main** метод перехватывает исключения, которые записываются в консоль.

```csharp
static void Main(string[] args)
{
        // ADD THIS PART TO YOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key to exit.");
                Console.ReadKey();
        }
```

Нажмите кнопку **DocumentDBGettingStarted**, чтобы создать и запустить приложение.

Поздравляем! Вы успешно подключились к учетной записи Azure Cosmos DB. Давайте теперь рассмотрим принципы работы с ресурсами Azure Cosmos DB.  

## <a name="step-4-create-a-database"></a>Этап 4: создание базы данных
Прежде чем добавлять код для создания базы данных, добавьте вспомогательный метод для записи на консоль.

Скопируйте и вставьте метод **WriteToConsoleAndPromptToContinue** под кодом метода **GetStartedDemo**.

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

[Базу данных](sql-api-resources.md#databases) Azure Cosmos DB можно создать с помощью метода [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) класса **DocumentClient**. База данных представляет собой логический контейнер для хранения документов JSON, разделенных между коллекциями.

Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом создания клиента. Это создает базу данных с именем *FamilyDB*.

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.

Поздравляем! Вы успешно создали базу данных Azure Cosmos DB.  

## <a id="CreateColl"></a>Этап 5: создание коллекции
> [!WARNING]
> **CreateDocumentCollectionAsync** создает новую коллекцию с зарезервированной пропускной способностью, имеющая цены последствия. Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).

Вы можете создать [коллекцию](sql-api-resources.md#collections), используя метод [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) класса **DocumentClient**. Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.

Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом создания базы данных. Создается коллекция документ с именем *FamilyCollection_oa*.

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.

Поздравляем! Вы успешно создали коллекцию документов Azure Cosmos DB.  

## <a id="CreateDoc"></a>Шаг 6. Создание документов JSON
Вы можете создать [документ](sql-api-resources.md#documents) с помощью метода [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx), который относится к классу **DocumentClient**. Документы относятся к пользовательскому (произвольному) содержимому JSON. Теперь мы можем добавить один или несколько документов. Если у вас уже есть данные, которые необходимо хранить в базе данных, можно использовать [средство миграции данных](import-data.md)в Azure Cosmos DB.

Сначала необходимо создать класс **Family**, который будет представлять объекты, хранящиеся в Azure Cosmos DB в этом примере. Мы также создадим подклассы **Parent**, **Child**, **Pet** и **Address**, используемые в классе **Family**. Обратите внимание, документы должны иметь свойство **Id**, сериализуемое как **id** в файле JSON. Для этого после метода **GetStartedDemo** необходимо добавить следующие подклассы.

Скопируйте и вставьте классы **Family**, **Parent**, **Child**, **Pet** и **Address** под кодом метода **WriteToConsoleAndPromptToContinue**.

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key to continue ...");
    Console.ReadKey();
}

// ADD THIS PART TO YOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

Скопируйте и вставьте метод **CreateFamilyDocumentIfNotExists** под кодом метода **CreateDocumentCollectionIfNotExists**.

```csharp
// ADD THIS PART TO YOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

Затем вставьте два документа, один для семьи Андерсен и один для семьи Вейкфилд.

Скопируйте и вставьте код после `// ADD THIS PART TO YOUR CODE` в метод **GetStartedDemo** под кодом создания коллекции документов.

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.

Поздравляем! Вы успешно создали два документа Azure Cosmos DB.  

![На схеме представлены иерархические отношения между учетной записью, оперативной базой данных, коллекцией и документами, используемыми в руководстве по NoSQL при создании консольного приложения C#.](./media/sql-api-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB
Azure Cosmos DB поддерживает [полнофункциональные запросы](sql-api-sql-query.md) к документам JSON, хранящимся в каждой коллекции.  Ниже приведены примеры кода разнообразных запросов с использованием как синтаксиса SQL в Azure Cosmos DB, так и LINQ, которые можно запускать для добавленных на предыдущем шаге документов.

Скопируйте и вставьте метод **ExecuteSimpleQuery** под кодом метода **CreateFamilyDocumentIfNotExists**.

```csharp
// ADD THIS PART TO YOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find the Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute the same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом создания второго документа.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.

Поздравляем! Вы успешно выполнили запрос коллекции Azure Cosmos DB.

На схеме ниже показано, как для созданной коллекции вызывается синтаксис запроса SQL для Azure Cosmos DB. Та же логика применяется и к запросам LINQ.

![На схеме представлен масштаб и значение запроса, используемого в руководстве по NoSQL при создании консольного приложения C#.](./media/sql-api-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

Ключевое слово [FROM](sql-api-sql-query.md#FromClause) использовать в запросе необязательно, так как запросы Azure Cosmos DB привязаны только к одной коллекции. Поэтому слова "FROM Families f" можно заменить на "FROM root r" или любое другое имя переменной. Azure Cosmos DB выводит семейств, корень или имя переменной, выбранный вами ссылка текущей коллекции по умолчанию.

## <a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON
Azure Cosmos DB поддерживает замену документов JSON.  

Скопируйте и вставьте метод **ReplaceFamilyDocument** под кодом метода **ExecuteSimpleQuery**.

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом выполнения запроса. После замены документа тот же запрос будет запущен повторно, чтобы вы могли просмотреть измененный документ.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.

Поздравляем! Вы успешно заменили документ Azure Cosmos DB.

## <a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON
Azure Cosmos DB поддерживает удаление документов JSON.  

Скопируйте и вставьте метод **DeleteFamilyDocument** под кодом метода **ReplaceFamilyDocument**.

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом выполнения второго запроса.

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.

Поздравляем! Вы успешно удалили документ Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Шаг 10. Удаление базы данных
Удаление созданной базы данных приведет к удалению базы данных и всех дочерних ресурсов (коллекций, документов и т. д.).

Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом удаления документа, чтобы удалить всю базу данных и все дочерние ресурсы.

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.

Поздравляем! Вы успешно удалили базу данных Azure Cosmos DB.

## <a id="Run"></a>Шаг 11. Запуск консольного приложения C#
В Visual Studio нажмите кнопку **DocumentDBGettingStarted**, чтобы создать приложение в режиме отладки.

В окне консоли должны отобразиться выходные данные вашего приложения. Они должны содержать результаты обработки добавленных запросов. При этом выглядеть они должны примерно так, как показано в примере ниже.

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
Press any key to continue ...
Created Family Andersen.1
Press any key to continue ...
Created Family Wakefield.7
Press any key to continue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key to continue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key to exit.
```

Поздравляем! Вы завершили работу с этим руководством, и теперь у вас есть работающее консольное приложение C#.

## <a id="GetSolution"></a>Получение готового решения для этого руководства
Чтобы собрать решение GetStarted, которое содержит все примеры из данной статьи, вам понадобится следующее:

* Активная учетная запись Azure. Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).
* [Учетная запись Azure Cosmos DB][create-sql-api-dotnet.md#create-account]
* решение [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) , доступное в GitHub.

Чтобы восстановить ссылки на API-Интерфейсы SQL для Azure Cosmos DB .NET Core SDK в Visual Studio, щелкните правой кнопкой мыши **GetStarted** решения в обозревателе решений, а затем выберите **включите восстановление пакетов NuGet**. Затем в файле Program.cs обновите значения EndpointUrl и AuthorizationKey согласно инструкциям в разделе о [подключении к учетной записи Azure Cosmos DB](#Connect).

## <a name="next-steps"></a>Дальнейшие действия
* Требуется более подробное руководство по ASP.NET MVC? См. [Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](sql-api-dotnet-application.md).
* Разработка Xamarin iOS, Android или формы приложения с помощью API-Интерфейсы SQL для пакета SDK для Azure Cosmos DB .NET Core? См. [Создание мобильных приложений с помощью Xamarin и Azure Cosmos DB](mobile-apps-with-xamarin.md).
* Хотите выполнять проверку масштабирования и производительности с помощью Azure Cosmos DB? См. [Проверка производительности и масштабирования с помощью Azure Cosmos DB](performance-testing.md)
* Узнайте, как организовать [мониторинг запросов, использования и хранилища Azure Cosmos DB](monitor-accounts.md).
* Отправьте запросы образцу набора данных в [Площадке для запросов](https://www.documentdb.com/sql/demo).
* Дополнительные сведения о модели программирования см. в статье [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

[create-sql-api-dotnet.md#create-account]: create-sql-api-dotnet.md#create-account
[keys]: media/sql-api-dotnetcore-get-started/nosql-tutorial-keys.png
