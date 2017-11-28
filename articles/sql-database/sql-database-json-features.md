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
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="12790-103">Приступая к работе с функциями JSON в Базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="12790-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="12790-104">База данных SQL Azure позволяет анализировать и запрашивать данные, представленные в формате [JSON](http://www.json.org/) (нотация объектов JavaScript), и экспортировать реляционные данные в виде текста JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="12790-105">JSON – это распространенный формат данных, который используются для обмена данными в современных мобильных и веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="12790-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="12790-106">Кроме того, формат JSON используется для хранения частично структурированных данных в файлах журнала или базах данных NoSQL, например [базе данных Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="12790-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="12790-107">Многие веб-службы REST возвращают результаты в виде текста JSON или принимают данные в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="12790-108">Большинство служб Azure, в том числе [Поиск Azure](https://azure.microsoft.com/services/search/), [служба хранилища Azure](https://azure.microsoft.com/services/storage/) и [база данных Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/), имеют конечные точки REST, которые возвращают или используют данные JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="12790-109">База данных SQL Azure позволяет легко работать с данными JSON и интегрировать свою базу данных с современными службами.</span><span class="sxs-lookup"><span data-stu-id="12790-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="12790-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="12790-110">Overview</span></span>
<span data-ttu-id="12790-111">База данных SQL Azure предоставляет следующие функции для работы с данными JSON hello.</span><span class="sxs-lookup"><span data-stu-id="12790-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![Функции JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="12790-113">Если у вас есть текст JSON, можно извлекать данные из JSON или убедитесь, что JSON имеет правильный формат с помощью встроенных функций hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), и [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="12790-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="12790-114">Hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) функция позволяет обновлять значения в тексте JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="12790-115">Если требуются более сложные запросы и анализ, то с помощью функции [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) можно преобразовать массив объектов JSON в набор строк.</span><span class="sxs-lookup"><span data-stu-id="12790-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="12790-116">SQL-запрос может выполняться на hello вернул результирующий набор.</span><span class="sxs-lookup"><span data-stu-id="12790-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="12790-117">Наконец, можно использовать предложение [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) , которое позволяет форматировать данные, хранящиеся в реляционных таблицах в виде текста JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="12790-118">Преобразование реляционных данных в формат JSON</span><span class="sxs-lookup"><span data-stu-id="12790-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="12790-119">При наличии веб-службы, что формат берет данные из базы данных hello слоя и предоставляет ответ в формате JSON или клиентские платформы или библиотеки JavaScript, принимающих данные в формате JSON, можно отформатировать как JSON содержимое базы данных непосредственно в SQL-запросе.</span><span class="sxs-lookup"><span data-stu-id="12790-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="12790-120">Больше не имеют toowrite кода приложения, который форматирует результатов из базы данных SQL Azure как JSON, или указать некоторые результатов табличных запросов JSON сериализации библиотеки tooconvert и последующей сериализации объектов tooJSON формат.</span><span class="sxs-lookup"><span data-stu-id="12790-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="12790-121">Вместо этого можно использовать hello для результатов запроса SQL tooformat предложение JSON как JSON в базе данных SQL Azure и использовать его непосредственно в приложении.</span><span class="sxs-lookup"><span data-stu-id="12790-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="12790-122">В следующем примере hello строки из таблицы Sales.Customer hello форматируются как JSON с помощью предложения FOR JSON hello:</span><span class="sxs-lookup"><span data-stu-id="12790-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="12790-123">предложение FOR JSON PATH Hello форматирует hello результаты запроса hello в виде текста JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="12790-124">Имена столбцов используются в качестве ключей, хотя значения ячеек hello создаются как значения JSON:</span><span class="sxs-lookup"><span data-stu-id="12790-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="12790-125">Hello результирующий набор форматируется как массив JSON, где каждая строка форматируется как отдельный объект JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="12790-126">ПУТЬ указывает, можно настраивать hello выходной формат результирующего JSON с помощью точечной нотации в псевдонимы столбцов.</span><span class="sxs-lookup"><span data-stu-id="12790-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="12790-127">приветствия при следующем запросе изменения hello имя ключа «CustomerName» hello в формате JSON в выходных данных hello и помещает номера телефонов и факсов в «Contact» hello объекта:</span><span class="sxs-lookup"><span data-stu-id="12790-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="12790-128">выходные данные Hello этот запрос выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="12790-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="12790-129">В этом примере мы вернул объект JSON вместо массива путем указания hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) параметр.</span><span class="sxs-lookup"><span data-stu-id="12790-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="12790-130">Этот параметр можно использовать, если вы знаете, что результатом запроса является отдельный объект.</span><span class="sxs-lookup"><span data-stu-id="12790-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="12790-131">Hello основной hello предложения FOR JSON равен, он позволяет возвращать сложный иерархические данные из базы данных в формате вложенных объектов JSON и массивами.</span><span class="sxs-lookup"><span data-stu-id="12790-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="12790-132">Привет, следуя примере показано, как tooinclude заказы, принадлежащие toohello клиента как вложенный массив заказов:</span><span class="sxs-lookup"><span data-stu-id="12790-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="12790-133">Вместо того чтобы отправлять данные клиента tooget отдельных запросов, а затем toofetch список связанных заказов можно получения всех необходимых данных hello в рамках одного запроса, как показано в hello следующий образец вывода:</span><span class="sxs-lookup"><span data-stu-id="12790-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="12790-134">Работа с данными JSON</span><span class="sxs-lookup"><span data-stu-id="12790-134">Working with JSON data</span></span>
<span data-ttu-id="12790-135">При отсутствии строго структурированные данные, при наличии сложных вложенных объектов, массивов или иерархических данных, или если по мере развития структуры данных, в формат JSON hello помочь toorepresent любой сложной структуры данных.</span><span class="sxs-lookup"><span data-stu-id="12790-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="12790-136">JSON — это текстовый формат, который можно использовать как любой другой строковый тип в Базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="12790-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="12790-137">Данные JSON можно отправлять или хранить как стандартные данные типа NVARCHAR.</span><span class="sxs-lookup"><span data-stu-id="12790-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="12790-138">данные JSON, используемые в этом примере Hello представляется с помощью типа NVARCHAR(MAX) hello.</span><span class="sxs-lookup"><span data-stu-id="12790-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="12790-139">Можно вставлять в эту таблицу или предоставляется в качестве аргумента hello хранимые процедуры, используя стандартный синтаксис Transact-SQL, как показано в следующий пример hello JSON:</span><span class="sxs-lookup"><span data-stu-id="12790-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="12790-140">Любой язык или библиотека на стороне клиента, которая работает со строковыми данными в Базе данных SQL Azure, также будет работать с данными JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="12790-141">JSON может храниться в таблице, которая поддерживает тип NVARCHAR hello, например оптимизированных для памяти таблицы или таблицы с системным управлением версиями.</span><span class="sxs-lookup"><span data-stu-id="12790-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="12790-142">JSON не вводит ограничений hello код на стороне клиента или в слой hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="12790-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="12790-143">Запрос данных JSON</span><span class="sxs-lookup"><span data-stu-id="12790-143">Querying JSON data</span></span>
<span data-ttu-id="12790-144">Если данные в формате JSON хранятся в таблицах Azure SQL, то с помощью функций JSON эти данные можно использовать в SQL-запросе.</span><span class="sxs-lookup"><span data-stu-id="12790-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="12790-145">Функции JSON, доступные в Базе данных SQL Azure, позволяют обрабатывать данные в формате JSON как данные SQL любого другого типа.</span><span class="sxs-lookup"><span data-stu-id="12790-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="12790-146">Можно легко извлечение значений из текста JSON hello и использующих данные JSON в любом запросе:</span><span class="sxs-lookup"><span data-stu-id="12790-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="12790-147">Hello функции JSON_VALUE извлекает значение из текста JSON, хранящийся в столбце данных hello.</span><span class="sxs-lookup"><span data-stu-id="12790-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="12790-148">Эта функция использует путь типа JavaScript tooreference значение в tooextract текст JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="12790-149">значение Hello извлечено может использоваться в любой части SQL-запроса.</span><span class="sxs-lookup"><span data-stu-id="12790-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="12790-150">Hello функции JSON_QUERY — примерно tooJSON_VALUE.</span><span class="sxs-lookup"><span data-stu-id="12790-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="12790-151">В отличие от JSON_VALUE, эта функция извлекает сложный подобъект, например массивы или объекты, которые помещаются в текст JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="12790-152">функции JSON_MODIFY Hello позволяет указать hello путь к значению hello в текст JSON hello, должны быть обновлены, а также новое значение, которое приведет к перезаписи hello старого.</span><span class="sxs-lookup"><span data-stu-id="12790-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="12790-153">Таким образом, можно легко обновить текст JSON без повторный синтаксический анализ hello всю структуру.</span><span class="sxs-lookup"><span data-stu-id="12790-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="12790-154">Поскольку JSON хранятся в виде обычного текста, нет гарантий hello значений, хранимых в текстовых столбцах правильно отформатированы.</span><span class="sxs-lookup"><span data-stu-id="12790-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="12790-155">Вы можете убедиться, что текст, хранящийся в столбце JSON имеет правильный формат, используя стандартные ограничения check для базы данных SQL Azure и hello функции ISJSON:</span><span class="sxs-lookup"><span data-stu-id="12790-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="12790-156">Если входной текст hello имеет правильный формат JSON, hello функции ISJSON возвращает hello значение 1.</span><span class="sxs-lookup"><span data-stu-id="12790-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="12790-157">При каждой операции вставки или обновления столбца JSON это ограничение будет проверять, правилен ли формат JSON нового текстового значения.</span><span class="sxs-lookup"><span data-stu-id="12790-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="12790-158">Преобразование данных JSON в табличный формат</span><span class="sxs-lookup"><span data-stu-id="12790-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="12790-159">База данных SQL Azure позволяет также преобразовать коллекции JSON в табличный формат и загрузить или запросить данные JSON.</span><span class="sxs-lookup"><span data-stu-id="12790-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="12790-160">OPENJSON является возвращающей табличное значение функцией, выполняет синтаксический анализ текста JSON, находит массив объектов JSON, перебор элементов hello hello массива и возвращает одну строку hello выходного результата для каждого элемента массива hello.</span><span class="sxs-lookup"><span data-stu-id="12790-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![Табличное представление JSON](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="12790-162">В приведенном выше примере hello мы можно указать, где toolocate hello массив JSON, который должен быть открыт (в hello $. Путь заказы), какие столбцы должны возвращаться как результат, а там, где toofind hello значения JSON, которые будут возвращены как ячейки.</span><span class="sxs-lookup"><span data-stu-id="12790-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="12790-163">Преобразовать массив JSON в hello @orders переменной в набор строк, проанализировать этот результирующий набор или вставки строк в таблицу standard:</span><span class="sxs-lookup"><span data-stu-id="12790-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="12790-164">Hello коллекцию заказов форматируется как массив JSON и как параметр toohello хранимой процедуры можно проанализировать и вставляются в таблицу Orders hello.</span><span class="sxs-lookup"><span data-stu-id="12790-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12790-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12790-165">Next steps</span></span>
<span data-ttu-id="12790-166">toolearn как toointegrate JSON в приложение, ознакомьтесь с этими ресурсами:</span><span class="sxs-lookup"><span data-stu-id="12790-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="12790-167">Блог TechNet</span><span class="sxs-lookup"><span data-stu-id="12790-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="12790-168">Документация MSDN</span><span class="sxs-lookup"><span data-stu-id="12790-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="12790-169">Видео Channel 9</span><span class="sxs-lookup"><span data-stu-id="12790-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="12790-170">toolearn о различных вариантах интеграции JSON в приложении, см. демонстрации hello в этом [видео Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) или найти сценарий, который соответствует вашей варианту использования в [JSON записи в блогах](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="12790-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

