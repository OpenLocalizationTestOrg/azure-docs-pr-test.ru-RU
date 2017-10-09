## <span data-ttu-id="e087b-101"><a name="create-client"></a>Создание подключения клиента</span><span class="sxs-lookup"><span data-stu-id="e087b-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="e087b-102">Создайте подключение клиента, создав объект `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="e087b-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="e087b-103">Замените `appUrl` с tooyour URL-адрес мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="e087b-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="e087b-104"><a name="table-reference"></a>Работа с таблицами</span><span class="sxs-lookup"><span data-stu-id="e087b-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="e087b-105">tooaccess или обновления данных, создать таблицу внутренних toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="e087b-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="e087b-106">Замените `tableName` с именем hello таблицы</span><span class="sxs-lookup"><span data-stu-id="e087b-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="e087b-107">Имея ссылку на таблицу, можно работать с этой таблицей:</span><span class="sxs-lookup"><span data-stu-id="e087b-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="e087b-108">Запрос к таблице</span><span class="sxs-lookup"><span data-stu-id="e087b-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="e087b-109">Фильтрация данных</span><span class="sxs-lookup"><span data-stu-id="e087b-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="e087b-110">Разбиение данных по страницам</span><span class="sxs-lookup"><span data-stu-id="e087b-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="e087b-111">Сортировка данных</span><span class="sxs-lookup"><span data-stu-id="e087b-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="e087b-112">Вставка данных</span><span class="sxs-lookup"><span data-stu-id="e087b-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="e087b-113">Изменение данных</span><span class="sxs-lookup"><span data-stu-id="e087b-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="e087b-114">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="e087b-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="e087b-115"><a name="querying"></a>Практическое руководство. Запрос ссылки на таблицу</span><span class="sxs-lookup"><span data-stu-id="e087b-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="e087b-116">При наличии ссылки на таблицу, ее можно использовать tooquery для данных на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="e087b-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="e087b-117">Запросы осуществляются на языке типа LINQ.</span><span class="sxs-lookup"><span data-stu-id="e087b-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="e087b-118">tooreturn все данные из таблицы hello, hello используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="e087b-118">tooreturn all data from hello table, use hello following code:</span></span>

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="e087b-119">Hello успеха функция вызывается с результатами hello.</span><span class="sxs-lookup"><span data-stu-id="e087b-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="e087b-120">Не используйте `for (var i in results)` в hello успешно работать так, как будет перебора сведения, включенные в результатах hello при других функций запроса (такие как `.includeTotalCount()`) используются.</span><span class="sxs-lookup"><span data-stu-id="e087b-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="e087b-121">Дополнительные сведения о hello синтаксис запроса см. в разделе hello [запрос объекта документации].</span><span class="sxs-lookup"><span data-stu-id="e087b-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="e087b-122"><a name="table-filter"></a>Фильтрация данных на сервере hello</span><span class="sxs-lookup"><span data-stu-id="e087b-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="e087b-123">Можно использовать `where` предложение на ссылку на таблицу hello:</span><span class="sxs-lookup"><span data-stu-id="e087b-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="e087b-124">Можно также использовать функцию, которая фильтрует hello объекта.</span><span class="sxs-lookup"><span data-stu-id="e087b-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="e087b-125">В этом случае hello `this` переменной присваивается текущему объекту toothe фильтруемой.</span><span class="sxs-lookup"><span data-stu-id="e087b-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="e087b-126">Hello после кода приведен пример предыдущих toohello функционально эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="e087b-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="e087b-127"><a name="table-paging"></a>Разбиение данных по страницам</span><span class="sxs-lookup"><span data-stu-id="e087b-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="e087b-128">Использовать hello `take()` и `skip()` методы.</span><span class="sxs-lookup"><span data-stu-id="e087b-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="e087b-129">Например, при желании toosplit hello таблицы в строке 100 записей:</span><span class="sxs-lookup"><span data-stu-id="e087b-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
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

<span data-ttu-id="e087b-130">Hello `.includeTotalCount()` в противном случае используется tooadd объект totalCount toohello поля результатов.</span><span class="sxs-lookup"><span data-stu-id="e087b-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="e087b-131">Поле totalCount заполняется hello общее количество записей, которые будут возвращены при использовании без разбиения на страницы.</span><span class="sxs-lookup"><span data-stu-id="e087b-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="e087b-132">Затем можно использовать переменную страницы hello и некоторые tooprovide кнопками ИП список страниц; Используйте `loadPage()` для загрузки hello новых записей для каждой страницы.</span><span class="sxs-lookup"><span data-stu-id="e087b-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="e087b-133">Реализуйте кэширования toorecords toospeed доступа, который уже загружен.</span><span class="sxs-lookup"><span data-stu-id="e087b-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="e087b-134"><a name="sorting-data"></a>Практическое руководство. Возврат отсортированных данных</span><span class="sxs-lookup"><span data-stu-id="e087b-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="e087b-135">Используйте hello `.orderBy()` или `.orderByDescending()` методы запроса:</span><span class="sxs-lookup"><span data-stu-id="e087b-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="e087b-136">Дополнительные сведения о hello объекта запроса см. в разделе hello [запрос объекта документации].</span><span class="sxs-lookup"><span data-stu-id="e087b-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="e087b-137"><a name="inserting"></a>Практическое руководство. Вставка данных</span><span class="sxs-lookup"><span data-stu-id="e087b-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="e087b-138">Создайте объект JavaScript и соответствующую дату hello и вызовите `table.insert()` асинхронно:</span><span class="sxs-lookup"><span data-stu-id="e087b-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="e087b-139">Для успешной вставки hello вставить элемент возвращается с hello дополнительные поля, которые требуются для синхронизации операций.</span><span class="sxs-lookup"><span data-stu-id="e087b-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="e087b-140">Обновите свой кэш, используя эти данные для последующих обновлений.</span><span class="sxs-lookup"><span data-stu-id="e087b-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="e087b-141">пакет SDK для Azure мобильных приложений Node.js сервера Hello поддерживает Динамическая схема для целей разработки.</span><span class="sxs-lookup"><span data-stu-id="e087b-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="e087b-142">Динамическая схема позволяет tooadd столбцы toohello таблицы, указав их в операции вставки или обновления.</span><span class="sxs-lookup"><span data-stu-id="e087b-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="e087b-143">Рекомендуется отключить динамической схемы перед перемещением tooproduction вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="e087b-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="e087b-144"><a name="modifying"></a>Практическое руководство. Изменение данных</span><span class="sxs-lookup"><span data-stu-id="e087b-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="e087b-145">Аналогичные toohello `.insert()` , вы должны создать объект обновления и затем вызвать `.update()`.</span><span class="sxs-lookup"><span data-stu-id="e087b-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="e087b-146">Hello обновления объекта должен содержать идентификатор hello записей toobe hello обновлен — hello код должен быть получен при чтении записи hello, или при вызове `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="e087b-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="e087b-147"><a name="deleting"></a>Практическое руководство. Удаление данных</span><span class="sxs-lookup"><span data-stu-id="e087b-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="e087b-148">toodelete запись, вызов hello `.del()` метод.</span><span class="sxs-lookup"><span data-stu-id="e087b-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="e087b-149">Передайте идентификатор hello ссылку на объект:</span><span class="sxs-lookup"><span data-stu-id="e087b-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
