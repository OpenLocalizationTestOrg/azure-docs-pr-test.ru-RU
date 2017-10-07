---
title: "Azure Cosmos DB. Руководство по началу работы с API DocumentDB с помощью .NET Core | Документация Майкрософт"
description: "Учебник, в котором создает консольное приложение на C#, с помощью hello Azure Cosmos DB DocumentDB API .NET Core SDK и оперативной базы данных."
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
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="de166-103">Azure Cosmos DB: Приступая к работе с DocumentDB API hello и .NET Core</span><span class="sxs-lookup"><span data-stu-id="de166-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de166-104">.NET</span><span class="sxs-lookup"><span data-stu-id="de166-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="de166-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="de166-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="de166-106">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="de166-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="de166-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="de166-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="de166-108">Java</span><span class="sxs-lookup"><span data-stu-id="de166-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="de166-109">C++</span><span class="sxs-lookup"><span data-stu-id="de166-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="de166-110">Вас приветствует toohello API DocumentDB для Приступая к работе с учебником .NET Core DB Cosmos Azure!</span><span class="sxs-lookup"><span data-stu-id="de166-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="de166-111">После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="de166-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="de166-112">Мы рассмотрим следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="de166-112">We'll cover:</span></span>

* <span data-ttu-id="de166-113">Создание и подключение учетной записи Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="de166-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="de166-114">настройка решения Visual Studio;</span><span class="sxs-lookup"><span data-stu-id="de166-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="de166-115">Создание оперативной базы данных</span><span class="sxs-lookup"><span data-stu-id="de166-115">Creating an online database</span></span>
* <span data-ttu-id="de166-116">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="de166-116">Creating a collection</span></span>
* <span data-ttu-id="de166-117">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="de166-117">Creating JSON documents</span></span>
* <span data-ttu-id="de166-118">Запрос к коллекции hello</span><span class="sxs-lookup"><span data-stu-id="de166-118">Querying hello collection</span></span>
* <span data-ttu-id="de166-119">замена документа;</span><span class="sxs-lookup"><span data-stu-id="de166-119">Replacing a document</span></span>
* <span data-ttu-id="de166-120">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="de166-120">Deleting a document</span></span>
* <span data-ttu-id="de166-121">Удаление базы данных hello</span><span class="sxs-lookup"><span data-stu-id="de166-121">Deleting hello database</span></span>

