---
title: "aaaHow toouse hello Azure мобильных приложений и пакет SDK для Android | Документы Microsoft"
description: "Как toouse hello пакет SDK Azure Mobile приложений для Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Как toouse hello пакет SDK Azure Mobile приложений для Android

В этом руководстве показано, как toouse hello Android пакет SDK для клиента в распространенных сценариях tooimplement мобильные приложения, такие как:

* запрос данных (вставка, обновление и удаления);
* аутентификация;
* обработка ошибок;
* Настройка клиента hello.

Это руководство посвящено hello клиентского пакета SDK для Android.  toolearn Подробнее о hello серверные пакеты SDK для мобильных приложений см. в разделе [работать с серверной части .NET SDK] [ 10] или [как toouse hello серверной Node.js SDK] [ 11].

## <a name="reference-documentation"></a>Справочная документация

Можно найти hello [Справочник по Javadocs API] [ 12] для hello Android клиентской библиотеки на сайте GitHub.

## <a name="supported-platforms"></a>Поддерживаемые платформы

Hello Azure мобильных приложений и пакет SDK для Android поддерживает уровни API 19 до 24 (KitKat через Nougat) для телефонов и планшетных ПК форм-факторов.  Проверка подлинности, в частности, использует общий подход framework web toogather учетные данные.  Серверный поток проверки подлинности не работает на устройствах малого форм-фактора, таких как часы.

## <a name="setup-and-prerequisites"></a>Настройка и необходимые компоненты

Полный hello [краткое руководство мобильные приложения](app-service-mobile-android-get-started.md) учебника.  Выполнение данной задачи гарантирует, что будут соблюдены все предварительные требования для разработки мобильных приложений Azure.  также Hello краткое руководство поможет вам настроить учетную запись и создать первый серверной части мобильное приложение.

Если вы решите не toocomplete hello краткого руководства, выполните следующие задачи hello.

