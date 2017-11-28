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
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="657bb-104">Azure Cosmos DB. Приступая к работе с API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="657bb-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="657bb-105">.NET</span><span class="sxs-lookup"><span data-stu-id="657bb-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="657bb-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="657bb-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="657bb-107">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="657bb-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="657bb-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="657bb-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="657bb-109">Java</span><span class="sxs-lookup"><span data-stu-id="657bb-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="657bb-110">C++</span><span class="sxs-lookup"><span data-stu-id="657bb-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="657bb-111">Учебник по началу Azure Cosmos DB DocumentDB API приветствия toohello работы!</span><span class="sxs-lookup"><span data-stu-id="657bb-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="657bb-112">После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="657bb-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="657bb-113">Мы рассмотрим следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="657bb-113">We'll cover:</span></span>

* <span data-ttu-id="657bb-114">Создание и подключение учетной записи Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="657bb-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="657bb-115">настройка решения Visual Studio;</span><span class="sxs-lookup"><span data-stu-id="657bb-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="657bb-116">Создание оперативной базы данных</span><span class="sxs-lookup"><span data-stu-id="657bb-116">Creating an online database</span></span>
* <span data-ttu-id="657bb-117">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="657bb-117">Creating a collection</span></span>
* <span data-ttu-id="657bb-118">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="657bb-118">Creating JSON documents</span></span>
* <span data-ttu-id="657bb-119">Запрос к коллекции hello</span><span class="sxs-lookup"><span data-stu-id="657bb-119">Querying hello collection</span></span>
* <span data-ttu-id="657bb-120">замена документа;</span><span class="sxs-lookup"><span data-stu-id="657bb-120">Replacing a document</span></span>
* <span data-ttu-id="657bb-121">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="657bb-121">Deleting a document</span></span>
* <span data-ttu-id="657bb-122">Удаление базы данных hello</span><span class="sxs-lookup"><span data-stu-id="657bb-122">Deleting hello database</span></span>

