---
title: "aaaHow toouse табличного хранилища Azure с hello SDK веб-заданий"
description: "Узнайте, как toouse Azure таблицу хранилища с hello SDK веб-заданий. Создание таблицы, добавить tootables сущностей и считывания существующих таблиц."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="4e229-104">Как toouse Azure таблицу хранилища с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="4e229-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="4e229-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="4e229-105">Overview</span></span>
<span data-ttu-id="4e229-106">В этом руководстве содержатся примеры кода C#, где показано, как tooread и записи хранилища Azure таблицы с помощью [SDK веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="4e229-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="4e229-107">Hello руководстве предполагается, вы знаете [как toocreate проект веб-задания в Visual Studio с подключением строки этой учетной записи хранения точки tooyour](websites-dotnet-webjobs-sdk-get-started.md) или слишком[нескольких учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="4e229-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="4e229-108">Некоторые из фрагментов кода hello показывают hello `Table` атрибута, используемого в функции, которые [вручную вызвать](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), то есть не с помощью одного из атрибутов hello триггера.</span><span class="sxs-lookup"><span data-stu-id="4e229-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="4e229-109"><a id="ingress"></a>Каким образом таблицы tooa tooadd сущностей</span><span class="sxs-lookup"><span data-stu-id="4e229-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="4e229-110">сущности tooa tooadd таблицы, используйте hello `Table` атрибутом `ICollector<T>` или `IAsyncCollector<T>` параметр где `T` указывает схему hello сущностей hello требуется tooadd.</span><span class="sxs-lookup"><span data-stu-id="4e229-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="4e229-111">Конструктор атрибута Hello принимает строковый параметр, задающий имя hello hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="4e229-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="4e229-112">Hello следующий код добавляет `Person` таблицу tooa сущности с именем *входящих*.</span><span class="sxs-lookup"><span data-stu-id="4e229-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="4e229-113">Здравствуйте, обычно используется с типом `ICollector` является производным от `TableEntity` или реализует `ITableEntity`, но не обязательно.</span><span class="sxs-lookup"><span data-stu-id="4e229-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="4e229-114">Одно из следующих hello `Person` классов с hello код, показанный в предыдущем hello `Ingress` метод.</span><span class="sxs-lookup"><span data-stu-id="4e229-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

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

<span data-ttu-id="4e229-115">Если требуется toowork непосредственно с hello хранилища Azure API, можно добавить `CloudStorageAccount` сигнатура метода toohello параметра.</span><span class="sxs-lookup"><span data-stu-id="4e229-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="4e229-116"><a id="monitor"></a> Мониторинг в реальном времени</span><span class="sxs-lookup"><span data-stu-id="4e229-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="4e229-117">Так как функции входящих данных часто обработки больших объемов данных, hello SDK веб-заданий панели мониторинга предоставляет мониторинга данных в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="4e229-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="4e229-118">Hello **вызов журнала** разделе рассказывается, выполняющихся функции hello.</span><span class="sxs-lookup"><span data-stu-id="4e229-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Запуск функции входа](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="4e229-120">Hello **сведения о вызове** страница сообщает hello ход выполнения функции (количество сущностей, которые записаны) во время выполнения и дает возможность tooabort его.</span><span class="sxs-lookup"><span data-stu-id="4e229-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![Запуск функции входа](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="4e229-122">Когда функции hello завершения hello **сведения о вызове** страницы сообщает число строк, записанных в hello.</span><span class="sxs-lookup"><span data-stu-id="4e229-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Функция входа выполнена](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="4e229-124"><a id="multiple"></a>Как tooread несколько сущностей из таблицы</span><span class="sxs-lookup"><span data-stu-id="4e229-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="4e229-125">tooread таблицы, используйте hello `Table` атрибутом `IQueryable<T>` параметр где введите `T` является производным от `TableEntity` или реализует `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="4e229-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="4e229-126">Hello следующий код считывает и записывает все строки из hello `Ingress` таблицы:</span><span class="sxs-lookup"><span data-stu-id="4e229-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

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

### <span data-ttu-id="4e229-127"><a id="readone"></a>Как tooread одной сущности из таблицы</span><span class="sxs-lookup"><span data-stu-id="4e229-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="4e229-128">Отсутствует `Table` конструктор атрибута две дополнительные параметры, позволяющие указать hello ключ раздела и ключом строки, при необходимости toobind tooa одной таблицы сущности.</span><span class="sxs-lookup"><span data-stu-id="4e229-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="4e229-129">Hello следующий код считывает строку таблицы для `Person` сущности на основе секции ключ и строки значений ключа в очереди сообщений:</span><span class="sxs-lookup"><span data-stu-id="4e229-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="4e229-130">Hello `Person` класса в этом примере нет tooimplement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="4e229-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="4e229-131"><a id="storageapi"></a>Как toouse hello API-Интерфейс хранилища .NET toowork непосредственно с таблицей</span><span class="sxs-lookup"><span data-stu-id="4e229-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="4e229-132">Можно также использовать hello `Table` атрибутом `CloudTable` объекта обеспечивает большую гибкость при работе с таблицей.</span><span class="sxs-lookup"><span data-stu-id="4e229-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="4e229-133">Hello следующем образце кода используется `CloudTable` tooadd toohello одной сущности объекта *входящих* таблицы.</span><span class="sxs-lookup"><span data-stu-id="4e229-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

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

<span data-ttu-id="4e229-134">Дополнительные сведения о том, как toouse hello `CloudTable` см. в разделе [как toouse хранилище таблиц из .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4e229-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="4e229-135"><a id="queues"></a>Связанные разделы, охватываемых hello очереди как tooarticle</span><span class="sxs-lookup"><span data-stu-id="4e229-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="4e229-136">Сведения о обработки таблицы toohandle запуска, очереди сообщений и для веб-задания сценариев SDK не обработки, содержатся определенного tootable [как хранилище с hello SDK веб-заданий очередей toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="4e229-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="4e229-137">В этой статье рассматриваются следующие hello:</span><span class="sxs-lookup"><span data-stu-id="4e229-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="4e229-138">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="4e229-138">Async functions</span></span>
* <span data-ttu-id="4e229-139">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="4e229-139">Multiple instances</span></span>
* <span data-ttu-id="4e229-140">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="4e229-140">Graceful shutdown</span></span>
* <span data-ttu-id="4e229-141">Использование пакета SDK веб-задания атрибутов в теле функции hello</span><span class="sxs-lookup"><span data-stu-id="4e229-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="4e229-142">Набор строк подключения пакета SDK для hello в коде</span><span class="sxs-lookup"><span data-stu-id="4e229-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="4e229-143">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="4e229-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="4e229-144">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="4e229-144">Trigger a function manually</span></span>
* <span data-ttu-id="4e229-145">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="4e229-145">Write logs</span></span>

## <span data-ttu-id="4e229-146"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e229-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="4e229-147">В этом руководстве предоставила код образцы где показано, как toohandle распространенные сценарии для работы с таблицами в Azure.</span><span class="sxs-lookup"><span data-stu-id="4e229-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="4e229-148">Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="4e229-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

