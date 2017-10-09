---
title: "Руководство по ASP.NET MVC для Azure Cosmos DB. Разработка веб-приложения | Документация Майкрософт"
description: "ASP.NET MVC учебника toocreate веб-приложения MVC с помощью Azure Cosmos DB. С помощью этого руководства по ASP NET MVC вы сможете сохранить файл JSON и получить доступ к данным из приложения \"Список дел\", размещенного на веб-сайтах Azure."
keywords: "руководство по asp.net mvc, разработка веб-приложений, веб-приложение mvc, пошаговое руководство asp net mvc"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight как можно эффективно использовать toostore Azure Cosmos DB и запрос документов JSON, эта статья содержит пошаговое руководство начала до конца, показывая, как toobuild приложения todo, с помощью Azure Cosmos DB. Hello задачи будут храниться в виде документов JSON в базе данных Azure Cosmos.

![Снимок экрана списка поручений hello веб-приложение MVC, созданные из этого учебника — ASP NET MVC учебника шаг за шагом](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

Это пошаговое руководство показывает, как toouse hello Azure Cosmos DB службы toostore и доступ к данным из веб-приложения ASP.NET MVC, размещенные в Azure. Если вы ищете учебник, в котором рассматривается только Azure Cosmos DB, и не hello компоненты ASP.NET MVC отображаются [построения консольного приложения Azure Cosmos DB C#](documentdb-get-started.md).

> [!TIP]
> Предполагается, что у вас есть опыт использования ASP.NET MVC и веб-сайтов Azure. Новый tooASP.NET или hello [готовности к установке средства](#_Toc395637760), рекомендуется загрузить проект полный образец hello из [GitHub] [ GitHub] и следуя инструкциям hello в этом примере. После построения, можно просмотреть этой статьи toogain подробные сведения о кода hello в контексте hello hello проекта.
> 
> 

## <a name="_Toc395637760"></a>Предварительные требования для изучения этого учебника по базам данных
Перед выполнением инструкции hello в этой статье, следует убедиться, что имеется следующее hello:

* Активная учетная запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 

    ИЛИ

    Локальная установка hello [DB эмулятор Azure Cosmos](local-emulator.md).
* [Visual Studio 2017](http://www.visualstudio.com/).  
* Microsoft Azure SDK для .NET для Visual Studio 2017 г., доступны через hello установщик Visual Studio.

Все снимки экрана приветствия в этой статье были выполнены с помощью Microsoft Visual Studio Community 2017 г.. Если система настроена с помощью другой версии экраны и параметры могут не соответствовать полностью, однако если соблюдаются hello выше необходимые условия Это решение должно работать.

## <a name="_Toc395637761"></a>Шаг 1. Создание учетной записи базы данных Azure Cosmos DB
Давайте сначала создадим учетную запись Azure Cosmos DB. Если вы уже учетной записи SQL (DocumentDB) для Azure Cosmos DB или при использовании hello эмулятор DB Cosmos Azure для этого учебника, можно пропустить слишком[Создание нового приложения ASP.NET MVC](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Теперь мы рассмотрим как toocreate нового приложения ASP.NET MVC от hello основ. 

## <a name="_Toc395637762"></a>Шаг 2. Создание нового приложения ASP.NET MVC

1. В Visual Studio в hello **файл** меню выберите пункт слишком**New**и нажмите кнопку **проекта**. Hello **новый проект** откроется диалоговое окно.

2. В hello **типов проектов** области, разверните **шаблоны**, **Visual C#**, **Web**и выберите **веб-приложение ASP.NET** .

      ![Снимок диалогового окна нового проекта hello с выделенной тип проекта веб-приложения ASP.NET hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. В hello **имя** введите имя hello hello проекта. В этом учебнике используется имя hello «todo». При выборе toouse нечто, отличное от этого, затем везде, где этот учебник рассмотрен hello todo пространства имен, необходимо toouse образцы кода hello предоставленный tooadjust все, что вы с именем приложения. 
4. Нажмите кнопку **Обзор** toonavigate toohello папку, где бы как toocreate hello проекта и нажмите кнопку **ОК**.
   
      Hello **новое веб-приложение ASP.NET** откроется диалоговое окно.
   
    ![Снимок экрана: hello диалоговое окно нового веб-приложения ASP.NET с hello шаблона MVC-приложения выделяются](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. В области "Шаблоны" hello, выберите **MVC**.

6. Нажмите кнопку **ОК** и позволяют выполнить эту операцию вокруг формирование шаблонов hello пустого шаблона ASP.NET MVC Visual Studio. 

          
7. После завершения создания hello шаблона MVC-приложения Visual Studio вы сможете пустое приложение ASP.NET, можно выполнять локально.
   
    Локально, так как я уверен, что у нас все замеченный hello ASP.NET «Hello World» будут пропущены, запущенном проекте hello приложения. Давайте рассмотрим прямой tooadding Azure Cosmos DB toothis проекта и построение приложения.

## <a name="_Toc395637767"></a>Шаг 3: Добавление проекта веб-приложения MVC tooyour Azure Cosmos DB
Теперь, когда у нас есть большая часть коммуникационного hello ASP.NET MVC, необходимую для этого решения, давайте toohello реальная цель этого учебника, Добавление веб-приложение MVC tooour Azure Cosmos DB.

1. Hello Azure Cosmos DB .NET SDK упаковывается и распространяется в виде пакета NuGet. tooget Здравствуйте пакета NuGet в Visual Studio, используйте диспетчер пакетов NuGet hello в Visual Studio, щелкнув проект hello в **обозревателе решений** и выбрав **управление пакетами NuGet**.
   
    ![Снимок экрана: hello контекстное меню для проекта веб-приложения hello в окне обозревателя решений с управление пакетами NuGet выделяются.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    Hello **управление пакетами NuGet** откроется диалоговое окно.
2. В hello NuGet **Обзор** введите ***Azure DocumentDB***. (имя пакета hello еще не обновленные tooAzure Cosmos DB.)
   
    На основе результатов hello установить hello **Microsoft.Azure.DocumentDB корпорацией Майкрософт** пакета. Это будет загрузить и установить пакет Azure Cosmos DB hello, а также все зависимости, такие как Newtonsoft.Json. Нажмите кнопку **ОК** в hello **предварительного просмотра** окна, и **принимаю** в hello **принятия условий лицензионного соглашения** установки hello toocomplete окна.
   
    ![Снимок Sreen окне Управление пакетами NuGet hello hello выделяются клиентской библиотеки Microsoft Azure DocumentDB](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      Кроме того, можно использовать hello пакета hello tooinstall консоль диспетчера пакетов. toodo в этом случае на hello **средства** меню, нажмите кнопку **диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**. В строке приветствия введите ниже hello.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. После установки пакета hello решения Visual Studio должен выглядеть в две новые ссылки добавлен, Microsoft.Azure.Documents.Client и Newtonsoft.Json следующим hello.
   
    ![Снимок Sreen две ссылки hello добавлены toohello JSON данных проекта в обозревателе решений](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>Шаг 4: Настройка hello приложение ASP.NET MVC
Теперь добавим hello модели, представления и контроллеры toothis MVC-приложения:

* [Добавление модели](#_Toc395637764).
* [Добавление контроллера](#_Toc395637765).
* [Добавление представлений](#_Toc395637766).

### <a name="_Toc395637764"></a>Добавление модели данных JSON
Давайте начнем с создания hello **M** в MVC hello модели. 

1. В **обозреватель решений**, щелкните правой кнопкой мыши hello **моделей** папку, нажмите кнопку **добавить**и нажмите кнопку **класса**.
   
      Hello **Добавление нового элемента** откроется диалоговое окно.
2. Назовите новый класс **Item.cs** и нажмите кнопку **Добавить**. 
3. В этом new **Item.cs** файл, добавьте следующее hello после hello последнего *с помощью инструкции*.
   
        using Newtonsoft.Json;
4. Теперь замените этот код 
   
        public class Item
        {
        }
   
    с hello, следующий код.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Все данные в базе данных Azure Cosmos передается по сети hello и хранятся в виде JSON. toocontrol hello способ объектов сериализовать и десериализовать JSON.NET, можно использовать hello **JsonProperty** атрибута, как показано в hello **элемент** только что созданный класс. Вы не **имеют** toodo это, но я требуется tooensure, Мои свойств следовать camelCase JSON hello соглашения об именовании. 
   
    Не только можно ли управлять hello формат имени свойства hello при переходе в JSON, но можно полностью переименовать свои свойства .NET, как я сделал с hello **описание** свойство. 

### <a name="_Toc395637765"></a>Добавление контроллера
Берет на себя hello **M**, а теперь давайте создадим hello **C** в класс контроллера MVC.

1. В **обозреватель решений**, щелкните правой кнопкой мыши hello **контроллеров** папку, нажмите кнопку **добавить**и нажмите кнопку **контроллера**.
   
    Hello **Добавление формирования шаблонов** откроется диалоговое окно.
2. Выберите **Контроллер MVC 5 — пустой** и нажмите кнопку **Добавить**.
   
    ![Диалоговое окно Добавление формирования шаблонов hello с hello контроллер MVC 5 - пустой параметр выделен снимок экрана](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Назовите новый контроллер **ItemController.**
   
    ![Снимок экрана: диалоговое окно добавления контроллера hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    После создания файла hello решения Visual Studio должна иметь вид следующие hello с использованием нового файла ItemController.cs hello в **обозревателе решений**. также показывается Hello Item.cs файл создан в более ранней версии.
   
    ![Hello решения Visual Studio - обозреватель решений с hello новый ItemController.cs и Item.cs файлы выделяются снимок экрана](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    Вы можете закрыть ItemController.cs, мы вернемся tooit позже. 

### <a name="_Toc395637766"></a>Добавление представлений
Теперь давайте создадим hello **V** в MVC hello представления:

* [Добавление представления «Индекс элементов»](#AddItemIndexView).
* [Добавление представления «Создание элементов»](#AddNewIndexView).
* [Добавление представления «Редактирование элементов»](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Добавление представления «Индекс элементов»
1. В **обозревателе решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши hello пустой **элемент** созданную папку Visual Studio автоматически при добавлении hello  **ItemController** ранее, нажмите кнопку **добавить**, а затем нажмите кнопку **представление**.
   
    ![В обозревателе решений папку элемента hello, созданным Visual Studio с выделенной команды Добавить представление hello (снимок экрана)](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. В hello **добавить представление** диалогового окна поле, hello следующие:
   
   * В hello **имя представления** введите ***индекса***.
   * В hello **шаблона** выберите ***списка***.
   * В hello **класс модели** выберите ***элемента (todo. Модели)***.
   * Введите в поле макет страницы приветствия ***~/Views/Shared/_Layout.cshtml***.
     
   ![Диалоговое окно добавления представления hello снимок экрана](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. После установки этих значений нажмите **Добавить** , и Visual Studio создаст представление. После его завершения, он будет открыт файл cshtml hello, который был создан. Как мы вернемся tooit позже можно закрыть этот файл в Visual Studio.

#### <a name="AddNewIndexView"></a>Добавление представления «Создание элементов»
Аналогичные toohow, мы создали **индекс элемента** представление, создадим новое представление для создания новых **элементы**.

1. В **обозреватель решений**, щелкните правой кнопкой мыши hello **элемента** папку еще раз, нажмите кнопку **добавить**и нажмите кнопку **представление**.
2. В hello **добавить представление** диалогового окна поле, hello следующие:
   
   * В hello **имя представления** введите ***создать***.
   * В hello **шаблона** выберите ***создать***.
   * В hello **класс модели** выберите ***элемента (todo. Модели)***.
   * Введите в поле макет страницы приветствия ***~/Views/Shared/_Layout.cshtml***.
   * Щелкните **Добавить**.
   
#### <a name="_Toc395888515"></a>Добавление представления «Редактирование элементов»
И наконец, добавьте одно последнее представление для редактирования **элемент** в hello так же как и раньше.

1. В **обозреватель решений**, щелкните правой кнопкой мыши hello **элемента** папку еще раз, нажмите кнопку **добавить**и нажмите кнопку **представление**.
2. В hello **добавить представление** диалогового окна поле, hello следующие:
   
   * В hello **имя представления** введите ***изменить***.
   * В hello **шаблона** выберите ***изменить***.
   * В hello **класс модели** выберите ***элемента (todo. Модели)***.
   * Введите в поле макет страницы приветствия ***~/Views/Shared/_Layout.cshtml***.
   * Щелкните **Добавить**.

После этого, закройте все документы cshtml hello в Visual Studio, как мы вернет toothese представления позже.

## <a name="_Toc395637769"></a>Шаг 5. Подключение Azure Cosmos DB
Теперь, когда уже обеспечена hello стандартные действия MVC, давайте рассмотрим tooadding hello кода для Azure Cosmos DB. 

В этом разделе мы добавим код toohandle hello следующее:

* [Вывод списка незавершенных элементов](#_Toc395637770).
* [Добавление элементов](#_Toc395637771).
* [Редактирование элементов](#_Toc395637772).

### <a name="_Toc395637770"></a>Отображение незавершенных элементов в веб-приложении MVC
Hello первый toodo вещь здесь добавить класс, содержащий hello логику tooconnect tooand используют базу данных Azure Cosmos. В этом учебнике мы будем инкапсулировать эту логику в класс tooa репозиторий с именем DocumentDBRepository. 

1. В **обозревателе решений**, правой кнопкой мыши проект hello, нажмите кнопку **добавить**, а затем нажмите кнопку **класса**. Имя нового класса hello **DocumentDBRepository** и нажмите кнопку **добавить**.
2. В только что созданный hello **DocumentDBRepository** и добавьте следующее hello *с помощью инструкций* выше hello *имен* объявления
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    Теперь замените этот код 
   
        public class DocumentDBRepository
        {
        }
   
    с hello, следующий код.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. Мы читаете некоторые значения из конфигурации, поэтому откройте hello **Web.config** файла приложения и добавьте следующие строки под заголовком hello hello `<AppSettings>` раздела.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. Теперь обновите значения hello *конечной точки* и *authKey* с помощью ключей колонке hello hello портала Azure. Использовать hello **URI** из колонки hello ключей в качестве значения hello приветствия конечной точки и используйте hello **ПЕРВИЧНОГО ключа**, или **ВТОРИЧНЫЙ ключ** из колонки hello ключей в качестве значения hello hello значение параметра authKey.

    Что позаботится о подключения хранилища Azure Cosmos DB hello, теперь позволяет добавить логику приложения.

1. Hello первое, что нам нужно будет toodo toobe с приложения списка задач — toodisplay hello неполных элементов.  Скопируйте и вставьте следующий фрагмент кода в любом месте в пределах hello hello **DocumentDBRepository** класса.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. Откройте hello **ItemController** мы добавленный ранее и добавьте следующее hello *с помощью инструкций* выше hello объявление пространства имен.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Если проект не называется «todo», то вам требуется tooupdate с помощью рабочих элементов». Моделей»; tooreflect hello имя проекта.
   
    Теперь замените этот код
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    с hello, следующий код.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. Откройте **Global.asax.cs** и добавьте следующие строки toohello hello **Application_Start** метод 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

На этом этапе решение должно быть возможности toobuild без ошибок.

Если вы запустили приложение hello, следует перейти toohello **HomeController** и hello **индекс** представление этого контроллера. Это поведение по умолчанию hello hello MVC шаблона проекта мы выбрали в начале hello, но мы не хотим! Изменим hello маршрутизации на этом tooalter приложения MVC это поведение.

Откройте ***приложения\_Start\RouteConfig.cs*** и найдите строку hello, начиная с «значения по умолчанию:» и измените его hello tooresemble следующие.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

Теперь сообщает ASP.NET MVC, если вы не указали значение в URL-адрес toocontrol hello hello поведения маршрутизации, чтобы вместо **Главная**, используйте **элемент** как контроллер hello и пользователь **индекса** как представление hello.

Теперь при запуске приложения hello, он будет вызывать ваш **ItemController** которого будет вызова в классе toohello репозитория и использовать метод tooreturn hello GetItems все toohello неполных элементов hello **представления** \\ **Элемент**\\**индекс** представления. 

Если создать и запустить этот проект сейчас, отобразится примерно следующие данные.    

![Снимок экрана: hello список todo веб-приложения, созданные из этого учебника базы данных](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Добавление элементов
Скажем некоторые элементы в базу данных, у нас есть больше, чем пустая сетка toolook на.

Давайте добавим код слишком Azure Cosmos DBRepository и ItemController toopersist hello записи в базу данных Azure Cosmos.

1. Добавьте следующий метод tooyour hello **DocumentDBRepository** класса.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   Этот метод принимает объект, переданный tooit и сохраняет ее в базе данных Azure Cosmos.
2. Откройте файл ItemController.cs hello и добавьте следующий фрагмент кода в классе hello hello. Это известно как ASP.NET MVC, какие toodo для hello **создать** действие. В этом случае просто отрисовки hello связанное представление Create.cshtml, созданного ранее.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    Теперь мы должны код в этот контроллер, принимается hello отправки с hello **создать** представления.
3. Добавьте следующий блок кода toohello ItemController.cs класс, который сообщает, какие toodo формы POST для этого контроллера ASP.NET MVC hello.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    Этот код вызывает в toohello DocumentDBRepository и использует hello CreateItemAsync метод toopersist hello новой todo элемента toohello базы данных. 
   
    **Примечание по безопасности**: hello **ValidateAntiForgeryToken** используется атрибут здесь toohelp защиты этого приложения от атак с подделкой межсайтовых запросов. Имеется несколько tooit, чем просто добавлять этот атрибут, представлений должны toowork с данным маркером защиты от подделки. Для получения дополнительных сведений об тема hello и примеры как tooimplement это неправильно, см. в разделе [препятствует подделки межсайтовых запросов][Preventing Cross-Site Request Forgery]. Здравствуйте, исходный код на [GitHub] [ GitHub] имеет полную реализацию hello на месте.
   
    **Примечание по безопасности**: мы также используем hello **привязки** атрибута toohelp параметр метода hello защититься от излишней учета атак. Дополнительные сведения см. в записи блога [Основные операции CRUD в ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].

Это заключительный шаг hello код, необходимый tooadd новые элементы tooour базы данных.

### <a name="_Toc395637772"></a>Редактирование элементов
Есть кое-что нам toodo, и это tooedit возможность hello tooadd **элементы** в базе данных hello и toomark их завершения. Hello представление для редактирования уже была добавлена toohello проекта, так нам нужна лишь tooadd иной код контроллера tooour и toohello **DocumentDBRepository** класса еще раз.

1. Добавьте следующие toohello hello **DocumentDBRepository** класса.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    Здравствуйте, первый из этих методов, **GetItem** извлекает элемент из DB Cosmos Azure, которая передается назад toohello **ItemController** и затем на toohello **изменить** представления.
   
    Здравствуйте, второй hello методов мы только что добавили hello заменяет **документа** в Azure DB Cosmos с версией hello hello **документа** hello, передаваемые в **ItemController**.
2. Добавьте следующие toohello hello **ItemController** класса.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    Hello первый метод обрабатывает hello Http GET, которое происходит при нажатии пользователем hello на hello **изменить** ссылка из hello **индекс** представления. Этот метод извлекает [ **документа** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) из базы данных Azure Cosmos и передает его toohello **изменить** представления.
   
    Hello **изменить** представление будет выполните Http POST toohello **IndexController**. 
   
    Второй метод Hello, мы добавили дескрипторы передачи обновлены hello объекта tooAzure Cosmos DB toobe сохраняются в базе данных hello.

Верно, который является все, что нам нужно toorun нашего приложения, список неполный **элементы**, добавить новые **элементы**и изменение **элементы**.

## <a name="_Toc395637773"></a>Шаг 6: Запуск приложения hello локально
приложение hello tootest на локальном компьютере, hello следующие:

1. Нажмите клавишу F5 в Visual Studio toobuild hello приложения в режиме отладки. Его следует построить приложение hello и запустить браузер с hello пустая страница «Сетка», мы видели до:
   
    ![Снимок экрана: hello список todo веб-приложения, созданные из этого учебника базы данных](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Нажмите кнопку hello **создать новый** ссылку и добавьте значения toohello **имя** и **описание** поля. Оставьте hello **завершено** флажок не выбран, в противном случае hello новый **элемент** будут добавлены в завершенном состоянии и не будет отображаться на исходный список hello.
   
    ![Снимок экрана: hello представления создания](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. Нажмите кнопку **создать** и являются перенаправленный назад toohello **индекс** представление и **элемент** отображается в списке hello.
   
    ![Снимок экрана: hello представлении индекса](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    Чувствовать себя свободного tooadd еще несколько **элементы** tooyour списка задач.
    
4. Нажмите кнопку **изменить** Далее tooan **элемент** на списке hello, берутся toohello **изменить** представление, где можно обновить любое свойство объекта, в том числе hello  **Завершено** флаг. Если пометить hello **завершить** пометить и выберите **Сохранить**, hello **элемент** удаляется из списка hello незавершенные задачи.
   
    ![Снимок экрана: hello представление Index этот флажок установлен, в котором выполнено hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. После тестирования приложения hello, нажмите клавиши Ctrl + F5 toostop отладки приложение hello. Вы будете готовы toodeploy!

## <a name="_Toc395637774"></a>Шаг 7: Разверните приложение hello tooAzure службы приложений 
Теперь, когда полное приложение hello правильность работы с Azure Cosmos DB мы будем toodeploy этот web app tooAzure службы приложений.  

1. — Это все приложение, необходимо toodo toopublish правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **публикации**.
   
    ![Снимок экрана: hello параметр публикации в обозревателе решений](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. В hello **публикации** диалоговое окно, нажмите кнопку **службу приложений Microsoft Azure**, а затем выберите **создать новый** toocreate службы приложения профиля, или нажмите кнопку **выберите Существующие** toouse существующего профиля.

    ![Диалоговое окно "Публикация" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. При наличии существующего профиля службы приложений Azure введите имя своей подписки. Используйте hello **представление** отфильтровать toosort группы ресурсов или тип ресурса, а затем выберите службу приложений Azure. 
   
    ![Диалоговое окно "Служба приложений" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. Щелкните toocreate профиля службы приложений Azure, **создать новый** в hello **публикации** диалоговое окно. В hello **Создание приложения службы** диалоговое окно, введите имя веб-приложения и соответствующие подписки, группы ресурсов и план служб приложений, а затем нажмите кнопку **создать**.

    ![Диалоговое окно "Создать службу приложений" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

Через несколько секунд Visual Studio завершит публикацию вашего веб-приложения и запустит браузер, где вы увидите свое творение, запущенное в Azure!



## <a name="_Toc395637775"></a>Дальнейшие действия
Поздравляем! Просто построен вашего первого ASP.NET MVC, веб-приложения, использующие Azure Cosmos DB и публикации его tooAzure. Здравствуйте, исходный код для завершения приложения hello, включая подробные hello и удалите функции, которые не были включены в это учебника можно скачать или клоном [GitHub][GitHub]. Поэтому если вы заинтересованы в добавлении tooyour приложение, захватите кода hello и добавьте его toothis приложения.

Дополнительные функциональные возможности tooyour tooadd приложения, просмотрите hello API-интерфейса в hello [библиотеки .NET DB Cosmos Azure](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) привычной свободного toocontribute toohello библиотеки .NET DB Cosmos Azure на [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
