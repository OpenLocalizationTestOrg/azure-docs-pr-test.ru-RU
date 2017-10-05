---
title: "Azure Cosmos DB. Приступая к работе с API DocumentDB | Документация Майкрософт"
description: "В этом руководстве описывается создание оперативной базы данных и консольного приложения C# с помощью API DocumentDB."
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
ms.openlocfilehash: 72f66081a6409f980ec6bca5188f585489245a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="b0a21-104">Azure Cosmos DB. Приступая к работе с API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b0a21-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0a21-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b0a21-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="b0a21-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b0a21-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="b0a21-107">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="b0a21-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="b0a21-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="b0a21-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="b0a21-109">Java</span><span class="sxs-lookup"><span data-stu-id="b0a21-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="b0a21-110">C++</span><span class="sxs-lookup"><span data-stu-id="b0a21-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="b0a21-111">Давайте приступим к обзору API DocumentDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-111">Welcome to the Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="b0a21-112">После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="b0a21-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="b0a21-113">Мы рассмотрим следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="b0a21-113">We'll cover:</span></span>

* <span data-ttu-id="b0a21-114">создание учетной записи Azure Cosmos DB и подключение к ней;</span><span class="sxs-lookup"><span data-stu-id="b0a21-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="b0a21-115">настройка решения Visual Studio;</span><span class="sxs-lookup"><span data-stu-id="b0a21-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="b0a21-116">Создание оперативной базы данных</span><span class="sxs-lookup"><span data-stu-id="b0a21-116">Creating an online database</span></span>
* <span data-ttu-id="b0a21-117">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="b0a21-117">Creating a collection</span></span>
* <span data-ttu-id="b0a21-118">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="b0a21-118">Creating JSON documents</span></span>
* <span data-ttu-id="b0a21-119">выполнение запросов к коллекции;</span><span class="sxs-lookup"><span data-stu-id="b0a21-119">Querying the collection</span></span>
* <span data-ttu-id="b0a21-120">замена документа;</span><span class="sxs-lookup"><span data-stu-id="b0a21-120">Replacing a document</span></span>
* <span data-ttu-id="b0a21-121">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="b0a21-121">Deleting a document</span></span>
* <span data-ttu-id="b0a21-122">удаление базы данных.</span><span class="sxs-lookup"><span data-stu-id="b0a21-122">Deleting the database</span></span>