* [Создание серверной части мобильное приложение] [ 13] toouse вместе с приложением Android.
* В Android Studio [файлы сборки hello обновления Gradle](#gradle-build).
* [Включение разрешение INTERNET](#enable-internet).

### <a name="gradle-build"></a>Обновить файл сборки Gradle hello

Измените оба файла **build.gradle** :

1. Добавьте этот код toohello *проекта* уровень **build.gradle** файла внутри hello *buildscript* тег:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Добавьте этот код toohello *модуль приложения* уровень **build.gradle** файла внутри hello *зависимости* тег:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    В настоящее время hello последняя версия — 3.3.0. Hello поддерживаемые версии перечислены [на bintray][14].

### <a name="enable-internet"></a>Включение разрешения INTERNET

tooaccess Azure приложения необходимо разрешение hello Интернет включено. Если он еще не включен, добавить hello, следующей строкой кода tooyour **AndroidManifest.xml** файла:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>Создание подключения клиента

Мобильные приложения Azure предоставляет четыре функции tooyour мобильного приложения.

* доступ к данным и их синхронизация в автономном режиме со службой мобильных приложений Azure;
* Вызов пользовательского API, написанную hello пакет SDK для приложений мобильных сервера Azure.
* проверка подлинности с помощью функции проверки подлинности и авторизации в службе приложений Azure;
* регистрация push-уведомлений в Центрах уведомлений.

Чтобы использовать каждую из этих функций, сначала необходимо создать объект `MobileServiceClient`.  В мобильном клиенте необходимо создать только один объект `MobileServiceClient` (то есть следует использовать шаблон с одним элементом).  toocreate `MobileServiceClient` объекта:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Hello `<MobileAppUrl>` — строка или объект URL-адрес, который указывает tooyour мобильной серверной части.  При использовании службы приложений Azure toohost серверной части мобильных устройств, затем используйте безопасный hello `https://` версии hello URL-адрес.

Hello клиента также требуется доступ toohello действия или контексте - hello `this` параметр в примере hello.  Hello построения MobileServiceClient должны быть выполнены в рамках hello `onCreate()` метод hello, на которые ссылается действие hello `AndroidManifest.xml` файла.

Мы советуем абстрагировать связь сервера в собственный класс (шаблон с одним элементом).  В этом случае следует передавать hello действия в конструктор tooappropriately hello настроить службу hello.  Например:

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

Теперь можно вызвать `AzureServiceAdapter.Initialize(this);` в hello `onCreate()` метод основных действия.  Использовать другие методы, создающие toohello клиента `AzureServiceAdapter.getInstance();` tooobtain адаптер службы toohello ссылки.

## <a name="data-operations"></a>Операции с данными

Hello hello пакет SDK Azure Mobile приложений лежит toodata tooprovide доступ, хранящихся в SQL Azure серверную часть мобильное приложение hello.  Доступ к этим данным можно получить, используя классы со строгим типом (предпочтительный способ) или нетипизированные запросы (нерекомендуемый способ).  Hello большая часть в этом разделе рассматриваются использование строго типизированных классов.

### <a name="define-client-data-classes"></a>Определение клиентских классов данных

tooaccess данные из таблиц SQL Azure, определяют клиентские классы данных, соответствующих таблиц toohello в серверном мобильное приложение hello. Примеры в этом разделе предполагается, таблица с именем **MyDataTable**, который имеет hello следующие столбцы:

* id
* текст
* complete

Hello соответствующий типизированный клиентский объект находится в файле с именем **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Включите методы Getter или Setter в каждое добавленное поле.  Если таблица SQL Azure содержит больше столбцов, необходимо добавить hello соответствующего поля toothis класса.  Например, если hello DTO (объект передачи данных) имеет приоритет целочисленном столбце, то можно добавить это поле, а также его методы get и set:

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

toolearn toocreate дополнительных таблиц в серверной части мобильных приложений, в статье [как: определить табличный контроллер] [ 15] (серверное приложение .NET) или [определения таблиц, с помощью динамической схемы] [ 16] (Серверное приложение Node.js).

Таблицу серверной части мобильных приложений Azure определяет пять специальные поля, четыре из которых будут доступны tooclients:

* `String id`: hello глобальный уникальный идентификатор записи hello.  Как рекомендуется сделать hello идентификатор hello строковое представление [UUID] [ 17] объекта.
* `DateTimeOffset updatedAt`: hello Дата и время последнего обновления hello.  поле updatedAt Hello задается сервером hello и никогда не должно задаваться в клиентской программе.
* `DateTimeOffset createdAt`: hello даты и времени создания этого hello объекта.  поле createdAt Hello задается сервером hello и никогда не должно задаваться в клиентской программе.
* `byte[] version`: Обычно представлено в виде строки, версия hello также устанавливается сервером hello.
* `boolean deleted`: Указывает, что запись hello был удален, но еще не очищаются.  Не используйте `deleted` в качестве свойства класса.

Hello `id` поле является обязательным.  Hello `updatedAt` поля и `version` поля используются для синхронизации в автономном режиме (для добавочной синхронизации и вступают в конфликт разрешения соответственно).  Hello `createdAt` поле поле ссылки и не используется клиентом hello.  имена Hello «на лету» имена свойств hello и не являются изменяемыми.  Тем не менее, можно создать сопоставление между объектом и hello имена «на лету», используя hello [gson] [ 3] библиотеки.  Например:

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a>Создание ссылки на таблицу

tooaccess таблицы, сначала создайте [MobileServiceTable] [ 8] объект, вызывающий hello **getTable** метод hello [MobileServiceClient][9].  У этого метода две перегрузки.

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

В следующий код, hello **метод mClient** является объектом ссылки tooyour MobileServiceClient.  первая перегрузка Hello используется где hello указаны имена класса и имя таблицы hello же Здравствуйте, и hello один служит hello краткое руководство:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Hello вторая перегрузка используется, когда имя таблицы hello отличается от имени класса hello: hello первым параметром является имя таблицы hello.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Запрос таблицы серверной части

Сначала получите ссылку на таблицу.  Выполните запрос на ссылку на таблицу hello.  Запрос сочетает в себе следующее:

* [предложение фильтра](#filtering) `.where()`;
* [предложение упорядочения](#sorting) `.orderBy()`;
* [предложение выбора поля](#selection) `.select()`;
* `.skip()` и `.top()` для [страничных результатов](#paging).

Hello предложений должны быть представлены на предшествующий порядок hello.

### <a name="filter"></a> Фильтрация результатов

Hello запроса выглядит следующим образом:

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Hello выше пример возвращает все результаты (вверх toohello максимальный размер страницы задается hello сервера).  Hello `.execute()` метод выполняет запрос hello hello серверную часть.  Hello запрос является преобразованный tooan [OData v3] [ 19] запрос перед серверной части мобильных приложений toohello передачи.  По получении серверной мобильные приложения hello преобразует hello запроса в инструкцию SQL перед его выполнением на экземпляр SQL Azure hello.  Здравствуйте, так как сетевой активности занимает некоторое время, `.execute()` возвращает [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Фильтрация возвращаемых данных

Привет, после выполнения запроса возвращает все элементы из hello **ToDoItem** таблицу, куда **завершения** равняется **false**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** таблицы мобильной службы toohello ссылка hello, созданную ранее.

Определение фильтра с помощью hello **где** вызова метода в ссылку на таблицу hello. Hello **где** следуют метод **поле** метод следуют метод, который определяет логический предикат hello. Возможные методы предиката: **eq** (равно), **ne** (не равно), **gt** (больше), **ge** (больше или равно), **lt** (меньше), **le** (меньше или равно). Эти методы позволяют сравнивать число и строку поля toospecific значения.

Фильтровать данные можно по датам. Hello следующие методы позволяют сравнивать hello дату полю или частей даты hello: **года**, **месяц**, **день**, **час**, **минуту**, и **второй**. Hello пример добавления фильтра для элементов которого *срок* равно 2013.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Hello следующие методы поддерживают сложные фильтры для полей строки: **startsWith**, **endsWith**, **concat**, **подстроки**, **indexOf**, **заменить**, **toLower**, **toUpper**, **trim**, и  **Длина**. Следующий пример фильтры для строки таблицы, где hello Hello *текст* столбцов начинается с «PRI0».

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

поддерживаются следующие методы операторов Hello числовых полей: **добавить**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, и **округления**. Следующий пример фильтры для строки таблицы, где hello Hello **длительность** является четным числом.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

Предикаты можно объединять с помощью логических методов **and**, **or** и **not**. Следующий пример Hello объединяет два предыдущих примерах hello.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Группирование и вложение логических операторов.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

Более подробные сведения и примеры фильтрации см. в разделе [изучение набора операторов hello hello Android клиентского запроса модели][20].

### <a name="sorting"></a>Сортировка возвращаемых данных

Hello следующий код возвращает все элементы из таблицы **ToDoItems** сортируются по возрастанию по hello *текст* поля. *mToDoTable* — hello toohello ссылочной серверной части таблицы, созданной ранее:

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

Здравствуйте, первый параметр hello **orderBy** метода является именем равно toohello строку hello поля на какие toosort. Второй параметр Hello использует hello **QueryOrder** toospecify перечисления ли toosort по возрастанию или убыванию.  Если фильтруется с использованием hello ***где*** метод, hello ***где*** метод должен вызываться перед hello ***orderBy*** метод.

### <a name="selection"></a>Выбор определенных столбцов

Hello следующий код показывает, как tooreturn все элементы из таблицы **ToDoItems**, но отображает только hello **завершения** и **текст** поля. **mToDoTable** hello toohello Справочник по серверной части таблицы, созданную ранее.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

Выберите функции Hello параметры toohello — имена строку hello hello таблицы столбцы, которые должны tooreturn.  Hello **выберите** метод должен toofollow методы, такие как **где** и **orderBy**. Затем можно вызывать такие методы разбивки на страницы, как **skip** и **top**.

### <a name="paging"></a>Возврат данных на страницах

Данные **всегда** возвращаются на страницах.  Максимальное число возвращаемых записей Hello устанавливается сервером hello.  Если клиент hello запрашивает несколько записей, hello server возвращает hello максимальное число записей.  По умолчанию hello максимальный размер страницы на сервере hello используется значение 50 записей.

Hello в первом примере показано, как tooselect hello первые пять элементы из таблицы. Hello запрос возвращает hello элементов из таблицы **ToDoItems**. **mToDoTable** — hello toohello ссылочной серверной части таблицы, созданной ранее:

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

Вот запрос пропускает hello первые пять элементов, которое затем возвращает hello пяти далее:

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

При желании tooget все записи в таблице, реализуют tooiterate кода всех страниц:

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

Запрос для всех записей с помощью этого метода создает как минимум два запроса toohello мобильные приложения, базы данных.

> [!TIP]
> Выбор размера правая страница hello — компромисс между использования памяти во время выполняется запрос hello, пропускная способность и задержка при получении данных hello полностью.  по умолчанию Hello (50 записей) подходит для всех устройств.  При эксплуатации исключительно на устройствах больше памяти, увеличьте вверх too500.  Обнаружено, увеличивающий размер страницы приветствия за пределами 500 записей результатов в неприемлемо задержки или проблемы большого объема памяти.

### <a name="chaining"></a>Практическое руководство. Объединение методов запросов

Hello методы, используемые в запросах к таблицам базы данных могут быть объединены. Цепочки запросов, методы позволяет tooselect определенными столбцами отфильтрованные строки, которые сортируются и разбиением на страницы. Можно создавать сложные логические фильтры.  Каждый метод запроса возвращает объект Query. tooend hello ряд методов и hello фактического выполнения запроса, вызов hello **выполнение** метод. Например:

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

Hello связанных данных запроса, который методы должны быть упорядочены следующим образом:

1. методы фильтрации (**где**);
2. методы сортировки (**orderBy**);
3. методы выборки (**выберите**);
4. методы разбиения по страницам (**skip** и **top**).

## <a name="binding"></a>Привязка данных toohello пользовательского интерфейса

Привязка данных состоит из трех компонентов:

* источник данных Hello
* макет экрана приветствия
* адаптер Hello, предложение WITH ties hello два друг с другом.

В нашем примере кода мы возвращаем hello данных из таблицы мобильных приложений SQL Azure hello **ToDoItem** в массив. Это действие типично для приложений для обработки данных.  Запросы к базе данных часто возвращают коллекцию строк, которые hello клиент получает в список или массив. В этом образце hello массива является hello источника данных.  Код Hello определяет макет экрана, который определяет представление hello hello данные, отображаемые на устройстве hello.  Hello двух связанных вместе с адаптер, который этот код — это расширение hello **ArrayAdapter&lt;ToDoItem&gt;**  класса.

#### <a name="layout"></a>Определение hello макета

Макет Hello определяется несколько фрагментов кода XML. Имея существующий макет, hello, следующий код представляет hello **ListView** мы хотим toopopulate с сервера данных.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

В предыдущих кода hello, hello *listitem* атрибут задает идентификатор hello hello макет для отдельной строки в списке hello. Этот код задает типа "флажок" и соответствующий текст и создается один раз для каждого элемента в списке hello. Этот макет не отображает hello **идентификатор** поля, а также более сложные макеты указать дополнительные поля в экран приветствия. Этот код находится в hello **row_list_to_do.xml** файла.

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <a name="adapter"></a>Определить адаптер hello
Так как источник данных hello наши представления — это массив **ToDoItem**, мы подкласс нашей адаптера из **ArrayAdapter&lt;ToDoItem&gt;**  класса. Этот подкласс создает представление для каждого **ToDoItem** с помощью hello **row_list_to_do** макета.  В приведенном коде определяется следующий класс, который является расширением hello hello **ArrayAdapter&lt;E&gt;**  класса:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Переопределить hello адаптеров **getView** метод. Например:

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

Мы создаем экземпляр этого класса в действии следующим образом:

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

Hello второй параметр toohello ToDoItemAdapter конструктор имеет toohello ссылки. Теперь мы допускающими hello **ListView** и назначить hello адаптера toohello **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Используйте hello адаптера tooBind toohello пользовательского интерфейса

Теперь вы находитесь готов toouse привязки данных. Hello следующий код показывает, как tooget элементов в таблице hello и заполняет hello локальный адаптер с hello вернул элементов.

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

Вызовите адаптера hello любое время изменить hello **ToDoItem** таблицы. Так как изменения выполняются на уровне отдельных записей, обрабатываться будут отдельные строки, а не коллекция. При вставке элемента вызовите hello **добавить** метод на hello адаптер; при удалении, вызовите hello **удалить** метод.

Полный пример можно найти в hello [проекта Android краткое руководство][21].

## <a name="inserting"></a>Вставка данных в серверной части hello

Создайте экземпляр элемента hello *ToDoItem* класса и задать его свойства.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

Затем с помощью **insert()** tooinsert объекта:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Hello возвращаемых соответствий сущности данных hello, вставленных в таблицу hello, идентификатор включается hello и любые другие значения (например hello `createdAt`, `updatedAt`, и `version` поля) на серверной hello.

Для таблиц мобильных приложений требуется столбец первичного ключа **id**. Этот столбец должен быть строкой. значение по умолчанию Hello hello идентификатор столбца — это GUID.  Можно указать другие уникальные значения, в том числе электронные адреса или имена пользователей. Если строковое значение идентификатора для вставленной записи не поддерживается, серверной hello создает новый идентификатор GUID.

Строковые значения идентификатора предоставляют hello следующие преимущества:

* Идентификаторы могут создаваться без создания базы данных toohello кругового пути.
* Записи, проще toomerge из различных таблиц или баз данных.
* Значения идентификаторов удобнее интегрировать с логикой приложения.

Строковые значения идентификатора **НЕОБХОДИМЫ** для поддержки автономной синхронизации.  Невозможно изменить идентификатор, когда он хранится в базе данных серверной части hello.

## <a name="updating"></a>Обновление данных в мобильном приложении

tooupdate данные в таблице, проходят hello новый объект toohello **update()** метод.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

В этом примере *элемент* строка tooa ссылку в hello *ToDoItem* таблицы, которое имело некоторые изменения, внесенные tooit.  Строка Hello с hello же **идентификатор** обновляется.

## <a name="deleting"></a>Удаление данных в мобильном приложении

Привет, следующий код показывает, как toodelete данные из таблицы, указав hello объекта данных.

```java
mToDoTable
    .delete(item);
```

Можно также удалить элемент, указав hello **идентификатор** поле toodelete строку hello.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Поиск определенного элемента по идентификатору

Поиск элемента с определенным **идентификатор** с hello **Просмотр()** метод:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Практическое руководство. Работа с нетипизированными данными

модель программирования нетипизированный Hello дает точный контроль над сериализации JSON.  Существуют некоторые распространенные сценарии, где вы можете toouse модель программирования нетипизированным. Например, если таблица базы данных содержит много столбцов, а требуется только подмножество столбцов hello tooreference.  типизированный модели Hello требуется toodefine все hello столбцов, определенных в серверной части мобильные приложения hello в класс данных.  Большинство вызовов API для доступа к данным hello toohello типизированного программирования вызовов. Hello основное отличие заключается в модели нетипизированный hello вызвать методы hello **MobileServiceJsonTable** объекта, а не hello **MobileServiceTable** объекта.

### <a name="json_instance"></a>Создание экземпляра нетипизированной таблицы

Аналогичные toohello типом модели, начать с получения ссылки на таблицу, но в данном случае это **MobileServicesJsonTable** объекта. Получить hello ссылку с помощью вызывающему Привет **getTable** метода для экземпляра hello клиента:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

После создания экземпляра hello **MobileServiceJsonTable**, он имеет практически hello же API доступна как с моделью программирования типизированный hello. В некоторых случаях hello методы принимают параметр нетипизированный вместо типизированных параметров.

### <a name="json_insert"></a>Вставка данных в нетипизированную таблицу
Здравствуйте, как следующий код показывает toodo инструкции insert. Hello первым шагом является toocreate [JsonObject][1], который является частью hello [gson] [ 3] библиотеки.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

Затем с помощью **insert()** tooinsert hello нетипизированный объект в таблицу hello.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Если вам требуется идентификатор hello tooget вставлены hello объекта, используйте hello **getAsJsonPrimitive()** метод.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Удаление данных из нетипизированной таблицы
Hello следующий код показывает, как toodelete экземпляра, в этом случае hello одного экземпляра **JsonObject** , созданных предыдущими hello *вставить* примере. Код Hello-hello так же, как hello типизированные регистр, но метод hello имеет другую подпись, поскольку она ссылается на **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

Вы также можете удалить экземпляр напрямую с помощью идентификатора:

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Получение всех строк из нетипизированной таблицы
Здравствуйте, как следующий код показывает tooretrieve всей таблицы. Так как вы используете таблицу JSON, можно получить только некоторых столбцов таблицы hello выборочно.

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

Hello одинаковых фильтрации, фильтрацию и разбиение по страницам методы, доступные для типизированных модели hello доступны для hello нетипизированный модели.

## <a name="offline-sync"></a>Реализация синхронизации в автономном режиме

Hello Azure Mobile приложения клиента SDK также реализует синхронизации данных в автономном режиме с помощью копирования данных сервера hello toostore базы данных SQLite локально.  Операции, выполняемые в автономной таблице toowork мобильного подключения не требуется.  Помогает автономной синхронизации в устойчивость и производительность за счет hello объекта более сложная логика разрешения конфликтов.  Hello Azure Mobile приложения клиента SDK реализует hello следующие атрибуты:

* Добавочная синхронизация. Загружаются только обновленные и новые записи. Это позволяет уменьшить потребление пропускной способности и памяти.
* Оптимистический параллелизм: Operations, считаются toosucceed.  Разрешение конфликтов, откладывается до обновления выполняются на сервере hello.
* Разрешение конфликтов: приветствия SDK обнаруживает, когда был сделан на сервере hello конфликтующее изменение и предоставляет подключает tooalert hello пользователя.
* Удаление с возможностью восстановления: Удаленных записей будут помечены как удаленные, позволяя другим tooupdate устройств их автономного кэша.

### <a name="initialize-offline-sync"></a>Инициализация синхронизации в автономном режиме

Каждая таблица вне сети должен быть определен в автономном кэше hello перед использованием.  Как правило определение таблицы выполняется сразу после создания hello hello клиента:

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Получить ссылку toohello автономной таблицы кэша

Для таблицы в Интернете используйте `.getTable()`,  а для автономной таблицы — `.getSyncTable()`:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Здравствуйте, все методы, доступные для документации таблиц (в том числе фильтрация, сортировка, разбиение по страницам, вставка данных, обновление данных и удаление данных) работают одинаково хорошо на подключенном и автономном таблиц.

### <a name="synchronize-hello-local-offline-cache"></a>Синхронизировать локальный кэш автономных hello

Синхронизация находится в элементе управления hello приложения.  Ниже приведен пример метода синхронизации.

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

Если указано имя запроса toohello `.pull(query, queryname)` метод, то добавочной синхронизации является tooreturn используется только записи, которые были созданы или изменены с момента последнего успешного завершения hello запросу.

### <a name="handle-conflicts-during-offline-synchronization"></a>Обработка конфликтов во время синхронизации в автономном режиме

Если конфликт происходит во время выполнения операции `.push()`, возникает исключение `MobileServiceConflictException`.   элемент, сформированных сервером Hello встроен в исключение hello и можно получить с `.getItem()` по исключению hello.  Настройка принудительной hello, вызывающему Привет следующих элементов в объекте MobileServiceSyncContext hello:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

Когда все конфликты, помечаются как надо, вызовите `.push()` снова tooresolve все hello конфликтов.

## <a name="custom-api"></a>Вызов настраиваемого интерфейса API

Пользовательский API позволяет toodefine пользовательских конечных точек, предоставляющих функциональные возможности сервера, которые не сопоставляются tooan вставки, обновления, удаления или операцию чтения. При использовании настраиваемого интерфейса API вы получаете больше возможностей для управления сообщениями, в том числе для чтения и установки заголовков HTTP-сообщений, а также определения форматов текста сообщений, отличных от JSON.

Из Android клиента, вызовите hello **invokeApi** toocall hello пользовательские API конечную точку метода. Hello следующем примере показано, как toocall конечную точку API именоваться **completeAll**, который возвращает класс коллекции с именем **MarkAllResult**.

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

Hello **invokeApi** метод будет вызван на приветствия клиента, который отправляет сообщение запроса toohello новый пользовательский интерфейс API. Hello результат, возвращаемый пользовательский API hello отображается в диалоговом окне сообщения, как ошибок. Другие версии **invokeApi** позволяют при необходимости отправлять в тексте запроса hello объекта, укажите метод hello HTTP и отправки параметров запроса с запросом hello. Кроме того, доступны нетипизированные версии **invokeApi** .

## <a name="authentication"></a>Добавить приложение tooyour проверки подлинности

Учебники по уже подробно описано как tooadd эти функции.

Служба приложений поддерживает [проверку подлинности пользователей приложения](app-service-mobile-android-get-started-users.md) с помощью разных внешних поставщиков удостоверений: Facebook, Google, учетной записи Майкрософт, Twitter и Azure Active Directory. Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей. Также можно использовать hello идентификаторов правил авторизации tooimplement прошедших проверку подлинности пользователей в серверной части.

Поддерживаются два потока аутентификации: **серверный** и **клиентский**. Hello server потока обеспечивает hello простой проверки подлинности, поскольку он основан на hello идентификаторов поставщиков веб-интерфейса.  Нет дополнительные пакеты SDK, tooimplement требуется аутентификация потока. Аутентификация потока не обеспечивает глубокую интеграцию в мобильном устройстве hello и рекомендуется только для проверки концепции сценариев.

поток клиентских Hello позволяет более глубокую интеграцию с возможности конкретного устройства, такие как единый вход как зависит от пакетов SDK, предоставляемые поставщиком удостоверений hello.  Например можно интегрировать hello Facebook SDK в мобильное приложение.  Мобильный клиент Hello меняет в приложение Facebook hello и подтверждает вашему входу, прежде чем переключаться задней tooyour мобильного приложения.

Четыре действия, необходимые tooenable проверки подлинности в приложении:

* Регистрация приложения для аутентификации в поставщике удостоверений.
* Настройка серверной части службы приложений.
* Запретить пользователям tooauthenticated таблиц разрешения только на hello серверной службы приложений.
* Добавьте приложение tooyour код проверки подлинности.

Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей. Можно также использовать hello SID toomodify прошедший проверку пользователь запросов.  Дополнительные сведения см. в статье [приступить к работе с проверкой подлинности] и hello документации HOWTO SDK сервера.

### <a name="caching"></a>Серверный поток проверки подлинности

Hello кода ниже выполняется запуск процесса входа в систему сервера потока с помощью поставщика Google hello.  Дополнительная настройка не требуется из-за требований безопасности hello для поставщика Google hello:

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

Кроме того добавьте следующий метод toohello основной класс действие hello:

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

Hello `GOOGLE_LOGIN_REQUEST_CODE` определен в с главным действие используется для hello `login()` метод и в пределах hello `onActivityResult()` метод.  Можно выбрать любой уникальный номер, при условии, что hello этим же номером используется внутри hello `login()` метод и hello `onActivityResult()` метод.  Если абстрактный hello клиентского кода в адаптер службы (как показано выше), следует вызвать соответствующие методы hello для hello службы адаптера.

Необходимо также tooconfigure hello проекта для customtabs.  Сначала укажите URL-адрес перенаправления.  Добавьте следующий фрагмент слишком hello`AndroidManifest.xml`:

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

Добавить hello **redirectUriScheme** toohello `build.gradle` файл для приложения:

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

Наконец, добавьте `com.android.support:customtabs:23.0.1` toohello список зависимостей в hello `build.gradle` файла:

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

Получить идентификатор hello hello вошедшего в систему пользователя из **MobileServiceUser** с помощью hello **getUserId** метод. Пример, как toocall toouse фьючерсов hello входа асинхронные интерфейсы API, см. [приступить к работе с проверкой подлинности].

> [!WARNING]
> Hello упомянутые схема URL-адресов с учетом регистра.  Убедитесь, что во всех вхождениях `{url_scheme_of_you_app}` используется один и тот же регистр.

### <a name="caching"></a>Кэширование токенов проверки подлинности

Кэширование маркеров проверки подлинности требует hello toostore идентификатор пользователя и маркер проверки подлинности локально на устройстве hello. Hello при следующем запуске приложения hello, вы проверяете hello кэша, и если эти значения, можно пропустить журнала hello в процедуре и повторно заполнить hello клиента с этими данными. Однако конфиденциальные данные, и должны быть сохранены, шифруются в целях безопасности в случае, если телефон hello кражи.  Вы увидите полный пример, как маркеры проверки подлинности toocache в [кэшировать раздел токены проверки подлинности][7].

При попытке toouse просроченного маркера, вы получаете *401 несанкционированный* ответа. Ошибки аутентификации можно обрабатывать с помощью фильтров.  Фильтры перехватывать запросы toohello серверной службы приложений. Код фильтра Hello проверяет ответ 401 hello, запускает hello процесса входа в и возобновляет hello запроса, создавшего hello 401.

### <a name="refresh"></a>Использование токенов обновления

Hello токен, возвращенный Azure приложение службы аутентификации и авторизации имеет время жизни определенных один час.  По истечении этого периода необходимо принудительную проверку подлинности пользователя hello.  В случае проверки подлинности службы приложения Azure с помощью долгоживущие маркер, который вы получили через проверку подлинности клиента потока, а затем можно принудительную проверку подлинности и авторизации с помощью hello тот же токен.  В процессе создается другой токен службы приложений Azure с новым временем существования.

Можно также зарегистрировать toouse hello поставщика токенов обновления.  Токен обновления не всегда доступен.  В этом случае необходимо выполнить дополнительную настройку:

* Для **Azure Active Directory**, настройте секрет клиента для hello приложения Azure Active Directory.  Укажите секрет клиента hello в службе приложений Azure hello при настройке проверки подлинности Azure Active Directory.  При вызове метода `.login()` передайте `response_type=code id_token` как параметр:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Для **Google**, передайте hello `access_type=offline` как параметр:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Для **учетную запись Майкрософт**выберите hello `wl.offline_access` области.

Вызовите toorefresh токене `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

Рекомендуется создайте фильтр, который обнаруживает 401 ответа от сервера hello и пытается токена пользователя toorefresh hello.

## <a name="log-in-with-client-flow-authentication"></a>Вход в систему с использованием клиентского потока проверки подлинности

Общая процедура Hello вход с помощью проверки подлинности клиента поток выглядит следующим образом:

* Настройка функции проверки подлинности и авторизации в службе приложений Azure, как и при серверном потоке проверки подлинности.
* Интеграция поставщика проверки подлинности hello пакета SDK для проверки подлинности tooproduce маркер доступа.
* Вызовите hello `.login()` метод следующим образом:

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

Замените hello `onSuccess()` метод с независимо от кода, которые хотите toouse на успешного входа.  Hello `{provider}` строка является действительным поставщиком: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, или **twitter**.  При реализации пользовательской проверки подлинности можно также использовать тег поставщика hello нестандартной проверки подлинности.

### <a name="adal"></a>Проверять подлинность пользователей с hello библиотеку проверки подлинности Active Directory (ADAL)

Пользователи toosign hello библиотеку проверки подлинности Active Directory (ADAL) можно использовать в приложении с помощью Azure Active Directory. Использование имени входа потока клиента часто является более предпочтительным, чем toousing hello `loginAsync()` методы, как он обеспечивает более естественным согласованность UX и обеспечивает дополнительные настройки.

1. Настройте внутренний сервер мобильных приложений для входа в AAD, следующие hello [как tooconfigure приложения службы для имени входа Active Directory] [ 22] учебника. Убедитесь, что необязательный шаг toocomplete hello регистрации собственного клиентского приложения.
2. Установка ADAL, изменив вашей hello tooinclude файл build.gradle следующие определения:

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. Добавьте hello следующие приложения tooyour кода, благодаря чему hello после замены:

* Замените **вставки ЦЕНТРА здесь** hello имя клиента hello, в котором подготовлено приложения. Hello формат должен быть https://login.microsoftonline.com/contoso.onmicrosoft.com.
* Замените **вставки РЕСУРСОВ-идентификатор здесь** с Идентификатором hello клиент для мобильного приложения серверной части. Можно получить идентификатор клиента hello hello **Дополнительно** в разделе **параметры Azure Active Directory** hello портала.
* Замените **вставки КЛИЕНТА-идентификатор здесь** с Идентификатором клиента hello, скопированные из собственного клиентского приложения hello.
* Замените **вставки ПЕРЕНАПРАВЛЕНИЯ-URI здесь** с веб-узла */.auth/login/done* конечную точку, используя hello схему HTTPS. Это значение должно быть примерно слишком*https://contoso.azurewebsites.net/.auth/login/done*.

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <a name="filters"></a>Настройка hello соединения клиент-сервер

Hello клиентского соединения — это обычно базовый HTTP-соединение с помощью hello базовый HTTP библиотеки, поставляемых вместе с hello пакета SDK для Android.  Существует несколько причин, почему нужно toochange:

* Вы хотите toouse альтернативный время ожидания tooadjust HTTP библиотеки.
* Вы хотите tooprovide индикатор хода выполнения.
* Вы хотите tooadd функциональность toosupport API пользовательского заголовка.
* Вы хотите toointercept сообщения об ошибке, чтобы можно было реализовать повторной проверки подлинности.
* Вы хотите toolog серверной запросов tooan analytics службы.

### <a name="using-an-alternate-http-library"></a>Использование альтернативной библиотеки HTTP

Вызовите hello `.setAndroidHttpClientFactory()` метод сразу после создания клиента справочной информации.  Например tooset hello подключения too60 ожидания (а не по умолчанию hello 10 секунд):

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a>Реализация фильтра хода выполнения

Реализовав атрибут `ServiceFilter`, вы сможете настроить перехват каждого запроса.  Например следующие hello обновляет предварительно созданной индикатор:

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

Можно присоединить этот клиент toohello фильтра следующим образом:

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>Настройка заголовков запросов

Используйте следующие hello `ServiceFilter` и присоединения hello фильтра hello так же, как hello `ProgressFilter`:

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <a name="conversions"></a>Настройка автоматической сериализации

Можно указать стратегию преобразования, которая применяет tooevery столбца с помощью hello [gson] [ 3] API. Hello Android клиентская библиотека использует [gson] [ 3] фоновом hello tooserialize Java объектов tooJSON данные перед отправкой данных hello tooAzure службы приложений.  Hello следующий код использует hello **setFieldNamingStrategy()** метод tooset hello стратегии. В этом примере приведет к удалению hello исходного символа («m»), а затем строчные hello следующего символа, для каждого имени поля. Например, он преобразует "mId" в "id".  Реализуйте необходимость преобразования стратегии tooreduce hello `SerializedName()` заметок на большинство полей.

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

Этот код должен выполняться перед созданием ссылку мобильного клиента с помощью hello **MobileServiceClient**.

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[приступить к работе с проверкой подлинности]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
