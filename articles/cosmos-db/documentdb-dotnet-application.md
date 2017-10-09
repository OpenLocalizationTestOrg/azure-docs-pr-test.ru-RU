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
# <span data-ttu-id="647ea-105"><a name="_Toc395809351"></a>Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="647ea-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="647ea-106">.NET</span><span class="sxs-lookup"><span data-stu-id="647ea-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="647ea-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="647ea-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="647ea-108">Java</span><span class="sxs-lookup"><span data-stu-id="647ea-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="647ea-109">Python</span><span class="sxs-lookup"><span data-stu-id="647ea-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="647ea-110">toohighlight как можно эффективно использовать toostore Azure Cosmos DB и запрос документов JSON, эта статья содержит пошаговое руководство начала до конца, показывая, как toobuild приложения todo, с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="647ea-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="647ea-111">Hello задачи будут храниться в виде документов JSON в базе данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="647ea-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Снимок экрана списка поручений hello веб-приложение MVC, созданные из этого учебника — ASP NET MVC учебника шаг за шагом](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="647ea-113">Это пошаговое руководство показывает, как toouse hello Azure Cosmos DB службы toostore и доступ к данным из веб-приложения ASP.NET MVC, размещенные в Azure.</span><span class="sxs-lookup"><span data-stu-id="647ea-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="647ea-114">Если вы ищете учебник, в котором рассматривается только Azure Cosmos DB, и не hello компоненты ASP.NET MVC отображаются [построения консольного приложения Azure Cosmos DB C#](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="647ea-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="647ea-115">Предполагается, что у вас есть опыт использования ASP.NET MVC и веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="647ea-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="647ea-116">Новый tooASP.NET или hello [готовности к установке средства](#_Toc395637760), рекомендуется загрузить проект полный образец hello из [GitHub] [ GitHub] и следуя инструкциям hello в этом примере.</span><span class="sxs-lookup"><span data-stu-id="647ea-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="647ea-117">После построения, можно просмотреть этой статьи toogain подробные сведения о кода hello в контексте hello hello проекта.</span><span class="sxs-lookup"><span data-stu-id="647ea-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="647ea-118"><a name="_Toc395637760"></a>Предварительные требования для изучения этого учебника по базам данных</span><span class="sxs-lookup"><span data-stu-id="647ea-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="647ea-119">Перед выполнением инструкции hello в этой статье, следует убедиться, что имеется следующее hello:</span><span class="sxs-lookup"><span data-stu-id="647ea-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="647ea-120">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="647ea-120">An active Azure account.</span></span> <span data-ttu-id="647ea-121">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="647ea-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="647ea-122">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="647ea-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="647ea-123">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="647ea-123">OR</span></span>

    <span data-ttu-id="647ea-124">Локальная установка hello [DB эмулятор Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="647ea-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="647ea-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="647ea-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="647ea-126">Microsoft Azure SDK для .NET для Visual Studio 2017 г., доступны через hello установщик Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="647ea-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="647ea-127">Все снимки экрана приветствия в этой статье были выполнены с помощью Microsoft Visual Studio Community 2017 г..</span><span class="sxs-lookup"><span data-stu-id="647ea-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="647ea-128">Если система настроена с помощью другой версии экраны и параметры могут не соответствовать полностью, однако если соблюдаются hello выше необходимые условия Это решение должно работать.</span><span class="sxs-lookup"><span data-stu-id="647ea-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="647ea-129"><a name="_Toc395637761"></a>Шаг 1. Создание учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="647ea-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="647ea-130">Давайте сначала создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="647ea-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="647ea-131">Если вы уже учетной записи SQL (DocumentDB) для Azure Cosmos DB или при использовании hello эмулятор DB Cosmos Azure для этого учебника, можно пропустить слишком[Создание нового приложения ASP.NET MVC](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="647ea-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="647ea-132">Теперь мы рассмотрим как toocreate нового приложения ASP.NET MVC от hello основ.</span><span class="sxs-lookup"><span data-stu-id="647ea-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="647ea-133"><a name="_Toc395637762"></a>Шаг 2. Создание нового приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="647ea-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="647ea-134">В Visual Studio в hello **файл** меню выберите пункт слишком**New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="647ea-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="647ea-135">Hello **новый проект** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="647ea-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="647ea-136">В hello **типов проектов** области, разверните **шаблоны**, **Visual C#**, **Web**и выберите **веб-приложение ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="647ea-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Снимок диалогового окна нового проекта hello с выделенной тип проекта веб-приложения ASP.NET hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="647ea-138">В hello **имя** введите имя hello hello проекта.</span><span class="sxs-lookup"><span data-stu-id="647ea-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="647ea-139">В этом учебнике используется имя hello «todo».</span><span class="sxs-lookup"><span data-stu-id="647ea-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="647ea-140">При выборе toouse нечто, отличное от этого, затем везде, где этот учебник рассмотрен hello todo пространства имен, необходимо toouse образцы кода hello предоставленный tooadjust все, что вы с именем приложения.</span><span class="sxs-lookup"><span data-stu-id="647ea-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="647ea-141">Нажмите кнопку **Обзор** toonavigate toohello папку, где бы как toocreate hello проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="647ea-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="647ea-142">Hello **новое веб-приложение ASP.NET** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="647ea-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Снимок экрана: hello диалоговое окно нового веб-приложения ASP.NET с hello шаблона MVC-приложения выделяются](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="647ea-144">В области "Шаблоны" hello, выберите **MVC**.</span><span class="sxs-lookup"><span data-stu-id="647ea-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="647ea-145">Нажмите кнопку **ОК** и позволяют выполнить эту операцию вокруг формирование шаблонов hello пустого шаблона ASP.NET MVC Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="647ea-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="647ea-146">После завершения создания hello шаблона MVC-приложения Visual Studio вы сможете пустое приложение ASP.NET, можно выполнять локально.</span><span class="sxs-lookup"><span data-stu-id="647ea-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="647ea-147">Локально, так как я уверен, что у нас все замеченный hello ASP.NET «Hello World» будут пропущены, запущенном проекте hello приложения.</span><span class="sxs-lookup"><span data-stu-id="647ea-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="647ea-148">Давайте рассмотрим прямой tooadding Azure Cosmos DB toothis проекта и построение приложения.</span><span class="sxs-lookup"><span data-stu-id="647ea-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="647ea-149"><a name="_Toc395637767"></a>Шаг 3: Добавление проекта веб-приложения MVC tooyour Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="647ea-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="647ea-150">Теперь, когда у нас есть большая часть коммуникационного hello ASP.NET MVC, необходимую для этого решения, давайте toohello реальная цель этого учебника, Добавление веб-приложение MVC tooour Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="647ea-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="647ea-151">Hello Azure Cosmos DB .NET SDK упаковывается и распространяется в виде пакета NuGet.</span><span class="sxs-lookup"><span data-stu-id="647ea-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="647ea-152">tooget Здравствуйте пакета NuGet в Visual Studio, используйте диспетчер пакетов NuGet hello в Visual Studio, щелкнув проект hello в **обозревателе решений** и выбрав **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="647ea-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Снимок экрана: hello контекстное меню для проекта веб-приложения hello в окне обозревателя решений с управление пакетами NuGet выделяются.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="647ea-154">Hello **управление пакетами NuGet** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="647ea-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="647ea-155">В hello NuGet **Обзор** введите ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="647ea-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="647ea-156">(имя пакета hello еще не обновленные tooAzure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="647ea-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="647ea-157">На основе результатов hello установить hello **Microsoft.Azure.DocumentDB корпорацией Майкрософт** пакета.</span><span class="sxs-lookup"><span data-stu-id="647ea-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="647ea-158">Это будет загрузить и установить пакет Azure Cosmos DB hello, а также все зависимости, такие как Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="647ea-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="647ea-159">Нажмите кнопку **ОК** в hello **предварительного просмотра** окна, и **принимаю** в hello **принятия условий лицензионного соглашения** установки hello toocomplete окна.</span><span class="sxs-lookup"><span data-stu-id="647ea-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Снимок Sreen окне Управление пакетами NuGet hello hello выделяются клиентской библиотеки Microsoft Azure DocumentDB](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="647ea-161">Кроме того, можно использовать hello пакета hello tooinstall консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="647ea-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="647ea-162">toodo в этом случае на hello **средства** меню, нажмите кнопку **диспетчера пакетов NuGet**и нажмите кнопку **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="647ea-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="647ea-163">В строке приветствия введите ниже hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="647ea-164">После установки пакета hello решения Visual Studio должен выглядеть в две новые ссылки добавлен, Microsoft.Azure.Documents.Client и Newtonsoft.Json следующим hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Снимок Sreen две ссылки hello добавлены toohello JSON данных проекта в обозревателе решений](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="647ea-166"><a name="_Toc395637763"></a>Шаг 4: Настройка hello приложение ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="647ea-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="647ea-167">Теперь добавим hello модели, представления и контроллеры toothis MVC-приложения:</span><span class="sxs-lookup"><span data-stu-id="647ea-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="647ea-168">[Добавление модели](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="647ea-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="647ea-169">[Добавление контроллера](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="647ea-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="647ea-170">[Добавление представлений](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="647ea-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="647ea-171"><a name="_Toc395637764"></a>Добавление модели данных JSON</span><span class="sxs-lookup"><span data-stu-id="647ea-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="647ea-172">Давайте начнем с создания hello **M** в MVC hello модели.</span><span class="sxs-lookup"><span data-stu-id="647ea-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="647ea-173">В **обозреватель решений**, щелкните правой кнопкой мыши hello **моделей** папку, нажмите кнопку **добавить**и нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="647ea-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="647ea-174">Hello **Добавление нового элемента** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="647ea-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="647ea-175">Назовите новый класс **Item.cs** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="647ea-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="647ea-176">В этом new **Item.cs** файл, добавьте следующее hello после hello последнего *с помощью инструкции*.</span><span class="sxs-lookup"><span data-stu-id="647ea-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="647ea-177">Теперь замените этот код</span><span class="sxs-lookup"><span data-stu-id="647ea-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="647ea-178">с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="647ea-178">with hello following code.</span></span>
   
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
   
    <span data-ttu-id="647ea-179">Все данные в базе данных Azure Cosmos передается по сети hello и хранятся в виде JSON.</span><span class="sxs-lookup"><span data-stu-id="647ea-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="647ea-180">toocontrol hello способ объектов сериализовать и десериализовать JSON.NET, можно использовать hello **JsonProperty** атрибута, как показано в hello **элемент** только что созданный класс.</span><span class="sxs-lookup"><span data-stu-id="647ea-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="647ea-181">Вы не **имеют** toodo это, но я требуется tooensure, Мои свойств следовать camelCase JSON hello соглашения об именовании.</span><span class="sxs-lookup"><span data-stu-id="647ea-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="647ea-182">Не только можно ли управлять hello формат имени свойства hello при переходе в JSON, но можно полностью переименовать свои свойства .NET, как я сделал с hello **описание** свойство.</span><span class="sxs-lookup"><span data-stu-id="647ea-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="647ea-183"><a name="_Toc395637765"></a>Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="647ea-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="647ea-184">Берет на себя hello **M**, а теперь давайте создадим hello **C** в класс контроллера MVC.</span><span class="sxs-lookup"><span data-stu-id="647ea-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="647ea-185">В **обозреватель решений**, щелкните правой кнопкой мыши hello **контроллеров** папку, нажмите кнопку **добавить**и нажмите кнопку **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="647ea-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="647ea-186">Hello **Добавление формирования шаблонов** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="647ea-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="647ea-187">Выберите **Контроллер MVC 5 — пустой** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="647ea-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Диалоговое окно Добавление формирования шаблонов hello с hello контроллер MVC 5 - пустой параметр выделен снимок экрана](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="647ea-189">Назовите новый контроллер **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="647ea-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Снимок экрана: диалоговое окно добавления контроллера hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="647ea-191">После создания файла hello решения Visual Studio должна иметь вид следующие hello с использованием нового файла ItemController.cs hello в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="647ea-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="647ea-192">также показывается Hello Item.cs файл создан в более ранней версии.</span><span class="sxs-lookup"><span data-stu-id="647ea-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Hello решения Visual Studio - обозреватель решений с hello новый ItemController.cs и Item.cs файлы выделяются снимок экрана](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="647ea-194">Вы можете закрыть ItemController.cs, мы вернемся tooit позже.</span><span class="sxs-lookup"><span data-stu-id="647ea-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="647ea-195"><a name="_Toc395637766"></a>Добавление представлений</span><span class="sxs-lookup"><span data-stu-id="647ea-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="647ea-196">Теперь давайте создадим hello **V** в MVC hello представления:</span><span class="sxs-lookup"><span data-stu-id="647ea-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="647ea-197">[Добавление представления «Индекс элементов»](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="647ea-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="647ea-198">[Добавление представления «Создание элементов»](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="647ea-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="647ea-199">[Добавление представления «Редактирование элементов»](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="647ea-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="647ea-200"><a name="AddItemIndexView"></a>Добавление представления «Индекс элементов»</span><span class="sxs-lookup"><span data-stu-id="647ea-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="647ea-201">В **обозревателе решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши hello пустой **элемент** созданную папку Visual Studio автоматически при добавлении hello  **ItemController** ранее, нажмите кнопку **добавить**, а затем нажмите кнопку **представление**.</span><span class="sxs-lookup"><span data-stu-id="647ea-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![В обозревателе решений папку элемента hello, созданным Visual Studio с выделенной команды Добавить представление hello (снимок экрана)](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="647ea-203">В hello **добавить представление** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="647ea-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="647ea-204">В hello **имя представления** введите ***индекса***.</span><span class="sxs-lookup"><span data-stu-id="647ea-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="647ea-205">В hello **шаблона** выберите ***списка***.</span><span class="sxs-lookup"><span data-stu-id="647ea-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="647ea-206">В hello **класс модели** выберите ***элемента (todo. Модели)***.</span><span class="sxs-lookup"><span data-stu-id="647ea-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="647ea-207">Введите в поле макет страницы приветствия ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="647ea-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Диалоговое окно добавления представления hello снимок экрана](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="647ea-209">После установки этих значений нажмите **Добавить** , и Visual Studio создаст представление.</span><span class="sxs-lookup"><span data-stu-id="647ea-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="647ea-210">После его завершения, он будет открыт файл cshtml hello, который был создан.</span><span class="sxs-lookup"><span data-stu-id="647ea-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="647ea-211">Как мы вернемся tooit позже можно закрыть этот файл в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="647ea-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="647ea-212"><a name="AddNewIndexView"></a>Добавление представления «Создание элементов»</span><span class="sxs-lookup"><span data-stu-id="647ea-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="647ea-213">Аналогичные toohow, мы создали **индекс элемента** представление, создадим новое представление для создания новых **элементы**.</span><span class="sxs-lookup"><span data-stu-id="647ea-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="647ea-214">В **обозреватель решений**, щелкните правой кнопкой мыши hello **элемента** папку еще раз, нажмите кнопку **добавить**и нажмите кнопку **представление**.</span><span class="sxs-lookup"><span data-stu-id="647ea-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="647ea-215">В hello **добавить представление** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="647ea-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="647ea-216">В hello **имя представления** введите ***создать***.</span><span class="sxs-lookup"><span data-stu-id="647ea-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="647ea-217">В hello **шаблона** выберите ***создать***.</span><span class="sxs-lookup"><span data-stu-id="647ea-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="647ea-218">В hello **класс модели** выберите ***элемента (todo. Модели)***.</span><span class="sxs-lookup"><span data-stu-id="647ea-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="647ea-219">Введите в поле макет страницы приветствия ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="647ea-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="647ea-220">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="647ea-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="647ea-221"><a name="_Toc395888515"></a>Добавление представления «Редактирование элементов»</span><span class="sxs-lookup"><span data-stu-id="647ea-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="647ea-222">И наконец, добавьте одно последнее представление для редактирования **элемент** в hello так же как и раньше.</span><span class="sxs-lookup"><span data-stu-id="647ea-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="647ea-223">В **обозреватель решений**, щелкните правой кнопкой мыши hello **элемента** папку еще раз, нажмите кнопку **добавить**и нажмите кнопку **представление**.</span><span class="sxs-lookup"><span data-stu-id="647ea-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="647ea-224">В hello **добавить представление** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="647ea-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="647ea-225">В hello **имя представления** введите ***изменить***.</span><span class="sxs-lookup"><span data-stu-id="647ea-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="647ea-226">В hello **шаблона** выберите ***изменить***.</span><span class="sxs-lookup"><span data-stu-id="647ea-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="647ea-227">В hello **класс модели** выберите ***элемента (todo. Модели)***.</span><span class="sxs-lookup"><span data-stu-id="647ea-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="647ea-228">Введите в поле макет страницы приветствия ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="647ea-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="647ea-229">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="647ea-229">Click **Add**.</span></span>

<span data-ttu-id="647ea-230">После этого, закройте все документы cshtml hello в Visual Studio, как мы вернет toothese представления позже.</span><span class="sxs-lookup"><span data-stu-id="647ea-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="647ea-231"><a name="_Toc395637769"></a>Шаг 5. Подключение Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="647ea-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="647ea-232">Теперь, когда уже обеспечена hello стандартные действия MVC, давайте рассмотрим tooadding hello кода для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="647ea-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="647ea-233">В этом разделе мы добавим код toohandle hello следующее:</span><span class="sxs-lookup"><span data-stu-id="647ea-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="647ea-234">[Вывод списка незавершенных элементов](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="647ea-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="647ea-235">[Добавление элементов](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="647ea-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="647ea-236">[Редактирование элементов](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="647ea-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="647ea-237"><a name="_Toc395637770"></a>Отображение незавершенных элементов в веб-приложении MVC</span><span class="sxs-lookup"><span data-stu-id="647ea-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="647ea-238">Hello первый toodo вещь здесь добавить класс, содержащий hello логику tooconnect tooand используют базу данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="647ea-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="647ea-239">В этом учебнике мы будем инкапсулировать эту логику в класс tooa репозиторий с именем DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="647ea-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="647ea-240">В **обозревателе решений**, правой кнопкой мыши проект hello, нажмите кнопку **добавить**, а затем нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="647ea-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="647ea-241">Имя нового класса hello **DocumentDBRepository** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="647ea-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="647ea-242">В только что созданный hello **DocumentDBRepository** и добавьте следующее hello *с помощью инструкций* выше hello *имен* объявления</span><span class="sxs-lookup"><span data-stu-id="647ea-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="647ea-243">Теперь замените этот код</span><span class="sxs-lookup"><span data-stu-id="647ea-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="647ea-244">с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="647ea-244">with hello following code.</span></span>
   
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
   
    
3. <span data-ttu-id="647ea-245">Мы читаете некоторые значения из конфигурации, поэтому откройте hello **Web.config** файла приложения и добавьте следующие строки под заголовком hello hello `<AppSettings>` раздела.</span><span class="sxs-lookup"><span data-stu-id="647ea-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="647ea-246">Теперь обновите значения hello *конечной точки* и *authKey* с помощью ключей колонке hello hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="647ea-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="647ea-247">Использовать hello **URI** из колонки hello ключей в качестве значения hello приветствия конечной точки и используйте hello **ПЕРВИЧНОГО ключа**, или **ВТОРИЧНЫЙ ключ** из колонки hello ключей в качестве значения hello hello значение параметра authKey.</span><span class="sxs-lookup"><span data-stu-id="647ea-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="647ea-248">Что позаботится о подключения хранилища Azure Cosmos DB hello, теперь позволяет добавить логику приложения.</span><span class="sxs-lookup"><span data-stu-id="647ea-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="647ea-249">Hello первое, что нам нужно будет toodo toobe с приложения списка задач — toodisplay hello неполных элементов.</span><span class="sxs-lookup"><span data-stu-id="647ea-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="647ea-250">Скопируйте и вставьте следующий фрагмент кода в любом месте в пределах hello hello **DocumentDBRepository** класса.</span><span class="sxs-lookup"><span data-stu-id="647ea-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="647ea-251">Откройте hello **ItemController** мы добавленный ранее и добавьте следующее hello *с помощью инструкций* выше hello объявление пространства имен.</span><span class="sxs-lookup"><span data-stu-id="647ea-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="647ea-252">Если проект не называется «todo», то вам требуется tooupdate с помощью рабочих элементов». Моделей»; tooreflect hello имя проекта.</span><span class="sxs-lookup"><span data-stu-id="647ea-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="647ea-253">Теперь замените этот код</span><span class="sxs-lookup"><span data-stu-id="647ea-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="647ea-254">с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="647ea-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="647ea-255">Откройте **Global.asax.cs** и добавьте следующие строки toohello hello **Application_Start** метод</span><span class="sxs-lookup"><span data-stu-id="647ea-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="647ea-256">На этом этапе решение должно быть возможности toobuild без ошибок.</span><span class="sxs-lookup"><span data-stu-id="647ea-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="647ea-257">Если вы запустили приложение hello, следует перейти toohello **HomeController** и hello **индекс** представление этого контроллера.</span><span class="sxs-lookup"><span data-stu-id="647ea-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="647ea-258">Это поведение по умолчанию hello hello MVC шаблона проекта мы выбрали в начале hello, но мы не хотим!</span><span class="sxs-lookup"><span data-stu-id="647ea-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="647ea-259">Изменим hello маршрутизации на этом tooalter приложения MVC это поведение.</span><span class="sxs-lookup"><span data-stu-id="647ea-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="647ea-260">Откройте ***приложения\_Start\RouteConfig.cs*** и найдите строку hello, начиная с «значения по умолчанию:» и измените его hello tooresemble следующие.</span><span class="sxs-lookup"><span data-stu-id="647ea-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="647ea-261">Теперь сообщает ASP.NET MVC, если вы не указали значение в URL-адрес toocontrol hello hello поведения маршрутизации, чтобы вместо **Главная**, используйте **элемент** как контроллер hello и пользователь **индекса** как представление hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="647ea-262">Теперь при запуске приложения hello, он будет вызывать ваш **ItemController** которого будет вызова в классе toohello репозитория и использовать метод tooreturn hello GetItems все toohello неполных элементов hello **представления** \\ **Элемент**\\**индекс** представления.</span><span class="sxs-lookup"><span data-stu-id="647ea-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="647ea-263">Если создать и запустить этот проект сейчас, отобразится примерно следующие данные.</span><span class="sxs-lookup"><span data-stu-id="647ea-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Снимок экрана: hello список todo веб-приложения, созданные из этого учебника базы данных](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="647ea-265"><a name="_Toc395637771"></a>Добавление элементов</span><span class="sxs-lookup"><span data-stu-id="647ea-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="647ea-266">Скажем некоторые элементы в базу данных, у нас есть больше, чем пустая сетка toolook на.</span><span class="sxs-lookup"><span data-stu-id="647ea-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="647ea-267">Давайте добавим код слишком Azure Cosmos DBRepository и ItemController toopersist hello записи в базу данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="647ea-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="647ea-268">Добавьте следующий метод tooyour hello **DocumentDBRepository** класса.</span><span class="sxs-lookup"><span data-stu-id="647ea-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="647ea-269">Этот метод принимает объект, переданный tooit и сохраняет ее в базе данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="647ea-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="647ea-270">Откройте файл ItemController.cs hello и добавьте следующий фрагмент кода в классе hello hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="647ea-271">Это известно как ASP.NET MVC, какие toodo для hello **создать** действие.</span><span class="sxs-lookup"><span data-stu-id="647ea-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="647ea-272">В этом случае просто отрисовки hello связанное представление Create.cshtml, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="647ea-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="647ea-273">Теперь мы должны код в этот контроллер, принимается hello отправки с hello **создать** представления.</span><span class="sxs-lookup"><span data-stu-id="647ea-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="647ea-274">Добавьте следующий блок кода toohello ItemController.cs класс, который сообщает, какие toodo формы POST для этого контроллера ASP.NET MVC hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="647ea-275">Этот код вызывает в toohello DocumentDBRepository и использует hello CreateItemAsync метод toopersist hello новой todo элемента toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="647ea-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="647ea-276">**Примечание по безопасности**: hello **ValidateAntiForgeryToken** используется атрибут здесь toohelp защиты этого приложения от атак с подделкой межсайтовых запросов.</span><span class="sxs-lookup"><span data-stu-id="647ea-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="647ea-277">Имеется несколько tooit, чем просто добавлять этот атрибут, представлений должны toowork с данным маркером защиты от подделки.</span><span class="sxs-lookup"><span data-stu-id="647ea-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="647ea-278">Для получения дополнительных сведений об тема hello и примеры как tooimplement это неправильно, см. в разделе [препятствует подделки межсайтовых запросов][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="647ea-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="647ea-279">Здравствуйте, исходный код на [GitHub] [ GitHub] имеет полную реализацию hello на месте.</span><span class="sxs-lookup"><span data-stu-id="647ea-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="647ea-280">**Примечание по безопасности**: мы также используем hello **привязки** атрибута toohelp параметр метода hello защититься от излишней учета атак.</span><span class="sxs-lookup"><span data-stu-id="647ea-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="647ea-281">Дополнительные сведения см. в записи блога [Основные операции CRUD в ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="647ea-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="647ea-282">Это заключительный шаг hello код, необходимый tooadd новые элементы tooour базы данных.</span><span class="sxs-lookup"><span data-stu-id="647ea-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="647ea-283"><a name="_Toc395637772"></a>Редактирование элементов</span><span class="sxs-lookup"><span data-stu-id="647ea-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="647ea-284">Есть кое-что нам toodo, и это tooedit возможность hello tooadd **элементы** в базе данных hello и toomark их завершения.</span><span class="sxs-lookup"><span data-stu-id="647ea-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="647ea-285">Hello представление для редактирования уже была добавлена toohello проекта, так нам нужна лишь tooadd иной код контроллера tooour и toohello **DocumentDBRepository** класса еще раз.</span><span class="sxs-lookup"><span data-stu-id="647ea-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="647ea-286">Добавьте следующие toohello hello **DocumentDBRepository** класса.</span><span class="sxs-lookup"><span data-stu-id="647ea-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="647ea-287">Здравствуйте, первый из этих методов, **GetItem** извлекает элемент из DB Cosmos Azure, которая передается назад toohello **ItemController** и затем на toohello **изменить** представления.</span><span class="sxs-lookup"><span data-stu-id="647ea-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="647ea-288">Здравствуйте, второй hello методов мы только что добавили hello заменяет **документа** в Azure DB Cosmos с версией hello hello **документа** hello, передаваемые в **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="647ea-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="647ea-289">Добавьте следующие toohello hello **ItemController** класса.</span><span class="sxs-lookup"><span data-stu-id="647ea-289">Add hello following toohello **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="647ea-290">Hello первый метод обрабатывает hello Http GET, которое происходит при нажатии пользователем hello на hello **изменить** ссылка из hello **индекс** представления.</span><span class="sxs-lookup"><span data-stu-id="647ea-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="647ea-291">Этот метод извлекает [ **документа** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) из базы данных Azure Cosmos и передает его toohello **изменить** представления.</span><span class="sxs-lookup"><span data-stu-id="647ea-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="647ea-292">Hello **изменить** представление будет выполните Http POST toohello **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="647ea-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="647ea-293">Второй метод Hello, мы добавили дескрипторы передачи обновлены hello объекта tooAzure Cosmos DB toobe сохраняются в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="647ea-294">Верно, который является все, что нам нужно toorun нашего приложения, список неполный **элементы**, добавить новые **элементы**и изменение **элементы**.</span><span class="sxs-lookup"><span data-stu-id="647ea-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="647ea-295"><a name="_Toc395637773"></a>Шаг 6: Запуск приложения hello локально</span><span class="sxs-lookup"><span data-stu-id="647ea-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="647ea-296">приложение hello tootest на локальном компьютере, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="647ea-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="647ea-297">Нажмите клавишу F5 в Visual Studio toobuild hello приложения в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="647ea-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="647ea-298">Его следует построить приложение hello и запустить браузер с hello пустая страница «Сетка», мы видели до:</span><span class="sxs-lookup"><span data-stu-id="647ea-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Снимок экрана: hello список todo веб-приложения, созданные из этого учебника базы данных](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="647ea-300">Нажмите кнопку hello **создать новый** ссылку и добавьте значения toohello **имя** и **описание** поля.</span><span class="sxs-lookup"><span data-stu-id="647ea-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="647ea-301">Оставьте hello **завершено** флажок не выбран, в противном случае hello новый **элемент** будут добавлены в завершенном состоянии и не будет отображаться на исходный список hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Снимок экрана: hello представления создания](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="647ea-303">Нажмите кнопку **создать** и являются перенаправленный назад toohello **индекс** представление и **элемент** отображается в списке hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Снимок экрана: hello представлении индекса](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="647ea-305">Чувствовать себя свободного tooadd еще несколько **элементы** tooyour списка задач.</span><span class="sxs-lookup"><span data-stu-id="647ea-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="647ea-306">Нажмите кнопку **изменить** Далее tooan **элемент** на списке hello, берутся toohello **изменить** представление, где можно обновить любое свойство объекта, в том числе hello  **Завершено** флаг.</span><span class="sxs-lookup"><span data-stu-id="647ea-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="647ea-307">Если пометить hello **завершить** пометить и выберите **Сохранить**, hello **элемент** удаляется из списка hello незавершенные задачи.</span><span class="sxs-lookup"><span data-stu-id="647ea-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Снимок экрана: hello представление Index этот флажок установлен, в котором выполнено hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="647ea-309">После тестирования приложения hello, нажмите клавиши Ctrl + F5 toostop отладки приложение hello.</span><span class="sxs-lookup"><span data-stu-id="647ea-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="647ea-310">Вы будете готовы toodeploy!</span><span class="sxs-lookup"><span data-stu-id="647ea-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="647ea-311"><a name="_Toc395637774"></a>Шаг 7: Разверните приложение hello tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="647ea-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="647ea-312">Теперь, когда полное приложение hello правильность работы с Azure Cosmos DB мы будем toodeploy этот web app tooAzure службы приложений.</span><span class="sxs-lookup"><span data-stu-id="647ea-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="647ea-313">— Это все приложение, необходимо toodo toopublish правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="647ea-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Снимок экрана: hello параметр публикации в обозревателе решений](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="647ea-315">В hello **публикации** диалоговое окно, нажмите кнопку **службу приложений Microsoft Azure**, а затем выберите **создать новый** toocreate службы приложения профиля, или нажмите кнопку **выберите Существующие** toouse существующего профиля.</span><span class="sxs-lookup"><span data-stu-id="647ea-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Диалоговое окно "Публикация" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="647ea-317">При наличии существующего профиля службы приложений Azure введите имя своей подписки.</span><span class="sxs-lookup"><span data-stu-id="647ea-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="647ea-318">Используйте hello **представление** отфильтровать toosort группы ресурсов или тип ресурса, а затем выберите службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="647ea-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Диалоговое окно "Служба приложений" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="647ea-320">Щелкните toocreate профиля службы приложений Azure, **создать новый** в hello **публикации** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="647ea-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="647ea-321">В hello **Создание приложения службы** диалоговое окно, введите имя веб-приложения и соответствующие подписки, группы ресурсов и план служб приложений, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="647ea-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Диалоговое окно "Создать службу приложений" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="647ea-323">Через несколько секунд Visual Studio завершит публикацию вашего веб-приложения и запустит браузер, где вы увидите свое творение, запущенное в Azure!</span><span class="sxs-lookup"><span data-stu-id="647ea-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="647ea-324"><a name="_Toc395637775"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="647ea-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="647ea-325">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="647ea-325">Congratulations!</span></span> <span data-ttu-id="647ea-326">Просто построен вашего первого ASP.NET MVC, веб-приложения, использующие Azure Cosmos DB и публикации его tooAzure.</span><span class="sxs-lookup"><span data-stu-id="647ea-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="647ea-327">Здравствуйте, исходный код для завершения приложения hello, включая подробные hello и удалите функции, которые не были включены в это учебника можно скачать или клоном [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="647ea-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="647ea-328">Поэтому если вы заинтересованы в добавлении tooyour приложение, захватите кода hello и добавьте его toothis приложения.</span><span class="sxs-lookup"><span data-stu-id="647ea-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="647ea-329">Дополнительные функциональные возможности tooyour tooadd приложения, просмотрите hello API-интерфейса в hello [библиотеки .NET DB Cosmos Azure](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) привычной свободного toocontribute toohello библиотеки .NET DB Cosmos Azure на [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="647ea-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
