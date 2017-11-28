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
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="513bf-103">Создание веб-приложения в Azure, который подключается tooMongoDB, работающий на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="513bf-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="513bf-104">С помощью Git, можно развернуть tooAzure приложения ASP.NET веб-приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="513bf-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="513bf-105">В этом учебнике будет создание простых переднего плана ASP.NET MVC приложение списка задач, который подключается tooa базы данных MongoDB работает на виртуальной машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="513bf-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="513bf-106">[MongoDB][MongoDB] — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="513bf-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="513bf-107">После выполнения и тестирование приложения ASP.NET hello на компьютере разработчика, будет отправлен tooApp приложения hello службы веб-приложений с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="513bf-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="513bf-108">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="513bf-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="513bf-109">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="513bf-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="513bf-110">Фоновые знания</span><span class="sxs-lookup"><span data-stu-id="513bf-110">Background knowledge</span></span>
<span data-ttu-id="513bf-111">Знание следующих hello полезно для этого учебника, но не требуется:</span><span class="sxs-lookup"><span data-stu-id="513bf-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="513bf-112">драйвер Hello C# для MongoDB.</span><span class="sxs-lookup"><span data-stu-id="513bf-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="513bf-113">Дополнительные сведения о разработке приложений C# для MongoDB. в разделе hello MongoDB [Center языка c#][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="513bf-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="513bf-114">Платформа для веб-приложения Hello ASP .NET.</span><span class="sxs-lookup"><span data-stu-id="513bf-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="513bf-115">Можно узнать об этом на hello [веб-сайта ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="513bf-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="513bf-116">Платформа для веб-приложения Hello ASP .NET MVC.</span><span class="sxs-lookup"><span data-stu-id="513bf-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="513bf-117">Можно узнать об этом на hello [веб-сайта ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="513bf-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="513bf-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="513bf-118">Azure.</span></span> <span data-ttu-id="513bf-119">Для начала можно ознакомиться с [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="513bf-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="513bf-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="513bf-120">Prerequisites</span></span>
* <span data-ttu-id="513bf-121">[Visual Studio 2013 Express для Web][VSEWeb] или [Visual Studio 2013][VSUlt].</span><span class="sxs-lookup"><span data-stu-id="513bf-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="513bf-122">Пакет Azure SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="513bf-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="513bf-123">Активная подписка на Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="513bf-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="513bf-124">Создание виртуальной машины и установка MongoDB</span><span class="sxs-lookup"><span data-stu-id="513bf-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="513bf-125">В этом учебном курсе предполагается, что вы создали виртуальную машину в Azure.</span><span class="sxs-lookup"><span data-stu-id="513bf-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="513bf-126">После создания виртуальной машины hello необходимо tooinstall MongoDB на виртуальной машине hello:</span><span class="sxs-lookup"><span data-stu-id="513bf-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="513bf-127">toocreate виртуальной машины Windows и установите MongoDB, в разделе [MongoDB установить на виртуальной машине под управлением Windows Server в Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="513bf-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="513bf-128">После создания hello виртуальной машины в Azure и установки MongoDB быть убедиться, что tooremember hello DNS-имя hello виртуальной машины (например, «testlinuxvm.cloudapp.net») и hello внешний порт, указанный в конечной hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="513bf-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="513bf-129">Необходимо будет эту информацию далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="513bf-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="513bf-130">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="513bf-130">Create hello application</span></span>
<span data-ttu-id="513bf-131">В этом разделе будет создавать приложения ASP.NET, называется «Мой список задач» в среде Visual Studio и выполнять tooAzure первоначального развертывания веб-приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="513bf-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="513bf-132">Вы будете запускать приложение hello локально, но он будет подключаться tooyour виртуальной машины в Azure и использовать созданного экземпляра MongoDB hello там.</span><span class="sxs-lookup"><span data-stu-id="513bf-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="513bf-133">В Visual Studio щелкните **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="513bf-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Начальная страница, новый проект][StartPageNewProject]
2. <span data-ttu-id="513bf-135">В hello **новый проект** окно hello левой панели выберите **Visual C#**, а затем выберите **Web**.</span><span class="sxs-lookup"><span data-stu-id="513bf-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="513bf-136">В средней области hello выберите **веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="513bf-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="513bf-137">Внизу hello имя проекта «MyTaskListApp» и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="513bf-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Диалоговое окно "Новый проект"][NewProjectMyTaskListApp]
3. <span data-ttu-id="513bf-139">В hello **новый проект ASP.NET** выберите **MVC**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="513bf-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Выбор шаблона MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="513bf-141">Если вы еще не вошли в Microsoft Azure, появится запрос toosign в.</span><span class="sxs-lookup"><span data-stu-id="513bf-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="513bf-142">Выполните запросы toosign hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="513bf-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="513bf-143">После входа можно будет настроить веб-приложение службы приложений.</span><span class="sxs-lookup"><span data-stu-id="513bf-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="513bf-144">Укажите hello **имя веб-приложения**, **план служб приложений**, **группы ресурсов**, и **область**, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="513bf-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="513bf-145">После завершения создания проекта hello ожидать toobe приложения hello web, созданных в службе приложений Azure, как указано в hello **активности службы приложения Azure** окна.</span><span class="sxs-lookup"><span data-stu-id="513bf-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="513bf-146">Нажмите кнопку **MyTaskListApp публикации toothis веб-приложения сейчас**.</span><span class="sxs-lookup"><span data-stu-id="513bf-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="513bf-147">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="513bf-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="513bf-148">Как только приложение ASP.NET по умолчанию tooAzure опубликованного приложения службы веб-приложений, запускается в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="513bf-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="513bf-149">Установка hello драйвер MongoDB C#</span><span class="sxs-lookup"><span data-stu-id="513bf-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="513bf-150">MongoDB обеспечивает поддержку на стороне клиента для приложений C# с помощью драйвер, который необходимо tooinstall на локального компьютера разработчика.</span><span class="sxs-lookup"><span data-stu-id="513bf-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="513bf-151">Hello C# драйвер доступен через NuGet.</span><span class="sxs-lookup"><span data-stu-id="513bf-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="513bf-152">hello tooinstall драйвер MongoDB C#:</span><span class="sxs-lookup"><span data-stu-id="513bf-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="513bf-153">В **обозреватель решений**, щелкните правой кнопкой мыши hello **MyTaskListApp** проект и выберите **управления NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="513bf-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Управление пакетами NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="513bf-155">В hello **управление пакетами NuGet** hello левой панели щелкните **Online**.</span><span class="sxs-lookup"><span data-stu-id="513bf-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="513bf-156">В hello **поиск в Интернете** поле на hello справа, введите «mongodb.driver».</span><span class="sxs-lookup"><span data-stu-id="513bf-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="513bf-157">Нажмите кнопку **установить** tooinstall hello драйвера.</span><span class="sxs-lookup"><span data-stu-id="513bf-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![Поиск драйвера C# для MongoDB][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="513bf-159">Нажмите кнопку **принимаю** tooaccept hello 10gen, Inc. условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="513bf-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="513bf-160">Нажмите кнопку **закрыть** после установки драйвера hello.</span><span class="sxs-lookup"><span data-stu-id="513bf-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="513bf-161">![Драйвер C# для MongoDB установлен][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="513bf-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="513bf-162">Hello MongoDB C# драйвер установлен.</span><span class="sxs-lookup"><span data-stu-id="513bf-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="513bf-163">Ссылки на toohello **MongoDB.Bson**, **MongoDB.Driver**, и **MongoDB.Driver.Core** библиотеки были добавлены toohello проекта.</span><span class="sxs-lookup"><span data-stu-id="513bf-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![Ссылки на драйвер C# для MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="513bf-165">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="513bf-165">Add a model</span></span>
<span data-ttu-id="513bf-166">В **обозревателе решений**, приветствия щелкните правой кнопкой мыши *моделей* папки и **добавить** новый **класса** и назовите его *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="513bf-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="513bf-167">В *TaskModel.cs*, замените существующий код hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="513bf-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="513bf-168">Добавление слоя доступа к данным hello</span><span class="sxs-lookup"><span data-stu-id="513bf-168">Add hello data access layer</span></span>
<span data-ttu-id="513bf-169">В **обозревателе решений**, щелкните правой кнопкой мыши hello *MyTaskListApp* проекта и **добавить** **новую папку** с именем *DAL*.</span><span class="sxs-lookup"><span data-stu-id="513bf-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="513bf-170">Щелкните правой кнопкой мыши hello *DAL* папки и **добавить** новый **класса**.</span><span class="sxs-lookup"><span data-stu-id="513bf-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="513bf-171">Имя файла класса hello *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="513bf-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="513bf-172">В *Dal.cs*, замените существующий код hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="513bf-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-a-controller"></a><span data-ttu-id="513bf-173">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="513bf-173">Add a controller</span></span>
<span data-ttu-id="513bf-174">Откройте hello *Controllers\HomeController.cs* файла в **обозревателе решений** и замените существующий код hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="513bf-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

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

## <a name="set-up-hello-styles"></a><span data-ttu-id="513bf-175">Настройка стилей hello</span><span class="sxs-lookup"><span data-stu-id="513bf-175">Set up hello styles</span></span>
<span data-ttu-id="513bf-176">Заголовок hello toochange вверху hello страницы приветствия, откройте hello *одну\\_Layout.cshtml* файла в **обозревателе решений** и замените «Мои задачи «Имя приложения» в заголовке hello переходов. Приложение списка», чтобы он выглядел следующим образом:</span><span class="sxs-lookup"><span data-stu-id="513bf-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="513bf-177">В порядке tooset hello меню, список задач, откройте hello *\Views\Home\Index.cshtml* и замените существующий код hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="513bf-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

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


<span data-ttu-id="513bf-178">tooadd hello возможности toocreate новую задачу, щелкните правой кнопкой мыши hello *Views\Home\\*  папки и **добавить** **представление**.</span><span class="sxs-lookup"><span data-stu-id="513bf-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="513bf-179">Имя представления hello *создать*.</span><span class="sxs-lookup"><span data-stu-id="513bf-179">Name hello view *Create*.</span></span> <span data-ttu-id="513bf-180">Замените код hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="513bf-180">Replace hello code with hello following:</span></span>

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

<span data-ttu-id="513bf-181">**Обозреватель решений** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="513bf-181">**Solution Explorer** should look like this:</span></span>

![Обозреватель решений][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="513bf-183">Задание строки подключения MongoDB hello</span><span class="sxs-lookup"><span data-stu-id="513bf-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="513bf-184">В **обозревателе решений**откройте hello *DAL/Dal.cs* файла.</span><span class="sxs-lookup"><span data-stu-id="513bf-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="513bf-185">Найти hello, следующей строкой кода:</span><span class="sxs-lookup"><span data-stu-id="513bf-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="513bf-186">Замените `<vm-dns-name>` с DNS-именем hello hello виртуальной машины под управлением MongoDB, созданный в hello [создать виртуальную машину и установите MongoDB] [ Create a virtual machine and install MongoDB] шаге этого учебника.</span><span class="sxs-lookup"><span data-stu-id="513bf-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="513bf-187">toofind hello DNS-имя виртуальной машины, перейдите в раздел toohello портал Azure, выберите **виртуальные машины**и найти **DNS-имя**.</span><span class="sxs-lookup"><span data-stu-id="513bf-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="513bf-188">Если MongoDB прослушивает порт по умолчанию hello 27017 hello DNS-имя виртуальной машины hello является «testlinuxvm.cloudapp.net», будет выглядеть hello соединения строки строку кода:</span><span class="sxs-lookup"><span data-stu-id="513bf-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="513bf-189">Если конечная точка виртуальной машины hello указывает внешний порт для MongoDB, вы можете порт hello укажите в строке подключения hello:</span><span class="sxs-lookup"><span data-stu-id="513bf-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="513bf-190">Дополнительные сведения о строках подключения MongoDB см. в разделе [Подключения][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="513bf-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="513bf-191">Локальное развертывание hello теста</span><span class="sxs-lookup"><span data-stu-id="513bf-191">Test hello local deployment</span></span>
<span data-ttu-id="513bf-192">Выберите приложение на компьютере разработчика toorun **начать отладку** из hello **отладки** меню или нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="513bf-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="513bf-193">IIS Express запускается и веб-браузер открывает и запускает приложение hello домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="513bf-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="513bf-194">Можно добавить новую задачу, которая будет добавляться toohello MongoDB базы данных, на виртуальной машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="513bf-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![Приложение "My Task List"][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="513bf-196">Публикации tooAzure приложения службы веб-приложений</span><span class="sxs-lookup"><span data-stu-id="513bf-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="513bf-197">В этом разделе описывается публикация вашей tooAzure изменения веб-приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="513bf-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="513bf-198">В обозревателе решений щелкните правой кнопкой мыши **MyTaskListApp** и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="513bf-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="513bf-199">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="513bf-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="513bf-200">Теперь вы увидите веб-приложения, запущенные в службе приложений Azure и доступ к базе данных MongoDB hello в виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="513bf-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="513bf-201">Сводка</span><span class="sxs-lookup"><span data-stu-id="513bf-201">Summary</span></span>
<span data-ttu-id="513bf-202">Успешно развернут вашей tooAzure приложения ASP.NET веб-приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="513bf-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="513bf-203">tooview hello веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="513bf-203">tooview hello web app:</span></span>

1. <span data-ttu-id="513bf-204">Войдите на портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="513bf-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="513bf-205">Нажмите **Веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="513bf-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="513bf-206">Выберите веб-приложения в hello **веб-приложений** списка.</span><span class="sxs-lookup"><span data-stu-id="513bf-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="513bf-207">Дополнительные сведения о разработке приложений C# для MongoDB см. в [центре языка CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="513bf-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
