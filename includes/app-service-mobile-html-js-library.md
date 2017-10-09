## <a name="create-client"></a>Создание подключения клиента
Создайте подключение клиента, создав объект `WindowsAzure.MobileServiceClient` .  Замените `appUrl` с tooyour URL-адрес мобильного приложения.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Работа с таблицами
tooaccess или обновления данных, создать таблицу внутренних toohello ссылки. Замените `tableName` с именем hello таблицы

```
var table = client.getTable(tableName);
```

Имея ссылку на таблицу, можно работать с этой таблицей:

* [Запрос к таблице](#querying)
  * [Фильтрация данных](#table-filter)
  * [Разбиение данных по страницам](#table-paging)
  * [Сортировка данных](#sorting-data)
* [Вставка данных](#inserting)
* [Изменение данных](#modifying)
* [Удаление данных](#deleting)

### <a name="querying"></a>Практическое руководство. Запрос ссылки на таблицу
При наличии ссылки на таблицу, ее можно использовать tooquery для данных на сервере hello.  Запросы осуществляются на языке типа LINQ.
tooreturn все данные из таблицы hello, hello используйте следующий код:

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

Hello успеха функция вызывается с результатами hello.  Не используйте `for (var i in results)` в hello успешно работать так, как будет перебора сведения, включенные в результатах hello при других функций запроса (такие как `.includeTotalCount()`) используются.

Дополнительные сведения о hello синтаксис запроса см. в разделе hello [запрос объекта документации].

#### <a name="table-filter"></a>Фильтрация данных на сервере hello
Можно использовать `where` предложение на ссылку на таблицу hello:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

Можно также использовать функцию, которая фильтрует hello объекта.  В этом случае hello `this` переменной присваивается текущему объекту toothe фильтруемой.  Hello после кода приведен пример предыдущих toohello функционально эквивалентны:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Разбиение данных по страницам
Использовать hello `take()` и `skip()` методы.  Например, при желании toosplit hello таблицы в строке 100 записей:

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

Hello `.includeTotalCount()` в противном случае используется tooadd объект totalCount toohello поля результатов.  Поле totalCount заполняется hello общее количество записей, которые будут возвращены при использовании без разбиения на страницы.

Затем можно использовать переменную страницы hello и некоторые tooprovide кнопками ИП список страниц; Используйте `loadPage()` для загрузки hello новых записей для каждой страницы.  Реализуйте кэширования toorecords toospeed доступа, который уже загружен.

#### <a name="sorting-data"></a>Практическое руководство. Возврат отсортированных данных
Используйте hello `.orderBy()` или `.orderByDescending()` методы запроса:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Дополнительные сведения о hello объекта запроса см. в разделе hello [запрос объекта документации].

### <a name="inserting"></a>Практическое руководство. Вставка данных
Создайте объект JavaScript и соответствующую дату hello и вызовите `table.insert()` асинхронно:

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

Для успешной вставки hello вставить элемент возвращается с hello дополнительные поля, которые требуются для синхронизации операций.  Обновите свой кэш, используя эти данные для последующих обновлений.

пакет SDK для Azure мобильных приложений Node.js сервера Hello поддерживает Динамическая схема для целей разработки.  Динамическая схема позволяет tooadd столбцы toohello таблицы, указав их в операции вставки или обновления.  Рекомендуется отключить динамической схемы перед перемещением tooproduction вашего приложения.

### <a name="modifying"></a>Практическое руководство. Изменение данных
Аналогичные toohello `.insert()` , вы должны создать объект обновления и затем вызвать `.update()`.  Hello обновления объекта должен содержать идентификатор hello записей toobe hello обновлен — hello код должен быть получен при чтении записи hello, или при вызове `.insert()`.

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

### <a name="deleting"></a>Практическое руководство. Удаление данных
toodelete запись, вызов hello `.del()` метод.  Передайте идентификатор hello ссылку на объект:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
