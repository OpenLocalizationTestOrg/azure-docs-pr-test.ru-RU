---
title: "Azure Cosmos DB. Руководство по началу работы с API DocumentDB с помощью .NET Core | Документация Майкрософт"
description: "В этом руководстве описано создание консольного приложения C# и оперативной базы данных с помощью пакета SDK для .NET Core для API DocumentDB в службе Azure Cosmos DB."
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
ms.openlocfilehash: 7536978bbb1e41b6484b66fd1b51c900fc3e545d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-documentdb-api-and-net-core"></a><span data-ttu-id="b99f5-103">Azure Cosmos DB. Приступая к работе с API DocumentDB и .NET Core</span><span class="sxs-lookup"><span data-stu-id="b99f5-103">Azure Cosmos DB: Getting started with the DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b99f5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b99f5-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="b99f5-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b99f5-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="b99f5-106">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="b99f5-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="b99f5-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="b99f5-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="b99f5-108">Java</span><span class="sxs-lookup"><span data-stu-id="b99f5-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="b99f5-109">C++</span><span class="sxs-lookup"><span data-stu-id="b99f5-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="b99f5-110">Добро пожаловать в руководство по началу работы с Azure Cosmos DB с помощью .NET Core!</span><span class="sxs-lookup"><span data-stu-id="b99f5-110">Welcome to the DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="b99f5-111">После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="b99f5-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="b99f5-112">Мы рассмотрим следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="b99f5-112">We'll cover:</span></span>

* <span data-ttu-id="b99f5-113">создание учетной записи Azure Cosmos DB и подключение к ней;</span><span class="sxs-lookup"><span data-stu-id="b99f5-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="b99f5-114">настройка решения Visual Studio;</span><span class="sxs-lookup"><span data-stu-id="b99f5-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="b99f5-115">Создание оперативной базы данных</span><span class="sxs-lookup"><span data-stu-id="b99f5-115">Creating an online database</span></span>
* <span data-ttu-id="b99f5-116">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="b99f5-116">Creating a collection</span></span>
* <span data-ttu-id="b99f5-117">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="b99f5-117">Creating JSON documents</span></span>
* <span data-ttu-id="b99f5-118">выполнение запросов к коллекции;</span><span class="sxs-lookup"><span data-stu-id="b99f5-118">Querying the collection</span></span>
* <span data-ttu-id="b99f5-119">замена документа;</span><span class="sxs-lookup"><span data-stu-id="b99f5-119">Replacing a document</span></span>
* <span data-ttu-id="b99f5-120">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="b99f5-120">Deleting a document</span></span>
* <span data-ttu-id="b99f5-121">удаление базы данных.</span><span class="sxs-lookup"><span data-stu-id="b99f5-121">Deleting the database</span></span>

