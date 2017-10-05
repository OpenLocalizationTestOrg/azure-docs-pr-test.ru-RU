---
title: "Приступая к работе с подключенными службами хранилища Azure и Visual Studio (проекты веб-заданий)"
description: "Как приступить к работе, используя табличное хранилище Azure в проекте веб-задания Azure в Visual Studio после подключения к учетной записи хранения с помощью подключенных служб Visual Studio."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 79fba102377cdc6b681f6798699767961040a7e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="48532-103">Начало работы со службой хранилища Azure (проекты веб-заданий Azure)</span><span class="sxs-lookup"><span data-stu-id="48532-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="48532-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="48532-104">Overview</span></span>
<span data-ttu-id="48532-105">Эта статья содержит примеры кода C#, в которых показано, как использовать пакет SDK для веб-заданий Azure версии 1.x со службой хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="48532-105">This article provides C# code samples that show show how to use the Azure WebJobs SDK version 1.x with the Azure table storage service.</span></span> <span data-ttu-id="48532-106">В примерах кода используется [пакет SDK для веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="48532-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="48532-107">В службе хранилища таблиц Azure можно хранить большие объемы структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="48532-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="48532-108">Эта служба — хранилище данных NoSQL, которое принимает вызовы внутри и снаружи облака Azure с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="48532-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="48532-109">Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="48532-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="48532-110">Дополнительные сведения см. в разделе [Приступая к работе с хранилищем таблиц Azure с помощью .NET](storage-dotnet-how-to-use-tables.md#create-a-table).</span><span class="sxs-lookup"><span data-stu-id="48532-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="48532-111">В некоторых фрагментах кода демонстрируется использование атрибута **Table** в функциях, вызванных вручную, т. е. без использования атрибутов активации.</span><span class="sxs-lookup"><span data-stu-id="48532-111">Some of the code snippets show the **Table** attribute used in functions that are called manually, that is, not by using one of the trigger attributes.</span></span>

## <a name="how-to-add-entities-to-a-table"></a><span data-ttu-id="48532-112">Как добавить сущность в таблицу</span><span class="sxs-lookup"><span data-stu-id="48532-112">How to add entities to a table</span></span>
<span data-ttu-id="48532-113">Чтобы добавить сущности в таблицу, используйте атрибут **Table** с параметром **ICollector<T>** или **IAsyncCollector<T>**, где **T** обозначает схему сущностей, которые нужно добавить.</span><span class="sxs-lookup"><span data-stu-id="48532-113">To add entities to a table, use the **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="48532-114">Конструктор атрибута принимает строковый параметр, который указывает имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="48532-114">The attribute constructor takes a string parameter that specifies the name of the table.</span></span>

<span data-ttu-id="48532-115">Следующий пример кода добавляет сущности **Person** в таблицу с именем *Ingress*.</span><span class="sxs-lookup"><span data-stu-id="48532-115">The following code sample adds **Person** entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="48532-116">Как правило, тип, используемый с **ICollector**, является производным от **TableEntity** или реализует **ITableEntity**, но не во всех случаях.</span><span class="sxs-lookup"><span data-stu-id="48532-116">Typically the type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="48532-117">Один из следующих классов **Person** работает с кодом, показанным в предыдущем методе **Ingress**.</span><span class="sxs-lookup"><span data-stu-id="48532-117">Either of the following **Person** classes work with the code shown in the preceding **Ingress** method.</span></span>

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

<span data-ttu-id="48532-118">При работе непосредственно с API хранилища Azure можно также добавить параметр **CloudStorageAccount** в сигнатуру метода.</span><span class="sxs-lookup"><span data-stu-id="48532-118">If you want to work directly with the Azure storage API, you can add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="48532-119">Мониторинг в реальном времени</span><span class="sxs-lookup"><span data-stu-id="48532-119">Real-time monitoring</span></span>
<span data-ttu-id="48532-120">Поскольку функции входящих данных часто обрабатывают тома данных большого размера, на панели мониторинга пакета SDK для заданий WebJob доступны данные мониторинга в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="48532-120">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="48532-121">В разделе **Журнал вызова** указывается, запущена ли еще функция.</span><span class="sxs-lookup"><span data-stu-id="48532-121">The **Invocation Log** section tells you if the function is still running.</span></span>

