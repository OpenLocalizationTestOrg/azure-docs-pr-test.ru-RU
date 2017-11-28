---
title: "Руководство по ASP.NET MVC для Azure Cosmos DB. Разработка веб-приложения | Документация Майкрософт"
description: "Это руководство по MVC для ASP.NET поможет вам создать веб-приложение MVC с использованием Azure Cosmos DB. С помощью этого руководства по ASP NET MVC вы сможете сохранить файл JSON и получить доступ к данным из приложения \"Список дел\", размещенного на веб-сайтах Azure."
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
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="adae6-105"><a name="_Toc395809351"></a>Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="adae6-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="adae6-106">.NET</span><span class="sxs-lookup"><span data-stu-id="adae6-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="adae6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="adae6-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="adae6-108">Java</span><span class="sxs-lookup"><span data-stu-id="adae6-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="adae6-109">Python</span><span class="sxs-lookup"><span data-stu-id="adae6-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="adae6-110">Чтобы показать, как эффективно использовать Azure Cosmos DB для хранения документов JSON и их запроса, в этой статье приведена пошаговая инструкция для создания приложения со списком задач с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="adae6-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="adae6-111">Задачи будут храниться в виде документов JSON в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="adae6-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Снимок экрана: веб-приложение "Список дел", созданное с помощью этого руководства. Пошаговое руководство по ASP.NET MVC](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="adae6-113">В этом пошаговом руководстве показан пример использования службы Azure Cosmos DB для хранения данных и доступа к ним из веб-приложения MVC для ASP.NET, размещенного на платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="adae6-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="adae6-114">Если вы ищете руководство, в котором рассматривается только Azure Cosmos DB, а не компоненты ASP.NET MVC, дополнительные сведения см. в статье о [создании консольного приложения Azure Cosmos DB на языке C#](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="adae6-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="adae6-115">Предполагается, что у вас есть опыт использования ASP.NET MVC и веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="adae6-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="adae6-116">Если вы никогда не работали с ASP.NET или [необходимыми инструментами](#_Toc395637760), мы рекомендуем скачать полный пример проекта с портала [GitHub][GitHub] и следовать инструкциям в этом примере.</span><span class="sxs-lookup"><span data-stu-id="adae6-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="adae6-117">После выполнения сборки вы можете просмотреть эту статью, чтобы разобраться в коде этого проекта.</span><span class="sxs-lookup"><span data-stu-id="adae6-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="adae6-118"><a name="_Toc395637760"></a>Предварительные требования для изучения этого учебника по базам данных</span><span class="sxs-lookup"><span data-stu-id="adae6-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="adae6-119">Перед выполнением инструкций, приведенных в этой статье, следует убедиться, что установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="adae6-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="adae6-120">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="adae6-120">An active Azure account.</span></span> <span data-ttu-id="adae6-121">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="adae6-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="adae6-122">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="adae6-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="adae6-123">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="adae6-123">OR</span></span>

    <span data-ttu-id="adae6-124">Локальная установка [эмулятора Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="adae6-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="adae6-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="adae6-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="adae6-126">Пакет Microsoft Azure SDK для .NET (Visual Studio 2017), доступный через Visual Studio Installer.</span><span class="sxs-lookup"><span data-stu-id="adae6-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="adae6-127">Все снимки экранов в этой статье сделаны с помощью Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="adae6-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="adae6-128">Если система настроена с помощью другой версии, то вполне вероятно, что ваши экраны и параметры не будут соответствовать полностью, но если выполнить все вышеуказанные требования, то это решение должно работать.</span><span class="sxs-lookup"><span data-stu-id="adae6-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="adae6-129"><a name="_Toc395637761"></a>Шаг 1. Создание учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="adae6-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="adae6-130">Давайте сначала создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="adae6-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="adae6-131">Если у вас уже есть учетная запись SQL (DocumentDB) для Azure Cosmos DB или вы используете эмулятор Azure Cosmos DB для этого руководства, то вы можете перейти к разделу [Создание нового приложения ASP.NET MVC](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="adae6-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="adae6-132">Теперь рассмотрим создание нового приложения ASP.NET MVC с нуля.</span><span class="sxs-lookup"><span data-stu-id="adae6-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="adae6-133"><a name="_Toc395637762"></a>Шаг 2. Создание нового приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="adae6-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="adae6-134">В меню Visual Studio **Файл** выберите **Создать**, а затем щелкните **Проект**.</span><span class="sxs-lookup"><span data-stu-id="adae6-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="adae6-135">Откроется диалоговое окно **Новый проект** .</span><span class="sxs-lookup"><span data-stu-id="adae6-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="adae6-136">На панели **Типы проектов** разверните **Шаблоны**, **Visual C#**, **Веб**, а затем выберите **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="adae6-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Снимок экрана: диалоговое окно "Новый проект" с выделенным типа проекта веб-приложения ASP.NET](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="adae6-138">В поле **Имя** введите имя проекта.</span><span class="sxs-lookup"><span data-stu-id="adae6-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="adae6-139">В этом учебнике используется имя todo.</span><span class="sxs-lookup"><span data-stu-id="adae6-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="adae6-140">Если вы решили использовать другое имя, в ситуациях, когда будет идти речь о пространстве имен todo, вы должны будете откорректировать представленные образцы кода, используя имя своего приложения.</span><span class="sxs-lookup"><span data-stu-id="adae6-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="adae6-141">Щелкните **Обзор**, чтобы перейти к папке, в которой вы хотите создать проект, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="adae6-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="adae6-142">Отобразится диалоговое окно **Создание веб-приложения ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="adae6-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Снимок экрана: диалоговое окно "Создание веб-приложения ASP.NET" с выделенным шаблоном приложения MVC](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="adae6-144">На панели «Шаблоны» выберите **MVC**.</span><span class="sxs-lookup"><span data-stu-id="adae6-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="adae6-145">Нажмите кнопку **OK** , и Visual Studio создаст пустой шаблон ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="adae6-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="adae6-146">После того как Visual Studio закончит создание шаблонного приложения MVC, у вас будет пустое приложение ASP.NET, которое можно запустить локально.</span><span class="sxs-lookup"><span data-stu-id="adae6-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="adae6-147">Мы не станем запускать этот проект локально, потому что я уверена, что мы все видели приложение ASP.NET "Hello World".</span><span class="sxs-lookup"><span data-stu-id="adae6-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="adae6-148">Давайте перейдем к добавлению Azure Cosmos DB в этот проект и созданию приложения.</span><span class="sxs-lookup"><span data-stu-id="adae6-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="adae6-149"><a name="_Toc395637767"></a>Шаг 3. Добавление Azure Cosmos DB в проект веб-приложения MVC</span><span class="sxs-lookup"><span data-stu-id="adae6-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="adae6-150">Теперь, когда мы установили большую часть коммуникаций MVC для ASP.NET, необходимых для этого решения, перейдем к основной цели этого руководства, т. е. к добавлению Azure Cosmos DB в веб-приложение MVC.</span><span class="sxs-lookup"><span data-stu-id="adae6-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="adae6-151">Пакет .NET SDK для Azure Cosmos DB комплектуется и распространяется как пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="adae6-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="adae6-152">Чтобы получить пакет NuGet в Visual Studio, используйте диспетчер пакетов NuGet в Visual Studio: щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="adae6-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Снимок экрана параметров контекстного меню проекта веб-приложения в обозревателе решений с выделенным параметром "Управление пакетами NuGet".](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="adae6-154">Откроется диалоговое окно **Управление пакетами NuGet** .</span><span class="sxs-lookup"><span data-stu-id="adae6-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="adae6-155">В окне NuGet в поле **Обзор** введите ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="adae6-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="adae6-156">(Имя пакета не обновлено для Azure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="adae6-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="adae6-157">В результатах поиска найдите пакет **Microsoft.Azure.DocumentDB от корпорации Майкрософт** и установите его.</span><span class="sxs-lookup"><span data-stu-id="adae6-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="adae6-158">При этом будет загружен и установлен пакет Azure Cosmos DB, а также все зависимости, такие как Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="adae6-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="adae6-159">В окне **предварительного просмотра** щелкните **ОК**, после чего в окне **Принятие условий лицензионного соглашения** выберите **Принять**. Установка будет завершена.</span><span class="sxs-lookup"><span data-stu-id="adae6-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Снимок экрана: окно "Управление пакетами NuGet" с выделенной библиотекой клиента Microsoft Azure DocumentDB](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="adae6-161">Для установки пакета можно также воспользоваться консолью диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="adae6-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="adae6-162">Для этого в меню **Инструменты** щелкните **Диспетчер пакетов NuGet**, а затем выберите **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="adae6-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="adae6-163">Когда появится запрос, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="adae6-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="adae6-164">После установки пакета в решение Visual Studio будут добавлены две ссылки, Microsoft.Azure.Documents.Client и Newtonsoft.Json, и оно будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="adae6-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Снимок экрана: две ссылки, добавленные в проект данных JSON в обозревателе решений](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="adae6-166"><a name="_Toc395637763"></a>Шаг 4. Настройка приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="adae6-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="adae6-167">Теперь добавим модели, представления и контроллеры в это приложение MVC.</span><span class="sxs-lookup"><span data-stu-id="adae6-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="adae6-168">[Добавление модели](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="adae6-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="adae6-169">[Добавление контроллера](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="adae6-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="adae6-170">[Добавление представлений](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="adae6-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="adae6-171"><a name="_Toc395637764"></a>Добавление модели данных JSON</span><span class="sxs-lookup"><span data-stu-id="adae6-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="adae6-172">Давайте начнем с буквы **M** из аббревиатуры MVC, с модели (Model).</span><span class="sxs-lookup"><span data-stu-id="adae6-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="adae6-173">В **обозревателе решений** щелкните правой кнопкой мыши папку **Модели**, выберите **Добавить**, а затем щелкните **Класс**.</span><span class="sxs-lookup"><span data-stu-id="adae6-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="adae6-174">Откроется диалоговое окно **Добавление нового элемента** .</span><span class="sxs-lookup"><span data-stu-id="adae6-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="adae6-175">Назовите новый класс **Item.cs** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="adae6-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="adae6-176">В этом новом файле **Item.cs** добавьте следующий код после последнего *оператора using*.</span><span class="sxs-lookup"><span data-stu-id="adae6-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="adae6-177">Теперь замените этот код</span><span class="sxs-lookup"><span data-stu-id="adae6-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="adae6-178">следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="adae6-178">with the following code.</span></span>
   
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
   
    <span data-ttu-id="adae6-179">Все данные в Azure Cosmos DB передаются по сети и сохраняются в виде JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="adae6-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="adae6-180">Для управления сериализацией и десериализацией объектов с помощью JSON.NET можно использовать атрибут **JsonProperty**, как показано на примере только что созданного класса **Item**.</span><span class="sxs-lookup"><span data-stu-id="adae6-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="adae6-181">Вам **не обязательно** это делать, но, присваивая имена свойствам, я придерживаюсь правил наименования camelCase JSON.</span><span class="sxs-lookup"><span data-stu-id="adae6-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="adae6-182">Можно не только контролировать формат имени свойства при его поступлении в JSON, но и полностью переименовывать свойства .NET, как мы сделали со свойством **Description**.</span><span class="sxs-lookup"><span data-stu-id="adae6-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="adae6-183"><a name="_Toc395637765"></a>Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="adae6-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="adae6-184">С буквой **M** (моделями) разобрались, теперь займемся **C**, т. е. классом контроллера.</span><span class="sxs-lookup"><span data-stu-id="adae6-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="adae6-185">В **обозревателе решений** щелкните правой кнопкой мыши папку **Контроллеры**, выберите **Добавить**, а затем щелкните **Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="adae6-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="adae6-186">Откроется диалоговое окно **Добавление элемента формирования шаблонов** .</span><span class="sxs-lookup"><span data-stu-id="adae6-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="adae6-187">Выберите **Контроллер MVC 5 — пустой** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="adae6-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Снимок экрана: диалоговое окно "Добавление элемента формирования шаблонов" с выделенным параметром "Контроллер MVC 5 — Пустой"](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="adae6-189">Назовите новый контроллер **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="adae6-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Снимок экрана: диалоговое окно "Добавление контроллера"](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="adae6-191">После создания файла решение Visual Studio с новым файлом ItemController.cs в **Обозревателе решений**должно выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="adae6-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="adae6-192">Новый файл Item.cs, созданный ранее, также отображается.</span><span class="sxs-lookup"><span data-stu-id="adae6-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Снимок экрана решения Visual Studio: обозреватель решений с выделенным новым файлом ItemController.cs и файлом Item.cs](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="adae6-194">Можно закрыть файл ItemController.cs, мы вернемся к нему позже.</span><span class="sxs-lookup"><span data-stu-id="adae6-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="adae6-195"><a name="_Toc395637766"></a>Добавление представлений</span><span class="sxs-lookup"><span data-stu-id="adae6-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="adae6-196">И наконец, займемся буквой **V** из аббревиатуры MVC, т. е. представлениями.</span><span class="sxs-lookup"><span data-stu-id="adae6-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="adae6-197">[Добавление представления «Индекс элементов»](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="adae6-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="adae6-198">[Добавление представления «Создание элементов»](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="adae6-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="adae6-199">[Добавление представления «Редактирование элементов»](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="adae6-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="adae6-200"><a name="AddItemIndexView"></a>Добавление представления «Индекс элементов»</span><span class="sxs-lookup"><span data-stu-id="adae6-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="adae6-201">В **обозревателе решений** разверните папку **Представления**, щелкните правой кнопкой мыши пустую папку **Элемент**, созданную Visual Studio при добавлении **ItemController** ранее, выберите **Добавить**, а затем щелкните **Представление**.</span><span class="sxs-lookup"><span data-stu-id="adae6-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Снимок экрана: обозреватель решений, отображающий папку "Элемент", созданную Visual Studio, с выделенными командами "Добавления представления"](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="adae6-203">В диалоговом окне **Добавление представления** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="adae6-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="adae6-204">В поле **Имя представления** введите ***Индекс***.</span><span class="sxs-lookup"><span data-stu-id="adae6-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="adae6-205">В поле **Шаблон** выберите ***Список***.</span><span class="sxs-lookup"><span data-stu-id="adae6-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="adae6-206">В поле **Класс модели** выберите ***Item (todo.Models)*** (Элемент (todo.Models)).</span><span class="sxs-lookup"><span data-stu-id="adae6-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="adae6-207">В поле страницы макета введите ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="adae6-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Снимок экрана: диалоговое окно "Добавление представления"](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="adae6-209">После установки этих значений нажмите **Добавить** , и Visual Studio создаст представление.</span><span class="sxs-lookup"><span data-stu-id="adae6-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="adae6-210">После этого откроется созданный CSHTML-файл.</span><span class="sxs-lookup"><span data-stu-id="adae6-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="adae6-211">Можно закрыть этот файл в Visual Studio, мы вернемся к нему позже.</span><span class="sxs-lookup"><span data-stu-id="adae6-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="adae6-212"><a name="AddNewIndexView"></a>Добавление представления «Создание элементов»</span><span class="sxs-lookup"><span data-stu-id="adae6-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="adae6-213">Точно так же, как мы создали представление **Индекс элементов**, теперь мы создадим новое представление для создания новых **элементов**.</span><span class="sxs-lookup"><span data-stu-id="adae6-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="adae6-214">В **обозревателе решений** снова щелкните правой кнопкой мыши папку **Элемент**, выберите **Добавить**, а затем щелкните **Представление**.</span><span class="sxs-lookup"><span data-stu-id="adae6-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="adae6-215">В диалоговом окне **Добавление представления** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="adae6-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="adae6-216">В поле **Имя представления** введите ***Создать***.</span><span class="sxs-lookup"><span data-stu-id="adae6-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="adae6-217">В поле **Шаблон** выберите ***Создать***.</span><span class="sxs-lookup"><span data-stu-id="adae6-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="adae6-218">В поле **Класс модели** выберите ***Item (todo.Models)*** (Элемент (todo.Models)).</span><span class="sxs-lookup"><span data-stu-id="adae6-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="adae6-219">В поле страницы макета введите ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="adae6-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="adae6-220">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="adae6-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="adae6-221"><a name="_Toc395888515"></a>Добавление представления «Редактирование элементов»</span><span class="sxs-lookup"><span data-stu-id="adae6-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="adae6-222">И, наконец, добавим последнее представление для редактирования **элементов** , как мы делали это ранее.</span><span class="sxs-lookup"><span data-stu-id="adae6-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="adae6-223">В **обозревателе решений** снова щелкните правой кнопкой мыши папку **Элемент**, выберите **Добавить**, а затем щелкните **Представление**.</span><span class="sxs-lookup"><span data-stu-id="adae6-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="adae6-224">В диалоговом окне **Добавление представления** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="adae6-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="adae6-225">В поле **Имя представления** введите ***Изменить***.</span><span class="sxs-lookup"><span data-stu-id="adae6-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="adae6-226">В поле **Шаблон** выберите ***Изменить***.</span><span class="sxs-lookup"><span data-stu-id="adae6-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="adae6-227">В поле **Класс модели** выберите ***Item (todo.Models)*** (Элемент (todo.Models)).</span><span class="sxs-lookup"><span data-stu-id="adae6-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="adae6-228">В поле страницы макета введите ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="adae6-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="adae6-229">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="adae6-229">Click **Add**.</span></span>

<span data-ttu-id="adae6-230">Как только все будет готово, закройте документы cshtml в Visual Studio, мы вернемся к этим представлениям позже.</span><span class="sxs-lookup"><span data-stu-id="adae6-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="adae6-231"><a name="_Toc395637769"></a>Шаг 5. Подключение Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="adae6-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="adae6-232">Теперь, когда мы позаботились об основных ресурсах MVC, давайте рассмотрим добавление кода для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="adae6-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="adae6-233">В этом разделе мы добавим код для обработки следующих команд</span><span class="sxs-lookup"><span data-stu-id="adae6-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="adae6-234">[Вывод списка незавершенных элементов](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="adae6-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="adae6-235">[Добавление элементов](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="adae6-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="adae6-236">[Редактирование элементов](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="adae6-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="adae6-237"><a name="_Toc395637770"></a>Отображение незавершенных элементов в веб-приложении MVC</span><span class="sxs-lookup"><span data-stu-id="adae6-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="adae6-238">Прежде всего следует добавить класс, который содержит всю необходимую логику для подключения к службе Azure Cosmos DB и ее использования.</span><span class="sxs-lookup"><span data-stu-id="adae6-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="adae6-239">В этом учебнике мы оформим всю эту логику в класс репозитория с именем DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="adae6-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="adae6-240">В **обозревателе решений** щелкните правой кнопкой мыши проект, выберите **Добавить**, а затем щелкните **Класс**.</span><span class="sxs-lookup"><span data-stu-id="adae6-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="adae6-241">Назовите новый класс **DocumentDBRepository** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="adae6-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="adae6-242">В только что созданном классе **DocumentDBRepository** добавьте следующие *операторы using* над объявлением *namespace*.</span><span class="sxs-lookup"><span data-stu-id="adae6-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="adae6-243">Теперь замените этот код</span><span class="sxs-lookup"><span data-stu-id="adae6-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="adae6-244">следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="adae6-244">with the following code.</span></span>
   
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
   
    
3. <span data-ttu-id="adae6-245">Некоторые значения будут считываться из конфигурации, поэтому нужно открыть файл **Web.config** и добавить следующие строки в разделе `<AppSettings>`.</span><span class="sxs-lookup"><span data-stu-id="adae6-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="adae6-246">Теперь обновите значения для параметров *endpoint* и *authKey*, используя колонку "Ключи" на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="adae6-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="adae6-247">Используйте **URI** из колонки "Ключи" в качестве значения параметра endpoint. Что касается значения параметра authKey, то в этом качестве используйте значение **первичного ключа** или **вторичного** из колонки "Ключи".</span><span class="sxs-lookup"><span data-stu-id="adae6-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="adae6-248">Это касается подключения репозитория Azure Cosmos DB. Теперь можно добавить логику приложения.</span><span class="sxs-lookup"><span data-stu-id="adae6-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="adae6-249">Первое, что мы хотим сделать с приложением списка заданий, — отображение незавершенных элементов.</span><span class="sxs-lookup"><span data-stu-id="adae6-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="adae6-250">Скопируйте и вставьте следующий фрагмент кода в любом месте в класса **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="adae6-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="adae6-251">Откройте **ItemController** , который мы добавили ранее, и добавьте следующие *операторы using* перед декларацией namespace.</span><span class="sxs-lookup"><span data-stu-id="adae6-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="adae6-252">Если проект не называется todo, необходимо выполнить обновление с помощью todo.Models в соответствии с именем проекта.</span><span class="sxs-lookup"><span data-stu-id="adae6-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="adae6-253">Теперь замените этот код</span><span class="sxs-lookup"><span data-stu-id="adae6-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="adae6-254">следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="adae6-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="adae6-255">Откройте файл **Global.asax.cs** и добавьте в метод **Application_Start** следующую строку:</span><span class="sxs-lookup"><span data-stu-id="adae6-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="adae6-256">На данном этапе ваше решение должно компилироваться без каких-либо ошибок.</span><span class="sxs-lookup"><span data-stu-id="adae6-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="adae6-257">Чтобы запустить приложение сейчас, нужно перейти к **главному контроллеру** и представлению **индекса** в этом контроллере.</span><span class="sxs-lookup"><span data-stu-id="adae6-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="adae6-258">Это поведение по умолчанию для шаблона проекта MVC мы выбрали вначале, но нам нужно кое-что другое!</span><span class="sxs-lookup"><span data-stu-id="adae6-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="adae6-259">Давайте изменим маршрутизацию в данном приложении MVC, чтобы изменить это поведение.</span><span class="sxs-lookup"><span data-stu-id="adae6-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="adae6-260">Откройте файл ***App\_Start\RouteConfig.cs***, найдите строку, начинающуюся с defaults:, и измените ее следующим образом:</span><span class="sxs-lookup"><span data-stu-id="adae6-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="adae6-261">Теперь приложение ASP.NET MVC будет знать, что, если вы не указали значение в поле URL-адреса для управления поведением маршрутизации, вместо **главной страницы** нужно использовать **Элемент** в качестве контроллера, а пользовательский **индекс** — в качестве представления.</span><span class="sxs-lookup"><span data-stu-id="adae6-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="adae6-262">Теперь при запуске приложения оно будет вызывать **ItemController**, который вызывает класс репозитория и использует метод GetItems, чтобы возвратить все незавершенные элементы в представлении **Представления**\\**Элемент**\\**Индекс**.</span><span class="sxs-lookup"><span data-stu-id="adae6-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="adae6-263">Если создать и запустить этот проект сейчас, отобразится примерно следующие данные.</span><span class="sxs-lookup"><span data-stu-id="adae6-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Снимок экрана: веб-приложение "Список дел", созданное с помощью этого учебника](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="adae6-265"><a name="_Toc395637771"></a>Добавление элементов</span><span class="sxs-lookup"><span data-stu-id="adae6-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="adae6-266">Добавим несколько элементов в нашу базу данных, чтобы не смотреть на пустую сетку.</span><span class="sxs-lookup"><span data-stu-id="adae6-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="adae6-267">Добавим код в репозиторий Azure Cosmos DBRepository и ItemController, чтобы сохранить запись в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="adae6-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="adae6-268">Добавьте следующий метод в класс **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="adae6-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="adae6-269">Этот метод просто принимает любой объект, переданный ему, и сохраняет его в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="adae6-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="adae6-270">Откройте файл ItemController.cs и добавьте следующий фрагмент кода в класс.</span><span class="sxs-lookup"><span data-stu-id="adae6-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="adae6-271">Теперь приложение ASP.NET MVC будет знать, что делать с действием **Создать** .</span><span class="sxs-lookup"><span data-stu-id="adae6-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="adae6-272">В этом случае просто выводится связанное представление Create.cshtml, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="adae6-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="adae6-273">Теперь нам нужно добавить еще немного кода в этом контроллере, который будет принимать данные из представления **Создание** .</span><span class="sxs-lookup"><span data-stu-id="adae6-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="adae6-274">Добавьте следующий блок кода в класс ItemController.cs, который указывает приложению ASP.NET MVC, что нужно делать с формой POST для этого контроллера.</span><span class="sxs-lookup"><span data-stu-id="adae6-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="adae6-275">Этот код вызывает DocumentDBRepository и использует метод CreateItemAsync для сохранения нового элемента списка дел в базе данных.</span><span class="sxs-lookup"><span data-stu-id="adae6-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="adae6-276">**Примечание по безопасности.** Атрибут **ValidateAntiForgeryToken** используется здесь для защиты этого приложения от атак с подделкой межсайтовых запросов.</span><span class="sxs-lookup"><span data-stu-id="adae6-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="adae6-277">Кроме добавления этого атрибута представления также должны работать с данным маркером защиты от подделки запросов.</span><span class="sxs-lookup"><span data-stu-id="adae6-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="adae6-278">Дополнительные сведения об этом и примеры правильной реализации этой технологии см. в записи блога [Предотвращение атак с подделкой межсайтовых запросов][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="adae6-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="adae6-279">Исходный код, предоставленный на [GitHub][GitHub], имеет полную реализацию.</span><span class="sxs-lookup"><span data-stu-id="adae6-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="adae6-280">**Примечание по безопасности.** Для защиты от атак overposting также используется атрибут **Bind** в параметре метода.</span><span class="sxs-lookup"><span data-stu-id="adae6-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="adae6-281">Дополнительные сведения см. в записи блога [Основные операции CRUD в ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="adae6-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="adae6-282">На этом мы завершаем написание кода, необходимого для добавления новых элементов в нашу базу данных.</span><span class="sxs-lookup"><span data-stu-id="adae6-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="adae6-283"><a name="_Toc395637772"></a>Редактирование элементов</span><span class="sxs-lookup"><span data-stu-id="adae6-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="adae6-284">И последнее, необходимо обеспечить возможность изменить **Элементы** в базе данных и отмечать их как завершенные.</span><span class="sxs-lookup"><span data-stu-id="adae6-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="adae6-285">Представление изменения уже добавлено в проект, поэтому просто нужно еще раз добавить дополнительный код в контроллер и класс **DocumentDBRepository**.</span><span class="sxs-lookup"><span data-stu-id="adae6-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="adae6-286">Добавьте следующие методы в класс **DocumentDBRepository** .</span><span class="sxs-lookup"><span data-stu-id="adae6-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="adae6-287">Первый из этих двух методов, **GetItem**, извлекает элемент из Azure Cosmos DB, который передается обратно в **ItemController**, а затем — в представление **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="adae6-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="adae6-288">Второй метод, который мы только что добавили, заменяет **документ** в Azure Cosmos DB версией **документа**, переданного из **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="adae6-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="adae6-289">Добавьте следующие методы в класс **ItemController** .</span><span class="sxs-lookup"><span data-stu-id="adae6-289">Add the following to the **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="adae6-290">Первый метод обрабатывает команду HTTP GET, формирующуюся, когда пользователь выбирает ссылку **Изменить** в представлении **Индекс**.</span><span class="sxs-lookup"><span data-stu-id="adae6-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="adae6-291">Этот метод извлекает [**документ**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) из Azure Cosmos DB и передает его в представление **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="adae6-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="adae6-292">Представление **Изменить** отправляет команду HTTP POST в **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="adae6-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="adae6-293">Второй метод, который мы добавили, обрабатывает передачу обновленного объекта в Azure Cosmos DB, чтобы сохранить его в базе данных.</span><span class="sxs-lookup"><span data-stu-id="adae6-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="adae6-294">Вот и все, что необходимо для запуска приложения, отображения списка незавершенных **элементов**, добавления новых **элементов** и изменения **элементов**.</span><span class="sxs-lookup"><span data-stu-id="adae6-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="adae6-295"><a name="_Toc395637773"></a>Шаг 6. Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="adae6-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="adae6-296">Для проверки приложения на локальном компьютере выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="adae6-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="adae6-297">Чтобы создать приложение в режиме отладки, откройте Visual Studio и нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="adae6-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="adae6-298">После этого будет создано приложение и откроется окно браузера с пустой сеткой, которую мы уже видели:</span><span class="sxs-lookup"><span data-stu-id="adae6-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Снимок экрана: веб-приложение "Список дел", созданное с помощью этого учебника](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="adae6-300">Щелкните ссылку **Создать**, введите значения в поля **Имя** и **Описание**.</span><span class="sxs-lookup"><span data-stu-id="adae6-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="adae6-301">Не устанавливайте флажок **Выполнено**, иначе новый **элемент** будет добавлен ​​в завершенном состоянии и не будет отображаться в начальном списке.</span><span class="sxs-lookup"><span data-stu-id="adae6-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Снимок экрана: представление "Создание"](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="adae6-303">Щелкните **Создать**. Вы будете перенаправлены в представление **Индекс**, а в списке появится ваш **элемент**.</span><span class="sxs-lookup"><span data-stu-id="adae6-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Снимок экрана: представление "Индекс"](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="adae6-305">Вы можете добавить еще несколько **Элементов** в список задач.</span><span class="sxs-lookup"><span data-stu-id="adae6-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="adae6-306">Нажмите кнопку **Изменить** рядом с **Элемент**. Вы будете перенаправлены в представление **Изменить**, где сможете изменить любое свойство объекта, в том числе флажок **Выполнено**.</span><span class="sxs-lookup"><span data-stu-id="adae6-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="adae6-307">Если установить флажок **Выполнено** и нажать кнопку **Сохранить**, **Элемент** будет удален из списка незавершенных задач.</span><span class="sxs-lookup"><span data-stu-id="adae6-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Снимок экрана: представление "Индекс" с установленным флажком возле параметра "Завершено"](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="adae6-309">После проверки приложения нажмите клавиши CONTROL+F5, чтобы остановить отладку приложения.</span><span class="sxs-lookup"><span data-stu-id="adae6-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="adae6-310">Теперь все готово к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="adae6-310">You're ready to deploy!</span></span>

## <span data-ttu-id="adae6-311"><a name="_Toc395637774"></a>Шаг 7. Развертывание приложения в службу приложений Azure</span><span class="sxs-lookup"><span data-stu-id="adae6-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="adae6-312">Теперь, когда у вас есть готовое приложение, которое корректно работает в Azure Cosmos DB, мы собираемся развернуть его в службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="adae6-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="adae6-313">Чтобы опубликовать это приложение, щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="adae6-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Снимок экрана: параметр "Публикация" в обозревателе решений](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="adae6-315">В диалоговом окне **Публикация** щелкните **Служба приложений Microsoft Azure**, затем выберите **Создать**, чтобы создать профиль службы приложений, или щелкните **Выбрать существующий**, чтобы использовать существующий профиль.</span><span class="sxs-lookup"><span data-stu-id="adae6-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Диалоговое окно "Публикация" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="adae6-317">При наличии существующего профиля службы приложений Azure введите имя своей подписки.</span><span class="sxs-lookup"><span data-stu-id="adae6-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="adae6-318">Используйте фильтр **Просмотр** для сортировки по группе ресурсов или типу ресурсов, а затем выберите службу приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="adae6-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Диалоговое окно "Служба приложений" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="adae6-320">Чтобы создать профиль службы приложений Azure, в диалоговом окне **Публикация** выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="adae6-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="adae6-321">В окне **Создать службу приложений** введите имя веб-приложения и соответствующие подписку, группу ресурсов и план службы приложений, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="adae6-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Диалоговое окно "Создать службу приложений" в Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="adae6-323">Через несколько секунд Visual Studio завершит публикацию вашего веб-приложения и запустит браузер, где вы увидите свое творение, запущенное в Azure!</span><span class="sxs-lookup"><span data-stu-id="adae6-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="adae6-324"><a name="_Toc395637775"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="adae6-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="adae6-325">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="adae6-325">Congratulations!</span></span> <span data-ttu-id="adae6-326">Вы только что создали свое первое веб-приложение ASP.NET MVC с помощью Azure Cosmos DB и опубликовали его в Azure.</span><span class="sxs-lookup"><span data-stu-id="adae6-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="adae6-327">Исходный код полного приложения, включая функции детализации и удаления, не описанные в этом руководстве, можно скачать или клонировать с портала [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="adae6-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="adae6-328">Поэтому, если вы хотите добавить эти функции в приложение, скопируйте код и добавьте его в это приложение.</span><span class="sxs-lookup"><span data-stu-id="adae6-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="adae6-329">Чтобы добавить дополнительные функции в приложение, ознакомьтесь с API-интерфейсами, доступными в [библиотеке .NET для Azure Cosmos DB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet). Вы также можете стать соавтором библиотеки .NET для Azure Cosmos DB на портале [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="adae6-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
