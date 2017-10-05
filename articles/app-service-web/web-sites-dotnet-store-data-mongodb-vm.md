---
title: "Создание веб-приложения в Azure, которое подключается к базе данных MongoDB, работающей на виртуальной машине"
description: "В этом учебнике показано, как использовать Git для развертывания приложения ASP.NET в службе приложений Azure, подключенной к MongoDB на виртуальной машине Azure."
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
ms.openlocfilehash: a3f289ed9c764d0859573de4f834e042d0f103c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="09d1f-103">Создание веб-приложения в Azure, которое подключается к базе данных MongoDB, работающей на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="09d1f-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="09d1f-104">С помощью Git можно развернуть приложение ASP.NET в веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="09d1f-105">В этом учебнике будет создано простое приложение списка задач ASP.NET MVC, которое подключается к базе данных MongoDB, работающей на виртуальной машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="09d1f-106">[MongoDB][MongoDB] — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="09d1f-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="09d1f-107">После запуска и тестирования приложения ASP.NET на компьютере разработчика приложение будет отправлено в веб-приложения службы Azure с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="09d1f-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="09d1f-108">Если вы хотите приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="09d1f-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="09d1f-109">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="09d1f-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="09d1f-110">Фоновые знания</span><span class="sxs-lookup"><span data-stu-id="09d1f-110">Background knowledge</span></span>
<span data-ttu-id="09d1f-111">При изучении данного учебника знание следующих тем может оказаться полезным, хотя и не является обязательным требованием:</span><span class="sxs-lookup"><span data-stu-id="09d1f-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="09d1f-112">Драйвер C# для MongoDB.</span><span class="sxs-lookup"><span data-stu-id="09d1f-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="09d1f-113">Дополнительные сведения о разработке приложений C# для MongoDB см. в [центре языка CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="09d1f-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="09d1f-114">Платформа веб-приложений ASP .NET.</span><span class="sxs-lookup"><span data-stu-id="09d1f-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="09d1f-115">Всестороннее описание данного вопроса см. на [веб-сайте ASP.NET][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="09d1f-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="09d1f-116">Платформа веб-приложений ASP .NET MVC.</span><span class="sxs-lookup"><span data-stu-id="09d1f-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="09d1f-117">Всестороннее описание данного вопроса см. на [веб-сайте ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="09d1f-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="09d1f-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-118">Azure.</span></span> <span data-ttu-id="09d1f-119">Для начала можно ознакомиться с [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="09d1f-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09d1f-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="09d1f-120">Prerequisites</span></span>
* <span data-ttu-id="09d1f-121">[Visual Studio 2013 Express для Web][VSEWeb] или [Visual Studio 2013][VSUlt].</span><span class="sxs-lookup"><span data-stu-id="09d1f-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="09d1f-122">Пакет Azure SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="09d1f-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="09d1f-123">Активная подписка на Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="09d1f-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="09d1f-124">Создание виртуальной машины и установка MongoDB</span><span class="sxs-lookup"><span data-stu-id="09d1f-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="09d1f-125">В этом учебном курсе предполагается, что вы создали виртуальную машину в Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="09d1f-126">После создания виртуальной машины необходимо установить на ней MongoDB.</span><span class="sxs-lookup"><span data-stu-id="09d1f-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="09d1f-127">Создание виртуальной машины Windows и установка MongoDB описаны в разделе [Установка MongoDB на виртуальную машину Windows][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="09d1f-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="09d1f-128">После создания виртуальной машины в Azure и установки MongoDB обязательно запомните DNS-имя виртуальной машины (например, "testlinuxvm.cloudapp.net") и внешний порт для MongoDB, указанный в конечной точке.</span><span class="sxs-lookup"><span data-stu-id="09d1f-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="09d1f-129">Эти сведения потребуются позже в данном учебном курсе.</span><span class="sxs-lookup"><span data-stu-id="09d1f-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="09d1f-130">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="09d1f-130">Create the application</span></span>
<span data-ttu-id="09d1f-131">В данном разделе с помощью Visual Studio будет создано приложение ASP.NET под именем "Мой список задач" и выполнено его первоначальное развертывание в веб-приложения службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="09d1f-132">Приложение будет выполняться локально, но будет подключаться к виртуальной машине в Azure и использовать созданный там экземпляр MongoDB.</span><span class="sxs-lookup"><span data-stu-id="09d1f-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="09d1f-133">В Visual Studio щелкните **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Начальная страница, новый проект][StartPageNewProject]
2. <span data-ttu-id="09d1f-135">В левой области окна **Новый проект** выберите **Visual C#**, а затем выберите **Веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="09d1f-136">В средней области выберите **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="09d1f-137">В нижней части введите имя "MyTaskListApp" для проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Диалоговое окно "Новый проект"][NewProjectMyTaskListApp]
3. <span data-ttu-id="09d1f-139">В диалоговом окне **Новый проект ASP.NET** выберите **MVC** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Выбор шаблона MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="09d1f-141">Если вы еще не выполнили вход в Microsoft Azure, будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="09d1f-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="09d1f-142">Следуйте инструкциям для входа в Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="09d1f-143">После входа можно будет настроить веб-приложение службы приложений.</span><span class="sxs-lookup"><span data-stu-id="09d1f-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="09d1f-144">Укажите **имя веб-приложения**, **план службы приложений**, **группу ресурсов** и **регион**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="09d1f-145">После завершения создания проекта дождитесь создания веб-приложения в службе приложений Azure, как указано в окне **Действия службы приложений Azure** .</span><span class="sxs-lookup"><span data-stu-id="09d1f-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="09d1f-146">Нажмите кнопку **Опубликовать MyTaskListApp в этом веб-приложении**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="09d1f-147">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="09d1f-148">После публикации приложения ASP.NET по умолчанию в веб-приложения службы приложений Azure приложение запустится в браузере.</span><span class="sxs-lookup"><span data-stu-id="09d1f-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="09d1f-149">Установка драйвера C# для MongoDB</span><span class="sxs-lookup"><span data-stu-id="09d1f-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="09d1f-150">MongoDB обеспечивает поддержку приложений C# на стороне клиента посредством драйвера, который необходимо установить на своем локальном компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="09d1f-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="09d1f-151">Драйвер C# можно получить через NuGet.</span><span class="sxs-lookup"><span data-stu-id="09d1f-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="09d1f-152">Порядок установки драйвера C# для MongoDB:</span><span class="sxs-lookup"><span data-stu-id="09d1f-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="09d1f-153">В **обозревателе решений** щелкните правой кнопкой мыши проект **MyTaskListApp** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Управление пакетами NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="09d1f-155">В левой части окна **Управление пакетами NuGet** щелкните **В сети**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="09d1f-156">В расположенном справа поле **Поиск в Интернете** введите "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="09d1f-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="09d1f-157">Щелкните элемент **Установить** , чтобы установить драйвер.</span><span class="sxs-lookup"><span data-stu-id="09d1f-157">Click **Install** to install the driver.</span></span>
   
    ![Поиск драйвера C# для MongoDB][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="09d1f-159">Нажмите кнопку **Принимаю** , чтобы принять условия лицензионного соглашения 10gen, Inc.</span><span class="sxs-lookup"><span data-stu-id="09d1f-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="09d1f-160">После установки драйвера нажмите кнопку **Закрыть** .</span><span class="sxs-lookup"><span data-stu-id="09d1f-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="09d1f-161">![Драйвер C# для MongoDB установлен][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="09d1f-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="09d1f-162">Теперь драйвер C# для MongoDB установлен.</span><span class="sxs-lookup"><span data-stu-id="09d1f-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="09d1f-163">В проект были добавлены ссылки на библиотеки **MongoDB.Bson**, **MongoDB.Driver** и **MongoDB.Driver.Core**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![Ссылки на драйвер C# для MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="09d1f-165">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="09d1f-165">Add a model</span></span>
<span data-ttu-id="09d1f-166">В **обозревателе решений** щелкните правой кнопкой мыши папку *Models* и выберите **Добавить** > **Класс**. Добавьте новый класс *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="09d1f-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="09d1f-167">Замените содержимое файла *TaskModel.cs* следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="09d1f-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-the-data-access-layer"></a><span data-ttu-id="09d1f-168">Добавление уровня доступа к данным</span><span class="sxs-lookup"><span data-stu-id="09d1f-168">Add the data access layer</span></span>
<span data-ttu-id="09d1f-169">В **обозревателе решений** щелкните правой кнопкой мыши проект *MyTaskListApp* и выберите **Добавить** > **Новая папка**. Присвойте новой папке имя *DAL*.</span><span class="sxs-lookup"><span data-stu-id="09d1f-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="09d1f-170">Щелкните правой кнопкой мыши папку *DAL* и выберите **Добавить** > **Класс**, чтобы добавить новый класс.</span><span class="sxs-lookup"><span data-stu-id="09d1f-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="09d1f-171">Назначьте файлу класса имя *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="09d1f-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="09d1f-172">Замените существующий код в файле *Dal.cs*на следующий код:</span><span class="sxs-lookup"><span data-stu-id="09d1f-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

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

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from the MongoDB server.        
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

            // Creates a Task and inserts it into the collection in MongoDB.
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

## <a name="add-a-controller"></a><span data-ttu-id="09d1f-173">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="09d1f-173">Add a controller</span></span>
<span data-ttu-id="09d1f-174">Откройте файл *Controllers\HomeController.cs* в **обозревателе решений** и замените имеющийся код приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="09d1f-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

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

## <a name="set-up-the-styles"></a><span data-ttu-id="09d1f-175">Настройка стилей</span><span class="sxs-lookup"><span data-stu-id="09d1f-175">Set up the styles</span></span>
<span data-ttu-id="09d1f-176">Чтобы изменить заголовок в верхней части страницы, откройте файл *Views\Shared\\\_Layout.cshtml* в **обозревателе решений** и замените "Имя приложения" в заголовке панели переходов строкой "Мое приложение списка задач", чтобы он выглядел следующим образом.</span><span class="sxs-lookup"><span data-stu-id="09d1f-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="09d1f-177">Для настройки меню списка задач откройте файл *\Views\Home\Index.cshtml* и замените существующий код приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="09d1f-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

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


<span data-ttu-id="09d1f-178">Чтобы добавить возможность создания новой задачи, щелкните правой кнопкой мыши папку *Views\Home\\\* и выберите **Добавить** > **Представление**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="09d1f-179">Присвойте представлению имя *Create*.</span><span class="sxs-lookup"><span data-stu-id="09d1f-179">Name the view *Create*.</span></span> <span data-ttu-id="09d1f-180">Замените код на приведенный ниже:</span><span class="sxs-lookup"><span data-stu-id="09d1f-180">Replace the code with the following:</span></span>

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

<span data-ttu-id="09d1f-181">**Обозреватель решений** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="09d1f-181">**Solution Explorer** should look like this:</span></span>

![обозревателе решений][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="09d1f-183">Установка строки подключения MongoDB</span><span class="sxs-lookup"><span data-stu-id="09d1f-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="09d1f-184">В **обозревателе решений**откройте файл *DAL/Dal.cs* .</span><span class="sxs-lookup"><span data-stu-id="09d1f-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="09d1f-185">Найдите следующую строку кода:</span><span class="sxs-lookup"><span data-stu-id="09d1f-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="09d1f-186">Замените `<vm-dns-name>` DNS-именем виртуальной машины, на которой выполняется база данных MongoDB, созданная на шаге [Создание виртуальной машины и установка MongoDB][Create a virtual machine and install MongoDB] в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="09d1f-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="09d1f-187">Чтобы найти DNS-имя своей виртуальной машины, перейдите на портал Azure, выберите **Виртуальные машины** и **DNS-имя**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="09d1f-188">Если DNS-имя виртуальной машины имеет значение "testlinuxvm.cloudapp.net" и MongoDB ведет прослушивание порта по умолчанию 27017, строка подключения в коде будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="09d1f-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="09d1f-189">Если конечная точка виртуальной машины задает другой внешний порт для MongoDB, можно указать этот порт в строке подключения:</span><span class="sxs-lookup"><span data-stu-id="09d1f-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="09d1f-190">Дополнительные сведения о строках подключения MongoDB см. в разделе [Подключения][MongoConnectionStrings].</span><span class="sxs-lookup"><span data-stu-id="09d1f-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="09d1f-191">Тестирование локального развертывания</span><span class="sxs-lookup"><span data-stu-id="09d1f-191">Test the local deployment</span></span>
<span data-ttu-id="09d1f-192">Для запуска приложения на компьютере разработчика в меню **Отладка** выберите **Начать отладку** или нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="09d1f-193">Запускается IIS Express, открывается браузер и запускается главная страница приложения.</span><span class="sxs-lookup"><span data-stu-id="09d1f-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="09d1f-194">Можно добавить новую задачу, которая будет добавлена в базу данных MongoDB, выполняемую на виртуальной машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![Приложение "My Task List"][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="09d1f-196">Публикация в веб-приложения службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="09d1f-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="09d1f-197">В этом разделе внесенные изменения будут опубликованы в веб-приложения службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="09d1f-198">В обозревателе решений щелкните правой кнопкой мыши **MyTaskListApp** и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="09d1f-199">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="09d1f-200">Веб-приложение будет работать в службе приложений Azure и получит доступ к базе данных MongoDB на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="09d1f-201">Сводка</span><span class="sxs-lookup"><span data-stu-id="09d1f-201">Summary</span></span>
<span data-ttu-id="09d1f-202">Вы успешно развернули приложение ASP.NET в веб-приложениях службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="09d1f-203">Просмотр веб-приложения</span><span class="sxs-lookup"><span data-stu-id="09d1f-203">To view the web app:</span></span>

1. <span data-ttu-id="09d1f-204">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="09d1f-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="09d1f-205">Нажмите **Веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="09d1f-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="09d1f-206">Выберите веб-приложение из списка **Веб-приложения** .</span><span class="sxs-lookup"><span data-stu-id="09d1f-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="09d1f-207">Дополнительные сведения о разработке приложений C# для MongoDB см. в [центре языка CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="09d1f-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp
