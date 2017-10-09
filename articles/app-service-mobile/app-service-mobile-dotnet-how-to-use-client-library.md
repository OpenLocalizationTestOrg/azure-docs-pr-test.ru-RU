---
title: "Клиентская библиотека управляемых aaaWorking с hello мобильные приложения службы приложений (Windows | Документы Microsoft"
description: "Узнайте, как toouse клиент .NET для приложений мобильных служб Azure приложения с приложениями Windows и Xamarin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Управление toouse hello клиента для мобильных приложений Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как tooperform распространенные сценарии, с помощью hello управление клиентскую библиотеку для приложений Azure приложение службы мобильных приложений для Windows и Xamarin. При наличии новых приложений tooMobile следует первый завершение hello [примеры использования мобильных приложений Azure] [ 1] учебника. В этом руководстве рассматривается hello клиентского управляемого пакета SDK. toolearn Подробнее о hello серверные пакеты SDK для мобильных приложений см. в разделе документации hello hello [.NET SDK сервера] [ 2] или [пакета SDK для Node.js Server] [ 3].

## <a name="reference-documentation"></a>Справочная документация
Hello справочная документация для клиента hello SDK находится здесь: [Справочник по клиентским Azure мобильных приложений .NET][4].
Несколько примеров клиента можно также найти в hello [репозитории GitHub примеров Azure][5].

## <a name="supported-platforms"></a>Поддерживаемые платформы
Hello платформой .NET поддерживает hello следующих платформ:

* выпуски Xamarin Android для API 19–24 (от KitKat до Nougat);
* выпуски Xamarin iOS для iOS 8.0 и более поздних версий;
* Универсальные приложения Windows
* Windows Phone 8.1
* Windows Phone 8.0, за исключением приложений Silverlight.

Проверка подлинности «сервер потока» Hello использует WebView для hello, представленных пользовательского интерфейса.  Если устройство hello не может toopresent WebView пользовательского интерфейса, другие методы проверки подлинности требуется.  Поэтому данный пакет SDK не подходит для различного рода часов и других устройств с аналогичными ограничениями.

## <a name="setup"></a>Настройка и необходимые компоненты
Предполагается, что вы уже создали и опубликовали проект внутреннего сервера мобильных приложений, который содержит по меньшей мере одну таблицу.  Hello код, используемый в этом разделе, с именем таблицы hello `TodoItem` и имеет hello следующие столбцы: `Id`, `Text`, и `Complete`. Эта таблица является hello в одной таблице, созданной при ознакомлении [примеры использования мобильных приложений Azure][1].

Hello соответствующий типизированный клиентский тип в C# — hello, следуя класса:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

Hello [JsonPropertyAttribute] [ 6] — hello используется toodefine *PropertyName* сопоставление между полями клиента hello и hello таблицы.

toolearn как toocreate таблицы в серверной части мобильных приложений, в разделе hello [разделе .NET SDK сервера] [ 7] или hello [пакета SDK для Node.js Server разделе] [ 8] . При создании серверной части мобильное приложение hello Azure с помощью портала hello краткое руководство, можно также использовать hello **простой таблицы** в hello [портал Azure].

### <a name="how-to-install-hello-managed-client-sdk-package"></a>Как: hello установки управляемого пакета SDK для клиента
Используйте один из следующих методов tooinstall hello hello управляемого пакета SDK для клиента для мобильных приложений от [NuGet][9]:

* **Visual Studio** правой кнопкой мыши проект, нажмите кнопку **управление пакетами NuGet**, поиск hello `Microsoft.Azure.Mobile.Client` пакета, а затем нажмите кнопку **установить**.
* **Xamarin Studio** правой кнопкой мыши проект, нажмите кнопку **добавить** > **Добавление пакетов NuGet**, поиск hello `Microsoft.Azure.Mobile.Client `пакета, а затем нажмите кнопку **добавить Пакет**.

В файле основного действия помните следующее hello tooadd **с помощью** инструкции:

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>Практическое руководство. Работа с отладочными символами в Visual Studio
Hello символы для имен Microsoft.Azure.Mobile hello доступны на [SymbolSource][10].  См. toothe [инструкции SymbolSource] [ 11] toointegrate SymbolSource вместе с Visual Studio.

## <a name="create-client"></a>Создание клиента мобильные приложения hello
Hello следующий код создает hello [MobileServiceClient] [ 12] объект, являющийся tooaccess используется внутренний сервер приложений для мобильных устройств.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

В предыдущих кода hello, замените `MOBILE_APP_URL` hello URL-адрес внутреннего сервера мобильного приложения hello, которая находится в серверной части мобильного приложения в hello в колонке [портал Azure]. Объект MobileServiceClient Hello должен быть Singleton-классом.

