---
title: "функции JSON базы данных SQL aaaAzure | Документы Microsoft"
description: "База данных SQL Azure позволяет tooparse, запроса и форматирование данных в формате JavaScript Object Notation (JSON)."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Приступая к работе с функциями JSON в Базе данных SQL Azure
База данных SQL Azure позволяет анализировать и запрашивать данные, представленные в формате [JSON](http://www.json.org/) (нотация объектов JavaScript), и экспортировать реляционные данные в виде текста JSON.

JSON – это распространенный формат данных, который используются для обмена данными в современных мобильных и веб-приложениях. Кроме того, формат JSON используется для хранения частично структурированных данных в файлах журнала или базах данных NoSQL, например [базе данных Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). Многие веб-службы REST возвращают результаты в виде текста JSON или принимают данные в формате JSON. Большинство служб Azure, в том числе [Поиск Azure](https://azure.microsoft.com/services/search/), [служба хранилища Azure](https://azure.microsoft.com/services/storage/) и [база данных Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/), имеют конечные точки REST, которые возвращают или используют данные JSON.

База данных SQL Azure позволяет легко работать с данными JSON и интегрировать свою базу данных с современными службами.

## <a name="overview"></a>Обзор
База данных SQL Azure предоставляет следующие функции для работы с данными JSON hello.

![Функции JSON](./media/sql-database-json-features/image_1.png)

Если у вас есть текст JSON, можно извлекать данные из JSON или убедитесь, что JSON имеет правильный формат с помощью встроенных функций hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), и [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) . Hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) функция позволяет обновлять значения в тексте JSON. Если требуются более сложные запросы и анализ, то с помощью функции [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) можно преобразовать массив объектов JSON в набор строк. SQL-запрос может выполняться на hello вернул результирующий набор. Наконец, можно использовать предложение [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) , которое позволяет форматировать данные, хранящиеся в реляционных таблицах в виде текста JSON.

## <a name="formatting-relational-data-in-json-format"></a>Преобразование реляционных данных в формат JSON
При наличии веб-службы, что формат берет данные из базы данных hello слоя и предоставляет ответ в формате JSON или клиентские платформы или библиотеки JavaScript, принимающих данные в формате JSON, можно отформатировать как JSON содержимое базы данных непосредственно в SQL-запросе. Больше не имеют toowrite кода приложения, который форматирует результатов из базы данных SQL Azure как JSON, или указать некоторые результатов табличных запросов JSON сериализации библиотеки tooconvert и последующей сериализации объектов tooJSON формат. Вместо этого можно использовать hello для результатов запроса SQL tooformat предложение JSON как JSON в базе данных SQL Azure и использовать его непосредственно в приложении.

В следующем примере hello строки из таблицы Sales.Customer hello форматируются как JSON с помощью предложения FOR JSON hello:

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

предложение FOR JSON PATH Hello форматирует hello результаты запроса hello в виде текста JSON. Имена столбцов используются в качестве ключей, хотя значения ячеек hello создаются как значения JSON:

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

Hello результирующий набор форматируется как массив JSON, где каждая строка форматируется как отдельный объект JSON.

ПУТЬ указывает, можно настраивать hello выходной формат результирующего JSON с помощью точечной нотации в псевдонимы столбцов. приветствия при следующем запросе изменения hello имя ключа «CustomerName» hello в формате JSON в выходных данных hello и помещает номера телефонов и факсов в «Contact» hello объекта:

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

выходные данные Hello этот запрос выглядит следующим образом:

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

В этом примере мы вернул объект JSON вместо массива путем указания hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) параметр. Этот параметр можно использовать, если вы знаете, что результатом запроса является отдельный объект.

Hello основной hello предложения FOR JSON равен, он позволяет возвращать сложный иерархические данные из базы данных в формате вложенных объектов JSON и массивами. Привет, следуя примере показано, как tooinclude заказы, принадлежащие toohello клиента как вложенный массив заказов:

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

Вместо того чтобы отправлять данные клиента tooget отдельных запросов, а затем toofetch список связанных заказов можно получения всех необходимых данных hello в рамках одного запроса, как показано в hello следующий образец вывода:

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a>Работа с данными JSON
При отсутствии строго структурированные данные, при наличии сложных вложенных объектов, массивов или иерархических данных, или если по мере развития структуры данных, в формат JSON hello помочь toorepresent любой сложной структуры данных.

