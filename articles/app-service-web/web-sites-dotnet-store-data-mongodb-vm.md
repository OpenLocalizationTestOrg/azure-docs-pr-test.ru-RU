---
title: "aaaCreate веб-приложения в Azure, которая подключается tooMongoDB, работающий на виртуальной машине"
description: "Учебник, в котором объясняется, как toouse Git toodeploy tooAzure приложения ASP.NET служб приложений подключаться tooMongoDB на виртуальной машине Azure."
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>Создание веб-приложения в Azure, который подключается tooMongoDB, работающий на виртуальной машине
С помощью Git, можно развернуть tooAzure приложения ASP.NET веб-приложений служб приложений. В этом учебнике будет создание простых переднего плана ASP.NET MVC приложение списка задач, который подключается tooa базы данных MongoDB работает на виртуальной машине в Azure.  [MongoDB][MongoDB] — это популярная высокопроизводительная база данных NoSQL с открытым кодом. После выполнения и тестирование приложения ASP.NET hello на компьютере разработчика, будет отправлен tooApp приложения hello службы веб-приложений с помощью Git.

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="background-knowledge"></a>Фоновые знания
Знание следующих hello полезно для этого учебника, но не требуется:

* драйвер Hello C# для MongoDB. Дополнительные сведения о разработке приложений C# для MongoDB. в разделе hello MongoDB [Center языка c#][MongoC#LangCenter]. 
* Платформа для веб-приложения Hello ASP .NET. Можно узнать об этом на hello [веб-сайта ASP.net][ASP.NET].
* Платформа для веб-приложения Hello ASP .NET MVC. Можно узнать об этом на hello [веб-сайта ASP.NET MVC][MVCWebSite].
* Azure. Для начала можно ознакомиться с [Azure][WindowsAzure].

