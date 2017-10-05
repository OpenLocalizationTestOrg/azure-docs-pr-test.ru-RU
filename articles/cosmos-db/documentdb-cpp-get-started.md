---
title: "Руководство по C++ для Azure Cosmos DB | Документация Майкрософт"
description: "Руководство по C++, в котором создается база данных и консольное приложение C++ с помощью Azure Cosmos DB с поддержкой пакета SDK для C++. Azure Cosmos DB — это глобально масштабируемая служба базы данных."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="b1e7c-104">Azure Cosmos DB. Руководство по использованию консольного приложения C++ для API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b1e7c-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1e7c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b1e7c-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="b1e7c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="b1e7c-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="b1e7c-107">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="b1e7c-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="b1e7c-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="b1e7c-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="b1e7c-109">Java</span><span class="sxs-lookup"><span data-stu-id="b1e7c-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="b1e7c-110">C++</span><span class="sxs-lookup"><span data-stu-id="b1e7c-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="b1e7c-111">Мы рады представить вам руководство по C++ для соответствующего пакета SDK для API DocumentDB Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="b1e7c-112">По завершении работы с этим руководством у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и выполняет запросы этих ресурсов, включая базу данных C++.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="b1e7c-113">Мы рассмотрим следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="b1e7c-113">We'll cover:</span></span>