## <a name="work-with-tables"></a>Работа с таблицами
Здравствуйте, приведенные ниже сведения раздела как toosearch и получить записи и изменение данных hello в таблице hello.  рассматриваются следующие вопросы Hello.

* [Создание ссылки на таблицу](#instantiating)
* [Запрос данных](#querying)
* [Фильтрация возвращаемых данных](#filtering)
* [Сортировка возвращаемых данных](#sorting)
* [Возврат данных на страницах](#paging)
* [Выбор определенных столбцов](#selecting)
* [Поиск записи по идентификатору](#lookingup)
* [Работа с нетипизированными запросами](#untypedqueries)
* [Вставка данных](#inserting)
* [Обновление данных](#updating)
* [Удаление данных](#deleting)
* [Разрешение конфликтов и оптимистичный параллелизм](#optimisticconcurrency)
* [Привязка tooa пользовательский интерфейс Windows](#binding)
* [Изменение размера страницы приветствия](#pagesize)

### <a name="instantiating"></a>Практическое руководство. Создание ссылки на таблицу
Все фрагменты кода hello, доступ к данным или изменяет данные в таблице базы данных вызывает функции hello `MobileServiceTable` объекта. Получить toohello ссылочной таблице, вызывающему Привет [Функция GetTable] метод следующим образом:

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

Hello вернул объект использует модель сериализации типизированных hello. Также поддерживается нетипизированная модель сериализации. Следующий пример [создает ссылочной таблице нетипизированного tooan]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

В нетипизированный запросов необходимо указывать hello базовой строки запроса OData.

### <a name="querying"></a>Практическое руководство. Запрос данных из мобильного приложения
В этом разделе описывается, как tooissue запрашивает внутренней toohello мобильного приложения, включая hello следующие функциональные возможности:

* [Фильтрация возвращаемых данных](#filtering)
* [Сортировка возвращаемых данных](#sorting)
* [Возврат данных на страницах](#paging)
* [Выбор определенных столбцов](#selecting)
* [Поиск данных по идентификатору](#lookingup)

> [!NOTE]
> Размер страницы управляемого сервера — принудительно tooprevent все строки из возвращаемых.  Разбиение на страницы предотвращает отрицательно влияет на службы hello запросов по умолчанию для больших наборов данных.  tooreturn более 50 строк используйте hello `Skip` и `Take` метода, как описано в [возвращать данные на страницах](#paging).

### <a name="filtering"></a>Практическое руководство. Фильтрация возвращаемых данных
Hello следующий код показывает, как toofilter данных, включая `Where` предложения в запросе. Возвращает все элементы из `todoTable` которого `Complete` значение свойства равно слишком`false`. Hello [где] функция применяется предикат для hello запрос к таблице hello фильтрации строк.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

Hello URI внутреннего toohello запрос, отправленный hello можно просмотреть с помощью программного обеспечения проверки сообщения, например средства разработчика браузера или [Fiddler]. Если взглянуть на URI запроса hello, обратите внимание, строка hello запроса было изменено:

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

Этот запрос OData преобразуется в SQL-запрос по hello Server SDK:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

Здравствуйте, функции, передаваемой toohello `Where` метод может иметь произвольное число условий.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

В этом примере это дерево будет преобразовано в SQL-запрос по hello Server SDK:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

Этот запрос также можно разбить на несколько предложений:

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

Здравствуйте, два метода являются эквивалентными и могут быть взаимозаменяемыми.  Здравствуйте первого варианта&mdash;объединения нескольких предикатов в одном запросе&mdash;является более компактным и рекомендуемые.

Hello `Where` предложение поддерживает операции, которые будет преобразовано в подмножестве OData hello. К этим операциям относятся:

* операторы сравнения (==,! =, <, < =, >, > =);
* арифметические операторы (+, -, /, *, %);
* указание точности чисел (Math.Floor, Math.Ceiling);
* строковые функции (Length, Substring, Replace, IndexOf, StartsWith, EndsWith);
* свойства даты (Year, Month, Day, Hour, Minute, Second);
* свойства доступа к объекту;
* выражения, сочетающие в себе любые из этих операций.

Если поддерживает учитывая то, что hello SDK сервера, можно рассмотреть hello [документации OData v3].

### <a name="sorting"></a>Практическое руководство. Сортировка возвращаемых данных
Hello следующий код показывает, как toosort данных, включая [OrderBy] или [OrderByDescending] функции в запросе hello. Возвращает элементы из `todoTable` сортируются по возрастанию по hello `Text` поля.

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <a name="paging"></a>Практическое руководство. Возврат данных на страницах
По умолчанию hello серверной возвращает hello только первые 50 строк. Можно увеличить hello число возвращенных строк, вызывающему Привет [принимать] метод. Используйте `Take` вместе с hello [пропустить] метод toorequest конкретных «страница» общего набора данных hello возвращаемых запросом hello. Hello при выполнении следующего запроса возвращает hello три верхних элементов в таблице hello.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Hello следующий измененный запрос пропускает hello первые три результаты и возвращает hello трех следующих результатов. Этот запрос получает hello второй «страницы» данных, где размер страницы приветствия трех элементов.

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Hello [IncludeTotalCount] метод запрашивает hello общее число *все* hello записей, которые были бы возвращены, условии указано любые ограничения или разбиения на страницы:

```
query = query.IncludeTotalCount();
```

В приложении реального мира можно использовать аналогичный toohello запросы предшествующий пример с сопоставимых пользовательского интерфейса или элемент управления страничного навигатора для перехода между страницами.

> [!NOTE]
> ограничение 50 строк toooverride hello в серверном приложении мобильного приложения, необходимо также применить hello [EnableQueryAttribute] toohello открытый метод GET и укажите hello разбиение по страницам. При toohello применяется метод, hello следующие задает too1000 максимальное число возвращенных строк:
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>Практическое руководство. Выбор определенных столбцов
Можно указать набор свойств tooinclude в hello, добавив [выберите] предложение tooyour запроса. Здравствуйте, например, как следующий код показывает одно поле tooselect и также как tooselect и отформатировать несколько полей:

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

Здравствуйте, все функции, описанные в данный момент являются аддитивными, поэтому мы можно сохранить цепочки их. Каждый вызов цепочек влияет на несколько запросов hello. Еще один пример:

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>Практическое руководство. Поиск данных по идентификатору
Hello [LookupAsync] функция может быть используется toolook объектов из базы данных hello с определенным идентификатором.

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>Практическое руководство. Выполнение нетипизированных запросов
При выполнении запроса с помощью объекта нетипизированного таблицы, необходимо явно указать строку запроса OData hello путем вызова [ReadAsync], как показано в следующий пример hello:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

Вы будете получать значения JSON, которые можно использовать в качестве контейнера свойств. Дополнительные сведения о JToken и Newtonsoft Json.NET см. в разделе hello [Json.NET] сайта.

### <a name="inserting"></a>Практическое руководство. Вставка данных в серверную часть мобильных приложений
Все типы клиентов должны содержать член с именем **Id**(идентификатор), который по умолчанию является строкой. Это **идентификатор** требуется для выполнения операций CRUD и hello в автономном режиме синхронизации. следующий код иллюстрирует способ toouse hello [InsertAsync] метод tooinsert новых строк в таблицу. параметр Hello содержит hello toobe данных, добавляются в виде объекта .NET.

```
await todoTable.InsertAsync(todoItem);
```

Если пользовательские уникальное значение идентификатора не включается в hello `todoItem` во время операции вставки, идентификатор GUID создается сервером hello.
Вы можете получить hello созданный идентификатор, изучая hello объекта после возвращения вызова hello.

tooinsert нетипизированных данных, могут воспользоваться преимуществами Json.NET:

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

Вот пример использования электронного адреса в качестве уникального строкового идентификатора.

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>Работа со значениями идентификаторов
Мобильные приложения поддерживает уникальная строка пользовательские значения для таблицы hello **идентификатор** столбца. Строковое значение позволяет приложениям toouse пользовательские значения, такие как адреса электронной почты или имена пользователей для идентификатора hello.  Идентификаторами строк предоставить hello следующие преимущества:

* Идентификаторы создаются без создания базы данных toohello кругового пути.
* Записи, проще toomerge из различных таблиц или баз данных.
* Значения идентификаторов можно удобно интегрировать с логикой приложения.

Если строковое значение идентификатора для вставленной записи не задан, внутреннего сервера мобильного приложения hello формирует уникальное значение для идентификатора. Можно использовать hello [Guid.NewGuid] toogenerate метод собственный идентификатор значения на приветствия клиента или на внутреннем сервере hello.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>Практическое руководство. Изменение данных в серверной части мобильных приложений
Hello следующий код показывает, как toouse hello [UpdateAsync] tooupdate метод существующей записи с hello таким же ИДЕНТИФИКАТОРОМ с новыми данными. параметр Hello содержит toobe данных hello обновлен как объект .NET.

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate нетипизированных данных, могут воспользоваться преимуществами [Json.NET] следующим образом:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

При выполнении обновления необходимо указать поле `id` . Hello внутренним сервером hello `id` tooidentify поля которого tooupdate строк. Hello `id` поля можно получить из результата hello hello `InsertAsync` вызова. `ArgumentException` Возникает при попытке tooupdate элемент без предоставления hello `id` значение.

### <a name="deleting"></a>Практическое руководство. Удаление данных в серверной части мобильных приложений
Hello следующий код показывает, как toouse hello [DeleteAsync] toodelete метод существующего экземпляра. экземпляр Hello определяется hello `id` наборе на hello полей `todoItem`.

```
await todoTable.DeleteAsync(todoItem);
```

toodelete нетипизированных данных, может использовать преимущества Json.NET следующим образом:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

При создании запроса на удаление необходимо указать идентификатор. Другие свойства, не передаются toohello службы или учитываются в службе hello. Здравствуйте, результат `DeleteAsync` обычно является вызов `null`. toopass идентификатор Hello в можно получить из результата hello hello `InsertAsync` вызова. Объект `MobileServiceInvalidOperationException` возникает при попытке toodelete элемент без указания hello `id` поля.

### <a name="optimisticconcurrency"></a>Практическое руководство. Использование оптимистичного параллелизма для устранения конфликтов
Два или несколько клиентов могут записывать изменения toohello же элемент в hello, же время. Без обнаружения конфликтов последняя запись hello перезапишет все предыдущие обновления. **управлении оптимистичным параллелизмом** предполагается, что каждая транзакция может фиксироваться, поэтому не использует блокировки каких-либо ресурсов.  Прежде чем фиксировать транзакции, управление оптимистичным параллелизмом проверяет, что никакая другая транзакция изменила данные hello. Если был изменен hello данных hello Фиксация транзакции выполняется откат.

Мобильные приложения поддерживает управление оптимистичным параллелизмом, отслеживая изменения tooeach элемента с помощью hello `version` столбец системного свойства, определенные для каждой таблицы в серверной части мобильного приложения. Каждый раз при обновлении записи мобильные приложения задает hello `version` свойства для этой записи tooa новое значение. Во время каждого запроса update hello `version` hello-записи, входящий в состав hello запроса является сравниваемых toohello же свойство для записи hello на сервере hello. При передаче версию с hello запроса не соответствует hello серверной части, а затем вызывает hello клиентская библиотека `MobileServicePreconditionFailedException<T>` исключение. Тип Hello, входящий в состав hello исключение — hello запись с hello серверной части содержащего hello серверы версий hello записи. Hello затем приложение может использовать этот toodecide сведения ли запрос tooexecute hello обновления, указав правильный hello `version` значение от изменений toocommit hello серверной части.

Определения столбцов для класса таблицы hello для hello `version` системы свойство tooenable оптимистичного параллелизма. Например:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

Приложения, использующие нетипизированный таблиц включите оптимистичного параллелизма, установка hello `Version` флаг `SystemProperties` из hello таблицы следующим образом.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

При оптимистическом параллелизме tooenabling сложения, должен перехватывать hello `MobileServicePreconditionFailedException<T>` исключений в коде, при вызове [UpdateAsync].  Разрешить конфликт hello, применяя hello правильный `version` toothe обновленные записи и вызов [UpdateAsync] с hello разрешил запись. Hello, следующий код показывает, как tooresolve записи один раз конфликт:

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

Дополнительные сведения см. в разделе hello [автономной синхронизации данных в мобильных приложениях Azure] раздела.

### <a name="binding"></a>Как: пользовательский интерфейс Windows tooa мобильных приложениях привязки данных
В этом разделе показано, как toodisplay возвращают объекты данных с помощью элементов пользовательского интерфейса в приложении Windows.  В следующем примере кода привязывает источник toohello hello списка с помощью запроса для неполных элементов. При использовании [MobileServiceCollection] создается коллекция привязок, поддерживающих мобильные приложения.

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

Некоторые элементы управления в hello управляемых поддержку среды выполнения, называют интерфейс [ISupportIncrementalLoading]. Этот интерфейс позволяет toorequest элементов управления при прокрутке hello дополнительные данные. Имеется встроенная поддержка для универсальных приложений Windows через этот интерфейс [MobileServiceIncrementalLoadingCollection], которая автоматически обрабатывает вызовы из элементов управления hello. Используйте `MobileServiceIncrementalLoadingCollection` в приложениях для Windows, как показано ниже.

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse hello новую коллекцию в приложениях Windows Phone 8 и «Silverlight», используйте hello `ToCollection` методы расширения в `IMobileServiceTableQuery<T>` и `IMobileServiceTable<T>`. вызов данных tooload `LoadMoreItemsAsync()`.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

При использовании коллекции hello создаются путем вызова `ToCollectionAsync` или `ToCollection`, получить коллекцию, которая может быть tooUI связанных элементов управления.  Эта коллекция поддерживает разбиение по страницам.  Так как коллекция элементов hello загружает данные из сети, иногда загрузка завершится ошибкой. toohandle таких сбоев переопределить hello `OnException` метод `MobileServiceIncrementalLoadingCollection` toohandle исключения, возникающие в результате вызовов слишком`LoadMoreItemsAsync`.

Рекомендуется, если таблица содержит много полей, но требуется только toodisplay некоторые из них в элементе управления. Вы можете использовать руководство hello в hello предшествующий раздел «[выбирать отдельные столбцы](#selecting)» tooselect toodisplay определенные столбцы в hello пользовательского интерфейса.

### <a name="pagesize"></a>Hello изменение размера страницы
По умолчанию мобильные приложения Azure выдают не больше 50 элементов на запрос.  Можно изменить объем подкачки hello увеличив hello максимальный размер страницы приветствия клиента и сервера.  tooincrease Здравствуйте запрошенный размер страницы, укажите `PullOptions` при использовании `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

При условии, что были внесены hello `PageSize` равно tooor больше 100 в пределах сервера hello, запрос возвращает до 100 элементов.

## <a name="#offlinesync"></a>Работа с автономными таблицами
Автономные таблицы используйте локального хранения данных toostore SQLite для использования в автономном режиме.  Все операции осуществляются с hello таблицы локального SQLite хранилища вместо хранилище hello удаленного сервера.  toocreate автономной таблицы, сначала подготовить проект:

1. В Visual Studio щелкните правой кнопкой мыши решение hello > **управление пакетами NuGet для решения...** , выполните поиск и установка **Microsoft.Azure.Mobile.Client.SQLiteStore** пакет NuGet для всех проектов в решении hello.
2. (Необязательно) toosupport устройства Windows, установите одно из следующих пакетов среды выполнения SQLite hello.

   * **Среда выполнения Windows 8.1**: установите [SQLite для Windows 8.1][3].
   * **Windows Phone 8.1**: установите [SQLite для Windows Phone 8.1][4].
   * **Универсальная платформа Windows** установить [SQLite для универсальных приложений Windows hello][5].
3. (необязательно). Для устройств Windows, нажмите кнопку **ссылки** > **добавить ссылку...** , разверните hello **Windows** папки > **расширения**, включите соответствующий hello **SQLite для Windows** пакета SDK, а также hello  **Среда выполнения 2013 Visual C++ для Windows** SDK.
    Hello SQLite SDK имена будут немного отличаться с каждой платформы Windows.

Чтобы можно было создать ссылку на таблицу, необходимо подготовить hello локального хранилища:

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

Инициализации хранилища, обычно осуществляется сразу после создания клиента hello.  Hello **OfflineDbPath** должно быть имя файла можно использовать на всех платформах, которые вы поддерживаете.  Если путь hello полный путь (то есть, он начинается с косой черты), то используется этот путь.  Если hello путь задан не полностью, hello файл помещается в месте конкретную платформу.

* Для устройств iOS и Android путь по умолчанию hello — папка «Личные файлы» hello.
* Для устройств Windows hello путь по умолчанию — папка «AppData» hello конкретного приложения.

Ссылки на таблицу можно получить, используя hello `GetSyncTable<>` метод:

```
var table = client.GetSyncTable<TodoItem>();
```

Tooauthenticate toouse автономной таблицы не обязательно.  Tooauthenticate необходим только в том случае, при которой осуществляется взаимодействие с серверной службы hello.

### <a name="syncoffline"></a>Синхронизация автономной таблицы
Автономные таблиц не синхронизирован с серверной hello по умолчанию.  Синхронизация происходит в два этапа.  Можно передавать изменения отдельно от скачивания новых элементов.  Ниже приведен типичный метод синхронизации.

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

Если слишком hello первый аргумент`PullAsync` имеет значение null, то добавочной синхронизации не используется.  Каждая операция синхронизации извлекает все записи.

Выполняет неявную Hello SDK `PushAsync()` прежде чем извлекать записей.

Обработка конфликтов происходит в методе `PullAsync()`.  Можно обработать конфликтов в hello таким же, как online таблиц.  Hello конфликтов производится при `PullAsync()` вызывается вместо во время hello insert, update или delete. Если возникает несколько конфликтов, они объединяются в одно исключение MobileServicePushFailedException.  Каждая ошибка должна обрабатываться отдельно.

## <a name="#customapi"></a>Работа с настраиваемым API
Пользовательский API позволяет toodefine пользовательских конечных точек, предоставляющих функциональные возможности сервера, которые не сопоставляются tooan вставки, обновления, удаления или операцию чтения. При использовании настраиваемого интерфейса API вы получаете больше возможностей для управления сообщениями, в том числе для чтения и установки заголовков HTTP-сообщений, а также определения форматов текста сообщений, отличных от JSON.

Вызов пользовательского API путем вызова одного из hello [InvokeApiAsync] методов на приветствия клиента. Например, следующая строка кода hello отправляет запрос POST toohello **completeAll** API hello серверную часть:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

Эта форма представляет собой вызов типизированный метод и требует этого hello **MarkAllResult** возвращают тип определен. Поддерживаются типизированные и нетипизированные методы.

метод InvokeApiAsync() Hello добавляет/api/toohello API обратиться toocall Если hello API начинается с «/».
Например:

* `InvokeApiAsync("completeAll",...)`вызывает /api/completeAll серверную часть hello
* `InvokeApiAsync("/.auth/me",...)`вызывает /.auth/me серверную часть hello

InvokeApiAsync toocall можно использовать любой WebAPI, включая те WebAPIs, которые не определены с помощью мобильных приложений Azure.  При использовании InvokeApiAsync() hello соответствующие заголовки, включая заголовки проверки подлинности, отправляются с запросом hello.

## <a name="authentication"></a>Аутентификация пользователей
Мобильные приложения поддерживают аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетной записи Майкрософт, Twitter и Azure Active Directory. Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей. Hello идентификаторов правил авторизации tooimplement прошедших проверку подлинности пользователей также можно использовать в серверных скриптах. Дополнительные сведения см. в разделе учебника hello [приложение tooyour authentication добавить].

Поддерживаются два потока аутентификации: *управляемой клиентом* и *управляемый сервером*. Поток управляемого сервером Hello обеспечивает hello простой проверки подлинности, как зависит от поставщика hello веб-интерфейс проверки подлинности. Hello клиента управляемого потока позволяет более глубокую интеграцию с возможности определенных устройств, как он основывается на пакеты SDK поставщика конкретного устройства.

> [!NOTE]
> Мы рекомендуем использовать в рабочих приложениях поток, управляемый клиентом.

tooset проверку подлинности, необходимо зарегистрировать приложение с одним или несколькими поставщиками удостоверений.  Поставщик удостоверений Hello создает идентификатор клиента и секрет клиента для приложения.  Затем эти значения устанавливаются в вашей серверной tooenable службе приложений Azure проверки подлинности и авторизации.  Для получения дополнительной информации выполните hello подробные инструкции в учебнике [приложение tooyour authentication добавить].

в этом разделе рассматриваются следующие вопросы Hello:

* [Управляемая клиентом проверка подлинности.](#clientflow)
* [Управляемая сервером проверка подлинности.](#serverflow)
* [Маркер проверки подлинности кэширования hello](#caching)

### <a name="clientflow"></a>Управляемая клиентом проверка подлинности.
Приложения могут независимо обращаться hello поставщика удостоверений и, после чего укажите hello возвращенный токен во время входа серверной части. Этот порядок клиента позволяет tooprovide единого интерфейса входа для пользователей или tooretrieve дополнительные пользовательские данные от поставщика удостоверений hello. Проверки подлинности для потока клиента — предпочтительный toousing потока сервере как поставщик удостоверений hello SDK предоставляет более естественным вид UX и обеспечивает дополнительные настройки.

Примеры для hello следующие шаблоны проверки подлинности клиента потока:

* [Библиотека проверки подлинности Active Directory](#adal)
* [Facebook или Google](#client-facebook)
* [Пакет Live SDK](#client-livesdk)

#### <a name="adal"></a>Проверять подлинность пользователей с hello библиотеку аутентификации Active Directory
Можно использовать hello библиотеку проверки подлинности Active Directory (ADAL) tooinitiate пользователя проверку подлинности от клиента hello, с использованием проверки подлинности Azure Active Directory.

1. Настройте внутренний сервер мобильных приложений для входа AAD, следующие hello [как tooconfigure приложения службы для имени входа Active Directory] учебника. Убедитесь, что необязательный шаг toocomplete hello регистрации собственного клиентского приложения.
2. В Visual Studio и Xamarin Studio, откройте проект и добавить toothe ссылки `Microsoft.IdentityModel.CLients.ActiveDirectory` пакет NuGet. Включите в диапазон поиска предварительные версии.
3. Добавьте hello следующие приложения tooyour кода, в соответствии с toohello платформы, которую вы используете. В каждой из них внесите hello после замены.

   * Замените **вставки ЦЕНТРА здесь** hello имя клиента hello, в котором подготовлено приложения. Формат должен быть следующим: https://login.microsoftonline.com/contoso.onmicrosoft.com. Это значение можно скопировать из hello вкладка домена в Azure Active Directory в hello [классический портал Azure].
   * Замените **вставки РЕСУРСОВ-идентификатор здесь** с Идентификатором hello клиент для мобильного приложения серверной части. Можно получить идентификатор клиента hello hello **Дополнительно** в разделе **параметры Azure Active Directory** hello портала.
   * Замените **вставки КЛИЕНТА-идентификатор здесь** с Идентификатором клиента hello, скопированные из собственного клиентского приложения hello.
   * Замените **вставки ПЕРЕНАПРАВЛЕНИЯ-URI здесь** с веб-узла */.auth/login/done* конечную точку, используя hello схему HTTPS. Это значение должно быть примерно слишком*https://contoso.azurewebsites.net/.auth/login/done*.

     Hello код, необходимый для каждой платформы выглядит следующим образом:

     **Windows:**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     **Xamarin.iOS**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     **Xamarin.Android**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <a name="client-facebook"></a>Единый вход с помощью маркера Google или Facebook
Вы можете использовать поток клиентских hello, как показано в этом фрагменте кода для Google или Facebook.

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <a name="client-livesdk"></a>Здравствуйте, единого входа в систему под учетной записью Майкрософт с помощью пакета SDK Live
tooauthenticate пользователей, необходимо зарегистрировать приложения в учетной записи Майкрософт Центр разработчиков hello. Настройте регистрационные данные для серверной части мобильного приложения. toocreate Microsoft Регистрация учетной записи и подключите его серверной tooyour мобильного приложения, завершения hello шагов в [регистрации вашего приложения toouse имя входа учетной записи Майкрософт]. При наличии магазина Windows и Windows Phone 8/Silverlight версии приложения сначала зарегистрируйте версии магазина Windows hello.

Hello следующий код выполняет проверку подлинности с помощью пакета SDK Live и использует hello, возвращается токен toosign в серверной части tooyour мобильное приложение.

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

Дополнительные сведения см. в разделе hello [пакета SDK Live Windows] документации.

### <a name="serverflow"></a>Управляемая сервером проверка подлинности.
После регистрации поставщика удостоверений, вызовите hello [LoginAsync] метод hello [MobileServiceClient] с hello [MobileServiceAuthenticationProvider] значение поставщика. Например hello следующий код инициирует вход потока сервера с помощью Facebook.

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

При использовании поставщика удостоверений, отличные от Facebook, измените значение hello [MobileServiceAuthenticationProvider] toohello значение для поставщика.

В потоке сервера службы приложений Azure управляет поток проверки подлинности OAuth hello путем отображения приветствия на странице входа hello выбранного поставщика.  Один раз возвращает поставщик удостоверений hello, службе приложений Azure создает маркер проверки подлинности службы приложений. Hello [LoginAsync] возвращает [MobileServiceUser], который предоставляет оба hello [UserId] из hello и проверкой подлинности пользователя hello [ MobileServiceAuthenticationToken], как веб-токен JSON (JWT). Этот маркер можно поместить в кэш и повторно использовать, пока не истечет срок его действия. Дополнительные сведения см. в разделе [токена проверки подлинности hello кэширование](#caching).

### <a name="caching"></a>Маркер проверки подлинности кэширования hello
В некоторых случаях можно избежать toohello входа hello вызов метода после первого успешного прохождения проверки подлинности hello, сохраняя hello токена проверки подлинности от поставщика hello.  Можно использовать для приложений магазина Windows и UWP [PasswordVault] toocache текущего проверки подлинности маркера после успешного входа в систему, следующим образом:

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

Hello UserId значение хранится в виде hello hello учетных данных пользователя и маркер hello — hello, хранятся в виде hello пароль. В последующих начинающих можно проверить hello **PasswordVault** для кэшированных учетных данных. Hello следующий пример использует кэшированные учетные данные, когда они находятся, а в противном случае попытки tooauthenticate с серверной hello.

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

Выйти из системы пользователя, также необходимо удалить hello хранимых учетных данных, следующим образом:

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Приложения Xamarin использовать hello [Xamarin.Auth] API-интерфейсы в учетных данных хранилища toosecurely **учетной записи** объекта. Пример использования этих интерфейсов API см. в разделе hello [AuthStore.cs] файл исходного кода в hello [совместное использование образец фото ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).

При использовании управляемой клиентом проверки подлинности, также могут кэшироваться hello токен доступа, полученный от поставщика, например Facebook или Twitter. Этот токен может быть предоставленный toorequest новый маркер проверки подлинности из внутренней hello, следующим образом:

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>Push-уведомления
Hello ниже описывается Push-уведомления:

* [Регистрация для получения push-уведомлений](#register-for-push)
* [Получение SID пакета Магазина Windows](#package-sid)
* [Регистрация с помощью межплатформенных шаблонов](#register-xplat)

### <a name="register-for-push"></a>Практическое руководство. Регистрация для получения push-уведомлений
Клиент мобильные приложения Hello позволяет tooregister для push-уведомлений с концентраторами уведомлений Azure. При регистрации, можно получить дескриптор, который получен из hello платформой службы Push-уведомлений (PNS). Затем укажите это значение вместе с любыми тегами, при создании регистрации hello. Hello следующий код регистрирует приложения Windows для push-уведомлений с hello Windows Notification Service (WNS):

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

При отправке tooWNS, необходимо [получить ИД безопасности пакета магазина Windows](#package-sid).  Дополнительные сведения о приложениях Windows включая tooregister для регистрации шаблонов, см. в [уведомления tooyour добавить push приложения].

Запрос теги из hello клиента не поддерживается.  Запросы тегов автоматически отбрасываются из регистрации.
При желании tooregister устройства с тегами, создайте настраиваемый API, который использует hello API концентраторов уведомлений tooperform hello регистрации от вашего имени.  [Вызов пользовательского API hello](#customapi) вместо hello `RegisterNativeAsync()` метод.

### <a name="package-sid"></a>Практическое руководство. Получение SID пакета Магазина Windows
Для включения push-уведомлений для приложений Магазина Windows необходим SID пакета.  tooreceive пакета SID, зарегистрировать приложение в магазине Windows hello.

tooobtain это значение:

1. В обозревателе решений Visual Studio, щелкните правой кнопкой мыши проект приложения для магазина Windows hello, щелкните **хранилища** > **связать приложение с hello хранилища...** .
2. В мастере приветствия щелкните **Далее**, войти в учетную запись Майкрософт, введите имя приложения в **зарезервировать новое имя приложения**, нажмите кнопку **резерва**.
3. После регистрации приложения hello hello успешно создан, выберите имя приложения, нажмите кнопку **Далее**, а затем нажмите кнопку **связать**.
4. Войдите в toohello [центра разработчиков Windows] с учетной записью Майкрософт. В разделе **Мои приложения**, нажмите кнопку регистрации приложения hello, вы создали.
5. Нажмите кнопку **управления приложениями** > **удостоверение приложения**, а затем прокрутите экран вниз toofind вашей **ИД безопасности пакета**.

В большинстве случаев идентификатор безопасности пакета hello рассматривать его как универсальный код Ресурса, в этом случае необходимо toouse *ms-app: / /* как схему hello. Запишите hello версии пакета SID, полученная путем сцепления это значение в качестве префикса.

Приложения Xamarin требуются некоторые возможности tooregister toobe дополнительный код приложение, запущенное на платформах hello iOS или Android. Дополнительные сведения см. в разделе hello для вашей платформы:

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>Как: Register извещающих шаблоны toosend кросс платформенных уведомлений
шаблоны tooregister использовать hello `RegisterAsync()` метод hello шаблонов, как показано ниже:

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

Шаблоны должны быть `JObject` типы и могут содержать несколько шаблонов в hello следующий формат JSON:

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

Здравствуйте, метод **RegisterAsync()** также принимает вторичной плитки:

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

Во время регистрации все теги удаляются в целях безопасности. теги tooadd tooinstallations или шаблоны в установках см. в разделе [работа с сервера базы данных hello .NET SDK для мобильных приложений Azure].

Использование этих зарегистрированных шаблонов уведомлений toosend ссылаться toohello [API-интерфейсов концентраторы уведомлений].

## <a name="misc"></a>Разное
### <a name="errors"></a>Практическое руководство. Обработка ошибок
При возникновении ошибки в серверном приложении hello hello клиент вызывает SDK `MobileServiceInvalidOperationException`.  В следующем примере показан способ toohandle исключение, которое возвращается сервером hello:

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

Еще один пример работы с состояниями ошибки можно найти в hello [пример файлов мобильных приложений]. [LoggingHandler] пример предоставляет делегат ведения журнала обработчик toolog hello запросов toohello серверной части.

### <a name="headers"></a>Практическое руководство. Настройка заголовков запроса
toosupport в данном случае определенное приложение, может потребоваться toocustomize связь с внутреннего сервера мобильного приложения hello. Например вы можете требуется tooadd исходящего запроса с tooevery пользовательский заголовок или даже коды состояния ответов. Можно использовать пользовательский [DelegatingHandler], как показано в следующий пример hello:

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[приложение tooyour authentication добавить]: app-service-mobile-windows-store-dotnet-get-started-users.md
[автономной синхронизации данных в мобильных приложениях Azure]: app-service-mobile-offline-data-sync.md
[уведомления tooyour добавить push приложения]: app-service-mobile-windows-store-dotnet-get-started-push.md
[регистрации вашего приложения toouse имя входа учетной записи Майкрософт]: app-service-mobile-how-to-configure-microsoft-authentication.md
[как tooconfigure приложения службы для имени входа Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[Функция GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[создает ссылочной таблице нетипизированного tooan]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[принимать]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[выберите]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[пропустить]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[где]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[портал Azure]: https://portal.azure.com/
[классический портал Azure]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[центра разработчиков Windows]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[пакета SDK Live Windows]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[API-интерфейсов концентраторы уведомлений]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[пример файлов мобильных приложений]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[документации OData v3]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
