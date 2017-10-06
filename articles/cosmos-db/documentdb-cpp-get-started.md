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
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Azure Cosmos DB: Учебник по приложения консоли C++ для hello DocumentDB API
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js для MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Учебник по C++ приветствия toohello для hello Azure Cosmos DB DocumentDB API SDK одобрены для C++! По завершении работы с этим руководством у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и выполняет запросы этих ресурсов, включая базу данных C++.

Мы рассмотрим следующие вопросы:

* Создание и подключение учетной записи Azure Cosmos DB tooan
* Настройка приложения
* создание базы данных Azure Cosmos DB для C++;
* создание коллекции;
* создание документов JSON;
* Запрос к коллекции hello
* замена документа;
* удаление документа;
* Удаление базы данных C++ Azure Cosmos DB hello

У вас нет времени? Не беспокойтесь! законченное решение Hello можно найти в [GitHub](https://github.com/stalker314314/DocumentDBCpp). В разделе [получить комплексное решение hello](#GetSolution) быстрого инструкции.

После прохождения учебника C++ hello, пожалуйста голосования hello используйте кнопки hello нижней части этой страницы toogive нам отзыв. 

Если вы хотите нам toocontact напрямую, если вам свободного tooinclude адрес вашей электронной почты в комментарии или [направляться toous здесь](https://www.research.net/r/8BKRJ3Z). 

А теперь приступим к работе!

## <a name="prerequisites-for-hello-c-tutorial"></a>Необходимые условия для учебника hello C++
Убедитесь, что у вас есть следующие hello:

* Активная учетная запись Azure. Если у вас нет такой учетной записи, вы можете зарегистрироваться для использования [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/), после установки компонентов языка hello C++.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Шаг 1. Создание учетной записи Azure Cosmos DB
Давайте создадим учетную запись Azure Cosmos DB. При наличии учетной записи требуется toouse можно сразу перейти слишком[установки приложения на C++](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>Шаг 2. Настройка приложения C++
1. Откройте Visual Studio и затем на hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**. 
2. В hello **новый проект** окна в hello **установленные** области, разверните **Visual C++**, нажмите кнопку **Win32**и нажмите кнопку  **Консольное приложение Win32**. Имя проекта hellodocumentdb hello и нажмите кнопку **ОК**. 
   
    ![Снимок экрана приветствия мастера создания проекта](media/documentdb-cpp-get-started/hello.png)
3. После запуска мастера приложений Win32 hello щелкните **Готово**.
4. После создания проекта hello откройте диспетчер пакетов NuGet hello, щелкнув правой кнопкой мыши hello **hellodocumentdb** проекта в **обозревателе решений** и щелкнув **управление пакетами NuGet**. 
   
    ![Снимок экрана, показывающий управление пакетами NuGet меню Проект hello](media/documentdb-cpp-get-started/nuget.png)
5. В hello **NuGet: hellodocumentdb** щелкните **Обзор**и выполните поиск *documentdbcpp*. В результатах hello выберите DocumentDbCPP, как показано на следующий снимок экрана приветствия. Этот пакет устанавливает ссылки tooC ++ REST SDK, являющееся зависимостей для hello DocumentDbCPP.  
   
    ![Снимок экрана, показывающий hello DocumentDbCpp пакета выделен](media/documentdb-cpp-get-started/cpp.png)
   
    После hello пакеты были добавлены tooyour проект, не все toostart набор написания кода.   

## <a id="Config"></a>Шаг 3. Копирование сведений о подключении для базы данных Azure Cosmos DB из портала Azure
Подключить [портал Azure](https://portal.azure.com) и проходят через toohello Azure Cosmos DB базы данных учетной записи. Нам понадобится hello URI и hello первичный ключ с портала Azure в hello следующий шаг tooestablish соединение из наших фрагмент кода C++. 

![Azure Cosmos DB URI и ключей в hello портал Azure](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>Шаг 4: Учетная запись Azure Cosmos DB tooan подключения
1. Добавить следующие заголовки и пространства имен исходного кода tooyour, после hello `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. Далее необходимо добавьте hello следующим кодом tooyour функция main и замените hello настройки учетной записи и первичного ключа toomatch параметры Azure Cosmos DB из шага 3. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Теперь, когда имеется hello кода tooinitialize hello documentdb клиента, давайте посмотрим на работе с ресурсами Azure Cosmos DB.

## <a id="CreateDBColl"></a>Шаг 5. Создание базы данных и коллекции C++
Прежде чем мы выполнить этот шаг, давайте посмотрим, взаимодействие базы данных, коллекции и документов для тех, кто уже новый tooAzure Cosmos DB. [База данных](documentdb-resources.md#databases) представляет собой логический контейнер для хранения документов, распределенных по коллекциям. Объект [коллекции](documentdb-resources.md#collections) — это контейнер документов JSON и hello связанные логика приложения JavaScript. Можно узнать дополнительные сведения о модели иерархической ресурсов Azure Cosmos DB hello и основные понятия в [модель Azure Cosmos DB иерархических ресурсов и понятия](documentdb-resources.md).

toocreate базу данных и соответствующую ему коллекцию добавьте hello следующему коду toohello конца функцию main. Это создает базу данных с именем «FamilyRegistry» и коллекцию с именем FamilyCollection с помощью конфигурации клиента hello, объявленного в предыдущем шаге hello.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>Шаг 6. Создание документа
[Документы](documentdb-resources.md#documents) относятся к пользовательскому (произвольному) JSON-содержимому. Теперь можно вставить документ в Azure Cosmos DB. Документ можно создать путем копирования hello, следующий код в конце hello основной функции hello. 

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

toosummarize, этот код создает базу данных Azure Cosmos DB, коллекции и документы, которые можно выполнить запрос в обозревателе документов на портале Azure. 

![Учебник по C++ - диаграмма, иллюстрирующая hello иерархическую связь между hello учетной записи, hello базы данных, коллекции hello и документы hello](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB
Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции. Hello следующем образце кода показан запрос, выполненные с помощью синтаксиса SQL, который можно запустить с документами hello, созданную на предыдущем шаге hello.

функция Hello принимает как аргументы hello уникальный идентификатор или идентификатор ресурса для базы данных hello и коллекции hello вместе с клиента hello документа. Добавьте следующий код перед функцией main.

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

## <a id="Replace"></a>Шаг 8. Замена документа
Azure Cosmos DB поддерживает вместо документов JSON, как показано в следующим hello. Добавьте следующий код после executesimplequery функции hello.

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

## <a id="Delete"></a>Шаг 9. Удаление документа
Azure Cosmos DB поддерживает удаление документов JSON, это можно сделать путем копирования и вставки hello после кода после функции replacedocument hello. 

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

## <a id="DeleteDB"></a>Шаг 10. Удаление базы данных
Удаление базы данных создана hello удаляет hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).

Скопируйте и вставьте следующий фрагмент кода (функция очистки) после hello deletedocument функция tooremove hello базы данных и все дочерние ресурсы hello hello.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>Шаг 11. Запуск консольного приложения C++
Мы добавили toocreate кода, запрос, изменение и удаление различных ресурсов Azure Cosmos DB.  Сообщите нам сейчас подключите это, добавив различные функции toothese вызовы из наших основная функция hellodocumentdb.cpp, а также некоторые диагностические сообщения.

Это можно сделать путем замены hello основная функция приложения hello, следующий код. Этой записи над hello account_configuration_uri и primary_key, скопированные в код hello в шаге 3, поэтому, строки или копирование значения hello в снова сохраните из портала hello. 

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

Теперь следует toobuild может быть и запуска кода в Visual Studio, нажав клавишу F5 или в качестве альтернативы hello исполняемый файл в окне терминала hello приложения hello и под управлением. 

Вы увидите выходные данные get работы приложения hello. Hello выходные данные должны соответствовать следующий снимок экрана приветствия.

![Выходные данные приложения C++ для Azure Cosmos DB](media/documentdb-cpp-get-started/console.png)

Поздравляем! После завершения учебника C++ hello и имеют первого приложения консоли Azure Cosmos DB!

## <a id="GetSolution"></a>Получить комплексное решение учебника hello C++
решение GetStarted toobuild hello, содержащий все образцы hello в этой статье, необходимо hello следующее:

* [Учетная запись Azure Cosmos DB][create-account].
* Hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) решения на сайте GitHub.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).
* Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).
* Дополнительные сведения о модели программирования hello в разделе Разработка hello hello [страницы документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account