## <a name="prerequisites"></a>Предварительные требования
* [Visual Studio 2013 Express для Web][VSEWeb] или [Visual Studio 2013][VSUlt].
* [Пакет Azure SDK для .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Активная подписка на Microsoft Azure

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Создание виртуальной машины и установка MongoDB
В этом учебном курсе предполагается, что вы создали виртуальную машину в Azure. После создания виртуальной машины hello необходимо tooinstall MongoDB на виртуальной машине hello:

* toocreate виртуальной машины Windows и установите MongoDB, в разделе [MongoDB установить на виртуальной машине под управлением Windows Server в Azure][InstallMongoOnWindowsVM].

После создания hello виртуальной машины в Azure и установки MongoDB быть убедиться, что tooremember hello DNS-имя hello виртуальной машины (например, «testlinuxvm.cloudapp.net») и hello внешний порт, указанный в конечной hello MongoDB.  Необходимо будет эту информацию далее в учебнике hello.

<a id="createapp"></a>

## <a name="create-hello-application"></a>Создание приложения hello
В этом разделе будет создавать приложения ASP.NET, называется «Мой список задач» в среде Visual Studio и выполнять tooAzure первоначального развертывания веб-приложений служб приложений. Вы будете запускать приложение hello локально, но он будет подключаться tooyour виртуальной машины в Azure и использовать созданного экземпляра MongoDB hello там.

1. В Visual Studio щелкните **Создать проект**.
   
    ![Начальная страница, новый проект][StartPageNewProject]
2. В hello **новый проект** окно hello левой панели выберите **Visual C#**, а затем выберите **Web**. В средней области hello выберите **веб-приложение ASP.NET**. Внизу hello имя проекта «MyTaskListApp» и нажмите кнопку **ОК**.
   
    ![Диалоговое окно "Новый проект"][NewProjectMyTaskListApp]
3. В hello **новый проект ASP.NET** выберите **MVC**, а затем нажмите кнопку **ОК**.
   
    ![Выбор шаблона MVC][VS2013SelectMVCTemplate]
4. Если вы еще не вошли в Microsoft Azure, появится запрос toosign в. Выполните запросы toosign hello в Azure.
5. После входа можно будет настроить веб-приложение службы приложений. Укажите hello **имя веб-приложения**, **план служб приложений**, **группы ресурсов**, и **область**, нажмите кнопку **создать**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. После завершения создания проекта hello ожидать toobe приложения hello web, созданных в службе приложений Azure, как указано в hello **активности службы приложения Azure** окна. Нажмите кнопку **MyTaskListApp публикации toothis веб-приложения сейчас**.
7. Щелкните **Опубликовать**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Как только приложение ASP.NET по умолчанию tooAzure опубликованного приложения службы веб-приложений, запускается в браузере hello.

## <a name="install-hello-mongodb-c-driver"></a>Установка hello драйвер MongoDB C#
MongoDB обеспечивает поддержку на стороне клиента для приложений C# с помощью драйвер, который необходимо tooinstall на локального компьютера разработчика. Hello C# драйвер доступен через NuGet.

hello tooinstall драйвер MongoDB C#:

1. В **обозреватель решений**, щелкните правой кнопкой мыши hello **MyTaskListApp** проект и выберите **управления NuGetPackages**.
   
    ![Управление пакетами NuGet][VS2013ManageNuGetPackages]
2. В hello **управление пакетами NuGet** hello левой панели щелкните **Online**. В hello **поиск в Интернете** поле на hello справа, введите «mongodb.driver».  Нажмите кнопку **установить** tooinstall hello драйвера.
   
    ![Поиск драйвера C# для MongoDB][SearchforMongoDBCSharpDriver]
3. Нажмите кнопку **принимаю** tooaccept hello 10gen, Inc. условия лицензионного соглашения.
4. Нажмите кнопку **закрыть** после установки драйвера hello.
    ![Драйвер C# для MongoDB установлен][MongoDBCsharpDriverInstalled]

Hello MongoDB C# драйвер установлен.  Ссылки на toohello **MongoDB.Bson**, **MongoDB.Driver**, и **MongoDB.Driver.Core** библиотеки были добавлены toohello проекта.

![Ссылки на драйвер C# для MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Добавление модели
В **обозревателе решений**, приветствия щелкните правой кнопкой мыши *моделей* папки и **добавить** новый **класса** и назовите его *TaskModel.cs* .  В *TaskModel.cs*, замените существующий код hello hello, следующий код:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-hello-data-access-layer"></a>Добавление слоя доступа к данным hello
В **обозревателе решений**, щелкните правой кнопкой мыши hello *MyTaskListApp* проекта и **добавить** **новую папку** с именем *DAL*.  Щелкните правой кнопкой мыши hello *DAL* папки и **добавить** новый **класса**. Имя файла класса hello *Dal.cs*.  В *Dal.cs*, замените существующий код hello hello, следующий код:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a>Добавление контроллера
Откройте hello *Controllers\HomeController.cs* файла в **обозревателе решений** и замените существующий код hello hello следующее:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-hello-styles"></a>Настройка стилей hello
Заголовок hello toochange вверху hello страницы приветствия, откройте hello *одну\\_Layout.cshtml* файла в **обозревателе решений** и замените «Мои задачи «Имя приложения» в заголовке hello переходов. Приложение списка», чтобы он выглядел следующим образом:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

В порядке tooset hello меню, список задач, откройте hello *\Views\Home\Index.cshtml* и замените существующий код hello hello, следующий код:

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


tooadd hello возможности toocreate новую задачу, щелкните правой кнопкой мыши hello *Views\Home\\*  папки и **добавить** **представление**.  Имя представления hello *создать*. Замените код hello hello следующее:

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

**Обозреватель решений** должен выглядеть следующим образом:

![Обозреватель решений][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a>Задание строки подключения MongoDB hello
В **обозревателе решений**откройте hello *DAL/Dal.cs* файла. Найти hello, следующей строкой кода:

    private string connectionString = "mongodb://<vm-dns-name>";

Замените `<vm-dns-name>` с DNS-именем hello hello виртуальной машины под управлением MongoDB, созданный в hello [создать виртуальную машину и установите MongoDB] [ Create a virtual machine and install MongoDB] шаге этого учебника.  toofind hello DNS-имя виртуальной машины, перейдите в раздел toohello портал Azure, выберите **виртуальные машины**и найти **DNS-имя**.

Если MongoDB прослушивает порт по умолчанию hello 27017 hello DNS-имя виртуальной машины hello является «testlinuxvm.cloudapp.net», будет выглядеть hello соединения строки строку кода:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Если конечная точка виртуальной машины hello указывает внешний порт для MongoDB, вы можете порт hello укажите в строке подключения hello:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Дополнительные сведения о строках подключения MongoDB см. в разделе [Подключения][MongoConnectionStrings].

## <a name="test-hello-local-deployment"></a>Локальное развертывание hello теста
Выберите приложение на компьютере разработчика toorun **начать отладку** из hello **отладки** меню или нажмите клавишу **F5**. IIS Express запускается и веб-браузер открывает и запускает приложение hello домашней страницы.  Можно добавить новую задачу, которая будет добавляться toohello MongoDB базы данных, на виртуальной машине в Azure.

![Приложение "My Task List"][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>Публикации tooAzure приложения службы веб-приложений
В этом разделе описывается публикация вашей tooAzure изменения веб-приложений служб приложений.

1. В обозревателе решений щелкните правой кнопкой мыши **MyTaskListApp** и выберите **Опубликовать**.
2. Щелкните **Опубликовать**.
   
    Теперь вы увидите веб-приложения, запущенные в службе приложений Azure и доступ к базе данных MongoDB hello в виртуальных машинах Azure.

## <a name="summary"></a>Сводка
Успешно развернут вашей tooAzure приложения ASP.NET веб-приложений служб приложений. tooview hello веб-приложения:

1. Войдите на портал Azure hello.
2. Нажмите **Веб-приложения**. 
3. Выберите веб-приложения в hello **веб-приложений** списка.

Дополнительные сведения о разработке приложений C# для MongoDB см. в [центре языка CSharp][MongoC#LangCenter]. 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
