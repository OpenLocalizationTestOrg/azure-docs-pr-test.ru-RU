## <span data-ttu-id="c782d-101"><a name="create-client"></a>Создание подключения клиента</span><span class="sxs-lookup"><span data-stu-id="c782d-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="c782d-102">Создайте подключение клиента, создав объект `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="c782d-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="c782d-103">Замените `appUrl` URL-адресом в своем мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="c782d-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="c782d-104"><a name="table-reference"></a>Работа с таблицами</span><span class="sxs-lookup"><span data-stu-id="c782d-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="c782d-105">Для доступа к данным или их обновления создайте ссылку на таблицу серверной части.</span><span class="sxs-lookup"><span data-stu-id="c782d-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="c782d-106">Замените `tableName` именем таблицы.</span><span class="sxs-lookup"><span data-stu-id="c782d-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="c782d-107">Имея ссылку на таблицу, можно работать с этой таблицей:</span><span class="sxs-lookup"><span data-stu-id="c782d-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="c782d-108">Запрос к таблице</span><span class="sxs-lookup"><span data-stu-id="c782d-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="c782d-109">Фильтрация данных</span><span class="sxs-lookup"><span data-stu-id="c782d-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="c782d-110">Разбиение данных по страницам</span><span class="sxs-lookup"><span data-stu-id="c782d-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="c782d-111">Сортировка данных</span><span class="sxs-lookup"><span data-stu-id="c782d-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="c782d-112">Вставка данных</span><span class="sxs-lookup"><span data-stu-id="c782d-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="c782d-113">Изменение данных</span><span class="sxs-lookup"><span data-stu-id="c782d-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="c782d-114">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="c782d-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="c782d-115"><a name="querying"></a>Практическое руководство. Запрос ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="c782d-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="c782d-116">Ссылку на таблицу можно использовать для запроса данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="c782d-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="c782d-117">Запросы осуществляются на языке типа LINQ.</span><span class="sxs-lookup"><span data-stu-id="c782d-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="c782d-118">Чтобы вернуть все данные из таблицы, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="c782d-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="c782d-119">Выполненная функция вызывается с результатами.</span><span class="sxs-lookup"><span data-stu-id="c782d-119">The success function is called with the results.</span></span>  <span data-ttu-id="c782d-120">Не используйте в этой функции свойство `for (var i in results)` — оно вызывает перебор данных, включаемых в результаты применения других функций запросов (таких как `.includeTotalCount()`).</span><span class="sxs-lookup"><span data-stu-id="c782d-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="c782d-121">Дополнительные сведения о синтаксисе запроса см. в [документации по объектам запросов].</span><span class="sxs-lookup"><span data-stu-id="c782d-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="c782d-122"><a name="table-filter"></a>Фильтрация данных на сервере</span><span class="sxs-lookup"><span data-stu-id="c782d-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="c782d-123">Используйте предложение `where` с ссылкой на таблицу.</span><span class="sxs-lookup"><span data-stu-id="c782d-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="c782d-124">Также можно использовать функцию фильтрации объектов.</span><span class="sxs-lookup"><span data-stu-id="c782d-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="c782d-125">В этом случае переменная `this` присваивается текущему объекту фильтрации.</span><span class="sxs-lookup"><span data-stu-id="c782d-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="c782d-126">Представленный ниже код функционально эквивалентен предыдущему примеру:</span><span class="sxs-lookup"><span data-stu-id="c782d-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="c782d-127"><a name="table-paging"></a>Разбиение данных по страницам</span><span class="sxs-lookup"><span data-stu-id="c782d-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="c782d-128">Используйте методы `take()` и `skip()`.</span><span class="sxs-lookup"><span data-stu-id="c782d-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="c782d-129">Например, если вы хотите разбить на строки таблицу, содержащую 100 записей:</span><span class="sxs-lookup"><span data-stu-id="c782d-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

<span data-ttu-id="c782d-130">Метод `.includeTotalCount()` добавляет в объект результатов поле totalCount.</span><span class="sxs-lookup"><span data-stu-id="c782d-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="c782d-131">В этом поле указывается общее количество записей, которое будет возвращено, если данные не разбиты на страницы.</span><span class="sxs-lookup"><span data-stu-id="c782d-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="c782d-132">После этого можно настроить список страниц, используя переменную pages и определенные кнопки пользовательского интерфейса, и загрузить новые данные на каждой странице с помощью метода `loadPage()`.</span><span class="sxs-lookup"><span data-stu-id="c782d-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="c782d-133">Чтобы ускорить доступ к уже загруженным записям, добавьте кэширование.</span><span class="sxs-lookup"><span data-stu-id="c782d-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="c782d-134"><a name="sorting-data"></a>Практическое руководство. Возврат отсортированных данных</span><span class="sxs-lookup"><span data-stu-id="c782d-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="c782d-135">Используйте методы запроса `.orderBy()` или `.orderByDescending()`:</span><span class="sxs-lookup"><span data-stu-id="c782d-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="c782d-136">Дополнительные сведения об объекте запроса см. в [документации по объектам запросов].</span><span class="sxs-lookup"><span data-stu-id="c782d-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="c782d-137"><a name="inserting"></a>Практическое руководство. Вставка данных</span><span class="sxs-lookup"><span data-stu-id="c782d-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="c782d-138">Создайте объект JavaScript с соответствующей датой и асинхронно вызовите метод `table.insert()`:</span><span class="sxs-lookup"><span data-stu-id="c782d-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

<span data-ttu-id="c782d-139">Вставленный элемент возвращается с дополнительными полями, необходимыми для операций синхронизации.</span><span class="sxs-lookup"><span data-stu-id="c782d-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="c782d-140">Обновите свой кэш, используя эти данные для последующих обновлений.</span><span class="sxs-lookup"><span data-stu-id="c782d-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="c782d-141">Серверный пакет SDK мобильных приложений Azure для Node.js поддерживает динамическую схему для целей разработки.</span><span class="sxs-lookup"><span data-stu-id="c782d-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="c782d-142">Динамическая схема позволяет добавлять столбцы в таблицу, указывая их в операциях вставки или обновления.</span><span class="sxs-lookup"><span data-stu-id="c782d-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="c782d-143">Перед переносом приложения в рабочую среду динамическую схему рекомендуется отключить.</span><span class="sxs-lookup"><span data-stu-id="c782d-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="c782d-144"><a name="modifying"></a>Практическое руководство. Изменение данных</span><span class="sxs-lookup"><span data-stu-id="c782d-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="c782d-145">Как и при использовании метода `.insert()`, в этом случае следует создать объект обновления и вызвать метод `.update()`.</span><span class="sxs-lookup"><span data-stu-id="c782d-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="c782d-146">Объект обновления должен содержать идентификатор обновляемой записи, получаемый при ее чтении или при вызове метода `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="c782d-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <span data-ttu-id="c782d-147"><a name="deleting"></a>Практическое руководство. Удаление данных</span><span class="sxs-lookup"><span data-stu-id="c782d-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="c782d-148">Для удаления записи вызовите метод `.del()`.</span><span class="sxs-lookup"><span data-stu-id="c782d-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="c782d-149">В ссылке на объект укажите идентификатор:</span><span class="sxs-lookup"><span data-stu-id="c782d-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
