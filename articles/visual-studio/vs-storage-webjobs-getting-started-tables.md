---
title: "aaaGetting работает с Visual Studio и хранилища Azure подключенные службы (для проектов веб-задания)"
description: "Как tooget к работе с хранилищем таблиц Azure в проекте веб-заданий Azure в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 80d9f8d8b493ce612623dfed7e89325fb154a1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="c1bb0-103">Начало работы со службой хранилища Azure (проекты веб-заданий Azure)</span><span class="sxs-lookup"><span data-stu-id="c1bb0-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="c1bb0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c1bb0-104">Overview</span></span>
<span data-ttu-id="c1bb0-105">В этой статье приведены образцы кода C#, которые показывают Показать, как toouse hello веб-заданий Azure SDK версии 1.x hello службы хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="c1bb0-106">Примеры кода Hello использовать hello [SDK веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="c1bb0-107">Hello службы хранилища таблиц Azure позволяет toostore больших объемов структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="c1bb0-108">Hello служба находится в хранилище данных NoSQL, принимающий вызовам c аутентификацией внутри и вне hello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="c1bb0-109">Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="c1bb0-110">Дополнительные сведения см. в разделе [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table).</span><span class="sxs-lookup"><span data-stu-id="c1bb0-110">See [Get started with Azure Table storage using .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) for more information.</span></span>

<span data-ttu-id="c1bb0-111">Некоторые из фрагментов кода hello показывают hello **таблицы** атрибута, используемого в функции, вызываемые вручную, то есть не с помощью одного из атрибутов hello триггера.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="c1bb0-112">Каким образом таблицы tooa tooadd сущностей</span><span class="sxs-lookup"><span data-stu-id="c1bb0-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="c1bb0-113">сущности tooa tooadd таблицы, используйте hello **таблицы** атрибутом **ICollector<T>**  или **IAsyncCollector<T>**  параметр где **T** указывает схему hello сущностей hello требуется tooadd.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="c1bb0-114">Конструктор атрибута Hello принимает строковый параметр, задающий имя hello hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="c1bb0-115">Hello следующий код добавляет **лицо** таблицу tooa сущности с именем *входящих*.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() {
                        PartitionKey = "Test",
                        RowKey = i.ToString(),
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="c1bb0-116">Здравствуйте, обычно используется с типом **ICollector** является производным от **TableEntity** или реализует **ITableEntity**, но не обязательно.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="c1bb0-117">Одно из следующих hello **лицо** классов с hello код, показанный в предыдущем hello **входящих** метод.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="c1bb0-118">Если требуется toowork непосредственно с hello хранилища Azure API, можно добавить **CloudStorageAccount** сигнатура метода toohello параметра.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="c1bb0-119">Мониторинг в реальном времени</span><span class="sxs-lookup"><span data-stu-id="c1bb0-119">Real-time monitoring</span></span>
<span data-ttu-id="c1bb0-120">Так как функции входящих данных часто обработки больших объемов данных, hello SDK веб-заданий панели мониторинга предоставляет мониторинга данных в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="c1bb0-121">Hello **вызов журнала** разделе рассказывается, выполняющихся функции hello.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Запуск функции входа](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="c1bb0-123">Hello **сведения о вызове** страница сообщает hello ход выполнения функции (количество сущностей, которые записаны) во время выполнения и дает возможность tooabort его.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Запуск функции входа](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="c1bb0-125">Когда функции hello завершения hello **сведения о вызове** страницы сообщает число строк, записанных в hello.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Функция входа выполнена](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="c1bb0-127">Как tooread несколько сущностей из таблицы</span><span class="sxs-lookup"><span data-stu-id="c1bb0-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="c1bb0-128">tooread таблицы, используйте hello **таблицы** атрибутом **IQueryable<T>**  параметр где введите **T** является производным от **TableEntity**или реализует **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="c1bb0-129">Hello следующий код считывает и записывает все строки из hello **входящих** таблицы:</span><span class="sxs-lookup"><span data-stu-id="c1bb0-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}",
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="c1bb0-130">Как tooread одной сущности из таблицы</span><span class="sxs-lookup"><span data-stu-id="c1bb0-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="c1bb0-131">Отсутствует **таблицы** конструктор атрибута две дополнительные параметры, позволяющие указать hello ключ раздела и ключом строки, при необходимости toobind tooa одной таблицы сущности.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="c1bb0-132">Hello следующий код считывает строку таблицы для **лицо** сущности на основе секции ключ и строки значений ключа в очереди сообщений:</span><span class="sxs-lookup"><span data-stu-id="c1bb0-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="c1bb0-133">Hello **лицо** класса в этом примере нет tooimplement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="c1bb0-134">Как toouse hello API-Интерфейс хранилища .NET toowork непосредственно с таблицей</span><span class="sxs-lookup"><span data-stu-id="c1bb0-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="c1bb0-135">Можно также использовать hello **таблицы** атрибутом **CloudTable** объектов обеспечивает большую гибкость при работе с таблицей.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="c1bb0-136">Hello следующем образце кода используется **CloudTable** tooadd toohello одной сущности объекта *входящих* таблицы.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="c1bb0-137">Дополнительные сведения о том, как toouse hello **CloudTable** см. в разделе [приступить к работе с хранилищем таблиц Azure, с помощью .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="c1bb0-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="c1bb0-138">Связанные разделы, охватываемых hello очереди как tooarticle</span><span class="sxs-lookup"><span data-stu-id="c1bb0-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="c1bb0-139">Сведения о обработки таблицы toohandle запуска, очереди сообщений и для веб-задания сценариев SDK не обработки, содержатся определенного tootable [Приступая к работе с хранилищем очередей Azure и Visual Studio подключенные службы (для проектов веб-задания) ](../storage/vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="c1bb0-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](../storage/vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1bb0-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1bb0-140">Next steps</span></span>
<span data-ttu-id="c1bb0-141">В этой статье был дан код образцы где показано, как toohandle распространенные сценарии для работы с таблицами в Azure.</span><span class="sxs-lookup"><span data-stu-id="c1bb0-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="c1bb0-142">Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [ресурсы документации веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="c1bb0-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

