---
title: "Azure Cosmos DB. Приступая к работе с API DocumentDB | Документация Майкрософт"
description: "Учебник, в котором создает консольное приложение на C#, с помощью DocumentDB API hello и оперативной базы данных."
keywords: "руководство nosql, оперативная база данных, консольное приложение c#"
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB. Приступая к работе с API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js для MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Учебник по началу Azure Cosmos DB DocumentDB API приветствия toohello работы! После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.

Мы рассмотрим следующие вопросы:

* Создание и подключение учетной записи Azure Cosmos DB tooan
* настройка решения Visual Studio;
* Создание оперативной базы данных
* создание коллекции;
* создание документов JSON;
* Запрос к коллекции hello
* замена документа;
* удаление документа;
* Удаление базы данных hello

У вас нет времени? Не беспокойтесь! законченное решение Hello можно найти в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). Переход toohello [получить hello весь раздел учебника решение NoSQL](#GetSolution) быстрого инструкции.

После этого выполните голосования hello используйте кнопки в hello верхней или нижней части этой страницы toogive нам отзыв. Если вы хотите нам toocontact напрямую, если вам свободного tooinclude адрес вашей электронной почты в комментарии.

А теперь приступим к работе!

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что у вас есть следующие hello:

* Активная учетная запись Azure. Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/). 
    * Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника.