<span data-ttu-id="657bb-123">У вас нет времени?</span><span class="sxs-lookup"><span data-stu-id="657bb-123">Don't have time?</span></span> <span data-ttu-id="657bb-124">Не беспокойтесь!</span><span class="sxs-lookup"><span data-stu-id="657bb-124">Don't worry!</span></span> <span data-ttu-id="657bb-125">законченное решение Hello можно найти в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="657bb-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="657bb-126">Переход toohello [получить hello весь раздел учебника решение NoSQL](#GetSolution) быстрого инструкции.</span><span class="sxs-lookup"><span data-stu-id="657bb-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="657bb-127">После этого выполните голосования hello используйте кнопки в hello верхней или нижней части этой страницы toogive нам отзыв.</span><span class="sxs-lookup"><span data-stu-id="657bb-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="657bb-128">Если вы хотите нам toocontact напрямую, если вам свободного tooinclude адрес вашей электронной почты в комментарии.</span><span class="sxs-lookup"><span data-stu-id="657bb-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="657bb-129">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="657bb-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="657bb-130">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="657bb-130">Prerequisites</span></span>
<span data-ttu-id="657bb-131">Убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="657bb-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="657bb-132">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="657bb-132">An active Azure account.</span></span> <span data-ttu-id="657bb-133">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="657bb-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="657bb-134">Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="657bb-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="657bb-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="657bb-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="657bb-136">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="657bb-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="657bb-137">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="657bb-138">При наличии учетной записи требуется toouse можно сразу перейти слишком[установки решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="657bb-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="657bb-139">Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[установки решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="657bb-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="657bb-140"><a id="SetupVS"></a> Шаг 2. Настройка решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="657bb-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="657bb-141">Откройте **Visual Studio 2017** у себя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="657bb-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="657bb-142">На hello **файл** последовательно выберите пункты **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="657bb-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="657bb-143">В hello **новый проект** диалогового окна выберите **шаблоны** / **Visual C#** / **консольное приложение**, имя проект, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="657bb-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="657bb-144">![Снимок экрана: hello окно нового проекта](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="657bb-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="657bb-145">В hello **обозревателе решений**, щелкните правой кнопкой мыши новое консольное приложение, который находится под управлением решения Visual Studio, и нажмите кнопку **управление пакетами NuGet...**</span><span class="sxs-lookup"><span data-stu-id="657bb-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Снимок hello справа щелчок меню для проекта hello](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="657bb-147">В hello **Nuget** щелкните **Обзор**и тип **azure documentdb** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="657bb-148">В результатах поиска hello, найти **Microsoft.Azure.DocumentDB** и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="657bb-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="657bb-149">Идентификатор пакета Hello hello клиентской библиотеки API DocumentDB Azure Cosmos DB [клиентской библиотеки Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="657bb-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="657bb-150">![Снимок экрана: hello меню Nuget для поиска Azure SDK клиента DB Cosmos](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="657bb-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="657bb-151">При получении сообщения о рецензировании решения toohello изменения, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="657bb-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="657bb-152">Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="657bb-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="657bb-153">Отлично!</span><span class="sxs-lookup"><span data-stu-id="657bb-153">Great!</span></span> <span data-ttu-id="657bb-154">Теперь, когда мы hello Настройка завершена, давайте начнем написания кода.</span><span class="sxs-lookup"><span data-stu-id="657bb-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="657bb-155">Вы можете найти проект готового кода для этого руководства в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="657bb-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="657bb-156"><a id="Connect"></a>Шаг 3: Учетная запись Azure Cosmos DB tooan подключения</span><span class="sxs-lookup"><span data-stu-id="657bb-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="657bb-157">Во-первых, добавьте эти ссылается на начало toohello приложение C# в файле Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="657bb-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="657bb-158">В учебнике hello toocomplete заказа убедитесь, что Добавление зависимостей hello выше.</span><span class="sxs-lookup"><span data-stu-id="657bb-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="657bb-159">Теперь добавьте эти две константы и переменную *client* в открытый класс *Program*.</span><span class="sxs-lookup"><span data-stu-id="657bb-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="657bb-160">Далее head резервное toohello [портала Azure](https://portal.azure.com) tooretrieve URL-адрес конечной точки и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="657bb-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="657bb-161">URL-адрес конечной точки Hello и первичный ключ, необходимые для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="657bb-162">В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour и нажмите кнопку **ключей**.</span><span class="sxs-lookup"><span data-stu-id="657bb-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="657bb-163">Скопируйте hello URI с портала hello и вставьте его в `<your endpoint URL>` в файле program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="657bb-164">Затем копировать hello первичный ключ с портала hello и вставьте его в `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="657bb-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Снимок экрана: hello портал Azure hello NoSQL учебника toocreate консольное приложение C#.][keys]

<span data-ttu-id="657bb-167">Далее, мы начнем приложения hello, создав новый экземпляр hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="657bb-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="657bb-168">Ниже hello **Main** метод, добавить эту новую асинхронную задачу, которая вызывается **GetStartedDemo**, который будет создан экземпляр наш новый **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="657bb-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="657bb-169">Добавьте следующий hello кода toorun асинхронную задачу из вашего **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="657bb-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="657bb-170">Hello **Main** метод будет перехватывать исключения и записывать их toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="657bb-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="657bb-171">Нажмите клавишу **F5** toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="657bb-172">выходные данные в окно консоли Hello отображает приветственное сообщение `End of demo, press any key tooexit.` подтверждения того, что hello подключение было создано.</span><span class="sxs-lookup"><span data-stu-id="657bb-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="657bb-173">После этого можно закрыть окно консоли hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-173">You can then close hello console window.</span></span> 

<span data-ttu-id="657bb-174">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-174">Congratulations!</span></span> <span data-ttu-id="657bb-175">Учетная запись Azure Cosmos DB tooan успешно подключились, теперь давайте рассмотрим работы с ресурсами Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="657bb-176">Этап 4: создание базы данных</span><span class="sxs-lookup"><span data-stu-id="657bb-176">Step 4: Create a database</span></span>
<span data-ttu-id="657bb-177">Перед добавлением hello код для создания базы данных, добавьте вспомогательный метод для записи toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="657bb-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="657bb-178">Скопируйте и вставьте hello **WriteToConsoleAndPromptToContinue** метод после hello **GetStartedDemo** метод.</span><span class="sxs-lookup"><span data-stu-id="657bb-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="657bb-179">Базы данных Azure Cosmos [базы данных](documentdb-resources.md#databases) могут быть созданы с помощью hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="657bb-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="657bb-180">База данных находится hello логический контейнер для хранения документов JSON, секционированный по коллекциям.</span><span class="sxs-lookup"><span data-stu-id="657bb-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="657bb-181">Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после создания клиента hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="657bb-182">Будет создана база данных с именем *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="657bb-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="657bb-183">Нажмите клавишу **F5** toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="657bb-184">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-184">Congratulations!</span></span> <span data-ttu-id="657bb-185">Вы успешно создали базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="657bb-186"><a id="CreateColl"></a>Этап 5: создание коллекции</span><span class="sxs-lookup"><span data-stu-id="657bb-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="657bb-187">С помощью метода **CreateDatabaseIfNotExistsAsync** можно создать новую коллекцию с зарезервированной пропускной способностью и соответствующей ценой.</span><span class="sxs-lookup"><span data-stu-id="657bb-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="657bb-188">Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="657bb-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="657bb-189">Объект [коллекции](documentdb-resources.md#collections) могут быть созданы с помощью hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="657bb-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="657bb-190">Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="657bb-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="657bb-191">Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после создания базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="657bb-192">Будет создана коллекция документов с именем *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="657bb-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="657bb-193">Нажмите клавишу **F5** toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="657bb-194">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-194">Congratulations!</span></span> <span data-ttu-id="657bb-195">Вы успешно создали коллекцию документов Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="657bb-196"><a id="CreateDoc"></a>Шаг 6. Создание документов JSON</span><span class="sxs-lookup"><span data-stu-id="657bb-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="657bb-197">Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="657bb-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="657bb-198">Документы относятся к пользовательскому (произвольному) содержимому JSON.</span><span class="sxs-lookup"><span data-stu-id="657bb-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="657bb-199">Теперь мы можем добавить один или несколько документов.</span><span class="sxs-lookup"><span data-stu-id="657bb-199">We can now insert one or more documents.</span></span> <span data-ttu-id="657bb-200">При наличии данных, отсылаемых toostore в базе данных можно использовать hello Azure Cosmos DB [средство переноса данных](import-data.md) tooimport hello данных в базу данных.</span><span class="sxs-lookup"><span data-stu-id="657bb-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="657bb-201">Во-первых, мы должны toocreate **семейства** класс, представляющий объекты в базе данных Azure Cosmos в этом образце.</span><span class="sxs-lookup"><span data-stu-id="657bb-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="657bb-202">Мы также создадим подклассы **Parent**, **Child**, **Pet** и **Address**, используемые в классе **Family**.</span><span class="sxs-lookup"><span data-stu-id="657bb-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="657bb-203">Обратите внимание, документы должны иметь свойство **Id**, сериализуемое как **id** в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="657bb-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="657bb-204">Эти классы можно создать, добавив следующие внутренние вложенные классы после hello hello **GetStartedDemo** метод.</span><span class="sxs-lookup"><span data-stu-id="657bb-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="657bb-205">Скопируйте и вставьте hello **семейства**, **родительского**, **дочерних**, **Pet**, и **адрес** классы после hello **WriteToConsoleAndPromptToContinue** метод.</span><span class="sxs-lookup"><span data-stu-id="657bb-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="657bb-206">Скопируйте и вставьте hello **CreateFamilyDocumentIfNotExists** под вашей **адрес** класса.</span><span class="sxs-lookup"><span data-stu-id="657bb-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="657bb-207">Добавьте два документа, одному для каждого семейства Андерсен hello и hello Wakefield семейства.</span><span class="sxs-lookup"><span data-stu-id="657bb-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="657bb-208">Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после создания коллекции документов hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

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

<span data-ttu-id="657bb-209">Нажмите клавишу **F5** toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="657bb-210">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-210">Congratulations!</span></span> <span data-ttu-id="657bb-211">Вы успешно создали два документа Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Схема, иллюстрирующая hello иерархическую связь между hello учетной записи, hello оперативную базу данных, коллекции hello и hello документов, созданных hello NoSQL учебника toocreate консольное приложение C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="657bb-213"><a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="657bb-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="657bb-214">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="657bb-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="657bb-215">Hello следующий образец кода показывает различные запросы — оба SQL Azure Cosmos базы данных с помощью синтаксиса, а также LINQ - что мы может выполняться hello документов, над которыми мы вставлены в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="657bb-216">Скопируйте и вставьте hello **ExecuteSimpleQuery** метод после вашей **CreateFamilyDocumentIfNotExists** метод.</span><span class="sxs-lookup"><span data-stu-id="657bb-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="657bb-217">Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после создания второго документа hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="657bb-218">Нажмите клавишу **F5** toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="657bb-219">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-219">Congratulations!</span></span> <span data-ttu-id="657bb-220">Вы успешно выполнили запрос коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="657bb-221">Hello следующей схеме показано, как hello базы данных SQL Azure Cosmos синтаксис называется с коллекцией hello созданный запрос и hello же принцип применяется также toohello запроса LINQ.</span><span class="sxs-lookup"><span data-stu-id="657bb-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Диаграмму, демонстрирующая области hello и это означает hello запроса используется hello NoSQL учебника toocreate консольное приложение C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="657bb-223">Hello [FROM](documentdb-sql-query.md#FromClause) ключевое слово является необязательным в hello запроса, так как запросы Azure Cosmos DB уже области tooa одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="657bb-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="657bb-224">Поэтому слова "FROM Families f" можно заменить на "FROM root r" или любое другое имя переменной.</span><span class="sxs-lookup"><span data-stu-id="657bb-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="657bb-225">Azure Cosmos DB определит, что семейств, корень или имя переменной hello выбрана, ссылка hello текущей коллекции по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="657bb-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="657bb-226"><a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON</span><span class="sxs-lookup"><span data-stu-id="657bb-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="657bb-227">Azure Cosmos DB поддерживает замену документов JSON.</span><span class="sxs-lookup"><span data-stu-id="657bb-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="657bb-228">Скопируйте и вставьте hello **ReplaceFamilyDocument** метод после вашей **ExecuteSimpleQuery** метод.</span><span class="sxs-lookup"><span data-stu-id="657bb-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="657bb-229">Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после выполнения запроса hello в конце hello метод hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="657bb-230">После замены hello документа, это будет выполняться hello же попытку запроса tooview hello изменения документа.</span><span class="sxs-lookup"><span data-stu-id="657bb-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="657bb-231">Нажмите клавишу **F5** toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="657bb-232">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-232">Congratulations!</span></span> <span data-ttu-id="657bb-233">Вы успешно заменили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="657bb-234"><a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON</span><span class="sxs-lookup"><span data-stu-id="657bb-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="657bb-235">Azure Cosmos DB поддерживает удаление документов JSON.</span><span class="sxs-lookup"><span data-stu-id="657bb-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="657bb-236">Скопируйте и вставьте hello **DeleteFamilyDocument** метод после вашей **ReplaceFamilyDocument** метод.</span><span class="sxs-lookup"><span data-stu-id="657bb-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="657bb-237">Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после выполнения второго запроса hello, в конце hello метод hello.</span><span class="sxs-lookup"><span data-stu-id="657bb-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="657bb-238">Нажмите клавишу **F5** toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="657bb-239">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-239">Congratulations!</span></span> <span data-ttu-id="657bb-240">Вы успешно удалили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="657bb-241"><a id="DeleteDatabase"></a>Шаг 10: Удаление hello базы данных</span><span class="sxs-lookup"><span data-stu-id="657bb-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="657bb-242">Идет удаление hello создана база данных приведет к удалению hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="657bb-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="657bb-243">Копировать и вставить hello следующий код tooyour **GetStartedDemo** метод после документа hello удалить toodelete hello всю базу данных и все дочерние ресурсы.</span><span class="sxs-lookup"><span data-stu-id="657bb-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="657bb-244">Нажмите клавишу **F5** toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="657bb-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="657bb-245">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-245">Congratulations!</span></span> <span data-ttu-id="657bb-246">Вы успешно удалили базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="657bb-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="657bb-247"><a id="Run"></a>Шаг 11. Запуск консольного приложения C#</span><span class="sxs-lookup"><span data-stu-id="657bb-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="657bb-248">Нажмите клавишу F5 в Visual Studio toobuild hello приложения в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="657bb-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="657bb-249">Вы увидите выходные данные hello get работы приложения в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="657bb-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="657bb-250">выходные данные Hello покажет результаты hello hello запросов мы добавлен и должен соответствовать hello пример текста ниже.</span><span class="sxs-lookup"><span data-stu-id="657bb-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

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

<span data-ttu-id="657bb-251">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="657bb-251">Congratulations!</span></span> <span data-ttu-id="657bb-252">После завершения учебника hello и иметь работу консольного приложения C#!</span><span class="sxs-lookup"><span data-stu-id="657bb-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="657bb-253"><a id="GetSolution"></a>Получить комплексное решение учебника hello</span><span class="sxs-lookup"><span data-stu-id="657bb-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="657bb-254">Если бы не было времени toocomplete hello шаги в этом учебнике или просто хотите toodownload hello образцы кода, можно получить его из [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="657bb-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="657bb-255">решение GetStarted toobuild hello, вам потребуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="657bb-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="657bb-256">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="657bb-256">An active Azure account.</span></span> <span data-ttu-id="657bb-257">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="657bb-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="657bb-258">[Учетная запись Azure Cosmos DB][cosmos-db-create-account]</span><span class="sxs-lookup"><span data-stu-id="657bb-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="657bb-259">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) решения на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="657bb-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="657bb-260">toohello ссылки toorestore hello Azure Cosmos DB .NET SDK в Visual Studio щелкните правой кнопкой мыши hello **GetStarted** решения в обозревателе решений, а затем выберите **включите восстановление пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="657bb-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="657bb-261">Затем в файле App.config hello, обновите значения EndpointUrl и AuthorizationKey hello как описано в [подключить учетную запись Azure Cosmos DB tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="657bb-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="657bb-262">Теперь все готово. Выполните сборку и начинайте работу с решением.</span><span class="sxs-lookup"><span data-stu-id="657bb-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="657bb-263">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="657bb-263">Next steps</span></span>
* <span data-ttu-id="657bb-264">Требуется более подробное руководство по ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="657bb-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="657bb-265">См. [Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="657bb-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="657bb-266">Требуется tooperform масштаб и производительность, тестирование с помощью Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="657bb-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="657bb-267">См. [Проверка производительности и масштабирования с помощью Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="657bb-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="657bb-268">Узнайте, каким образом слишком[отслеживать запросы, использования и хранилища Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="657bb-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="657bb-269">Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="657bb-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="657bb-270">toolearn Дополнительные сведения о базе данных Azure Cosmos, в разделе [Добро пожаловать tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="657bb-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