<span data-ttu-id="de166-122">У вас нет времени?</span><span class="sxs-lookup"><span data-stu-id="de166-122">Don't have time?</span></span> <span data-ttu-id="de166-123">Не беспокойтесь!</span><span class="sxs-lookup"><span data-stu-id="de166-123">Don't worry!</span></span> <span data-ttu-id="de166-124">законченное решение Hello можно найти в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="de166-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="de166-125">Переход toohello [Получает раздел законченное решение hello](#GetSolution) быстрого инструкции.</span><span class="sxs-lookup"><span data-stu-id="de166-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="de166-126">Хотите toobuild Xamarin iOS, Android или формы с помощью приложения hello DocumentDB API и пакета SDK для .NET Core?</span><span class="sxs-lookup"><span data-stu-id="de166-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="de166-127">См. [Создание мобильных приложений с помощью Xamarin и Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="de166-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="de166-128">Hello Azure Cosmos DB .NET Core SDK используемые в этом учебнике не совместим с приложениями универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="de166-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="de166-129">Для предварительной версии hello .NET Core SDK, который поддерживает приложения UWP, отправки электронной почты слишком[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="de166-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="de166-130">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="de166-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de166-131">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="de166-131">Prerequisites</span></span>
<span data-ttu-id="de166-132">Убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="de166-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="de166-133">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="de166-133">An active Azure account.</span></span> <span data-ttu-id="de166-134">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="de166-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="de166-135">Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="de166-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="de166-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="de166-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="de166-137">При работе на MacOS или Linux, можно разрабатывать приложения .NET Core из командной строки hello, установив hello [пакета SDK для .NET Core](https://www.microsoft.com/net/core#macos) для hello платформы по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="de166-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="de166-138">При работе в Windows, можно разрабатывать приложения .NET Core из командной строки hello, установив hello [пакета SDK для .NET Core](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="de166-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="de166-139">Можно использовать свой редактор или скачать бесплатный [Visual Studio Code](https://code.visualstudio.com/), который работает в Windows, Linux и MacOS.</span><span class="sxs-lookup"><span data-stu-id="de166-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="de166-140">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de166-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="de166-141">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="de166-142">При наличии учетной записи требуется toouse можно сразу перейти слишком[установки решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="de166-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="de166-143">Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[установки решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="de166-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="de166-144"><a id="SetupVS"></a> Шаг 2. Настройка решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de166-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="de166-145">Откройте **Visual Studio 2017** у себя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="de166-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="de166-146">На hello **файл** последовательно выберите пункты **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="de166-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="de166-147">В hello **новый проект** диалогового окна выберите **шаблоны** / **Visual C#** / **.NET Core** / **Консольного приложения (.NET Core)**, присвойте проекту имя **DocumentDBGettingStarted**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="de166-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Снимок экрана: hello окно нового проекта](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="de166-149">В hello **обозревателе решений**, щелкните правой кнопкой мыши **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="de166-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="de166-150">Не выходя из меню hello, щелкните **управление пакетами NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="de166-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Снимок hello справа щелчок меню для проекта hello](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="de166-152">В hello **NuGet** щелкните **Обзор** hello верхней части окна hello и тип **azure documentdb** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="de166-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="de166-153">В результатах поиска hello, найти **Microsoft.Azure.DocumentDB.Core** и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="de166-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="de166-154">Идентификатор пакета Hello hello DocumentDB клиентская библиотека для .NET Core [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="de166-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="de166-155">Если используется версия .NET Framework (например, net461), которая не поддерживается для этого пакета .NET Core NuGet, используйте [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB), поддерживающую все версии .NET Framework, начиная с .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="de166-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="de166-156">На экране приветствия принятие установки пакета NuGet hello и hello лицензионное соглашение.</span><span class="sxs-lookup"><span data-stu-id="de166-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="de166-157">Отлично!</span><span class="sxs-lookup"><span data-stu-id="de166-157">Great!</span></span> <span data-ttu-id="de166-158">Теперь, когда мы hello Настройка завершена, давайте начнем написания кода.</span><span class="sxs-lookup"><span data-stu-id="de166-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="de166-159">Вы можете найти проект готового кода для этого руководства в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="de166-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="de166-160"><a id="Connect"></a>Шаг 3: Учетная запись Azure Cosmos DB tooan подключения</span><span class="sxs-lookup"><span data-stu-id="de166-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="de166-161">Во-первых, добавьте эти ссылается на начало toohello приложение C# в файле Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="de166-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="de166-162">В заказ toocomplete этого учебника, убедитесь, что Добавление зависимостей hello выше.</span><span class="sxs-lookup"><span data-stu-id="de166-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="de166-163">Теперь добавьте эти две константы и переменную *client* в открытый класс *Program*.</span><span class="sxs-lookup"><span data-stu-id="de166-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="de166-164">Далее head toohello [портала Azure](https://portal.azure.com) tooretrieve URI и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="de166-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="de166-165">Hello Azure Cosmos DB URI и первичный ключ, необходимые для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="de166-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="de166-166">В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour и нажмите кнопку **ключей**.</span><span class="sxs-lookup"><span data-stu-id="de166-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="de166-167">Скопируйте hello URI с портала hello и вставьте его в `<your endpoint URI>` в файле program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="de166-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="de166-168">Затем копировать hello первичный ключ с портала hello и вставьте его в `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="de166-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="de166-169">При использовании hello DB эмулятор Azure Cosmos используйте `https://localhost:8081` как конечная точка hello и hello четко определенных авторизации ключа из [как с помощью toodevelop hello DB эмулятор Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="de166-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="de166-170">Убедитесь, что hello tooremove < и >, но оставьте hello двойные кавычки вокруг конечную точку и ключ.</span><span class="sxs-lookup"><span data-stu-id="de166-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Снимок экрана: hello портал Azure hello NoSQL учебника toocreate консольное приложение C#.][keys]

<span data-ttu-id="de166-173">Мы начнем началу работы приложения hello, создав новый экземпляр hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="de166-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="de166-174">Ниже hello **Main** метод, добавить эту новую асинхронную задачу, которая вызывается **GetStartedDemo**, который будет создан экземпляр наш новый **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="de166-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="de166-175">Добавьте следующий hello кода toorun асинхронную задачу из вашего **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="de166-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="de166-176">Hello **Main** метод будет перехватывать исключения и записывать их toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="de166-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

```csharp
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
```

<span data-ttu-id="de166-177">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку toobuild и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="de166-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="de166-178">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-178">Congratulations!</span></span> <span data-ttu-id="de166-179">Учетная запись Azure Cosmos DB tooan успешно подключились, теперь давайте рассмотрим работы с ресурсами Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="de166-180">Этап 4: создание базы данных</span><span class="sxs-lookup"><span data-stu-id="de166-180">Step 4: Create a database</span></span>
<span data-ttu-id="de166-181">Перед добавлением hello код для создания базы данных, добавьте вспомогательный метод для записи toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="de166-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="de166-182">Скопируйте и вставьте hello **WriteToConsoleAndPromptToContinue** под hello **GetStartedDemo** метод.</span><span class="sxs-lookup"><span data-stu-id="de166-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="de166-183">Базы данных Azure Cosmos [базы данных](documentdb-resources.md#databases) могут быть созданы с помощью hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="de166-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="de166-184">База данных находится hello логический контейнер для хранения документов JSON, секционированный по коллекциям.</span><span class="sxs-lookup"><span data-stu-id="de166-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="de166-185">Копировать и вставить hello следующий код tooyour **GetStartedDemo** под hello создания клиента.</span><span class="sxs-lookup"><span data-stu-id="de166-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="de166-186">Будет создана база данных с именем *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="de166-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="de166-187">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="de166-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="de166-188">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-188">Congratulations!</span></span> <span data-ttu-id="de166-189">Вы успешно создали базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="de166-190"><a id="CreateColl"></a>Этап 5: создание коллекции</span><span class="sxs-lookup"><span data-stu-id="de166-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="de166-191">С использованием элемента **CreateDocumentCollectionAsync** можно создать новую коллекцию с зарезервированной пропускной способностью и соответствующей ценой.</span><span class="sxs-lookup"><span data-stu-id="de166-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="de166-192">Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="de166-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="de166-193">Объект [коллекции](documentdb-resources.md#collections) могут быть созданы с помощью hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="de166-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="de166-194">Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="de166-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="de166-195">Копировать и вставить hello следующий код tooyour **GetStartedDemo** под hello создания базы данных.</span><span class="sxs-lookup"><span data-stu-id="de166-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="de166-196">Будет создана коллекция документов с именем *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="de166-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="de166-197">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="de166-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="de166-198">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-198">Congratulations!</span></span> <span data-ttu-id="de166-199">Вы успешно создали коллекцию документов Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="de166-200"><a id="CreateDoc"></a>Шаг 6. Создание документов JSON</span><span class="sxs-lookup"><span data-stu-id="de166-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="de166-201">Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="de166-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="de166-202">Документы относятся к пользовательскому (произвольному) содержимому JSON.</span><span class="sxs-lookup"><span data-stu-id="de166-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="de166-203">Теперь мы можем добавить один или несколько документов.</span><span class="sxs-lookup"><span data-stu-id="de166-203">We can now insert one or more documents.</span></span> <span data-ttu-id="de166-204">При наличии данных, отсылаемых toostore в базе данных можно использовать базу данных Cosmos Azure [средство переноса данных](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="de166-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="de166-205">Во-первых, мы должны toocreate **семейства** класс, представляющий объекты в базе данных Azure Cosmos в этом образце.</span><span class="sxs-lookup"><span data-stu-id="de166-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="de166-206">Мы также создадим подклассы **Parent**, **Child**, **Pet** и **Address**, используемые в классе **Family**.</span><span class="sxs-lookup"><span data-stu-id="de166-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="de166-207">Обратите внимание, документы должны иметь свойство **Id**, сериализуемое как **id** в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="de166-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="de166-208">Эти классы можно создать, добавив следующие внутренние вложенные классы после hello hello **GetStartedDemo** метод.</span><span class="sxs-lookup"><span data-stu-id="de166-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="de166-209">Скопируйте и вставьте hello **семейства**, **родительского**, **дочерних**, **Pet**, и **адрес** классы под Hello **WriteToConsoleAndPromptToContinue** метод.</span><span class="sxs-lookup"><span data-stu-id="de166-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="de166-210">Скопируйте и вставьте hello **CreateFamilyDocumentIfNotExists** под вашей **CreateDocumentCollectionIfNotExists** метод.</span><span class="sxs-lookup"><span data-stu-id="de166-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="de166-211">Добавьте два документа, одному для каждого семейства Андерсен hello и hello Wakefield семейства.</span><span class="sxs-lookup"><span data-stu-id="de166-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="de166-212">Скопируйте и вставьте код hello, следующий за `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** под создание коллекции hello документа.</span><span class="sxs-lookup"><span data-stu-id="de166-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

<span data-ttu-id="de166-213">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="de166-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="de166-214">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-214">Congratulations!</span></span> <span data-ttu-id="de166-215">Вы успешно создали два документа Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Схема, иллюстрирующая hello иерархическую связь между hello учетной записи, hello оперативную базу данных, коллекции hello и hello документов, созданных hello NoSQL учебника toocreate консольное приложение C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="de166-217"><a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="de166-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="de166-218">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="de166-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="de166-219">Hello следующий образец кода показывает различные запросы — оба SQL Azure Cosmos базы данных с помощью синтаксиса, а также LINQ - что мы может выполняться hello документов, над которыми мы вставлены в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="de166-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="de166-220">Скопируйте и вставьте hello **ExecuteSimpleQuery** под вашей **CreateFamilyDocumentIfNotExists** метод.</span><span class="sxs-lookup"><span data-stu-id="de166-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="de166-221">Копировать и вставить hello следующий код tooyour **GetStartedDemo** под hello второй создания документа.</span><span class="sxs-lookup"><span data-stu-id="de166-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="de166-222">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="de166-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="de166-223">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-223">Congratulations!</span></span> <span data-ttu-id="de166-224">Вы успешно выполнили запрос коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="de166-225">Hello следующей схеме показано, как hello базы данных SQL Azure Cosmos синтаксис называется с коллекцией hello созданный запрос и hello же принцип применяется также toohello запроса LINQ.</span><span class="sxs-lookup"><span data-stu-id="de166-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Диаграмму, демонстрирующая области hello и это означает hello запроса используется hello NoSQL учебника toocreate консольное приложение C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="de166-227">Hello [FROM](documentdb-sql-query.md#FromClause) ключевое слово является необязательным в hello запроса, так как запросы Azure Cosmos DB уже области tooa одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="de166-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="de166-228">Поэтому слова "FROM Families f" можно заменить на "FROM root r" или любое другое имя переменной.</span><span class="sxs-lookup"><span data-stu-id="de166-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="de166-229">DocumentDB будет построена, семейств, корень или имя переменной hello выбранные, ссылка hello текущей коллекции по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="de166-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="de166-230"><a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON</span><span class="sxs-lookup"><span data-stu-id="de166-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="de166-231">Azure Cosmos DB поддерживает замену документов JSON.</span><span class="sxs-lookup"><span data-stu-id="de166-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="de166-232">Скопируйте и вставьте hello **ReplaceFamilyDocument** под вашей **ExecuteSimpleQuery** метод.</span><span class="sxs-lookup"><span data-stu-id="de166-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="de166-233">Копировать и вставить hello следующий код tooyour **GetStartedDemo** под hello выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="de166-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="de166-234">После замены hello документа, это будет выполняться hello же попытку запроса tooview hello изменения документа.</span><span class="sxs-lookup"><span data-stu-id="de166-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="de166-235">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="de166-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="de166-236">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-236">Congratulations!</span></span> <span data-ttu-id="de166-237">Вы успешно заменили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="de166-238"><a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON</span><span class="sxs-lookup"><span data-stu-id="de166-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="de166-239">Azure Cosmos DB поддерживает удаление документов JSON.</span><span class="sxs-lookup"><span data-stu-id="de166-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="de166-240">Скопируйте и вставьте hello **DeleteFamilyDocument** под вашей **ReplaceFamilyDocument** метод.</span><span class="sxs-lookup"><span data-stu-id="de166-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="de166-241">Копировать и вставить hello следующий код tooyour **GetStartedDemo** под hello второго выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="de166-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="de166-242">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="de166-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="de166-243">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-243">Congratulations!</span></span> <span data-ttu-id="de166-244">Вы успешно удалили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="de166-245"><a id="DeleteDatabase"></a>Шаг 10: Удаление hello базы данных</span><span class="sxs-lookup"><span data-stu-id="de166-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="de166-246">Идет удаление hello создана база данных приведет к удалению hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="de166-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="de166-247">Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод под hello документа удалить toodelete hello всю базу данных и все дочерние ресурсы.</span><span class="sxs-lookup"><span data-stu-id="de166-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="de166-248">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="de166-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="de166-249">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-249">Congratulations!</span></span> <span data-ttu-id="de166-250">Вы успешно удалили базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de166-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="de166-251"><a id="Run"></a>Шаг 11. Запуск консольного приложения C#</span><span class="sxs-lookup"><span data-stu-id="de166-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="de166-252">Нажмите клавишу hello **DocumentDBGettingStarted** кнопку в приложение hello toobuild Visual Studio в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="de166-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="de166-253">Вы увидите выходные данные get работы приложения в окне консоли hello hello.</span><span class="sxs-lookup"><span data-stu-id="de166-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="de166-254">выходные данные Hello покажет результаты hello hello запросов мы добавлен и должен соответствовать hello пример текста ниже.</span><span class="sxs-lookup"><span data-stu-id="de166-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="de166-255">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="de166-255">Congratulations!</span></span> <span data-ttu-id="de166-256">После завершения учебника hello и иметь работу консольного приложения C#!</span><span class="sxs-lookup"><span data-stu-id="de166-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="de166-257"><a id="GetSolution"></a>Получить комплексное решение учебника hello</span><span class="sxs-lookup"><span data-stu-id="de166-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="de166-258">решение GetStarted toobuild hello, содержащий все образцы hello в этой статье, вам потребуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="de166-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="de166-259">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="de166-259">An active Azure account.</span></span> <span data-ttu-id="de166-260">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="de166-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="de166-261">[Учетная запись Azure Cosmos DB][create-documentdb-dotnet.md#create-account]</span><span class="sxs-lookup"><span data-stu-id="de166-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="de166-262">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) решения на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="de166-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="de166-263">toohello ссылки toorestore hello API DocumentDB для Azure Cosmos DB .NET Core SDK в Visual Studio щелкните правой кнопкой мыши hello **GetStarted** решения в обозревателе решений, а затем выберите **включите восстановление пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="de166-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="de166-264">Затем в файле Program.cs hello, обновите значения EndpointUrl и AuthorizationKey hello как описано в [подключить учетную запись Azure Cosmos DB tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="de166-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de166-265">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de166-265">Next steps</span></span>
* <span data-ttu-id="de166-266">Требуется более подробное руководство по ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="de166-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="de166-267">См. [Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="de166-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="de166-268">Хотите toodevelop Xamarin iOS, Android или формы с помощью приложения hello DocumentDB API для пакета SDK для Azure Cosmos DB .NET Core?</span><span class="sxs-lookup"><span data-stu-id="de166-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="de166-269">См. [Создание мобильных приложений с помощью Xamarin и Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="de166-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="de166-270">Требуется tooperform масштаб и производительность, тестирование с помощью Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="de166-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="de166-271">См. [Проверка производительности и масштабирования с помощью Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="de166-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="de166-272">Узнайте, каким образом слишком[DB Cosmos Azure монитор запросов, использования и хранения](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="de166-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="de166-273">Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="de166-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="de166-274">в разделе toolearn Дополнительные сведения о модели программирования hello, [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="de166-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
