---
title: "aaaUse Azure Cosmos DB API для MongoDB toobuild веб-приложения | Документы Microsoft"
description: "Azure Cosmos DB учебник, в котором создается веб-приложение базы данных в сети, используя hello API для MongoDB."
keywords: "примеры mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="7fea9-104">Azure Cosmos DB: Подключение tooa MongoDB приложения, с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="7fea9-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="7fea9-105">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7fea9-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7fea9-106">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="7fea9-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7fea9-107">В этом учебнике показано, как Azure Cosmos DB учетной записи с помощью toocreate hello портал Azure и как hello toocreate базы данных коллекции toostore данных и с помощью [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7fea9-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="7fea9-108">В этом учебнике hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="7fea9-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7fea9-109">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="7fea9-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="7fea9-110">обновили строку подключения;</span><span class="sxs-lookup"><span data-stu-id="7fea9-110">Update your connection string</span></span>
> * <span data-ttu-id="7fea9-111">создание приложения MongoDB на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="7fea9-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="7fea9-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="7fea9-112">Create a database account</span></span>

<span data-ttu-id="7fea9-113">Давайте начнем с создания учетной записи Azure Cosmos DB в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7fea9-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="7fea9-114">Уже есть учетная запись Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="7fea9-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="7fea9-115">Если Да, пропустить слишком[Настройка решения Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="7fea9-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="7fea9-116">У вас была учетная запись Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="7fea9-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="7fea9-117">Если таким образом, учетной записи теперь учетную запись Azure Cosmos DB и можно сразу перейти слишком[Настройка решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7fea9-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="7fea9-118">Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить решение Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7fea9-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="7fea9-119">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="7fea9-119">Update your connection string</span></span>

1. <span data-ttu-id="7fea9-120">В hello в hello портале Azure **Azure Cosmos DB** выберите hello API для учетной записи MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7fea9-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="7fea9-121">В левой панели hello колонка hello учетной записи, нажмите кнопку **краткого**.</span><span class="sxs-lookup"><span data-stu-id="7fea9-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="7fea9-122">Выберите платформу (*драйвер .NET*, *Node.js*, *Java*, *Python* или *оболочка MongoDB*).</span><span class="sxs-lookup"><span data-stu-id="7fea9-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="7fea9-123">Если соответствующего драйвера или средства нет в списке, не беспокойтесь, мы постоянно добавляем дополнительные фрагменты кода для подключения.</span><span class="sxs-lookup"><span data-stu-id="7fea9-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="7fea9-124">Скопируйте и вставьте фрагмент кода hello в приложении MongoDB и будут готовы toogo.</span><span class="sxs-lookup"><span data-stu-id="7fea9-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="7fea9-125">Настройка приложения MongoDB</span><span class="sxs-lookup"><span data-stu-id="7fea9-125">Set up your MongoDB app</span></span>

<span data-ttu-id="7fea9-126">Можно использовать hello [Создание веб-приложения в Azure, который подключается tooMongoDB, работающий на виртуальной машине](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) учебника с минимальными изменениями tooquickly установки приложения MongoDB (либо локально или опубликованного tooan веб-приложение Azure), подключается tooan API для учетной записи MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7fea9-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="7fea9-127">Выполните действия из учебника hello, с одно изменение.</span><span class="sxs-lookup"><span data-stu-id="7fea9-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="7fea9-128">Замените код Dal.cs hello это:</span><span class="sxs-lookup"><span data-stu-id="7fea9-128">Replace hello Dal.cs code with this:</span></span>

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
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
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
   
                MongoClient client = new MongoClient(settings);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClientSettings settings = new MongoClientSettings();
                settings.Server = new MongoServerAddress(host, 10255);
                settings.UseSsl = true;
                settings.SslSettings = new SslSettings();
                settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;
   
                MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
                MongoIdentityEvidence evidence = new PasswordEvidence(password);
   
                settings.Credentials = new List<MongoCredential>()
                {
                    new MongoCredential("SCRAM-SHA-1", identity, evidence)
                };
                MongoClient client = new MongoClient(settings);
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
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. <span data-ttu-id="7fea9-129">Измените следующие переменные в файлах Dal.cs hello в параметры учетной записи со страницы приветствия ключи hello портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7fea9-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="7fea9-130">Используйте приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7fea9-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7fea9-131">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fea9-131">Clean up resources</span></span>

<span data-ttu-id="7fea9-132">Если вы не будете toocontinue toouse это приложение, используйте следующие шаги toodelete все ресурсы, созданные этого учебника в hello портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7fea9-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="7fea9-133">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="7fea9-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="7fea9-134">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="7fea9-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fea9-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fea9-135">Next steps</span></span>

<span data-ttu-id="7fea9-136">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="7fea9-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7fea9-137">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="7fea9-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="7fea9-138">обновили строку подключения;</span><span class="sxs-lookup"><span data-stu-id="7fea9-138">Update your connection string</span></span>
> * <span data-ttu-id="7fea9-139">создание приложения MongoDB на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="7fea9-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="7fea9-140">Можно продолжить toohello следующее руководство и импортировать вашей tooAzure данных MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7fea9-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fea9-141">Перенос данных в DocumentDB с помощью mongoimport и mongorestore</span><span class="sxs-lookup"><span data-stu-id="7fea9-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