* [Visual Studio Community 2017](http://www.visualstudio.com/).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Шаг 1. Создание учетной записи Azure Cosmos DB
Давайте создадим учетную запись Azure Cosmos DB. При наличии учетной записи требуется toouse можно сразу перейти слишком[установки решения Visual Studio](#SetupVS). Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[установки решения Visual Studio](#SetupVS).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a> Шаг 2. Настройка решения Visual Studio
1. Откройте **Visual Studio 2017** у себя на компьютере.
2. На hello **файл** последовательно выберите пункты **New**и нажмите кнопку **проекта**.
3. В hello **новый проект** диалогового окна выберите **шаблоны** / **Visual C#** / **консольное приложение**, имя проект, а затем щелкните **ОК**.
   ![Снимок экрана: hello окно нового проекта](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. В hello **обозревателе решений**, щелкните правой кнопкой мыши новое консольное приложение, который находится под управлением решения Visual Studio, и нажмите кнопку **управление пакетами NuGet...**
    
    ![Снимок hello справа щелчок меню для проекта hello](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. В hello **Nuget** щелкните **Обзор**и тип **azure documentdb** в поле поиска hello.
6. В результатах поиска hello, найти **Microsoft.Azure.DocumentDB** и нажмите кнопку **установить**.
   Идентификатор пакета Hello hello клиентской библиотеки API DocumentDB Azure Cosmos DB [клиентской библиотеки Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).
   ![Снимок экрана: hello меню Nuget для поиска Azure SDK клиента DB Cosmos](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    При получении сообщения о рецензировании решения toohello изменения, нажмите кнопку **ОК**. Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.

Отлично! Теперь, когда мы hello Настройка завершена, давайте начнем написания кода. Вы можете найти проект готового кода для этого руководства в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).

## <a id="Connect"></a>Шаг 3: Учетная запись Azure Cosmos DB tooan подключения
Во-первых, добавьте эти ссылается на начало toohello приложение C# в файле Program.cs hello:

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> В учебнике hello toocomplete заказа убедитесь, что Добавление зависимостей hello выше.
> 
> 

Теперь добавьте эти две константы и переменную *client* в открытый класс *Program*.

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

Далее head резервное toohello [портала Azure](https://portal.azure.com) tooretrieve URL-адрес конечной точки и первичный ключ. URL-адрес конечной точки Hello и первичный ключ, необходимые для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения.

В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour и нажмите кнопку **ключей**.

Скопируйте hello URI с портала hello и вставьте его в `<your endpoint URL>` в файле program.cs hello. Затем копировать hello первичный ключ с портала hello и вставьте его в `<your primary key>`.

![Снимок экрана: hello портал Azure hello NoSQL учебника toocreate консольное приложение C#. Показывает Cosmos Azure DB учетной записи, с hello общаются выделен, hello выделенной колонке учетная запись Azure Cosmos DB hello кнопкой ключи и значения URI, первичный ключ и ВТОРИЧНЫЙ ключ hello выделены на hello колонке ключей][keys]

Далее, мы начнем приложения hello, создав новый экземпляр hello **DocumentClient**.

Ниже hello **Main** метод, добавить эту новую асинхронную задачу, которая вызывается **GetStartedDemo**, который будет создан экземпляр наш новый **DocumentClient**.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

Добавьте следующий hello кода toorun асинхронную задачу из вашего **Main** метод. Hello **Main** метод будет перехватывать исключения и записывать их toohello консоли.

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
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
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

Нажмите клавишу **F5** toorun приложения. выходные данные в окно консоли Hello отображает приветственное сообщение `End of demo, press any key tooexit.` подтверждения того, что hello подключение было создано.  После этого можно закрыть окно консоли hello. 

Поздравляем! Учетная запись Azure Cosmos DB tooan успешно подключились, теперь давайте рассмотрим работы с ресурсами Azure Cosmos DB.  

## <a name="step-4-create-a-database"></a>Этап 4: создание базы данных
Перед добавлением hello код для создания базы данных, добавьте вспомогательный метод для записи toohello консоли.

Скопируйте и вставьте hello **WriteToConsoleAndPromptToContinue** метод после hello **GetStartedDemo** метод.

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Базы данных Azure Cosmos [базы данных](documentdb-resources.md#databases) могут быть созданы с помощью hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) метод hello **DocumentClient** класса. База данных находится hello логический контейнер для хранения документов JSON, секционированный по коллекциям.

Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после создания клиента hello. Будет создана база данных с именем *FamilyDB*.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

Нажмите клавишу **F5** toorun приложения.

Поздравляем! Вы успешно создали базу данных Azure Cosmos DB.  

## <a id="CreateColl"></a>Этап 5: создание коллекции
> [!WARNING]
> С помощью метода **CreateDatabaseIfNotExistsAsync** можно создать новую коллекцию с зарезервированной пропускной способностью и соответствующей ценой. Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Объект [коллекции](documentdb-resources.md#collections) могут быть созданы с помощью hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) метод hello **DocumentClient** класса. Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.

Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после создания базы данных hello. Будет создана коллекция документов с именем *FamilyCollection*.

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

Нажмите клавишу **F5** toorun приложения.

Поздравляем! Вы успешно создали коллекцию документов Azure Cosmos DB.  

## <a id="CreateDoc"></a>Шаг 6. Создание документов JSON
Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) метод hello **DocumentClient** класса. Документы относятся к пользовательскому (произвольному) содержимому JSON. Теперь мы можем добавить один или несколько документов. При наличии данных, отсылаемых toostore в базе данных можно использовать hello Azure Cosmos DB [средство переноса данных](import-data.md) tooimport hello данных в базу данных.

Во-первых, мы должны toocreate **семейства** класс, представляющий объекты в базе данных Azure Cosmos в этом образце. Мы также создадим подклассы **Parent**, **Child**, **Pet** и **Address**, используемые в классе **Family**. Обратите внимание, документы должны иметь свойство **Id**, сериализуемое как **id** в файле JSON. Эти классы можно создать, добавив следующие внутренние вложенные классы после hello hello **GetStartedDemo** метод.

Скопируйте и вставьте hello **семейства**, **родительского**, **дочерних**, **Pet**, и **адрес** классы после hello **WriteToConsoleAndPromptToContinue** метод.

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
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

Скопируйте и вставьте hello **CreateFamilyDocumentIfNotExists** под вашей **адрес** класса.

    // ADD THIS PART tooYOUR CODE
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

Добавьте два документа, одному для каждого семейства Андерсен hello и hello Wakefield семейства.

Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после создания коллекции документов hello.

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

Нажмите клавишу **F5** toorun приложения.

Поздравляем! Вы успешно создали два документа Azure Cosmos DB.  

![Схема, иллюстрирующая hello иерархическую связь между hello учетной записи, hello оперативную базу данных, коллекции hello и hello документов, созданных hello NoSQL учебника toocreate консольное приложение C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB
Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.  Hello следующий образец кода показывает различные запросы — оба SQL Azure Cosmos базы данных с помощью синтаксиса, а также LINQ - что мы может выполняться hello документов, над которыми мы вставлены в предыдущем шаге hello.

Скопируйте и вставьте hello **ExecuteSimpleQuery** метод после вашей **CreateFamilyDocumentIfNotExists** метод.

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после создания второго документа hello.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Нажмите клавишу **F5** toorun приложения.

Поздравляем! Вы успешно выполнили запрос коллекции Azure Cosmos DB.

Hello следующей схеме показано, как hello базы данных SQL Azure Cosmos синтаксис называется с коллекцией hello созданный запрос и hello же принцип применяется также toohello запроса LINQ.

![Диаграмму, демонстрирующая области hello и это означает hello запроса используется hello NoSQL учебника toocreate консольное приложение C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Hello [FROM](documentdb-sql-query.md#FromClause) ключевое слово является необязательным в hello запроса, так как запросы Azure Cosmos DB уже области tooa одну коллекцию. Поэтому слова "FROM Families f" можно заменить на "FROM root r" или любое другое имя переменной. Azure Cosmos DB определит, что семейств, корень или имя переменной hello выбрана, ссылка hello текущей коллекции по умолчанию.

## <a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON
Azure Cosmos DB поддерживает замену документов JSON.  

Скопируйте и вставьте hello **ReplaceFamilyDocument** метод после вашей **ExecuteSimpleQuery** метод.

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после выполнения запроса hello в конце hello метод hello. После замены hello документа, это будет выполняться hello же попытку запроса tooview hello изменения документа.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Нажмите клавишу **F5** toorun приложения.

Поздравляем! Вы успешно заменили документ Azure Cosmos DB.

## <a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON
Azure Cosmos DB поддерживает удаление документов JSON.  

Скопируйте и вставьте hello **DeleteFamilyDocument** метод после вашей **ReplaceFamilyDocument** метод.

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после выполнения второго запроса hello, в конце hello метод hello.

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

Нажмите клавишу **F5** toorun приложения.

Поздравляем! Вы успешно удалили документ Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Шаг 10: Удаление hello базы данных
Идет удаление hello создана база данных приведет к удалению hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).

Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после документа hello удалить toodelete hello всю базу данных и все дочерние ресурсы.

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

Нажмите клавишу **F5** toorun приложения.

Поздравляем! Вы успешно удалили базу данных Azure Cosmos DB.

## <a id="Run"></a>Шаг 11. Запуск консольного приложения C#
Нажмите клавишу F5 в Visual Studio toobuild hello приложения в режиме отладки.

Вы увидите выходные данные hello get работы приложения в окне консоли. выходные данные Hello покажет результаты hello hello запросов мы добавлен и должен соответствовать hello пример текста ниже.

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

Поздравляем! После завершения учебника hello и иметь работу консольного приложения C#!

## <a id="GetSolution"></a>Получить комплексное решение учебника hello
Если бы не было времени toocomplete hello шаги в этом учебнике или просто хотите toodownload hello образцы кода, можно получить его из [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). 

решение GetStarted toobuild hello, вам потребуется hello следующее:

* Активная учетная запись Azure. Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).
* [Учетная запись Azure Cosmos DB][cosmos-db-create-account]
* Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) решения на сайте GitHub.

toohello ссылки toorestore hello Azure Cosmos DB .NET SDK в Visual Studio щелкните правой кнопкой мыши hello **GetStarted** решения в обозревателе решений, а затем выберите **включите восстановление пакетов NuGet**. Затем в файле App.config hello, обновите значения EndpointUrl и AuthorizationKey hello как описано в [подключить учетную запись Azure Cosmos DB tooan](#Connect).

Теперь все готово. Выполните сборку и начинайте работу с решением.


## <a name="next-steps"></a>Дальнейшие действия
* Требуется более подробное руководство по ASP.NET MVC? См. [Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](documentdb-dotnet-application.md).
* Требуется tooperform масштаб и производительность, тестирование с помощью Azure Cosmos DB? См. [Проверка производительности и масштабирования с помощью Azure Cosmos DB](performance-testing.md)
* Узнайте, каким образом слишком[отслеживать запросы, использования и хранилища Azure Cosmos DB](monitor-accounts.md).
* Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).
* toolearn Дополнительные сведения о базе данных Azure Cosmos, в разделе [Добро пожаловать tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