<span data-ttu-id="b99f5-122">У вас нет времени?</span><span class="sxs-lookup"><span data-stu-id="b99f5-122">Don't have time?</span></span> <span data-ttu-id="b99f5-123">Не беспокойтесь!</span><span class="sxs-lookup"><span data-stu-id="b99f5-123">Don't worry!</span></span> <span data-ttu-id="b99f5-124">Полное решение доступно на [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="b99f5-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="b99f5-125">Краткие инструкции см. в разделе [Получение полного решения NoSQL для этого руководства](#GetSolution).</span><span class="sxs-lookup"><span data-stu-id="b99f5-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="b99f5-126">Хотите создать приложение Xamarin iOS, Android или Forms с помощью API DocumentDB и пакета SDK для .NET Core?</span><span class="sxs-lookup"><span data-stu-id="b99f5-126">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="b99f5-127">См. [Создание мобильных приложений с помощью Xamarin и Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="b99f5-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b99f5-128">Пакет SDK .NET Core для Azure Cosmos DB, используемый в этом руководстве, не совместим с приложениями универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="b99f5-128">The Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="b99f5-129">Чтобы получить предварительную версию пакета SDK для .NET Core, которая поддерживает приложения UWP, отправьте сообщение по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b99f5-129">For a preview version of the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="b99f5-130">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="b99f5-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b99f5-131">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b99f5-131">Prerequisites</span></span>
<span data-ttu-id="b99f5-132">Убедитесь, что у вас есть указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="b99f5-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="b99f5-133">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b99f5-133">An active Azure account.</span></span> <span data-ttu-id="b99f5-134">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b99f5-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="b99f5-135">Кроме того, в этом руководстве можно использовать [эмулятор Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="b99f5-135">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="b99f5-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b99f5-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="b99f5-137">Если вы работаете в MacOS или Linux, вы можете разрабатывать приложения .NET Core с помощью командной строки, установив для этого пакет [SDK для .NET Core ](https://www.microsoft.com/net/core#macos) с учетом платформы.</span><span class="sxs-lookup"><span data-stu-id="b99f5-137">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="b99f5-138">Если вы работаете в Windows, приложения .NET Core можно разрабатывать с помощью командной строки, установив для этого пакет [SDK для .NET Core](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="b99f5-138">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="b99f5-139">Можно использовать свой редактор или скачать бесплатный [Visual Studio Code](https://code.visualstudio.com/), который работает в Windows, Linux и MacOS.</span><span class="sxs-lookup"><span data-stu-id="b99f5-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="b99f5-140">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b99f5-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="b99f5-141">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="b99f5-142">Если у вас уже есть учетная запись, которую вы собираетесь использовать, можно перейти к шагу [Настройка решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b99f5-142">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="b99f5-143">Если вы используете эмулятор Azure Cosmos DB, выполните действия, описанные в статье об [эмуляторе Azure Cosmos DB](local-emulator.md), чтобы его настроить и сразу перейти к [настройке решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b99f5-143">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="b99f5-144"><a id="SetupVS"></a> Шаг 2. Настройка решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b99f5-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="b99f5-145">Откройте **Visual Studio 2017** у себя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b99f5-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="b99f5-146">В меню **Файл** выберите пункт **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-146">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="b99f5-147">В диалоговом окне **Новый проект** выберите **Шаблоны** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)** (Консольное приложение (.NET Core)), а затем присвойте проекту имя **DocumentDBGettingStarted** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-147">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Снимок экрана: диалоговое окно «Новый проект»](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="b99f5-149">В **обозревателе решений** щелкните правой кнопкой мыши **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-149">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="b99f5-150">Не выходя из меню, щелкните элемент **Управление пакетами NuGet…**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-150">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![Снимок экрана: меню «Проект», вызванное щелчком правой кнопки мыши](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="b99f5-152">На вкладке **NuGet** в верхней части окна щелкните **Обзор** и в поле поиска введите **azure documentdb**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-152">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="b99f5-153">В результатах найдите **Microsoft.Azure.DocumentDB.Core** и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-153">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="b99f5-154">Идентификатором пакета для клиентской библиотеки DocumentDB для .NET Core является [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="b99f5-154">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="b99f5-155">Если используется версия .NET Framework (например, net461), которая не поддерживается для этого пакета .NET Core NuGet, используйте [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB), поддерживающую все версии .NET Framework, начиная с .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="b99f5-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="b99f5-156">При появлении запросов подтвердите установку пакета NuGet и примите условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="b99f5-156">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="b99f5-157">Отлично!</span><span class="sxs-lookup"><span data-stu-id="b99f5-157">Great!</span></span> <span data-ttu-id="b99f5-158">Теперь, когда мы завершили настройку, начнем писать код.</span><span class="sxs-lookup"><span data-stu-id="b99f5-158">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="b99f5-159">Вы можете найти проект готового кода для этого руководства в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="b99f5-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="b99f5-160"><a id="Connect"></a>Шаг 3. Подключение к учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b99f5-160"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="b99f5-161">Во-первых, добавьте эти ссылки в начало приложения C# в файле Program.cs:</span><span class="sxs-lookup"><span data-stu-id="b99f5-161">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

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
> <span data-ttu-id="b99f5-162">Чтобы завершить работу с этим руководством, добавьте приведенные выше зависимости.</span><span class="sxs-lookup"><span data-stu-id="b99f5-162">In order to complete this tutorial, make sure you add the dependencies above.</span></span>

<span data-ttu-id="b99f5-163">Теперь добавьте эти две константы и переменную *client* в открытый класс *Program*.</span><span class="sxs-lookup"><span data-stu-id="b99f5-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="b99f5-164">Затем войдите на [портал Azure](https://portal.azure.com) , чтобы получить URI и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="b99f5-164">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="b99f5-165">URI и первичный ключ Azure Cosmos DB позволяют приложению предоставлять данные о расположении, в котором будет устанавливаться подключение, делая подключение вашего приложения доверенным для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-165">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="b99f5-166">На портале Azure перейдите к учетной записи Azure Cosmos DB, а затем щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-166">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="b99f5-167">Скопируйте универсальный код ресурса (URI) с портала и вставьте его в параметр `<your endpoint URI>` в файле program.cs.</span><span class="sxs-lookup"><span data-stu-id="b99f5-167">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="b99f5-168">Затем скопируйте на портале значение поля "Первичный ключ" и вставьте его в параметр `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="b99f5-168">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="b99f5-169">Если вы используете эмулятор Azure Cosmos DB, укажите `https://localhost:8081` как конечную точку, а также примените четко определенный ключ авторизации, описанный в статье об [использовании эмулятора Azure Cosmos DB для разработки](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="b99f5-169">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="b99f5-170">Не забудьте удалить символы "<" и ">", но оставьте двойные кавычки, в которые заключены конечная точка и ключ.</span><span class="sxs-lookup"><span data-stu-id="b99f5-170">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![Снимок экрана портала Azure в ходе работы с руководством по NoSQL при создании консольного приложения C#.][keys]

<span data-ttu-id="b99f5-173">Мы запустим ознакомительное приложение, создав экземпляр **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-173">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="b99f5-174">В методе **Main** добавьте эту новую асинхронную задачу с именем **GetStartedDemo**, которая создает экземпляр **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-174">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

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

<span data-ttu-id="b99f5-175">Добавьте указанный далее код, чтобы запустить асинхронную задачу из метода **Main** .</span><span class="sxs-lookup"><span data-stu-id="b99f5-175">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="b99f5-176">Метод **Main** будет перехватывать исключения и записывать их в консоли.</span><span class="sxs-lookup"><span data-stu-id="b99f5-176">The **Main** method will catch exceptions and write them to the console.</span></span>

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

<span data-ttu-id="b99f5-177">Нажмите кнопку **DocumentDBGettingStarted**, чтобы создать и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b99f5-177">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="b99f5-178">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-178">Congratulations!</span></span> <span data-ttu-id="b99f5-179">Вы успешно подключились к учетной записи Azure Cosmos DB. Давайте теперь рассмотрим принципы работы с ресурсами Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-179">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="b99f5-180">Этап 4: создание базы данных</span><span class="sxs-lookup"><span data-stu-id="b99f5-180">Step 4: Create a database</span></span>
<span data-ttu-id="b99f5-181">Прежде чем добавлять код для создания базы данных, добавьте вспомогательный метод для записи на консоль.</span><span class="sxs-lookup"><span data-stu-id="b99f5-181">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="b99f5-182">Скопируйте и вставьте метод **WriteToConsoleAndPromptToContinue** под кодом метода **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-182">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="b99f5-183">[Базу данных](documentdb-resources.md#databases) Azure Cosmos DB можно создать с помощью метода [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) класса **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b99f5-184">База данных представляет собой логический контейнер для хранения документов JSON, разделенных между коллекциями.</span><span class="sxs-lookup"><span data-stu-id="b99f5-184">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="b99f5-185">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом создания клиента.</span><span class="sxs-lookup"><span data-stu-id="b99f5-185">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="b99f5-186">Будет создана база данных с именем *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="b99f5-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="b99f5-187">Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b99f5-187">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="b99f5-188">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-188">Congratulations!</span></span> <span data-ttu-id="b99f5-189">Вы успешно создали базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="b99f5-190"><a id="CreateColl"></a>Этап 5: создание коллекции</span><span class="sxs-lookup"><span data-stu-id="b99f5-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="b99f5-191">С использованием элемента **CreateDocumentCollectionAsync** можно создать новую коллекцию с зарезервированной пропускной способностью и соответствующей ценой.</span><span class="sxs-lookup"><span data-stu-id="b99f5-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="b99f5-192">Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b99f5-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="b99f5-193">Вы можете создать [коллекцию](documentdb-resources.md#collections), используя метод [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) класса **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-193">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b99f5-194">Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b99f5-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="b99f5-195">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом создания базы данных.</span><span class="sxs-lookup"><span data-stu-id="b99f5-195">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="b99f5-196">Будет создана коллекция документов с именем *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="b99f5-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="b99f5-197">Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b99f5-197">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="b99f5-198">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-198">Congratulations!</span></span> <span data-ttu-id="b99f5-199">Вы успешно создали коллекцию документов Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="b99f5-200"><a id="CreateDoc"></a>Шаг 6. Создание документов JSON</span><span class="sxs-lookup"><span data-stu-id="b99f5-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="b99f5-201">Вы можете создать [документ](documentdb-resources.md#documents) с помощью метода [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx), который относится к классу **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-201">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b99f5-202">Документы относятся к пользовательскому (произвольному) содержимому JSON.</span><span class="sxs-lookup"><span data-stu-id="b99f5-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="b99f5-203">Теперь мы можем добавить один или несколько документов.</span><span class="sxs-lookup"><span data-stu-id="b99f5-203">We can now insert one or more documents.</span></span> <span data-ttu-id="b99f5-204">Если у вас уже есть данные, которые необходимо хранить в базе данных, можно использовать [средство миграции данных](import-data.md)в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-204">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="b99f5-205">Сначала необходимо создать класс **Family**, который будет представлять объекты, хранящиеся в Azure Cosmos DB в этом примере.</span><span class="sxs-lookup"><span data-stu-id="b99f5-205">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="b99f5-206">Мы также создадим подклассы **Parent**, **Child**, **Pet** и **Address**, используемые в классе **Family**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="b99f5-207">Обратите внимание, документы должны иметь свойство **Id**, сериализуемое как **id** в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="b99f5-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="b99f5-208">Для этого после метода **GetStartedDemo** необходимо добавить следующие подклассы.</span><span class="sxs-lookup"><span data-stu-id="b99f5-208">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="b99f5-209">Скопируйте и вставьте классы **Family**, **Parent**, **Child**, **Pet** и **Address** под кодом метода **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-209">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="b99f5-210">Скопируйте и вставьте метод **CreateFamilyDocumentIfNotExists** под кодом метода **CreateDocumentCollectionIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-210">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

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

<span data-ttu-id="b99f5-211">Затем вставьте два документа, один для семьи Андерсен и один для семьи Вейкфилд.</span><span class="sxs-lookup"><span data-stu-id="b99f5-211">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="b99f5-212">Скопируйте и вставьте код после `// ADD THIS PART TO YOUR CODE` в метод **GetStartedDemo** под кодом создания коллекции документов.</span><span class="sxs-lookup"><span data-stu-id="b99f5-212">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

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

<span data-ttu-id="b99f5-213">Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b99f5-213">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="b99f5-214">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-214">Congratulations!</span></span> <span data-ttu-id="b99f5-215">Вы успешно создали два документа Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![На схеме представлены иерархические отношения между учетной записью, оперативной базой данных, коллекцией и документами, используемыми в руководстве по NoSQL при создании консольного приложения C#.](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="b99f5-217"><a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b99f5-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="b99f5-218">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="b99f5-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="b99f5-219">Ниже приведены примеры кода разнообразных запросов с использованием как синтаксиса SQL в Azure Cosmos DB, так и LINQ, которые можно запускать для добавленных на предыдущем шаге документов.</span><span class="sxs-lookup"><span data-stu-id="b99f5-219">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="b99f5-220">Скопируйте и вставьте метод **ExecuteSimpleQuery** под кодом метода **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-220">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="b99f5-221">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом создания второго документа.</span><span class="sxs-lookup"><span data-stu-id="b99f5-221">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="b99f5-222">Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b99f5-222">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="b99f5-223">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-223">Congratulations!</span></span> <span data-ttu-id="b99f5-224">Вы успешно выполнили запрос коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="b99f5-225">На схеме ниже показано, как для созданной коллекции вызывается синтаксис запроса SQL для Azure Cosmos DB. Та же логика применяется и к запросам LINQ.</span><span class="sxs-lookup"><span data-stu-id="b99f5-225">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![На схеме представлен масштаб и значение запроса, используемого в руководстве по NoSQL при создании консольного приложения C#.](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="b99f5-227">Ключевое слово [FROM](documentdb-sql-query.md#FromClause) использовать в запросе необязательно, так как запросы Azure Cosmos DB привязаны только к одной коллекции.</span><span class="sxs-lookup"><span data-stu-id="b99f5-227">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="b99f5-228">Поэтому слова "FROM Families f" можно заменить на "FROM root r" или любое другое имя переменной.</span><span class="sxs-lookup"><span data-stu-id="b99f5-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="b99f5-229">Поведение службы DocumentDB будет таким, будто Families, root или любая другая переменная указывает на текущую коллекцию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b99f5-229">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="b99f5-230"><a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON</span><span class="sxs-lookup"><span data-stu-id="b99f5-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="b99f5-231">Azure Cosmos DB поддерживает замену документов JSON.</span><span class="sxs-lookup"><span data-stu-id="b99f5-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="b99f5-232">Скопируйте и вставьте метод **ReplaceFamilyDocument** под кодом метода **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-232">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

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

<span data-ttu-id="b99f5-233">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="b99f5-233">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="b99f5-234">После замены документа тот же запрос будет запущен повторно, чтобы вы могли просмотреть измененный документ.</span><span class="sxs-lookup"><span data-stu-id="b99f5-234">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="b99f5-235">Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b99f5-235">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="b99f5-236">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-236">Congratulations!</span></span> <span data-ttu-id="b99f5-237">Вы успешно заменили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="b99f5-238"><a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON</span><span class="sxs-lookup"><span data-stu-id="b99f5-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="b99f5-239">Azure Cosmos DB поддерживает удаление документов JSON.</span><span class="sxs-lookup"><span data-stu-id="b99f5-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="b99f5-240">Скопируйте и вставьте метод **DeleteFamilyDocument** под кодом метода **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="b99f5-240">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

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

<span data-ttu-id="b99f5-241">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом выполнения второго запроса.</span><span class="sxs-lookup"><span data-stu-id="b99f5-241">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="b99f5-242">Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b99f5-242">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="b99f5-243">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-243">Congratulations!</span></span> <span data-ttu-id="b99f5-244">Вы успешно удалили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="b99f5-245"><a id="DeleteDatabase"></a>Шаг 10. Удаление базы данных</span><span class="sxs-lookup"><span data-stu-id="b99f5-245"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="b99f5-246">Удаление созданной базы данных приведет к удалению базы данных и всех дочерних ресурсов (коллекций, документов и т. д.).</span><span class="sxs-lookup"><span data-stu-id="b99f5-246">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="b99f5-247">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** под кодом удаления документа, чтобы удалить всю базу данных и все дочерние ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b99f5-247">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="b99f5-248">Нажмите кнопку **DocumentDBGettingStarted**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b99f5-248">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="b99f5-249">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-249">Congratulations!</span></span> <span data-ttu-id="b99f5-250">Вы успешно удалили базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b99f5-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="b99f5-251"><a id="Run"></a>Шаг 11. Запуск консольного приложения C#</span><span class="sxs-lookup"><span data-stu-id="b99f5-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="b99f5-252">В Visual Studio нажмите кнопку **DocumentDBGettingStarted**, чтобы создать приложение в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="b99f5-252">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="b99f5-253">В окне консоли должны отобразиться выходные данные вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b99f5-253">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="b99f5-254">Они должны содержать результаты обработки добавленных запросов. При этом выглядеть они должны примерно так, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="b99f5-254">The output will show the results of the queries we added and should match the example text below.</span></span>

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

<span data-ttu-id="b99f5-255">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b99f5-255">Congratulations!</span></span> <span data-ttu-id="b99f5-256">Вы завершили работу с этим руководством, и теперь у вас есть работающее консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="b99f5-256">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="b99f5-257"><a id="GetSolution"></a>Получение готового решения для этого руководства</span><span class="sxs-lookup"><span data-stu-id="b99f5-257"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="b99f5-258">Чтобы собрать решение GetStarted, которое содержит все примеры из данной статьи, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="b99f5-258">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="b99f5-259">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b99f5-259">An active Azure account.</span></span> <span data-ttu-id="b99f5-260">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b99f5-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="b99f5-261">[Учетная запись Azure Cosmos DB][create-documentdb-dotnet.md#create-account]</span><span class="sxs-lookup"><span data-stu-id="b99f5-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="b99f5-262">решение [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) , доступное в GitHub.</span><span class="sxs-lookup"><span data-stu-id="b99f5-262">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="b99f5-263">Чтобы в Visual Studio восстановить ссылки на API DocumentDB для пакета SDK .NET Core для Azure Cosmos DB, в обозревателе решений щелкните правой кнопкой мыши решение **GetStarted**, а затем выберите пункт **Enable NuGet Package Restore** (Включить восстановление пакета NuGet).</span><span class="sxs-lookup"><span data-stu-id="b99f5-263">To restore the references to the DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="b99f5-264">Затем в файле Program.cs обновите значения EndpointUrl и AuthorizationKey согласно инструкциям в разделе о [подключении к учетной записи Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="b99f5-264">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b99f5-265">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b99f5-265">Next steps</span></span>
* <span data-ttu-id="b99f5-266">Требуется более подробное руководство по ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="b99f5-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="b99f5-267">См. [Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="b99f5-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="b99f5-268">Хотите разработать приложение Xamarin iOS, Android или Forms с помощью API DocumentDB для пакета SDK .NET Core для Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="b99f5-268">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="b99f5-269">См. [Создание мобильных приложений с помощью Xamarin и Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="b99f5-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="b99f5-270">Хотите выполнять проверку масштабирования и производительности с помощью Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="b99f5-270">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="b99f5-271">См. [Проверка производительности и масштабирования с помощью Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="b99f5-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="b99f5-272">Узнайте, как организовать [мониторинг запросов, использования и хранилища Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="b99f5-272">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="b99f5-273">Отправьте запросы образцу набора данных в [Площадке для запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="b99f5-273">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="b99f5-274">Дополнительные сведения о модели программирования см. в статье [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b99f5-274">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