![Запуск функции входа](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="48532-123">На странице **Подробности о вызове** отображаются данные о ходе выполнения функции (количество записанных сущностей) и предоставляется возможность ее прервать.</span><span class="sxs-lookup"><span data-stu-id="48532-123">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span>

![Запуск функции входа](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="48532-125">По завершении выполнения функции на странице **Подробности о вызове** отображается количество записанных строк.</span><span class="sxs-lookup"><span data-stu-id="48532-125">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Функция входа выполнена](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-to-read-multiple-entities-from-a-table"></a><span data-ttu-id="48532-127">Как выполнять чтение нескольких сущностей из таблицы</span><span class="sxs-lookup"><span data-stu-id="48532-127">How to read multiple entities from a table</span></span>
<span data-ttu-id="48532-128">Для чтения таблиц используйте атрибут **Table** с параметром **IQueryable<T>**, где тип **T** является производным от **TableEntity** или реализует **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="48532-128">To read a table, use the **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="48532-129">Следующий пример кода считывает и записывает все строки таблицы **Ingress** .</span><span class="sxs-lookup"><span data-stu-id="48532-129">The following code sample reads and logs all rows from the **Ingress** table:</span></span>

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

### <a name="how-to-read-a-single-entity-from-a-table"></a><span data-ttu-id="48532-130">Как выполнять чтение одной сущности из таблицы</span><span class="sxs-lookup"><span data-stu-id="48532-130">How to read a single entity from a table</span></span>
<span data-ttu-id="48532-131">Конструктор атрибута **Table** с двумя дополнительными параметрами позволяет указать ключ раздела и ключ строки, если необходимо выполнить привязку к одной сущности таблицы.</span><span class="sxs-lookup"><span data-stu-id="48532-131">There is a **Table** attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="48532-132">Следующий пример кода считывает строку таблицы для сущности **Person** на основе значений ключа раздела и ключа строки, полученных в сообщении очереди.</span><span class="sxs-lookup"><span data-stu-id="48532-132">The following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="48532-133">В этом примере класс **Person** не обязательно должен реализовывать **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="48532-133">The **Person** class in this example does not have to implement **ITableEntity**.</span></span>

## <a name="how-to-use-the-net-storage-api-directly-to-work-with-a-table"></a><span data-ttu-id="48532-134">Как использовать API службы хранения .NET непосредственно для работы с таблицей</span><span class="sxs-lookup"><span data-stu-id="48532-134">How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="48532-135">Чтобы сделать работу с таблицей более гибкой, можно также использовать атрибут **Table** для объекта **CloudTable**.</span><span class="sxs-lookup"><span data-stu-id="48532-135">You can also use the **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="48532-136">В следующем примере кода объект **CloudTable** используется для добавления одной сущности в таблицу *Ingress* .</span><span class="sxs-lookup"><span data-stu-id="48532-136">The following code sample uses a **CloudTable** object to add a single entity to the *Ingress* table.</span></span>

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

<span data-ttu-id="48532-137">Дополнительную информацию об использовании объекта **CloudTable** см. в статье [Приступая к работе с хранилищем таблиц Azure с помощью .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="48532-137">For more information about how to use the **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-the-queues-how-to-article"></a><span data-ttu-id="48532-138">Связанные разделы, которые описаны в практическом руководстве по работе с очередями</span><span class="sxs-lookup"><span data-stu-id="48532-138">Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="48532-139">Дополнительную информацию об управлении обработкой таблиц, которая инициируется сообщением очереди, а также несвязанные с обработкой таблиц сценарии применения пакета SDK для веб-заданий см. в статье [Приступая к работе с подключенными службами хранилища очередей Azure и Visual Studio (проекты веб-заданий)](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="48532-139">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48532-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="48532-140">Next steps</span></span>
<span data-ttu-id="48532-141">В этой статье предоставлены примеры кода обработки обычных сценариев для работы с таблицами Azure.</span><span class="sxs-lookup"><span data-stu-id="48532-141">This article has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="48532-142">Дополнительная информация об использовании веб-заданий Azure и пакета SDK для веб-заданий доступна в [ресурсах с документацией по веб-заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="48532-142">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

