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
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>Как toouse Azure таблицу хранилища с hello SDK веб-заданий
## <a name="overview"></a>Обзор
В этом руководстве содержатся примеры кода C#, где показано, как tooread и записи хранилища Azure таблицы с помощью [SDK веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1.x.

Hello руководстве предполагается, вы знаете [как toocreate проект веб-задания в Visual Studio с подключением строки этой учетной записи хранения точки tooyour](websites-dotnet-webjobs-sdk-get-started.md) или слишком[нескольких учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Некоторые из фрагментов кода hello показывают hello `Table` атрибута, используемого в функции, которые [вручную вызвать](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), то есть не с помощью одного из атрибутов hello триггера. 

## <a id="ingress"></a>Каким образом таблицы tooa tooadd сущностей
сущности tooa tooadd таблицы, используйте hello `Table` атрибутом `ICollector<T>` или `IAsyncCollector<T>` параметр где `T` указывает схему hello сущностей hello требуется tooadd. Конструктор атрибута Hello принимает строковый параметр, задающий имя hello hello таблицы. 

Hello следующий код добавляет `Person` таблицу tooa сущности с именем *входящих*.

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

Здравствуйте, обычно используется с типом `ICollector` является производным от `TableEntity` или реализует `ITableEntity`, но не обязательно. Одно из следующих hello `Person` классов с hello код, показанный в предыдущем hello `Ingress` метод.

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

Если требуется toowork непосредственно с hello хранилища Azure API, можно добавить `CloudStorageAccount` сигнатура метода toohello параметра.

## <a id="monitor"></a> Мониторинг в реальном времени
Так как функции входящих данных часто обработки больших объемов данных, hello SDK веб-заданий панели мониторинга предоставляет мониторинга данных в реальном времени. Hello **вызов журнала** разделе рассказывается, выполняющихся функции hello.

![Запуск функции входа](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

Hello **сведения о вызове** страница сообщает hello ход выполнения функции (количество сущностей, которые записаны) во время выполнения и дает возможность tooabort его. 

![Запуск функции входа](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Когда функции hello завершения hello **сведения о вызове** страницы сообщает число строк, записанных в hello.

![Функция входа выполнена](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Как tooread несколько сущностей из таблицы
tooread таблицы, используйте hello `Table` атрибутом `IQueryable<T>` параметр где введите `T` является производным от `TableEntity` или реализует `ITableEntity`.

Hello следующий код считывает и записывает все строки из hello `Ingress` таблицы:

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

### <a id="readone"></a>Как tooread одной сущности из таблицы
Отсутствует `Table` конструктор атрибута две дополнительные параметры, позволяющие указать hello ключ раздела и ключом строки, при необходимости toobind tooa одной таблицы сущности.

Hello следующий код считывает строку таблицы для `Person` сущности на основе секции ключ и строки значений ключа в очереди сообщений:  

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


Hello `Person` класса в этом примере нет tooimplement `ITableEntity`.

## <a id="storageapi"></a>Как toouse hello API-Интерфейс хранилища .NET toowork непосредственно с таблицей
Можно также использовать hello `Table` атрибутом `CloudTable` объекта обеспечивает большую гибкость при работе с таблицей.

Hello следующем образце кода используется `CloudTable` tooadd toohello одной сущности объекта *входящих* таблицы. 

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

Дополнительные сведения о том, как toouse hello `CloudTable` см. в разделе [как toouse хранилище таблиц из .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Связанные разделы, охватываемых hello очереди как tooarticle
Сведения о обработки таблицы toohandle запуска, очереди сообщений и для веб-задания сценариев SDK не обработки, содержатся определенного tootable [как хранилище с hello SDK веб-заданий очередей toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

В этой статье рассматриваются следующие hello:

* Асинхронные функции
* Выполнение на нескольких экземплярах
* Корректное завершение работы
* Использование пакета SDK веб-задания атрибутов в теле функции hello
* Набор строк подключения пакета SDK для hello в коде
* Установка значений параметров конструктора пакета SDK для заданий WebJob в коде
* Вызов функции вручную
* Запись журналов

## <a id="nextsteps"></a> Дальнейшие действия
В этом руководстве предоставила код образцы где показано, как toohandle распространенные сценарии для работы с таблицами в Azure. Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).