* <span data-ttu-id="b1e7c-114">создание учетной записи Azure Cosmos DB и подключение к ней;</span><span class="sxs-lookup"><span data-stu-id="b1e7c-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="b1e7c-115">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="b1e7c-115">Setting up your application</span></span>
* <span data-ttu-id="b1e7c-116">создание базы данных Azure Cosmos DB для C++;</span><span class="sxs-lookup"><span data-stu-id="b1e7c-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="b1e7c-117">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="b1e7c-117">Creating a collection</span></span>
* <span data-ttu-id="b1e7c-118">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="b1e7c-118">Creating JSON documents</span></span>
* <span data-ttu-id="b1e7c-119">выполнение запросов к коллекции;</span><span class="sxs-lookup"><span data-stu-id="b1e7c-119">Querying the collection</span></span>
* <span data-ttu-id="b1e7c-120">замена документа;</span><span class="sxs-lookup"><span data-stu-id="b1e7c-120">Replacing a document</span></span>
* <span data-ttu-id="b1e7c-121">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="b1e7c-121">Deleting a document</span></span>
* <span data-ttu-id="b1e7c-122">удаление базы данных Azure Cosmos DB для C++.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="b1e7c-123">У вас нет времени?</span><span class="sxs-lookup"><span data-stu-id="b1e7c-123">Don't have time?</span></span> <span data-ttu-id="b1e7c-124">Не беспокойтесь!</span><span class="sxs-lookup"><span data-stu-id="b1e7c-124">Don't worry!</span></span> <span data-ttu-id="b1e7c-125">Полное решение доступно на [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="b1e7c-126">Краткие инструкции см. в разделе [Получение полного решения для руководства по Node.js](#GetSolution).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="b1e7c-127">Ознакомившись с руководством по C++, воспользуйтесь кнопками голосования в нижней части этой страницы, чтобы отправить нам отзыв.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="b1e7c-128">Если вы хотите, чтобы мы связались с вами, укажите свой электронный адрес в комментариях или [оправьте свои данные отсюда](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="b1e7c-129">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="b1e7c-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="b1e7c-130">Предварительные требования для прохождения руководства по C++</span><span class="sxs-lookup"><span data-stu-id="b1e7c-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="b1e7c-131">Убедитесь, что у вас есть указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="b1e7c-132">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-132">An active Azure account.</span></span> <span data-ttu-id="b1e7c-133">Если у вас нет такой учетной записи, вы можете зарегистрироваться для использования [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b1e7c-134">[Visual Studio](https://www.visualstudio.com/downloads/) и установленные компоненты языка C++.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="b1e7c-135">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b1e7c-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="b1e7c-136">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="b1e7c-137">Если у вас уже есть учетная запись, которую вы собираетесь использовать, можно перейти к шагу [Настройка приложения C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="b1e7c-138"><a id="SetupC++"></a>Шаг 2. Настройка приложения C++</span><span class="sxs-lookup"><span data-stu-id="b1e7c-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="b1e7c-139">Откройте Visual Studio, выберите меню **Файл**, щелкните команду **Создать**, а затем **Проект**.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="b1e7c-140">В окне **Создание проекта** в области **Установленные** разверните узел **Visual C++**, щелкните **Win32**, а затем **Консольное приложение Win32**.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="b1e7c-141">Присвойте проекту имя hellodocumentdb и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Снимок экрана с изображением мастера создания проектов](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="b1e7c-143">Когда мастер настройки приложений Win32 запустится, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="b1e7c-144">Когда проект будет создан, откройте диспетчер пакетов NuGet. Для этого щелкните правой кнопкой мыши проект **hellodocumentdb** в **обозревателе решений** и выберите пункт **Manage NuGet Packages** (Управление пакетами NuGet).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Снимок экрана с изображением пункта Manage NuGet Packages ("Управление пакетами NuGet") в меню проекта](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="b1e7c-146">На вкладке **NuGet: hellodocumentdb** щелкните раздел **Browse** (Обзор) и найдите *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="b1e7c-147">Среди результатов выберите DocumentDbCPP, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="b1e7c-148">Этот пакет устанавливает ссылки на пакет C++ REST SDK, который зависит от DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![Снимок экрана с изображением выделенного пакета DocumentDbCpp](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="b1e7c-150">После добавления пакетов в проект, можно приступить к написанию кода.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="b1e7c-151"><a id="Config"></a>Шаг 3. Копирование сведений о подключении для базы данных Azure Cosmos DB из портала Azure</span><span class="sxs-lookup"><span data-stu-id="b1e7c-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="b1e7c-152">Откройте [портал Azure](https://portal.azure.com) и просмотрите созданную учетную запись базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="b1e7c-153">Для следующего шага понадобится универсальный код ресурса (URI) и первичный ключ из портала Azure, чтобы установить подключение с помощью фрагмента кода C++.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![Универсальный код ресурса (URI) и ключи Azure Cosmos DB на портале Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="b1e7c-155"><a id="Connect"></a>Шаг 4. Подключение к учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b1e7c-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="b1e7c-156">Добавьте в исходный код после `#include "stdafx.h"` следующие пространства имен и заголовки.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="b1e7c-157">Далее добавьте следующий код к функции main, а затем замените настройки учетной записи и первичный ключ соответствующими параметрами Azure Cosmos DB, скопированными на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="b1e7c-158">Теперь, когда у нас есть код для инициализации клиента DocumentDB, мы рассмотрим принципы работы с ресурсами Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="b1e7c-159"><a id="CreateDBColl"></a>Шаг 5. Создание базы данных и коллекции C++</span><span class="sxs-lookup"><span data-stu-id="b1e7c-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="b1e7c-160">Прежде чем выполнить этот шаг, рассмотрим, как взаимодействуют база данных, коллекция и документы, на случай если вы еще не знакомы с принципами работы Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="b1e7c-161">[База данных](documentdb-resources.md#databases) представляет собой логический контейнер для хранения документов, распределенных по коллекциям.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="b1e7c-162">[Коллекция](documentdb-resources.md#collections) — это контейнер JSON-документов и связанной логики приложения на JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="b1e7c-163">Дополнительные сведения об иерархической модели ресурсов и основных понятиях Azure Cosmos DB см. в [этой статье](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="b1e7c-164">Чтобы создать базу данных и соответствующую коллекцию, добавьте следующий код в конец функции main.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="b1e7c-165">Так вы создадите базу данных с именем FamilyRegistry и коллекцию FamilyCollection, используя конфигурацию клиента, объявленного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="b1e7c-166"><a id="CreateDoc"></a>Шаг 6. Создание документа</span><span class="sxs-lookup"><span data-stu-id="b1e7c-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="b1e7c-167">[Документы](documentdb-resources.md#documents) относятся к пользовательскому (произвольному) JSON-содержимому.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="b1e7c-168">Теперь можно вставить документ в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="b1e7c-169">Документ можно создать, скопировав следующий код в конец функции main.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-169">You can create a document by copying the following code into the end of the main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="b1e7c-170">Таким образом, этот код создает базу данных, коллекцию и документы Azure Cosmos DB, которые можно запросить на портале Azure в проводнике документов.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Руководство по C++. Схема, иллюстрирующая иерархические отношения между учетной записью, базой данных, коллекцией и документами](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="b1e7c-172"><a id="QueryDB"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b1e7c-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="b1e7c-173">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="b1e7c-174">Ниже приведен пример кода запроса, в котором используется синтаксис SQL. Его можно запускать, чтобы запрашивать документы, созданные на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="b1e7c-175">Функция принимает в качестве аргументов уникальный идентификатор или идентификатор ресурса для базы данных и коллекции, а также клиента документов.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="b1e7c-176">Добавьте следующий код перед функцией main.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="b1e7c-177"><a id="Replace"></a>Шаг 8. Замена документа</span><span class="sxs-lookup"><span data-stu-id="b1e7c-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="b1e7c-178">Azure Cosmos DB поддерживает замену JSON-документов, как показано в коде ниже.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="b1e7c-179">Добавьте этот код после функции executesimplequery.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-179">Add this code after the executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="b1e7c-180"><a id="Delete"></a>Шаг 9. Удаление документа</span><span class="sxs-lookup"><span data-stu-id="b1e7c-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="b1e7c-181">Azure Cosmos DB поддерживает удаление JSON-документов. Чтобы удалить документ, скопируйте код ниже и вставьте его после функции replacedocument.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="b1e7c-182"><a id="DeleteDB"></a>Шаг 10. Удаление базы данных</span><span class="sxs-lookup"><span data-stu-id="b1e7c-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="b1e7c-183">Удаление созданной базы данных влечет удаление всех ее дочерних ресурсов (коллекций, документов и т. д.).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="b1e7c-184">Скопируйте и вставьте следующий фрагмент кода (функция cleanup) после функции deletedocument, чтобы удалить базу данных и все ее дочерние ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="b1e7c-185"><a id="Run"></a>Шаг 11. Запуск консольного приложения C++</span><span class="sxs-lookup"><span data-stu-id="b1e7c-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="b1e7c-186">Мы добавили код для создания, запроса, изменения и удаления различных ресурсов Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="b1e7c-187">А теперь мы объединим все это, добавив вызовы различных функций с помощью функции main в hellodocumentdb.cpp, а также некоторые диагностические сообщения.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="b1e7c-188">Чтобы сделать это, замените функцию main приложения кодом ниже.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="b1e7c-189">Данные account_configuration_uri и primary_key, скопированные в код на шаге 3, будут перезаписаны, поэтому сохраните соответствующую строку или скопируйте значения на портале.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="b1e7c-190">Теперь можно собрать и запустить код в Visual Studio, нажав клавишу F5, или в окне терминала через приложение, запустив исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="b1e7c-191">Должны отобразиться выходные данные вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-191">You should see the output of your get started app.</span></span> <span data-ttu-id="b1e7c-192">Выходные данные должны соответствовать показанным на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-192">The output should match the following screenshot.</span></span>

![Выходные данные приложения C++ для Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="b1e7c-194">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b1e7c-194">Congratulations!</span></span> <span data-ttu-id="b1e7c-195">Вы ознакомились с руководством по C++ и создали первое консольное приложение Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="b1e7c-196"><a id="GetSolution"></a>Получение завершенного решения C++ для этого руководства</span><span class="sxs-lookup"><span data-stu-id="b1e7c-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="b1e7c-197">Чтобы собрать решение GetStarted, содержащее все примеры из этой статьи, вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="b1e7c-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="b1e7c-198">[Учетная запись Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="b1e7c-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="b1e7c-199">решение [GetStarted](https://github.com/stalker314314/DocumentDBCpp) , доступное в GitHub.</span><span class="sxs-lookup"><span data-stu-id="b1e7c-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1e7c-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1e7c-200">Next steps</span></span>
* <span data-ttu-id="b1e7c-201">Узнайте, как выполнять [мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="b1e7c-202">Отправьте запросы образцу набора данных в [Площадке для запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="b1e7c-203">Дополнительные сведения о модели программирования см. в разделе "Разработка" [на странице документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="b1e7c-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