<span data-ttu-id="b0a21-123">У вас нет времени?</span><span class="sxs-lookup"><span data-stu-id="b0a21-123">Don't have time?</span></span> <span data-ttu-id="b0a21-124">Не беспокойтесь!</span><span class="sxs-lookup"><span data-stu-id="b0a21-124">Don't worry!</span></span> <span data-ttu-id="b0a21-125">Полное решение доступно на [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="b0a21-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="b0a21-126">Краткие инструкции см. в разделе [Получение полного решения NoSQL для этого руководства](#GetSolution).</span><span class="sxs-lookup"><span data-stu-id="b0a21-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="b0a21-127">После этого используйте кнопки голосования в верхней или нижней части этой страницы, чтобы отправить нам отзыв.</span><span class="sxs-lookup"><span data-stu-id="b0a21-127">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="b0a21-128">Если вы хотите, чтобы мы связались с вами, укажите ваш электронный адрес в комментариях.</span><span class="sxs-lookup"><span data-stu-id="b0a21-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="b0a21-129">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="b0a21-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0a21-130">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b0a21-130">Prerequisites</span></span>
<span data-ttu-id="b0a21-131">Убедитесь, что у вас есть указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="b0a21-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="b0a21-132">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a21-132">An active Azure account.</span></span> <span data-ttu-id="b0a21-133">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b0a21-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="b0a21-134">Кроме того, в этом руководстве можно использовать [эмулятор Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="b0a21-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="b0a21-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="b0a21-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="b0a21-136">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b0a21-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="b0a21-137">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="b0a21-138">Если у вас уже есть учетная запись, которую вы собираетесь использовать, можно перейти к шагу [Настройка решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b0a21-138">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="b0a21-139">Если вы используете эмулятор Azure Cosmos DB, выполните действия, описанные в статье об [эмуляторе Azure Cosmos DB](local-emulator.md), чтобы его настроить и сразу перейти к [настройке решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b0a21-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="b0a21-140"><a id="SetupVS"></a> Шаг 2. Настройка решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0a21-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="b0a21-141">Откройте **Visual Studio 2017** у себя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b0a21-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="b0a21-142">В меню **Файл** выберите пункт **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-142">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="b0a21-143">В диалоговом окне **Новый проект** выберите **Шаблоны** / **Visual C#** / **Консольное приложение**, а затем укажите имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-143">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="b0a21-144">![Снимок экрана: диалоговое окно «Новый проект»](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="b0a21-144">![Screen shot of the New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="b0a21-145">В **обозревателе решений** щелкните правой кнопкой мыши новое консольное приложение (оно находится в решении Visual Studio). Затем щелкните **Управление пакетами NuGet...**</span><span class="sxs-lookup"><span data-stu-id="b0a21-145">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Снимок экрана: меню «Проект», вызванное щелчком правой кнопки мыши](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="b0a21-147">На вкладке **Nuget** щелкните **Обзор** и в поле поиска введите **azure documentdb**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-147">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="b0a21-148">В результатах найдите **Microsoft.Azure.DocumentDB** и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-148">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="b0a21-149">Идентификатор пакета для клиентской библиотеки API Azure Cosmos DB и DocumentDB — [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="b0a21-149">The package ID for the Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="b0a21-150">![Снимок экрана меню NuGet для поиска пакета SDK для клиента Azure Cosmos DB](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="b0a21-150">![Screen shot of the Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="b0a21-151">Если появится сообщение о просмотре изменений в решении, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-151">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="b0a21-152">Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="b0a21-153">Отлично!</span><span class="sxs-lookup"><span data-stu-id="b0a21-153">Great!</span></span> <span data-ttu-id="b0a21-154">Теперь, когда мы завершили настройку, начнем писать код.</span><span class="sxs-lookup"><span data-stu-id="b0a21-154">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="b0a21-155">Вы можете найти проект готового кода для этого руководства в [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="b0a21-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="b0a21-156"><a id="Connect"></a>Шаг 3. Подключение к учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b0a21-156"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="b0a21-157">Во-первых, добавьте эти ссылки в начало приложения C# в файле Program.cs:</span><span class="sxs-lookup"><span data-stu-id="b0a21-157">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="b0a21-158">Чтобы завершить работу с этим руководством, добавьте приведенные выше зависимости.</span><span class="sxs-lookup"><span data-stu-id="b0a21-158">In order to complete the tutorial, make sure you add the dependencies above.</span></span>
> 
> 

<span data-ttu-id="b0a21-159">Теперь добавьте эти две константы и переменную *client* в открытый класс *Program*.</span><span class="sxs-lookup"><span data-stu-id="b0a21-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="b0a21-160">Далее вернитесь на [портал Azure](https://portal.azure.com), чтобы получить URL-адрес конечной точки и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="b0a21-160">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="b0a21-161">URL-адрес конечной точки и первичный ключ позволяют приложению предоставлять данные о расположении, в котором будет устанавливаться подключение, что делает подключение вашего приложения доверенным для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-161">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="b0a21-162">На портале Azure перейдите к учетной записи Azure Cosmos DB, а затем щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-162">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="b0a21-163">Скопируйте универсальный код ресурса (URI) с портала и вставьте его в параметр `<your endpoint URL>` в файле program.cs.</span><span class="sxs-lookup"><span data-stu-id="b0a21-163">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="b0a21-164">Затем скопируйте на портале значение поля "Первичный ключ" и вставьте его в параметр `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="b0a21-164">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![Снимок экрана портала Azure в ходе работы с руководством по NoSQL при создании консольного приложения C#.][keys]

<span data-ttu-id="b0a21-167">Теперь мы запустим приложение, создав экземпляр **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-167">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="b0a21-168">В методе **Main** добавьте эту новую асинхронную задачу с именем **GetStartedDemo**, которая создает экземпляр **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-168">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="b0a21-169">Добавьте указанный далее код, чтобы запустить асинхронную задачу из метода **Main** .</span><span class="sxs-lookup"><span data-stu-id="b0a21-169">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="b0a21-170">Метод **Main** будет перехватывать исключения и записывать их в консоли.</span><span class="sxs-lookup"><span data-stu-id="b0a21-170">The **Main** method will catch exceptions and write them to the console.</span></span>

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

<span data-ttu-id="b0a21-171">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0a21-171">Press **F5** to run your application.</span></span> <span data-ttu-id="b0a21-172">Результаты в окне консоли отображают сообщение `End of demo, press any key to exit.`. Это означает, что подключение выполнено.</span><span class="sxs-lookup"><span data-stu-id="b0a21-172">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="b0a21-173">Теперь можно закрыть окно консоли.</span><span class="sxs-lookup"><span data-stu-id="b0a21-173">You can then close the console window.</span></span> 

<span data-ttu-id="b0a21-174">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-174">Congratulations!</span></span> <span data-ttu-id="b0a21-175">Вы успешно подключились к учетной записи Azure Cosmos DB. Давайте теперь рассмотрим принципы работы с ресурсами Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-175">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="b0a21-176">Этап 4: создание базы данных</span><span class="sxs-lookup"><span data-stu-id="b0a21-176">Step 4: Create a database</span></span>
<span data-ttu-id="b0a21-177">Прежде чем добавлять код для создания базы данных, добавьте вспомогательный метод для записи на консоль.</span><span class="sxs-lookup"><span data-stu-id="b0a21-177">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="b0a21-178">Скопируйте и вставьте метод **WriteToConsoleAndPromptToContinue** после кода метода **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-178">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="b0a21-179">Вы можете создать [базу данных](documentdb-resources.md#databases) Azure Cosmos DB с помощью метода [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) класса **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b0a21-180">База данных представляет собой логический контейнер для хранения документов JSON, разделенных между коллекциями.</span><span class="sxs-lookup"><span data-stu-id="b0a21-180">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="b0a21-181">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** после кода создания клиента.</span><span class="sxs-lookup"><span data-stu-id="b0a21-181">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="b0a21-182">Будет создана база данных с именем *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="b0a21-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="b0a21-183">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0a21-183">Press **F5** to run your application.</span></span>

<span data-ttu-id="b0a21-184">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-184">Congratulations!</span></span> <span data-ttu-id="b0a21-185">Вы успешно создали базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="b0a21-186"><a id="CreateColl"></a>Этап 5: создание коллекции</span><span class="sxs-lookup"><span data-stu-id="b0a21-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="b0a21-187">С помощью метода **CreateDatabaseIfNotExistsAsync** можно создать новую коллекцию с зарезервированной пропускной способностью и соответствующей ценой.</span><span class="sxs-lookup"><span data-stu-id="b0a21-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="b0a21-188">Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b0a21-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="b0a21-189">Вы можете создать [коллекцию](documentdb-resources.md#collections), используя метод [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) класса **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-189">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b0a21-190">Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b0a21-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="b0a21-191">Скопируйте и вставьте следующий код в метод **GetStartedDemo** после кода создания базы данных.</span><span class="sxs-lookup"><span data-stu-id="b0a21-191">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="b0a21-192">Будет создана коллекция документов с именем *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="b0a21-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="b0a21-193">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0a21-193">Press **F5** to run your application.</span></span>

<span data-ttu-id="b0a21-194">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-194">Congratulations!</span></span> <span data-ttu-id="b0a21-195">Вы успешно создали коллекцию документов Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="b0a21-196"><a id="CreateDoc"></a>Шаг 6. Создание документов JSON</span><span class="sxs-lookup"><span data-stu-id="b0a21-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="b0a21-197">Вы можете создать [документ](documentdb-resources.md#documents) с помощью метода [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx), который относится к классу **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-197">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="b0a21-198">Документы относятся к пользовательскому (произвольному) содержимому JSON.</span><span class="sxs-lookup"><span data-stu-id="b0a21-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="b0a21-199">Теперь мы можем добавить один или несколько документов.</span><span class="sxs-lookup"><span data-stu-id="b0a21-199">We can now insert one or more documents.</span></span> <span data-ttu-id="b0a21-200">Если у вас уже есть данные, которые вы хотите хранить в базе данных, вы можете использовать [средство миграции данных](import-data.md) Azure Cosmos DB, чтобы импортировать эти данные в базу данных.</span><span class="sxs-lookup"><span data-stu-id="b0a21-200">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="b0a21-201">Сначала необходимо создать класс **Family**, который будет представлять объекты, хранящиеся в Azure Cosmos DB в этом примере.</span><span class="sxs-lookup"><span data-stu-id="b0a21-201">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="b0a21-202">Мы также создадим подклассы **Parent**, **Child**, **Pet** и **Address**, используемые в классе **Family**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="b0a21-203">Обратите внимание, документы должны иметь свойство **Id**, сериализуемое как **id** в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="b0a21-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="b0a21-204">Для этого после метода **GetStartedDemo** необходимо добавить следующие подклассы.</span><span class="sxs-lookup"><span data-stu-id="b0a21-204">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="b0a21-205">Скопируйте и вставьте классы **Family**, **Parent**, **Child**, **Pet** и **Address** после кода метода **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-205">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="b0a21-206">Скопируйте и вставьте метод **CreateFamilyDocumentIfNotExists** под кодом класса **Address**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-206">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="b0a21-207">Затем вставьте два документа, один для семьи Андерсен и один для семьи Вейкфилд.</span><span class="sxs-lookup"><span data-stu-id="b0a21-207">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="b0a21-208">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** после кода создания коллекции документов.</span><span class="sxs-lookup"><span data-stu-id="b0a21-208">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


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

<span data-ttu-id="b0a21-209">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0a21-209">Press **F5** to run your application.</span></span>

<span data-ttu-id="b0a21-210">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-210">Congratulations!</span></span> <span data-ttu-id="b0a21-211">Вы успешно создали два документа Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![На схеме представлены иерархические отношения между учетной записью, оперативной базой данных, коллекцией и документами, используемыми в руководстве по NoSQL при создании консольного приложения C#.](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="b0a21-213"><a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b0a21-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="b0a21-214">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="b0a21-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="b0a21-215">Ниже приведены примеры кода разнообразных запросов с использованием как синтаксиса SQL в Azure Cosmos DB, так и LINQ, которые можно запускать для добавленных на предыдущем шаге документов.</span><span class="sxs-lookup"><span data-stu-id="b0a21-215">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="b0a21-216">Скопируйте и вставьте метод **ExecuteSimpleQuery** после кода метода **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-216">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="b0a21-217">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** после кода создания второго документа.</span><span class="sxs-lookup"><span data-stu-id="b0a21-217">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="b0a21-218">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0a21-218">Press **F5** to run your application.</span></span>

<span data-ttu-id="b0a21-219">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-219">Congratulations!</span></span> <span data-ttu-id="b0a21-220">Вы успешно выполнили запрос коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="b0a21-221">На схеме ниже показано, как для созданной коллекции вызывается синтаксис запроса SQL для Azure Cosmos DB. Та же логика применяется и к запросам LINQ.</span><span class="sxs-lookup"><span data-stu-id="b0a21-221">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![На схеме представлен масштаб и значение запроса, используемого в руководстве по NoSQL при создании консольного приложения C#.](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="b0a21-223">Ключевое слово [FROM](documentdb-sql-query.md#FromClause) использовать в запросе необязательно, так как запросы Azure Cosmos DB привязаны только к одной коллекции.</span><span class="sxs-lookup"><span data-stu-id="b0a21-223">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="b0a21-224">Поэтому слова "FROM Families f" можно заменить на "FROM root r" или любое другое имя переменной.</span><span class="sxs-lookup"><span data-stu-id="b0a21-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="b0a21-225">Поведение службы Azure Cosmos DB будет таким, будто Families, root или любая другая переменная указывает на текущую коллекцию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b0a21-225">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="b0a21-226"><a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON</span><span class="sxs-lookup"><span data-stu-id="b0a21-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="b0a21-227">Azure Cosmos DB поддерживает замену документов JSON.</span><span class="sxs-lookup"><span data-stu-id="b0a21-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="b0a21-228">Скопируйте и вставьте метод **ReplaceFamilyDocument** после кода метода **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-228">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="b0a21-229">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** после кода выполнения запроса в конце метода.</span><span class="sxs-lookup"><span data-stu-id="b0a21-229">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="b0a21-230">После замены документа тот же запрос будет запущен повторно, чтобы вы могли просмотреть измененный документ.</span><span class="sxs-lookup"><span data-stu-id="b0a21-230">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="b0a21-231">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0a21-231">Press **F5** to run your application.</span></span>

<span data-ttu-id="b0a21-232">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-232">Congratulations!</span></span> <span data-ttu-id="b0a21-233">Вы успешно заменили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="b0a21-234"><a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON</span><span class="sxs-lookup"><span data-stu-id="b0a21-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="b0a21-235">Azure Cosmos DB поддерживает удаление документов JSON.</span><span class="sxs-lookup"><span data-stu-id="b0a21-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="b0a21-236">Скопируйте и вставьте метод **DeleteFamilyDocument** после кода метода **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="b0a21-236">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="b0a21-237">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** после кода выполнения второго запроса в конце метода.</span><span class="sxs-lookup"><span data-stu-id="b0a21-237">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="b0a21-238">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0a21-238">Press **F5** to run your application.</span></span>

<span data-ttu-id="b0a21-239">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-239">Congratulations!</span></span> <span data-ttu-id="b0a21-240">Вы успешно удалили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="b0a21-241"><a id="DeleteDatabase"></a>Шаг 10. Удаление базы данных</span><span class="sxs-lookup"><span data-stu-id="b0a21-241"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="b0a21-242">Удаление созданной базы данных приведет к удалению базы данных и всех дочерних ресурсов (коллекций, документов и т. д.).</span><span class="sxs-lookup"><span data-stu-id="b0a21-242">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="b0a21-243">Скопируйте и вставьте приведенный код в метод **GetStartedDemo** после кода удаления документа, чтобы удалить всю базу данных и все дочерние ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b0a21-243">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="b0a21-244">Нажмите клавишу **F5** , чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0a21-244">Press **F5** to run your application.</span></span>

<span data-ttu-id="b0a21-245">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-245">Congratulations!</span></span> <span data-ttu-id="b0a21-246">Вы успешно удалили базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0a21-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="b0a21-247"><a id="Run"></a>Шаг 11. Запуск консольного приложения C#</span><span class="sxs-lookup"><span data-stu-id="b0a21-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="b0a21-248">Чтобы создать приложение в режиме отладки, откройте Visual Studio и нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="b0a21-248">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="b0a21-249">В окне консоли должны отобразиться выходные данные вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b0a21-249">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="b0a21-250">Они должны содержать результаты обработки добавленных запросов. При этом выглядеть они должны примерно так, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="b0a21-250">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
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

<span data-ttu-id="b0a21-251">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b0a21-251">Congratulations!</span></span> <span data-ttu-id="b0a21-252">Вы завершили работу с этим руководством, и теперь у вас есть работающее консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="b0a21-252">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="b0a21-253"><a id="GetSolution"></a>Получение готового решения для этого руководства</span><span class="sxs-lookup"><span data-stu-id="b0a21-253"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="b0a21-254">Если у вас нет времени на выполнение шагов из этого руководства или вы хотите просто скачать примеры кода, это можно сделать на портале [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="b0a21-254">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="b0a21-255">Чтобы создать решение GetStarted, требуются следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="b0a21-255">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="b0a21-256">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a21-256">An active Azure account.</span></span> <span data-ttu-id="b0a21-257">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b0a21-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="b0a21-258">[Учетная запись Azure Cosmos DB][cosmos-db-create-account]</span><span class="sxs-lookup"><span data-stu-id="b0a21-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="b0a21-259">решение [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) , доступное в GitHub.</span><span class="sxs-lookup"><span data-stu-id="b0a21-259">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="b0a21-260">Чтобы в Visual Studio восстановить ссылки на пакет SDK .NET для Azure Cosmos DB, в обозревателе решений щелкните правой кнопкой мыши решение **GetStarted**, а затем выберите пункт **Enable NuGet Package Restore** (Включить восстановление пакета NuGet).</span><span class="sxs-lookup"><span data-stu-id="b0a21-260">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="b0a21-261">Затем в файле App.config обновите значения EndpointUrl и AuthorizationKey согласно инструкциям, описанным в разделе о [подключении к учетной записи Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="b0a21-261">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="b0a21-262">Теперь все готово. Выполните сборку и начинайте работу с решением.</span><span class="sxs-lookup"><span data-stu-id="b0a21-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="b0a21-263">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0a21-263">Next steps</span></span>
* <span data-ttu-id="b0a21-264">Требуется более подробное руководство по ASP.NET MVC?</span><span class="sxs-lookup"><span data-stu-id="b0a21-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="b0a21-265">См. [Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="b0a21-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="b0a21-266">Хотите выполнять проверку масштабирования и производительности с помощью Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="b0a21-266">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="b0a21-267">См. [Проверка производительности и масштабирования с помощью Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="b0a21-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="b0a21-268">Узнайте, как организовать [мониторинг запросов, использования и хранилища Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="b0a21-268">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="b0a21-269">Отправьте запросы образцу набора данных в [Площадке для запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="b0a21-269">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="b0a21-270">Дополнительные сведения об Azure Cosmos DB см. в статье [Добро пожаловать в базу данных Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="b0a21-270">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
