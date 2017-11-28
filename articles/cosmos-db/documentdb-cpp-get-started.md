---
title: "aaaC ++ учебник по базе данных Azure Cosmos | Документы Microsoft"
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
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="015bc-104">Azure Cosmos DB: Учебник по приложения консоли C++ для hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="015bc-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="015bc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="015bc-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="015bc-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="015bc-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="015bc-107">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="015bc-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="015bc-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="015bc-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="015bc-109">Java</span><span class="sxs-lookup"><span data-stu-id="015bc-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="015bc-110">C++</span><span class="sxs-lookup"><span data-stu-id="015bc-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="015bc-111">Учебник по C++ приветствия toohello для hello Azure Cosmos DB DocumentDB API SDK одобрены для C++!</span><span class="sxs-lookup"><span data-stu-id="015bc-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="015bc-112">По завершении работы с этим руководством у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и выполняет запросы этих ресурсов, включая базу данных C++.</span><span class="sxs-lookup"><span data-stu-id="015bc-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="015bc-113">Мы рассмотрим следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="015bc-113">We'll cover:</span></span>

* <span data-ttu-id="015bc-114">Создание и подключение учетной записи Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="015bc-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="015bc-115">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="015bc-115">Setting up your application</span></span>
* <span data-ttu-id="015bc-116">создание базы данных Azure Cosmos DB для C++;</span><span class="sxs-lookup"><span data-stu-id="015bc-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="015bc-117">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="015bc-117">Creating a collection</span></span>
* <span data-ttu-id="015bc-118">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="015bc-118">Creating JSON documents</span></span>
* <span data-ttu-id="015bc-119">Запрос к коллекции hello</span><span class="sxs-lookup"><span data-stu-id="015bc-119">Querying hello collection</span></span>
* <span data-ttu-id="015bc-120">замена документа;</span><span class="sxs-lookup"><span data-stu-id="015bc-120">Replacing a document</span></span>
* <span data-ttu-id="015bc-121">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="015bc-121">Deleting a document</span></span>
* <span data-ttu-id="015bc-122">Удаление базы данных C++ Azure Cosmos DB hello</span><span class="sxs-lookup"><span data-stu-id="015bc-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="015bc-123">У вас нет времени?</span><span class="sxs-lookup"><span data-stu-id="015bc-123">Don't have time?</span></span> <span data-ttu-id="015bc-124">Не беспокойтесь!</span><span class="sxs-lookup"><span data-stu-id="015bc-124">Don't worry!</span></span> <span data-ttu-id="015bc-125">законченное решение Hello можно найти в [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="015bc-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="015bc-126">В разделе [получить комплексное решение hello](#GetSolution) быстрого инструкции.</span><span class="sxs-lookup"><span data-stu-id="015bc-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="015bc-127">После прохождения учебника C++ hello, пожалуйста голосования hello используйте кнопки hello нижней части этой страницы toogive нам отзыв.</span><span class="sxs-lookup"><span data-stu-id="015bc-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="015bc-128">Если вы хотите нам toocontact напрямую, если вам свободного tooinclude адрес вашей электронной почты в комментарии или [направляться toous здесь](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="015bc-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="015bc-129">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="015bc-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="015bc-130">Необходимые условия для учебника hello C++</span><span class="sxs-lookup"><span data-stu-id="015bc-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="015bc-131">Убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="015bc-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="015bc-132">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="015bc-132">An active Azure account.</span></span> <span data-ttu-id="015bc-133">Если у вас нет такой учетной записи, вы можете зарегистрироваться для использования [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="015bc-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="015bc-134">[Visual Studio](https://www.visualstudio.com/downloads/), после установки компонентов языка hello C++.</span><span class="sxs-lookup"><span data-stu-id="015bc-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="015bc-135">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="015bc-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="015bc-136">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="015bc-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="015bc-137">При наличии учетной записи требуется toouse можно сразу перейти слишком[установки приложения на C++](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="015bc-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="015bc-138"><a id="SetupC++"></a>Шаг 2. Настройка приложения C++</span><span class="sxs-lookup"><span data-stu-id="015bc-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="015bc-139">Откройте Visual Studio и затем на hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="015bc-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="015bc-140">В hello **новый проект** окна в hello **установленные** области, разверните **Visual C++**, нажмите кнопку **Win32**и нажмите кнопку  **Консольное приложение Win32**.</span><span class="sxs-lookup"><span data-stu-id="015bc-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="015bc-141">Имя проекта hellodocumentdb hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="015bc-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Снимок экрана приветствия мастера создания проекта](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="015bc-143">После запуска мастера приложений Win32 hello щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="015bc-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="015bc-144">После создания проекта hello откройте диспетчер пакетов NuGet hello, щелкнув правой кнопкой мыши hello **hellodocumentdb** проекта в **обозревателе решений** и щелкнув **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="015bc-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Снимок экрана, показывающий управление пакетами NuGet меню Проект hello](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="015bc-146">В hello **NuGet: hellodocumentdb** щелкните **Обзор**и выполните поиск *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="015bc-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="015bc-147">В результатах hello выберите DocumentDbCPP, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="015bc-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="015bc-148">Этот пакет устанавливает ссылки tooC ++ REST SDK, являющееся зависимостей для hello DocumentDbCPP.</span><span class="sxs-lookup"><span data-stu-id="015bc-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![Снимок экрана, показывающий hello DocumentDbCpp пакета выделен](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="015bc-150">После hello пакеты были добавлены tooyour проект, не все toostart набор написания кода.</span><span class="sxs-lookup"><span data-stu-id="015bc-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="015bc-151"><a id="Config"></a>Шаг 3. Копирование сведений о подключении для базы данных Azure Cosmos DB из портала Azure</span><span class="sxs-lookup"><span data-stu-id="015bc-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="015bc-152">Подключить [портал Azure](https://portal.azure.com) и проходят через toohello Azure Cosmos DB базы данных учетной записи.</span><span class="sxs-lookup"><span data-stu-id="015bc-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="015bc-153">Нам понадобится hello URI и hello первичный ключ с портала Azure в hello следующий шаг tooestablish соединение из наших фрагмент кода C++.</span><span class="sxs-lookup"><span data-stu-id="015bc-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos DB URI и ключей в hello портал Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="015bc-155"><a id="Connect"></a>Шаг 4: Учетная запись Azure Cosmos DB tooan подключения</span><span class="sxs-lookup"><span data-stu-id="015bc-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="015bc-156">Добавить следующие заголовки и пространства имен исходного кода tooyour, после hello `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="015bc-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="015bc-157">Далее необходимо добавьте hello следующим кодом tooyour функция main и замените hello настройки учетной записи и первичного ключа toomatch параметры Azure Cosmos DB из шага 3.</span><span class="sxs-lookup"><span data-stu-id="015bc-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="015bc-158">Теперь, когда имеется hello кода tooinitialize hello documentdb клиента, давайте посмотрим на работе с ресурсами Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="015bc-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="015bc-159"><a id="CreateDBColl"></a>Шаг 5. Создание базы данных и коллекции C++</span><span class="sxs-lookup"><span data-stu-id="015bc-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="015bc-160">Прежде чем мы выполнить этот шаг, давайте посмотрим, взаимодействие базы данных, коллекции и документов для тех, кто уже новый tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="015bc-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="015bc-161">[База данных](documentdb-resources.md#databases) представляет собой логический контейнер для хранения документов, распределенных по коллекциям.</span><span class="sxs-lookup"><span data-stu-id="015bc-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="015bc-162">Объект [коллекции](documentdb-resources.md#collections) — это контейнер документов JSON и hello связанные логика приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="015bc-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="015bc-163">Можно узнать дополнительные сведения о модели иерархической ресурсов Azure Cosmos DB hello и основные понятия в [модель Azure Cosmos DB иерархических ресурсов и понятия](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="015bc-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="015bc-164">toocreate базу данных и соответствующую ему коллекцию добавьте hello следующему коду toohello конца функцию main.</span><span class="sxs-lookup"><span data-stu-id="015bc-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="015bc-165">Это создает базу данных с именем «FamilyRegistry» и коллекцию с именем FamilyCollection с помощью конфигурации клиента hello, объявленного в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="015bc-166"><a id="CreateDoc"></a>Шаг 6. Создание документа</span><span class="sxs-lookup"><span data-stu-id="015bc-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="015bc-167">[Документы](documentdb-resources.md#documents) относятся к пользовательскому (произвольному) JSON-содержимому.</span><span class="sxs-lookup"><span data-stu-id="015bc-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="015bc-168">Теперь можно вставить документ в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="015bc-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="015bc-169">Документ можно создать путем копирования hello, следующий код в конце hello основной функции hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

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

<span data-ttu-id="015bc-170">toosummarize, этот код создает базу данных Azure Cosmos DB, коллекции и документы, которые можно выполнить запрос в обозревателе документов на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="015bc-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![Учебник по C++ - диаграмма, иллюстрирующая hello иерархическую связь между hello учетной записи, hello базы данных, коллекции hello и документы hello](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="015bc-172"><a id="QueryDB"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="015bc-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="015bc-173">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="015bc-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="015bc-174">Hello следующем образце кода показан запрос, выполненные с помощью синтаксиса SQL, который можно запустить с документами hello, созданную на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="015bc-175">функция Hello принимает как аргументы hello уникальный идентификатор или идентификатор ресурса для базы данных hello и коллекции hello вместе с клиента hello документа.</span><span class="sxs-lookup"><span data-stu-id="015bc-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="015bc-176">Добавьте следующий код перед функцией main.</span><span class="sxs-lookup"><span data-stu-id="015bc-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="015bc-177"><a id="Replace"></a>Шаг 8. Замена документа</span><span class="sxs-lookup"><span data-stu-id="015bc-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="015bc-178">Azure Cosmos DB поддерживает вместо документов JSON, как показано в следующим hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="015bc-179">Добавьте следующий код после executesimplequery функции hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-179">Add this code after hello executesimplequery function.</span></span>

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

## <span data-ttu-id="015bc-180"><a id="Delete"></a>Шаг 9. Удаление документа</span><span class="sxs-lookup"><span data-stu-id="015bc-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="015bc-181">Azure Cosmos DB поддерживает удаление документов JSON, это можно сделать путем копирования и вставки hello после кода после функции replacedocument hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

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

## <span data-ttu-id="015bc-182"><a id="DeleteDB"></a>Шаг 10. Удаление базы данных</span><span class="sxs-lookup"><span data-stu-id="015bc-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="015bc-183">Удаление базы данных создана hello удаляет hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="015bc-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="015bc-184">Скопируйте и вставьте следующий фрагмент кода (функция очистки) после hello deletedocument функция tooremove hello базы данных и все дочерние ресурсы hello hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="015bc-185"><a id="Run"></a>Шаг 11. Запуск консольного приложения C++</span><span class="sxs-lookup"><span data-stu-id="015bc-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="015bc-186">Мы добавили toocreate кода, запрос, изменение и удаление различных ресурсов Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="015bc-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="015bc-187">Сообщите нам сейчас подключите это, добавив различные функции toothese вызовы из наших основная функция hellodocumentdb.cpp, а также некоторые диагностические сообщения.</span><span class="sxs-lookup"><span data-stu-id="015bc-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="015bc-188">Это можно сделать путем замены hello основная функция приложения hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="015bc-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="015bc-189">Этой записи над hello account_configuration_uri и primary_key, скопированные в код hello в шаге 3, поэтому, строки или копирование значения hello в снова сохраните из портала hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

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

<span data-ttu-id="015bc-190">Теперь следует toobuild может быть и запуска кода в Visual Studio, нажав клавишу F5 или в качестве альтернативы hello исполняемый файл в окне терминала hello приложения hello и под управлением.</span><span class="sxs-lookup"><span data-stu-id="015bc-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="015bc-191">Вы увидите выходные данные get работы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="015bc-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="015bc-192">Hello выходные данные должны соответствовать следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="015bc-192">hello output should match hello following screenshot.</span></span>

![Выходные данные приложения C++ для Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="015bc-194">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="015bc-194">Congratulations!</span></span> <span data-ttu-id="015bc-195">После завершения учебника C++ hello и имеют первого приложения консоли Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="015bc-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="015bc-196"><a id="GetSolution"></a>Получить комплексное решение учебника hello C++</span><span class="sxs-lookup"><span data-stu-id="015bc-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="015bc-197">решение GetStarted toobuild hello, содержащий все образцы hello в этой статье, необходимо hello следующее:</span><span class="sxs-lookup"><span data-stu-id="015bc-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="015bc-198">[Учетная запись Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="015bc-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="015bc-199">Hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) решения на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="015bc-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="015bc-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="015bc-200">Next steps</span></span>
* <span data-ttu-id="015bc-201">Узнайте, каким образом слишком[мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="015bc-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="015bc-202">Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="015bc-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="015bc-203">Дополнительные сведения о модели программирования hello в разделе Разработка hello hello [страницы документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="015bc-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


