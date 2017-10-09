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
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Начало работы со службой хранилища Azure (проекты веб-заданий Azure)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Обзор
В этой статье приведены образцы кода C#, которые показывают Показать, как toouse hello веб-заданий Azure SDK версии 1.x hello службы хранилища таблиц Azure. Примеры кода Hello использовать hello [SDK веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk.md) версии 1.x.

Hello службы хранилища таблиц Azure позволяет toostore больших объемов структурированных данных. Hello служба находится в хранилище данных NoSQL, принимающий вызовам c аутентификацией внутри и вне hello облако Azure. Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.  Дополнительные сведения см. в разделе [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table).

Некоторые из фрагментов кода hello показывают hello **таблицы** атрибута, используемого в функции, вызываемые вручную, то есть не с помощью одного из атрибутов hello триггера.

## <a name="how-tooadd-entities-tooa-table"></a>Каким образом таблицы tooa tooadd сущностей
сущности tooa tooadd таблицы, используйте hello **таблицы** атрибутом **ICollector<T>**  или **IAsyncCollector<T>**  параметр где **T** указывает схему hello сущностей hello требуется tooadd. Конструктор атрибута Hello принимает строковый параметр, задающий имя hello hello таблицы.

Hello следующий код добавляет **лицо** таблицу tooa сущности с именем *входящих*.

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

Здравствуйте, обычно используется с типом **ICollector** является производным от **TableEntity** или реализует **ITableEntity**, но не обязательно. Одно из следующих hello **лицо** классов с hello код, показанный в предыдущем hello **входящих** метод.

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

Если требуется toowork непосредственно с hello хранилища Azure API, можно добавить **CloudStorageAccount** сигнатура метода toohello параметра.

## <a name="real-time-monitoring"></a>Мониторинг в реальном времени
Так как функции входящих данных часто обработки больших объемов данных, hello SDK веб-заданий панели мониторинга предоставляет мониторинга данных в реальном времени. Hello **вызов журнала** разделе рассказывается, выполняющихся функции hello.

![Запуск функции входа](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Hello **сведения о вызове** страница сообщает hello ход выполнения функции (количество сущностей, которые записаны) во время выполнения и дает возможность tooabort его.

![Запуск функции входа](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Когда функции hello завершения hello **сведения о вызове** страницы сообщает число строк, записанных в hello.

![Функция входа выполнена](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>Как tooread несколько сущностей из таблицы
tooread таблицы, используйте hello **таблицы** атрибутом **IQueryable<T>**  параметр где введите **T** является производным от **TableEntity**или реализует **ITableEntity**.

Hello следующий код считывает и записывает все строки из hello **входящих** таблицы:

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>Как tooread одной сущности из таблицы
Отсутствует **таблицы** конструктор атрибута две дополнительные параметры, позволяющие указать hello ключ раздела и ключом строки, при необходимости toobind tooa одной таблицы сущности.

Hello следующий код считывает строку таблицы для **лицо** сущности на основе секции ключ и строки значений ключа в очереди сообщений:  

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


Hello **лицо** класса в этом примере нет tooimplement **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>Как toouse hello API-Интерфейс хранилища .NET toowork непосредственно с таблицей
Можно также использовать hello **таблицы** атрибутом **CloudTable** объектов обеспечивает большую гибкость при работе с таблицей.

Hello следующем образце кода используется **CloudTable** tooadd toohello одной сущности объекта *входящих* таблицы.

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

Дополнительные сведения о том, как toouse hello **CloudTable** см. в разделе [приступить к работе с хранилищем таблиц Azure, с помощью .NET](../storage/storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Связанные разделы, охватываемых hello очереди как tooarticle
Сведения о обработки таблицы toohandle запуска, очереди сообщений и для веб-задания сценариев SDK не обработки, содержатся определенного tootable [Приступая к работе с хранилищем очередей Azure и Visual Studio подключенные службы (для проектов веб-задания) ](../storage/vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Дальнейшие действия
В этой статье был дан код образцы где показано, как toohandle распространенные сценарии для работы с таблицами в Azure. Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [ресурсы документации веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).