JSON — это текстовый формат, который можно использовать как любой другой строковый тип в Базе данных SQL Azure. Данные JSON можно отправлять или хранить как стандартные данные типа NVARCHAR.

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

данные JSON, используемые в этом примере Hello представляется с помощью типа NVARCHAR(MAX) hello. Можно вставлять в эту таблицу или предоставляется в качестве аргумента hello хранимые процедуры, используя стандартный синтаксис Transact-SQL, как показано в следующий пример hello JSON:

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Любой язык или библиотека на стороне клиента, которая работает со строковыми данными в Базе данных SQL Azure, также будет работать с данными JSON. JSON может храниться в таблице, которая поддерживает тип NVARCHAR hello, например оптимизированных для памяти таблицы или таблицы с системным управлением версиями. JSON не вводит ограничений hello код на стороне клиента или в слой hello базы данных.

## <a name="querying-json-data"></a>Запрос данных JSON
Если данные в формате JSON хранятся в таблицах Azure SQL, то с помощью функций JSON эти данные можно использовать в SQL-запросе.

Функции JSON, доступные в Базе данных SQL Azure, позволяют обрабатывать данные в формате JSON как данные SQL любого другого типа. Можно легко извлечение значений из текста JSON hello и использующих данные JSON в любом запросе:

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

Hello функции JSON_VALUE извлекает значение из текста JSON, хранящийся в столбце данных hello. Эта функция использует путь типа JavaScript tooreference значение в tooextract текст JSON. значение Hello извлечено может использоваться в любой части SQL-запроса.

Hello функции JSON_QUERY — примерно tooJSON_VALUE. В отличие от JSON_VALUE, эта функция извлекает сложный подобъект, например массивы или объекты, которые помещаются в текст JSON.

функции JSON_MODIFY Hello позволяет указать hello путь к значению hello в текст JSON hello, должны быть обновлены, а также новое значение, которое приведет к перезаписи hello старого. Таким образом, можно легко обновить текст JSON без повторный синтаксический анализ hello всю структуру.

Поскольку JSON хранятся в виде обычного текста, нет гарантий hello значений, хранимых в текстовых столбцах правильно отформатированы. Вы можете убедиться, что текст, хранящийся в столбце JSON имеет правильный формат, используя стандартные ограничения check для базы данных SQL Azure и hello функции ISJSON:

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Если входной текст hello имеет правильный формат JSON, hello функции ISJSON возвращает hello значение 1. При каждой операции вставки или обновления столбца JSON это ограничение будет проверять, правилен ли формат JSON нового текстового значения.

## <a name="transforming-json-into-tabular-format"></a>Преобразование данных JSON в табличный формат
База данных SQL Azure позволяет также преобразовать коллекции JSON в табличный формат и загрузить или запросить данные JSON.

OPENJSON является возвращающей табличное значение функцией, выполняет синтаксический анализ текста JSON, находит массив объектов JSON, перебор элементов hello hello массива и возвращает одну строку hello выходного результата для каждого элемента массива hello.

![Табличное представление JSON](./media/sql-database-json-features/image_2.png)

В приведенном выше примере hello мы можно указать, где toolocate hello массив JSON, который должен быть открыт (в hello $. Путь заказы), какие столбцы должны возвращаться как результат, а там, где toofind hello значения JSON, которые будут возвращены как ячейки.

Преобразовать массив JSON в hello @orders переменной в набор строк, проанализировать этот результирующий набор или вставки строк в таблицу standard:

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
Hello коллекцию заказов форматируется как массив JSON и как параметр toohello хранимой процедуры можно проанализировать и вставляются в таблицу Orders hello.

## <a name="next-steps"></a>Дальнейшие действия
toolearn как toointegrate JSON в приложение, ознакомьтесь с этими ресурсами:

* [Блог TechNet](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [Документация MSDN](https://msdn.microsoft.com/library/dn921897.aspx)
* [Видео Channel 9](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

toolearn о различных вариантах интеграции JSON в приложении, см. демонстрации hello в этом [видео Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) или найти сценарий, который соответствует вашей варианту использования в [JSON записи в блогах](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

