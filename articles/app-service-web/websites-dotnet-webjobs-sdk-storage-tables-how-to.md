---
title: "Как использовать табличное хранилище Azure с пакетом SDK для WebJob"
description: "Информация об использовании табличного хранилища Azure с пакетом SDK для WebJob Создавайте таблицы, добавляйте в них сущности и считывайте существующие таблицы."
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
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="e2522-104">Как использовать табличное хранилище Azure с пакетом SDK для WebJob</span><span class="sxs-lookup"><span data-stu-id="e2522-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="e2522-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="e2522-105">Overview</span></span>
<span data-ttu-id="e2522-106">Это руководство содержит примеры кода C#, в которых показано, как выполнять чтение и запись таблиц службы хранилища Azure с использованием [пакета SDK для веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e2522-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="e2522-107">В этом руководстве предполагается, что вы уже знаете, [как создать проект веб-задания в Visual Studio со строками подключения, указывающими на вашу учетную запись хранения](websites-dotnet-webjobs-sdk-get-started.md) или [несколько учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="e2522-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="e2522-108">В некоторых фрагментах кода демонстрируется использование атрибута `Table` в функциях, [вызванных вручную](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), т. е. без использования атрибутов триггера.</span><span class="sxs-lookup"><span data-stu-id="e2522-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="e2522-109"><a id="ingress"></a> Как добавить сущность в таблицу</span><span class="sxs-lookup"><span data-stu-id="e2522-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="e2522-110">Чтобы добавить сущности в таблицу, используйте атрибут `Table` с параметром `ICollector<T>` или `IAsyncCollector<T>`, где `T` указывает схему сущностей, которые нужно добавить.</span><span class="sxs-lookup"><span data-stu-id="e2522-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="e2522-111">Конструктор атрибута принимает строковый параметр, который указывает имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="e2522-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="e2522-112">Следующий пример кода добавляет сущности `Person` в таблицу с именем *Ingress*.</span><span class="sxs-lookup"><span data-stu-id="e2522-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

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

<span data-ttu-id="e2522-113">Как правило, тип, используемый с `ICollector`, является производным от `TableEntity` или реализует `ITableEntity`, но не во всех случаях.</span><span class="sxs-lookup"><span data-stu-id="e2522-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="e2522-114">Один из следующих классов `Person` работает с кодом, показанным в предыдущем методе `Ingress`.</span><span class="sxs-lookup"><span data-stu-id="e2522-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

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

<span data-ttu-id="e2522-115">Если требуется работать непосредственно с API службы хранилища Azure, можно добавить параметр `CloudStorageAccount` в сигнатуру метода.</span><span class="sxs-lookup"><span data-stu-id="e2522-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="e2522-116"><a id="monitor"></a> Мониторинг в реальном времени</span><span class="sxs-lookup"><span data-stu-id="e2522-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="e2522-117">Поскольку функции входящих данных часто обрабатывают тома данных большого размера, на панели мониторинга пакета SDK для заданий WebJob доступны данные мониторинга в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="e2522-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="e2522-118">В разделе **Журнал вызова** указывается, запущена ли еще функция.</span><span class="sxs-lookup"><span data-stu-id="e2522-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Запуск функции входа](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="e2522-120">На странице **Подробности о вызове** отображаются данные о ходе выполнения функции (количество записанных сущностей) и предоставляется возможность ее прервать.</span><span class="sxs-lookup"><span data-stu-id="e2522-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Запуск функции входа](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="e2522-122">По завершении выполнения функции на странице **Подробности о вызове** отображается количество записанных строк.</span><span class="sxs-lookup"><span data-stu-id="e2522-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Функция входа выполнена](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="e2522-124"><a id="multiple"></a> Как выполнять чтение нескольких сущностей из таблицы</span><span class="sxs-lookup"><span data-stu-id="e2522-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="e2522-125">Для чтения таблиц используйте атрибут `Table` с параметром `IQueryable<T>`, где тип `T` является производным от `TableEntity` или реализует `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="e2522-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="e2522-126">Следующий пример кода считывает и записывает все строки таблицы `Ingress`:</span><span class="sxs-lookup"><span data-stu-id="e2522-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

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

### <span data-ttu-id="e2522-127"><a id="readone"></a> Как выполнять чтение одной сущности из таблицы</span><span class="sxs-lookup"><span data-stu-id="e2522-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="e2522-128">Конструктор атрибута `Table` с двумя дополнительными параметрами позволяет указать ключ раздела и ключ строки, если необходимо выполнить привязку к одной сущности таблицы.</span><span class="sxs-lookup"><span data-stu-id="e2522-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="e2522-129">Следующий пример кода считывает строку таблицы для сущности `Person` на основе значений ключа раздела и ключа строки, полученных в сообщении очереди:</span><span class="sxs-lookup"><span data-stu-id="e2522-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="e2522-130">В этом примере класс `Person` не должен реализовывать `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="e2522-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="e2522-131"><a id="storageapi"></a> Как использовать API хранилища .NET непосредственно для работы с таблицей</span><span class="sxs-lookup"><span data-stu-id="e2522-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="e2522-132">Чтобы сделать работу с таблицей более гибкой, можно также использовать атрибут `Table` для объекта `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="e2522-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="e2522-133">В следующем примере кода объект `CloudTable` используется для добавления одной сущности в таблицу *Ingress* .</span><span class="sxs-lookup"><span data-stu-id="e2522-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

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

<span data-ttu-id="e2522-134">Дополнительную информацию об использовании объекта `CloudTable` см. в статье [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e2522-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="e2522-135"><a id="queues"></a>Связанные разделы, которые описаны в практическом руководстве по работе с очередями</span><span class="sxs-lookup"><span data-stu-id="e2522-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="e2522-136">Дополнительную информацию об обработке таблиц, которая инициируется сообщением очереди, а также несвязанные с обработкой таблиц сценарии для пакета SDK для веб-заданий см. в статье [Использование пакета SDK веб-заданий для работы с хранилищем очередей Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="e2522-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="e2522-137">В этой статье рассматриваются следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="e2522-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="e2522-138">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="e2522-138">Async functions</span></span>
* <span data-ttu-id="e2522-139">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="e2522-139">Multiple instances</span></span>
* <span data-ttu-id="e2522-140">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="e2522-140">Graceful shutdown</span></span>
* <span data-ttu-id="e2522-141">Использование атрибутов пакета SDK для заданий WebJob очереди в теле функции</span><span class="sxs-lookup"><span data-stu-id="e2522-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="e2522-142">Установка строк подключения пакета SDK в коде.</span><span class="sxs-lookup"><span data-stu-id="e2522-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="e2522-143">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="e2522-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="e2522-144">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="e2522-144">Trigger a function manually</span></span>
* <span data-ttu-id="e2522-145">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="e2522-145">Write logs</span></span>

## <span data-ttu-id="e2522-146"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2522-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="e2522-147">В этом руководстве предоставлены примеры кода обработки обычных сценариев для работы с таблицами Azure.</span><span class="sxs-lookup"><span data-stu-id="e2522-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="e2522-148">Дополнительную информацию об использовании веб-заданий Azure и пакета SDK для веб-заданий см. в [рекомендуемых ресурсах для веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="e2522-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

