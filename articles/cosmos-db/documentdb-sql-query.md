---
title: "aaaSQL запрашивает Azure Cosmos DB DocumentDB API | Документы Microsoft"
description: "Сведения о синтаксисе SQL, основных понятиях баз данных и запросах SQL для Azure Cosmos DB. SQL можно использовать в качестве языка запросов JSON в Azure Cosmos DB."
keywords: "синтаксис SQL, запрос SQL, язык запросов JSON, понятия баз данных и запросы SQL, статистические функции"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>SQL-запросы для API DocumentDB в Azure Cosmos DB
Служба Microsoft Azure Cosmos DB поддерживает запросы документов с помощью SQL (язык структурированных запросов) как языка запросов JSON. Cosmos DB действительно не имеет схемы. Посредством его обязательств toohello JSON модели данных непосредственно в компонент database engine hello он обеспечивает автоматическое индексирование документов JSON не требуя явной схемы или создания вторичных индексов. 

При проектировании Cosmos DB hello язык запросов, мы должны были в уме две цели:

* Вместо изобретать новый язык запросов JSON, нам необходимо было toosupport SQL. SQL является одним из языков запросов наиболее знакомых и популярных hello. SQL в Cosmos DB предоставляет формальную модель программирования для выполнения многофункциональных запросов к документам JSON.
* Как JSON документа база данных может выполнять JavaScript непосредственно в ядре СУБД hello нам необходимо было модель программирования toouse JavaScript как hello foundation нашей языка запросов. Hello DocumentDB API SQL заключена в системе типов языка JavaScript, вычисление выражений и вызова функции. Это, в свою очередь, обеспечивает естественную модель программирования для реляционных проекций, иерархической навигации по документам JSON, внутренних соединений, пространственных данных и вызовов определяемых пользователем функций (UDF), написанных полностью на JavaScript, наряду с другими особенностями. 

Мы надеемся, что эти возможности являются трения hello ключа tooreducing между приложения hello и hello базы данных и особенно важны для повышения производительности разработчиков.

Мы рекомендуем Приступая к работе, посмотрите следующие видео, где Aravind Ramachandran показывает Cosmos DB возможности выполнения запросов, hello и, посетив нашей [площадку запросов](http://www.documentdb.com/sql/demo), где можно опробовать Cosmos DB и выполнения запросов SQL к наш набор данных.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

После этого вернитесь toothis статьи, где мы начнем с учебник запроса SQL, в котором рассматриваются некоторые простые документы JSON и команды SQL.

## <a id="GettingStarted"></a>Приступая к работе с командами SQL в Cosmos DB
toosee Cosmos SQL базы данных на работы, давайте начинаются с несколько простых документов JSON и показывает, как некоторые простые запросы. Рассмотрим эти два JSON документа о двух семьях. С помощью Cosmos DB не должны toocreate любой схемы или вторичных индексов явным образом. Мы просто tooinsert hello JSON документы tooa Cosmos DB коллекции и впоследствии запросов. Здесь у нас есть простая JSON документов для семейства Андерсен hello, hello родительских, дочерних (и их животных), адрес и сведения о регистрации. Hello документ имеет строки, числа, логические значения, массивы и вложенных свойств. 

**Документ**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

Это второй документ с одним небольшим различием: `givenName` и `familyName` используются вместо `firstName` и `lastName`.

**Документ**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Теперь попробуем несколько запросов от этого toounderstand данных некоторые hello ключевые аспекты DocumentDB API SQL. Например, hello следующий запрос возвращает документы hello которых соответствует поле id hello `AndersenFamily`. Так как она является `SELECT *`, hello выходные данные запроса hello: hello полный документ JSON:

**Запрос**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Результаты**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


Теперь рассмотрим случай hello, где мы должны tooreformat hello выходных данных JSON в другой форме. Этот запрос, проекты новый JSON объекта с двумя выбранные поля Name и City, когда hello адрес Город hello одинаковые имена, как состояние hello. В этом случае совпадут NY и NY.

**Запрос**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**Результаты**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


Hello следующий запрос возвращает все имена заданным hello дочерних элементов в hello семейства, идентификатор которого соответствует `WakefieldFamily` упорядоченные по hello города проживания.

**Запрос**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**Результаты**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


Мы хотели бы tooa внимания toodraw мало внимания аспектов hello Cosmos DB языка hello примеров, которые мы видели в данный момент запросов:  

* В API DocumentDB язык SQL работает со значениями JSON, т. е. имеет дело с сущностями в виде деревьев, а не со строками и столбцами. Таким образом, hello языка позволяет ссылаться toonodes дерева hello любой произвольной глубины, таких как `Node1.Node2.Node3…..Nodem`, аналогичные toorelational SQL обращения toohello две ссылки на компонент из `<table>.<column>`.   
* Hello структуру языка запрос будет работать с данными без схемы. Таким образом, динамически hello границы toobe требованиям системы типа. Hello того же выражения может дать различных типов в различных документах. Hello результатом запроса является допустимым значением JSON, но не гарантируется, что toobe фиксированной схемы.  
* Cosmos DB поддерживает только документы, строго соответствующие JSON. Это означает, что система типов hello и выражения являются ограниченными toodeal только с типами JSON. См. toohello [спецификации JSON](http://www.json.org/) для получения дополнительных сведений.  
* Коллекция Cosmos DB является контейнером документов JSON, не имеющим схемы. Hello связи в данных сущности в одной и нескольких документов в коллекции регистрируются неявно путем включения, а не первичного ключа и внешнего ключа связи. Это важный аспект стоит обратить внимание в свете hello соединения внутри документа, описанных далее в этой статье.

## <a id="Indexing"></a>Индексирование в Cosmos DB
Прежде чем мы перейдем hello синтаксис DocumentDB API SQL, стоит изучение hello индексирования конструктора в Cosmos DB. 

Hello индексов базы данных предназначено tooserve запросов в различных форм и фигур с потреблением ресурсов минимальное (например, ЦП и ввода вывода) то же время предоставляя высокой пропускной способности и низкой задержкой. Часто Выбор hello hello правой индекса для запросов к базе данных требует много планирования и экспериментов. Этот подход возникают сложности для баз данных без схемы, где hello данные не соответствуют tooa strict схемы и развития быстро. 

Таким образом когда мы разработали hello Cosmos DB индексирования подсистемы, задается hello следующих целей:

* Индексировать документы без необходимости схемы: hello индексирования подсистемы требует информации о схеме, и не делать никаких предположений о схеме hello документов. 
* Поддержка для эффективных и многофункциональных иерархических и реляционных запросов: hello индексы поддерживают язык запросов Cosmos DB hello эффективно, включая поддержку иерархических и реляционные проекции.
* Поддержка согласованное запросов на длительной объем операций записи: для высокого уровня записи пропускная способность рабочих нагрузок с согласованной запросами hello индекс обновляется постепенно, эффективно и через Интернет в лицевой стороны hello тома длительной операции записи. Обновление согласованное индекса Hello является ключевым tooserve hello запросы на уровне согласованности hello в какой hello пользователя настроен hello документа службы.
* Поддержка мультитенантности: задано модель на основе резервирования hello регулирование ресурсов клиентов, в пределах бюджета hello системных ресурсов (ЦП, памяти и операций ввода вывода в секунду) в реплике, выделенных выполняется обновление индекса. 
* Эффективность хранения: для экономической эффективности hello хранилище на диске издержки hello индекса является связанной и прогнозируемого. Это важно, поскольку Cosmos DB допускает hello разработчика toomake основанный на стоимости компромисса между затраты на индекса производительности запроса toohello отношения.  

См. toohello [примеров Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) в MSDN для образцов, показывающий, каким образом tooconfigure hello политики индексирования для коллекции. Теперь давайте hello Дополнительные сведения о hello синтаксис SQL базы данных Azure Cosmos.

## <a id="Basics"></a>Основы использования SQL-запросов Azure Cosmos DB
Каждый запрос состоит из предложения SELECT и необязательных предложений FROM и WHERE в соответствии со стандартами ANSI-SQL. Как правило для каждого запроса перечисляется hello источника в предложении FROM hello. После этого hello фильтрацию в предложение WHERE применяется на tooretrieve источника hello hello подмножество документов JSON. Наконец, используется предложение SELECT hello tooproject hello запрошенный список выбора значения JSON в hello.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>Предложение FROM
Hello `FROM <from_specification>` предложение является необязательным, если источник hello отфильтрованы или спроецировать позже в запросе hello. Hello это предложение предназначено источника данных toospecify hello, после которого hello запрос должен работать. Часто вся коллекция hello является источником hello, но один вместо этого указать подмножество hello коллекции. 

Запрос, например `SELECT * FROM Families` указывает, hello всего семейства коллекция источника hello через какие tooenumerate. Специальный идентификатор КОРНЕВОГО может представлять коллекцию hello используется toorepresent вместо использования имени коллекции hello. Hello следующий список содержит hello правила, которые применяются для каждого запроса.

* Hello коллекции может быть присвоен псевдоним, таких как `SELECT f.id FROM Families AS f` или просто `SELECT f.id FROM Families f`. Здесь `f` является эквивалентом hello `Families`. `AS`является идентификатором hello tooalias Необязательное ключевое слово.
* Один раз псевдоним hello исходный источник не может быть привязана. Например `SELECT Families.id FROM Families f` является синтаксически недопустимым, поскольку не удается разрешить больше hello идентификатор «Семейства».
* Все свойства, которые требуется ссылка на toobe должно быть полным. В отсутствие hello схемы строгого соответствия, это принудительная tooavoid неоднозначных привязок. Таким образом `SELECT id FROM Families f` является синтаксически недопустимый с момента hello свойство `id` не привязан.

### <a name="subdocuments"></a>Вложенные документы
Источник Hello также может быть более ограниченной tooa ограниченный набор. Для экземпляра tooenumerating поддерево в каждом документе hello subroot затем станут hello источника, как показано в следующий пример hello:

**Запрос**

    SELECT * 
    FROM Families.children

**Результаты**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

Хотя hello в приведенном выше примере массив используется как источник hello, объект также может использоваться в качестве источника hello, которым элементы, отображаемые в следующий пример hello: для включения в результат hello считается любым допустимым значением JSON (не определено), можно найти в источнике hello запрос Hello. Если у вас нет некоторые семейства `address.state` значения, они исключаются из результата запроса hello.

**Запрос**

    SELECT * 
    FROM Families.address.state

**Результаты**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>Предложение WHERE
Здравствуйте, предложение WHERE (**`WHERE <filter_condition>`**) является необязательным. Он указывает, что hello условия, которым документы JSON hello hello источника должны удовлетворять в порядке toobe включается как часть результата hello. Любой документ JSON должно быть указано hello условия слишком «true» toobe рассматриваться в качестве результата hello. Здравствуйте, ГДЕ используется предложение hello уровне индекса в порядке toodetermine hello абсолютный наименьшее подмножество исходных документов, которые могут быть частью результирующего hello. 

Hello следующий запрос запрашивает документы, содержащие имя свойства, значение которого является `AndersenFamily`. Любой другой документ, у которого нет свойства name, или где hello значение не соответствует `AndersenFamily` исключается. 

**Запрос**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Результаты**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


Hello предыдущем примере показан запрос простого равенства. SQL для API DocumentDB также поддерживает различные скалярные выражения. наиболее часто используемые Hello — это двоичное кодирование и унарные выражения. Ссылки на свойства из объекта JSON источника hello также являются допустимыми выражениями. 

Следующие бинарные операторы Hello в настоящее время поддерживаются и могут использоваться в запросах, как показано в следующих примерах hello:  

<table>
<tr>
<td>Арифметические</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>Побитовые</td>    
<td>|, &, ^, <<, >>, >>> (нулевой сдвиг вправо)</td>
</tr>
<tr>
<td>Логические</td>
<td>AND, OR, NOT</td>
</tr>
<tr>
<td>Сравнение</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>Строка</td>    
<td>|| (конкатенация)</td>
</tr>
</table>  


Давайте рассмотрим примеры запросов с двоичными операторами.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


Здравствуйте, унарные операторы +,-, ~ не поддерживаются также и может использоваться в запросах, как показано в следующий пример hello:

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



В дополнение к этому toobinary и унарные операторы, ссылки на свойства также можно использовать. Например `SELECT * FROM Families f WHERE f.isRegistered` возвращает hello документ JSON, содержащий свойства hello `isRegistered` которого значение свойства hello равно toohello JSON `true` значение. Любые другие значения (false, значение null, определено, `<number>`, `<string>`, `<object>`, `<array>`и т.д.) ведет toohello исходного документа, исключенного из результата hello. 

### <a name="equality-and-comparison-operators"></a>Операторы равенства и сравнения
Hello приведенной ниже таблице показано hello результат сравнения на равенство в DocumentDB API SQL любые два типа JSON.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>Оператор</strong>
         </td>
         <td valign="top">
            <strong>Не определено</strong>
         </td>
         <td valign="top">
            <strong>NULL</strong>
         </td>
         <td valign="top">
            <strong>Логическое значение</strong>
         </td>
         <td valign="top">
            <strong>Число</strong>
         </td>
         <td valign="top">
            <strong>Строка</strong>
         </td>
         <td valign="top">
            <strong>Объект</strong>
         </td>
         <td valign="top">
            <strong>Массив</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Не определено<strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>NULL<strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
            <strong>Допустимо</strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Логическое значение<strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
            <strong>Допустимо</strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Число<strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
            <strong>Допустимо</strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Строка<strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
            <strong>Допустимо</strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Объект<strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
            <strong>Допустимо</strong>
         </td>
         <td valign="top">
Не определено </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Массив<strong>
         </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
Не определено </td>
         <td valign="top">
            <strong>Допустимо</strong>
         </td>
      </tr>
   </tbody>
</table>

Для других операторов сравнения, например, >, > =,! =, < и < =, hello применяются следующие правила:   

* Сравнение типов приводит к неопределенному результату.
* Сравнение двух объектов или двух массивов приводит к неопределенному результату.   

Если результат hello hello скалярное выражение в фильтре hello не определен, соответствующего документа hello бы не будут включены в результат hello, так как не определено не соответствуют логически слишком «true».

### <a name="between-keyword"></a>Ключевое слово BETWEEN (МЕЖДУ)
Также можно использовать hello BETWEEN ключевое слово tooexpress запросами диапазоны значений как в ANSI SQL. BETWEEN может использоваться для строк или чисел.

Например этот запрос возвращает все семейства документы, в которых hello оценка первый дочерний элемент — от 1 до 5 (включительно для обоих). 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

В отличие от в ANSI SQL, можно также использовать предложение BETWEEN hello в предложении FROM hello как следующий пример hello.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

Для ускорения времени выполнения запроса помните toocreate политику индексации, которая использует тип диапазона индекса для любого числового свойства и пути, которые фильтруются в предложении BETWEEN hello. 

Hello основное различие между использованием BETWEEN в DocumentDB API и ANSI SQL — что можно выразить запросов в диапазоне от свойства смешанных типов — например, возможно, «уровень» быть числом (5) в некоторых документах и строк в других («grade4»). Таким образом как на языке JavaScript, сравнение двух различных типов результатов в «undefined» и hello документа будут пропущены.

### <a name="logical-and-or-and-not-operators"></a>Логические операторы (AND, OR или NOT)
Логические операторы работают над значениями типа Boolean. в hello в следующей таблице показаны Hello логические таблицы истинности этих операторов.

| ИЛИ | Истина | Ложь | Не определено |
| --- | --- | --- | --- |
| Истина |Истина |Истина |Истина |
| Ложь |Истина |Ложь |Не определено |
| Не определено |Истина |Не определено |Не определено |

| И | Истина | Ложь | Не определено |
| --- | --- | --- | --- |
| Истина |Истина |Ложь |Не определено |
| Ложь |Ложь |Ложь |Ложь |
| Не определено |Не определено |Ложь |Не определено |

| НЕ |  |
| --- | --- |
| Истина |Ложь |
| Ложь |Истина |
| Не определено |Не определено |

### <a name="in-keyword"></a>Ключевое слово IN
Ключевое слово Hello в может быть используется toocheck, является ли указанное значение совпадает с любым значением в виде списка. Например этот запрос возвращает все документы семейства идентификатор hello где «WakefieldFamily» или «AndersenFamily». 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

Этот пример возвращает все документы, где hello состояния — это любые hello указанного значения.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>Операторы Ternary (?) и Coalesce (??)
операторы Hello троичный и Coalesce может быть используется toobuild условные выражения, примерно toopopular программирования языками, такими как C# и JavaScript. 

оператор Hello троичный (?) могут быть очень удобны при создании новых свойств JSON hello полет. Например теперь можно написать запросы tooclassify hello класс уровни в удобной для чтения форме, как и для новичков/промежуточных и дополнительно как показано ниже.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

Также можно вложить hello вызовов toohello оператором, например в запросе hello ниже.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

Как с другими операторами запроса, если hello упоминаемого в условном выражении hello отсутствуют свойства в любой документ или типы hello сравниваемых различны, затем эти документы исключаются в результатах запроса hello.

Hello Coalesce (?) оператор может быть (так называемый используется tooefficiently Проверьте наличие hello свойства (или его определения) в документе. Это удобно при запросах к частично структурированным данным или данным разных типов. Например этот запрос возвращает hello «lastName» при его наличии или hello «Фамилия», если он отсутствует.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>Доступ к свойству, заключенному в кавычки
Также можно использовать свойства, с помощью оператора hello указанное свойство `[]`. Например, выражение `SELECT c.grade` and `SELECT c["grade"]` являются эквивалентными. Этот синтаксис полезно в тех случаях, когда требуется свойство, которое содержит пробелы, специальные символы, или происходит точно такое же имя, как ключевое слово SQL или зарезервированное слово hello tooshare tooescape.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>Предложение SELECT
предложение SELECT Hello (**`SELECT <select_list>`**) является обязательным и указывает, какие значения извлекаются из запроса hello так же, как в ANSI SQL. подмножество Hello, фильтруется на основе hello исходные документы передаются на этап отображения hello, где указан hello извлекаются значения JSON и создается новый объект JSON, для каждой входной параметр, переданный в него. 

Hello в следующем примере показан типичный запрос SELECT. 

**Запрос**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Результаты**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>Вложенные свойства
В следующем примере hello, мы проецирование двух вложенных свойств `f.address.state` и `f.address.city`.

**Запрос**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Результаты**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


Проекция также поддерживает выражения JSON, как показано в следующий пример hello:

**Запрос**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Результаты**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


Давайте рассмотрим роль hello `$1` здесь. Hello `SELECT` предложение должен toocreate объекта JSON и без ключа предоставляется, мы используем неявный аргумент имена переменных, начиная с `$1`. Например, этот запрос возвращает две неявные переменные аргументов, помеченные как `$1` and `$2`.

**Запрос**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Результаты**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>Псевдонимы
Теперь давайте расширить hello приведенном выше примере с помощью явных псевдонимов значений. КАК ключевое слово, используемое для присвоения псевдонимов hello. Это необязательно, как показано во время проецирования hello второе значение как `NameInfo`. 

Если запрос содержит два свойства с hello таким же именем, совмещение имен должно быть используется toorename одно или оба hello свойства, чтобы они отличаются в hello проецируется результат.

**Запрос**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Результаты**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>Скалярные выражения
Кроме ссылается tooproperty, предложение SELECT hello также поддерживает скалярные выражения, такие как константы, арифметических выражений, логические выражения и т. д. Например, вот простой запрос "Hello World".

**Запрос**

    SELECT "Hello World"

**Результаты**

    [{
      "$1": "Hello World"
    }]


Вот более сложный пример с использованием скалярного выражения:

**Запрос**

    SELECT ((2 + 11 % 7)-2)/3    

**Результаты**

    [{
      "$1": 1.33333
    }]


В следующем примере hello результат hello hello скалярное выражение является логическим.

**Запрос**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**Результаты**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>Создание объектов и массивов
Еще одной ключевой возможностью языка SQL для API DocumentDB является создание объектов и массивов. В предыдущем примере hello Обратите внимание, что мы создали новый объект JSON. Аналогично один можно также создать массивы как показано в следующих примерах hello:

**Запрос**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**Результаты**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>Ключевое слово VALUE
Hello **значение** ключевое слово предоставляет значение JSON tooreturn способом. Например, запрос hello, показано ниже hello возвращает скалярное `"Hello World"` вместо `{$1: "Hello World"}`.

**Запрос**

    SELECT VALUE "Hello World"

**Результаты**

    [
      "Hello World"
    ]


Hello следующий запрос возвращает значение JSON hello без hello `"address"` метки в результатах hello.

**Запрос**

    SELECT VALUE f.address
    FROM Families f    

**Результаты**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

Hello следующий пример расширяет это tooshow как простые значения в JSON tooreturn (hello конечный уровень дерева hello JSON). 

**Запрос**

    SELECT VALUE f.address.state
    FROM Families f    

**Результат**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>Оператор *
Hello специальный оператор (*) — поддерживаемые tooproject hello документ как-является. При использовании, он должен быть hello проецировать только поля. Хотя запрос наподобие `SELECT * FROM Families f` допустим, `SELECT VALUE * FROM Families f ` и `SELECT *, f.id FROM Families f ` недопустимы.

**Запрос**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Результаты**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>Оператор TOP
Ключевое слово TOP Hello может быть использован toolimit hello количество значения из запроса. Если предложение TOP используется в сочетании с предложением ORDER BY hello, hello результирующего набора является ограниченной toohello первое число N последовательных значений; в противном случае возвращается первое число N hello результатов в неопределенном порядке. Рекомендуется в инструкции SELECT всегда используйте предложение ORDER BY с предложением TOP hello. Это является единственным способом hello toopredictably указывают, какие строки будут изменены предложением TOP. 

**Запрос**

    SELECT TOP 1 * 
    FROM Families f 

**Результат**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

TOP можно использовать с постоянным значением (как показано выше) или с переменным значением посредством параметризованных запросов. Дополнительные сведения см. в описании параметризованных запросов ниже.

### <a id="Aggregates"></a>Статистические функции
Можно также выполнить агрегатов в hello `SELECT` предложения. Статистические функции выполняют вычисление на наборе значений и возвращают одиночное значение. Например, hello следующий запрос возвращает число hello семейства документов в коллекции hello.

**Запрос**

    SELECT COUNT(1) 
    FROM Families f 

**Результаты**

    [{
        "$1": 2
    }]

Можно также вернуть hello скалярное значение hello статистические с помощью hello `VALUE` ключевое слово. Например, hello следующий запрос возвращает количество значений в hello как одно число:

**Запрос**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**Результаты**

    [ 2 ]

Также можно выполнять статистические вычисления в сочетании с фильтрами. Например, hello следующий запрос возвращает hello число документов с адресом hello в hello штата Вашингтон, США.

**Запрос**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**Результаты**

    [ 1 ]

Hello Следующая таблица показывает hello список статистических функций, поддерживаемых в DocumentDB API. `SUM`и `AVG` выполняются над числовыми значениями, тогда как `COUNT`, `MIN` и `MAX` можно выполнять над числами, строками, логическими значениями и значениями NULL. 

| Использование | Описание |
|-------|-------------|
| COUNT | Возвращает hello количество элементов в выражении hello. |
| SUM   | Возвращает hello сумму всех значений hello в выражении hello. |
| MIN   | Возвращает hello минимальное значение в выражении hello. |
| MAX   | Возвращает hello максимальное значение в выражении hello. |
| AVG   | Возвращает hello среднее значений hello в выражении hello. |

Статистические функции также могут быть выполнены над hello результатов итерации массива. Дополнительные сведения см. в разделе [Итерация](#Iteration).

> [!NOTE]
> При с помощью hello Explorer запроса портал Azure, обратите внимание, что статистических запросов может возвращать hello частично сводных результатов по запроса страницы. Hello SDK создает одно совокупное значение на всех страницах. 
> 
> В порядке tooperform статистических запросов с помощью кода, .NET SDK 1.12.0, пакет SDK для .NET Core 1.1.0 или Java SDK 1.9.5.\ или более поздней версии.    
>

## <a id="OrderByClause"></a>Предложение ORDER BY
Как и в ANSI-SQL, вы можете включить в запрос необязательное предложение ORDER BY. Hello предложение может включать необязательный ASC или DESC toospecify hello порядок аргументов получить результаты.

Например ниже приведен запрос, получающий семейств в порядке название резидентного города hello.

**Запрос**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**Результаты**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

А вот запрос, получающий семейств в порядке, Дата создания, который хранится как число, представляющее hello времени начала эпохи, т. е., затраченного времени с 1 января 1970 года в секундах.

**Запрос**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**Результаты**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>Дополнительные понятия базы данных и SQL-запросов

### <a id="Iteration"></a>Итерация
Было добавлено новую конструкцию hello **в** ключевое слово в DocumentDB API SQL tooprovide поддержку перебора массивов JSON. Источник Hello FROM обеспечивает поддержку для итерации. Начнем с hello в следующем примере:

**Запрос**

    SELECT * 
    FROM Families.children

**Результаты**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

Теперь давайте рассмотрим другой запрос, который выполняет итерацию по дочерним элементам в коллекции hello. Обратите внимание, hello разница в выходном массиве hello. В этом примере разбивает `children` и сводит результаты hello в один массив.  

**Запрос**

    SELECT * 
    FROM c IN Families.children

**Результаты**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

Это может быть дополнительно используется toofilter на каждой отдельной операции hello массива, как показано в следующий пример hello:

**Запрос**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**Результаты**  

    [{
      "givenName": "Lisa"
    }]

Можно также выполнить статистическую результирующим hello итерации массива. Например hello следующий запрос подсчитывает hello количество дочерних элементов среди всех семейств.

**Запрос**

    SELECT COUNT(child) 
    FROM child IN Families.children

**Результаты**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>Соединения
В реляционной базе данных важно toojoin необходимость hello по таблицам. Он является hello логических toodesigning следствие нормализовать схемы. Противоположные toothis, DocumentDB API связана с моделью hello денормализованные данные без схемы документов. Это hello логический эквивалент a «самосоединение».

синтаксис Hello, поддерживающий язык hello является СОЕДИНЕНИЕМ СОЕДИНЕНИЯ < from_source2 > < from_source1 >... JOIN <from_sourceN>. В целом будет возвращаться набор **N**-кортежей (кортежей, у которых число значений равно **N**). Каждый кортеж будет иметь значения, полученные путем итерации всех псевдонимов коллекции среди их наборов. Другими словами это полное перекрестное произведение наборов hello, участвующих в соединении hello.

Hello примеры показывают, как работает предложение JOIN hello. В следующем примере hello hello результат является пустым, поскольку hello перекрестное произведение каждого документа из источника и пустой набор пуст.

**Запрос**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**Результаты**  

    [{
    }]


В следующем примере hello, hello соединения находится между корень документа hello и hello `children` subroot. Это векторное произведение между двумя объектами JSON. Hello факт, что дочерние элементы массива не позволяет эффективно hello СОЕДИНЕНИЯ, так как мы работаем с один корень, hello дочерних элементов массива. Таким образом hello результат содержит только два результата, поскольку hello перекрестное произведение каждого документа с массивом hello дает точно только один документ.

**Запрос**

    SELECT f.id
    FROM Families f
    JOIN f.children

**Результаты**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


Следующий пример Hello показано более традиционных соединение:

**Запрос**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**Результаты**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



Hello первое, что toonote является, hello `from_source` из hello **JOIN** предложение является итератором. Таким образом поток hello в данном случае составляет:  

* Разверните каждый дочерний элемент **c** в массиве hello.
* Применение перекрестного произведения со hello корень документа hello **f** с каждого дочернего элемента **c** , плоский формат в первом шаге hello.
* Наконец, проект hello корневой объект **f** только свойство name. 

Первый документ Hello (`AndersenFamily`) содержит только один дочерний элемент, поэтому hello результирующий набор содержит только один объект соответствующего toothis документа. Hello второго документа (`WakefieldFamily`) содержит два дочерних элемента. Таким образом hello перекрестное произведение создает отдельный объект для каждого дочернего элемента, тем самым в результате чего два объекта: один для каждого дочернего соответствующий toothis документа. поля в обоих этих документов являются корневым Hello hello таким же, как и следовало ожидать в перекрестное произведение.

Hello real служебной программы из hello СОЕДИНЕНИЯ является tooform кортежей из перекрестного произведения hello в форме, в противном случае сложно tooproject. Кроме того, как показано в следующем примере hello, можно отфильтровать hello сочетания кортеж hello, которая позволяет пользователь выбрал условия удовлетворены hello кортежей в целом.

**Запрос**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**Результаты**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



В этом примере является естественным расширением предшествующий пример hello и выполняет двойные соединения. Таким образом hello векторное произведение можно рассматривать как hello, следующий код:

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily` имеется один ребенок, у которого один питомец. Таким образом, hello перекрестное произведение возвращает одну строку (1\*1\*1) из этого семейства. Однако семейство Wakefield включает двух детей, но только у одного ребенка «Джесси» есть питомцы. У Джесси два питомца. Поэтому hello перекрестное произведение дает результат 1\*1\*2 = 2 строки из этого семейства.

В следующем примере hello имеется дополнительный фильтр на `pet`. Это исключает все кортежи hello, где имя pet hello не является «Тени». Обратите внимание, что мы являются кортежами может toobuild из массивов, фильтр для любого из элементов hello кортежа hello любое сочетание hello элементов проекта. 

**Запрос**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**Результаты**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>Интеграция JavaScript
Azure Cosmos DB предоставляет модель программирования для выполнения логики приложения на основе JavaScript непосредственно в коллекциях hello с точки зрения хранимых процедур и триггеров. Это позволяет:

* Транзакционных операций CRUD возможность toodo высокой производительности и запросов к документам в коллекции посредством hello глубокой интеграции среды выполнения JavaScript непосредственно в компонент database engine hello. 
* Добиться естественного моделирования потока управления, областей видимости переменных, присвоения и интеграции обработки исключений примитивов с транзакциями базы данных. Дополнительные сведения о поддержке Azure Cosmos DB интеграция с JavaScript см. документацию программирования на стороне сервера toohello JavaScript.

### <a id="UserDefinedFunctions"></a>Определяемые пользователем функции (UDF)
Вместе с типами hello уже определен в этой статье DocumentDB API SQL обеспечивает поддержку для пользовательской функции (UDF). В частности определяемые пользователем скалярные функции поддерживаются, где разработчики hello можно передавать в ноль или несколько аргументов и возвращают результат обратно один аргумент. Каждый из этих аргументов проверяется на соответствие допустимым значениям JSON.  

синтаксис DocumentDB API SQL Hello расширяется toosupport настраиваемую прикладную логику, с помощью этих определяемые пользователем функции. Пользовательские функции могут быть зарегистрированы в API DocumentDB, а затем на них можно ссылаться как на часть SQL-запроса. На самом деле hello exquisitely представляют UDFs предназначены toobe вызывается по запросам. Как следствие toothis выбора, определяемые пользователем функции не имеют доступа к toohello контекста объекта Здравствуйте, других JavaScript имеют типы (хранимые процедуры и триггеры). Поскольку запросы выполняются только для чтения, они могут работать как на первичной, так на вторичной репликах. Таким образом определяемые пользователем функции, разработанные toorun во вторичных репликах, в отличие от других типов JavaScript.

Ниже приведен пример как определяемой пользователем функции могут быть зарегистрированы в базе данных Cosmos DB hello, в частности в коллекции документов.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

Hello предыдущий пример создает определяемую пользователем Функцию с именем `REGEX_MATCH`. Он принимает два строковых значения JSON `input` и `pattern` и проверяет, не указан шаблон hello в первые совпадения hello Здравствуйте, во-вторых, с помощью функции string.match() языка JavaScript.

Теперь мы можем использовать эту определяемую пользователем функцию в запросе в проекции. Определяемые пользователем функции должны быть дополнены hello с учетом регистра префикс «udf.» с учетом регистра. 

> [!NOTE]
> Предыдущий too3/17/2015, Cosmos DB поддерживаются вызовы определяемых пользователем Функций без hello «udf.» например SELECT REGEX_MATCH(). Теперь этот метод выполнения вызовов устарел.  
> 
> 

**Запрос**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**Результаты**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

Hello определяемой пользователем функции также может использоваться внутри фильтра, как показано в hello приведенном ниже примере также дополнены hello «udf.» как показано в примере ниже.

**Запрос**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**Результаты**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


В сущности, определяемые пользователем функции являются корректными скалярными выражениями и могут быть использованы в проекциях и фильтрах. 

tooexpand на степень hello определяемых пользователем функций, давайте рассмотрим другой пример с условной логики:

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


Ниже приведен пример hello, упражнения определяемой пользователем функции.

**Запрос**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**Результаты**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


Как hello предыдущей демонстрации примеры, определяемые пользователем функции интегрировать power hello языка JavaScript tooprovide DocumentDB API SQL hello форматированного программируемый интерфейс toodo сложную процедурных, условного логику с помощью hello встроенных среды выполнения JavaScript возможности.

DocumentDB API SQL аргументы hello toohello определяемых пользователем функций для каждого документа в источнике hello по использованию hello текущую стадию (предложение WHERE или предложение SELECT) обработки hello определяемой пользователем функции. Hello результат будет включено в легко hello общую конвейерной обработки. Если ссылка tooby hello UDF параметры недоступны в hello значение JSON hello, параметр считается свойства hello не определено и поэтому hello полностью пропускается вызова определяемой пользователем функции. Аналогично, если результат hello hello определяемой пользователем функции не определен, он не включается в результат hello. 

Таким образом определяемые пользователем функции являются значительные средства toodo сложной бизнес-логики как часть запроса hello.

### <a name="operator-evaluation"></a>Оценивание операторов
Cosmos база данных с тем hello того, что базы данных JSON, рисование parallels с операторами JavaScript и его семантику оценки. Время Cosmos DB семантики JavaScript toopreserve с точки зрения поддержки JSON, в некоторых случаях отличается hello операцию вычисления.

В API SQL DocumentDB в отличие от традиционных SQL, hello типы значений часто неизвестны до hello значения извлекаются из базы данных. В tooefficiently порядок выполнения запросов, большинство hello операторов имеют строгие требования к типам. 

SQL в API DocumentDB не выполняет неявные преобразования, в отличие от JavaScript. Например, запрос `SELECT * FROM Person p WHERE p.Age = 21` соответствует документам, которые содержат свойство "Возраст" со значением 21. Любой документ, свойство "возраст" в котором равно строке "21" или другим вариациям, таким как "021", "21.0", "0021", "00021" и т. д. не будут возвращены. Это напротив toohello JavaScript, где hello строковые значения, неявно приведен toonumbers (зависимости от оператора, например: ==). Этот выбор имеет решающее значение для эффективного согласования индексов в SQL API DocumentDB. 

## <a name="parameterized-sql-queries"></a>Параметризованные SQL-запросы
Cosmos DB поддерживают запросы с параметрами, в соответствии со знаком нотацию @ hello. Параметризованный SQL обеспечивает надежную обработку и экранирование пользовательского ввода, предотвращая случайное раскрытие данных через внедрение кода SQL. 

Например, можно написать запрос, который принимает в качестве параметров фамилию и состояние адреса, а затем выполнить его для различных значений параметров фамилия и состояние адреса на основе ввода пользователя.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

Этот запрос можно затем отправить tooCosmos DB как параметризованный запрос JSON, как показано ниже.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

Аргумент tooTOP Hello можно задать использование параметризованных запросов, как показано ниже.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

Значениями параметров могут быть любые допустимые JSON (строки, числа, логические значения, значения null, даже массивы или вложенные JSON). Кроме этого, так как Cosmos DB не имеет схемы, параметры не проверяются на соответствие типам.

## <a id="BuiltinFunctions"></a>Встроенные функции
Cosmos DB также поддерживает несколько встроенных функций для общих операций, которые можно использовать в запросах как определяемые пользователем функции.

| Группа функций          | Операции                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Математические функции  | ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN и TAN |
| Функции проверки типа | IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED и IS_PRIMITIVE                                                           |
| Строковые функции        | CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING и UPPER       |
| Функции массивов         | ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH и ARRAY_SLICE                                                                                         |
| Пространственные функции       | ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID и ST_ISVALIDDETAILED                                                                           | 

Если вы используете определяемой пользователем функции (UDF) для которого доступна встроенной функции, соответствующей встроенной функции hello следует использовать как он будет быстрее toorun toobe и многое другое эффективно. 

### <a name="mathematical-functions"></a>Математические функции
Hello математические функции производят вычисления, основанные на числовых значениях, заданных в качестве аргументов и возвращают числовое значение. Здесь приведен список поддерживаемых встроенных математических функций.


| Использование | Описание |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS (num_expr)](#bk_abs) | Возвращает hello абсолютное (положительное) значение hello указанного числового выражения. |
| [CEILING (num_expr)](#bk_ceiling) | Возвращает hello наименьшее целочисленное значение больше или равно, hello указанного числового выражения. |
| [FLOOR (num_expr)](#bk_floor) | Возвращает наибольшее целое число hello меньше или равно toohello указанного числового выражения. |
| [EXP (num_expr)](#bk_exp) | Возвращает экспоненты hello hello указанного числового выражения. |
| [LOG (num_expr [,base])](#bk_log) | Возвращает hello натуральный логарифм hello указаны числовое выражение, или с помощью hello логарифм hello базы |
| [LOG10 (num_expr)](#bk_log10) | Возвращает hello по основанию 10 логарифмической значение hello заданное числовое выражение. |
| [ROUND (num_expr)](#bk_round) | Возвращает числовое значение, округленное toohello ближайшего целого значения. |
| [TRUNC (num_expr)](#bk_trunc) | Возвращает числовое значение, усеченное toohello ближайшего целого значения. |
| [SQRT (num_expr)](#bk_sqrt) | Возвращает hello квадратный корень из hello указанного числового выражения. |
| [SQUARE (num_expr)](#bk_square) | Hello возвращает квадрат для hello указанного числового выражения. |
| [POWER (num_expr, num_expr)](#bk_power) | Возвращает степень hello hello указан toohello значение числового выражения. |
| [SIGN (num_expr)](#bk_sign) | Возвращает hello знак (-1, 0, 1) hello указано нулевое значение числового выражения. |
| [ACOS (num_expr)](#bk_acos) | Возвращает hello угол в радианах, косинус которого является hello указанного числового выражения; также называется арккосинусом. |
| [ASIN (num_expr)](#bk_asin) | Hello Возвращает угол в радианах, синус которого равен hello указано числовое выражение. Также называется арксинусом. |
| [ATAN (num_expr)](#bk_atan) | Hello Возвращает угол в радианах, тангенс которого равен hello указано числовое выражение. Также называется арктангенсом. |
| [ATN2 (num_expr)](#bk_atn2) | Возвращает hello угол в радианах между положительным направлением оси x hello и hello лучом, проведенным из hello toohello координат (y, x), где x и y являются значениями hello hello два числа с плавающей выражения. |
| [COS (num_expr)](#bk_cos) | Возвращает hello hello в тригонометрический косинус указанного угла в радианах, в hello указанного выражения. |
| [COT (num_expr)](#bk_cot) | Возвращает hello hello в тригонометрический котангенс указанного угла в радианах, в hello указанного числового выражения. |
| [DEGREES (num_expr)](#bk_degrees) | Возвращает hello соответствующее значение угла в градусах для значения угла в радианах. |
| [PI ()](#bk_pi) | Возвращает hello константное значение PI. |
| [RADIANS (num_expr)](#bk_radians) | Возвращает значение угла в радианах для числового значения, указанного в градусах. |
| [SIN (num_expr)](#bk_sin) | Возвращает hello hello в Тригонометрический синус указанного угла в радианах, в hello указанное выражение. |
| [TAN (num_expr)](#bk_tan) | Возвращает тангенс hello входное выражение hello в hello указанном выражении. |

Например теперь можно запускать запросы hello следующим образом:

**Запрос**

    SELECT VALUE ABS(-4)

**Результаты**

    [4]

Hello основное различие между tooANSI функций по сравнению Cosmos DB SQL является они спроектированный toowork с данные без схемы, так и схемы. Например при наличии документа, где свойство размера hello отсутствует или имеет нечисловое значение, например «неизвестно», а затем hello документов пропускается, вместо возвращения ошибки.

### <a name="type-checking-functions"></a>Функции проверки типа
функции проверки типа Hello разрешить toocheck hello тип выражения в запросах SQL. Тип может иметь функции проверки используется тип hello toodetermine свойств в документах на лету hello, когда переменная или неизвестный. Здесь приведен список поддерживаемых встроенных функций проверки типа.

<table>
<tr>
  <td><strong>Использование</strong></td>
  <td><strong>Описание</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></td>
  <td>Возвращает логическое значение, указывающее, если тип hello hello значения массива.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></td>
  <td>Возвращает логическое значение, указывающее, если тип hello значения hello логическое значение.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></td>
  <td>Возвращает логическое значение, указывающее, если тип hello hello значения null.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></td>
  <td>Возвращает логическое значение, указывающее, если тип hello hello значение является числом.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></td>
  <td>Возвращает логическое значение, указывающее, если тип hello значения hello объекта JSON.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></td>
  <td>Возвращает логическое значение, указывающее, если тип hello hello значение является строкой.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></td>
  <td>Возвращает логическое значение, указывающее, если свойство hello назначено значение.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></td>
  <td>Возвращает логическое значение, указывающее, если тип hello значения hello является строка, число, логическое значение или значение null.</td>
</tr>

</table>

Используя эти функции, теперь можно выполнить запросы hello следующим образом:

**Запрос**

    SELECT VALUE IS_NUMBER(-4)

**Результаты**

    [true]

### <a name="string-functions"></a>Строковые функции
Hello следующие скалярные функции выполняют операцию над входным строковым значением и возвращают строковое, числовое или логическое значение. Ниже приведена таблица встроенных строковых функций:

| Использование | Description (Описание) |
| --- | --- |
| [LENGTH (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |Количество символов для hello hello возвращает указанного строкового выражения |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |Возвращает строку, являющуюся результатом объединения двух или более строковых значений hello. |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |Возвращает часть строкового выражения. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |Возвращает логическое значение, указывающее, было ли первое строковое выражение hello заканчивается hello второй |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |Возвращает логическое значение, указывающее, было ли первое строковое выражение hello заканчивается hello второй |
| [CONTAINS (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |Возвращает логическое значение, указывающее, является ли hello первое строковое выражение содержит hello второй. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Возвращает hello, начальная позиция первого вхождения hello hello второго строкового выражения внутри первого указанного строкового выражения hello, или значение -1, если строка hello не найдена. |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |Возвращает hello левую часть строки с hello указанное число символов. |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Возвращает hello правой части строки с hello указанное число символов. |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |Возвращает строковое выражение после удаления начальных пробелов. |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |Возвращает строковое выражение после усечения всех конечных пробелов. |
| [LOWER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |Возвращает строковое выражение после преобразования данных toolowercase символ верхнего регистра. |
| [UPPER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |Возвращает строковое выражение после преобразования данных toouppercase строчные буквы. |
| [REPLACE (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |Заменяет все вхождения указанного строкового значения другим строковым значением. |
| [REPLICATE (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |Повторяет строковое значение указанное число раз. |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Возвращает hello строковое значение в обратном порядке. |

Используя эти функции, теперь можно запустить запросы hello следующим образом. Например можно получить имя семейства hello в верхнем регистре следующим образом:

**Запрос**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**Результаты**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

Или объединить строки, как в этом примере:

**Запрос**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**Результаты**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


Строковые функции могут также использоваться в hello ГДЕ предложение toofilter результаты, например в следующий пример hello:

**Запрос**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**Результаты**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>Функции массивов
Следующие скалярные функции Hello операции над входным значением массива и возвращают числовое, логическое значение или значение массива. Ниже приведена таблица встроенных функций над массивом:

| Использование | Описание |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |Возвращает число hello элементов hello указано выражение массива. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |Возвращает массив, который является результатом объединения двух или более значений массивов hello. |
| [ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |Возвращает логическое значение, указывающее, содержит ли массив hello hello заданного значения. Можно указать, если hello совпадение полной или частичной. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |Возвращает часть выражения массива. |

Функции массивов можно использовать toomanipulate массивов в JSON. Например ниже приведен запрос, возвращающий все документы, где hello родительских элементов он «Циклический перебор Wakefield». 

**Запрос**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**Результаты**

    [{
      "id": "WakefieldFamily"
    }]

Можно указать фрагмент частичного для сопоставления элементов в массиве hello. Hello следующем запросе выполняется поиск всех родительских элементов с hello `givenName` из `Robin`.

**Запрос**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**Результаты**

    [{
      "id": "WakefieldFamily"
    }]


Вот другой пример, использующий ARRAY_LENGTH tooget hello количество детей в семействе.

**Запрос**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**Результаты**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>Пространственные функции
Cosmos DB поддерживает следующие встроенные функции Open Geospatial Consortium (OGC) для выполнения запросов к геопространственных hello. 

<table>
<tr>
  <td><strong>Использование</strong></td>
  <td><strong>Описание</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr, point_expr)</td>
  <td>Возвращает hello расстояние между выражениями hello две точки GeoJSON Polygon и LineString.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Возвращает выражение типа Boolean, показывающего, является hello GeoJSON сперва (точка Polygon и LineString) в рамках hello второй GeoJSON объекта (точка Polygon и LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Возвращает логическое выражение, указывающее, пересекается ли hello двух указанных GeoJSON объектов (точка Polygon и LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Возвращает логическое значение, указывающее, является ли hello точки GeoJSON Polygon и LineString выражение допустимо.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Возвращает значение JSON, содержащий логическое значение, указываемое hello точки GeoJSON Polygon и LineString выражение является допустимым и если недействительной, кроме того hello причина как строковое значение.</td>
</tr>
</table>

Пространственные функции могут быть запросами сходству используется tooperform пространственных данных. Например ниже приведен запрос, возвращающий все семейство документы, в течение 30 км hello указанное расположение используется встроенная функция ST_DISTANCE hello. 

**Запрос**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Результаты**

    [{
      "id": "WakefieldFamily"
    }]

Дополнительные сведения о поддержке геопространственных данных в Cosmos DB см. в статье [Работа с геопространственными данными и данными расположений GeoJSON в Azure Cosmos DB](geospatial.md). Что мы и добрались до Пространственные функции и hello синтаксис SQL для Cosmos DB. Теперь давайте рассмотрим как LINQ запрос работает и его взаимодействия с синтаксисом hello мы видели к текущему моменту.

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
LINQ является моделью программирования .NET, которая выражает вычисления в виде запросов потоков объектов. Cosmos DB предоставляет клиентская библиотека toointerface с помощью LINQ, облегчая преобразование между объектами JSON и .NET и сопоставления из подмножества LINQ запросы tooCosmos DB. 

Hello рисунок ниже показана архитектура hello, поддерживающих запросы LINQ с помощью Cosmos DB.  С помощью клиента Cosmos DB hello, разработчики могут создавать **IQueryable** объекта, напрямую запросы hello Cosmos DB поставщик запросов, который затем преобразует запрос LINQ hello в запрос Cosmos DB. Hello запрос передается toohello tooretrieve server Cosmos DB набор результатов в формате JSON. Hello возвращаемые результаты будут десериализованы в поток объектов .NET на стороне клиента hello.

![Архитектура поддержки запросов LINQ с помощью API DocumentDB — синтаксис SQL, язык запросов JSON, основные понятия баз данных и SQL-запросы][1]

### <a name="net-and-json-mapping"></a>Сопоставление .NET и JSON
Hello сопоставление объектов .NET и документы JSON является естественным - для каждого поля данных элемент сопоставляется tooa объект JSON, где — имя поля hello сопоставлены toohello «ключ» часть hello объекта и часть «value» hello будет сопоставлен рекурсивно toohello часть значения hello объекта. Рассмотрим следующий пример hello: hello семейства объектом, созданным — сопоставленных toohello JSON документ, как показано ниже. И наоборот, hello JSON документ сопоставленных задней tooa объект .NET.

**Класс C#**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>Перевод tooSQL LINQ
Поставщик запросов Cosmos DB Hello выполняет сопоставление наиболее усилий из запроса LINQ в Cosmos DB SQL-запроса. В следующих описание hello предполагается, что hello читатель имеет общее представление о языка LINQ.

Во-первых для системы типов hello, поддерживают все JSON примитивные типы — числовые типы, логическое значение, строка и null. Поддерживаются только эти типы JSON. поддерживаются следующие скалярные выражения Hello.

* Постоянные значения — следующие значения констант hello примитивных типов данных во время hello, оценки запроса hello.
* Индексные выражения свойства или массива — эти выражения см. свойство toohello объекта или элемента массива.
  
     family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n — это целочисленная переменная
* Арифметические выражения. К ним относятся общие арифметические выражения на основе численных и логических значений. Полный список hello можно найти toohello спецификации SQL.
  
     2 * family.children[0].grade;    x + y;
* Строка выражения сравнения — к ним относятся сравнивают строковое значение toosome постоянное строковое значение.  
  
     mother.familyName == "Smith";    child.givenName == s; //s — это строковая переменная
* Выражение создания объекта/массива. Возвращают объект комбинированного типа, или анонимного типа, или массив таких объектов. Эти значения могут быть вложенными.
  
     new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //анонимный тип с двумя полями              
     new int[] { 3, child.grade, 5 };

### <a id="SupportedLinqOperators"></a>Список поддерживаемых операторов LINQ
Ниже приведен список поддерживаемых операторов LINQ в поставщике LINQ hello, входящий в состав пакета SDK для .NET DocumentDB hello.

* **Выберите**: проекций перевести toohello SQL SELECT, включая создание объектов
* **Где**: фильтры переводить toohello SQL WHERE и поддерживает преобразование между & &, || и! операторы SQL toohello
* **SelectMany**: позволяет очистки массивы toohello SQL JOIN предложения. Может быть toofilter используется toochain или вложенные выражения на элементы массива
* **OrderBy и OrderByDescending**: преобразует tooORDER по возрастанию или по убыванию
* Операторы для агрегирования **Count**, **Sum**, **Min**, **Max**, **Average** и их асинхронные эквиваленты **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** и **AverageAsync**.
* **CompareTo**: преобразует toorange сравнения. Обычно используется для строк, так как их нельзя сравнивать в .NET.
* **Принимать**: преобразует toohello SQL TOP для ограничения результатов запроса
* **Математические функции**: поддерживает преобразование. В NET Abs Acos, Asin, Atan, верхний предел, Cos, Exp, функция Floor, журнал, Log10, Pow, циклов, знак, Sin, Sqrt, Tan, Truncate toohello эквивалент SQL встроенных функций.
* **Строковые функции**: поддерживает преобразование. NET Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, обратное, TrimEnd, StartsWith, подстроку, ToUpper toohello эквивалентные встроенные функции SQL.
* **Массив функции**: поддерживает преобразование. В NET Concat "," содержит "и" число toohello эквивалент SQL встроенных функций.
* **Геопространственные функции расширения**: поддерживает преобразование из методы-заглушки расстояние в пределах IsValid и IsValidDetailed toohello эквивалентные встроенные функции SQL.
* **Пользовательские функции расширения**: поддерживает преобразования из hello заглушки метода UserDefinedFunctionProvider.Invoke toohello соответствующего определяемой пользователем функции.
* **Прочие**: поддерживает объединенный перевод hello и условные операторы. Может транслировать Contains tooString CONTAINS, ARRAY_CONTAINS или hello в SQL, в зависимости от контекста.

### <a name="sql-query-operators"></a>Операторы SQL-запросов
Ниже приведены некоторые примеры, иллюстрирующие, как некоторые стандартные операторы запросов LINQ hello преобразуются вниз tooCosmos DB запросов.

#### <a name="select-operator"></a>Оператор Select
синтаксис Hello `input.Select(x => f(x))`, где `f` является скалярным выражением.

**Лямбда-выражение LINQ**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**Лямбда-выражение LINQ**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**Лямбда-выражение LINQ**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>Оператор SelectMany
синтаксис Hello `input.SelectMany(x => f(x))`, где `f` является скалярным выражением, которое возвращает тип коллекции.

**Лямбда-выражение LINQ**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Оператор Where
синтаксис Hello `input.Where(x => f(x))`, где `f` является скалярным выражением, которое возвращает значение типа Boolean.

**Лямбда-выражение LINQ**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**Лямбда-выражение LINQ**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>Составные SQL-запросы
Hello выше операторы можно включать tooform более мощные средства запросов. Поскольку Cosmos DB поддерживает вложенные коллекции, hello композиции может быть сцеплены или вложенные.

#### <a name="concatenation"></a>Объединение
синтаксис Hello `input(.|.SelectMany())(.Select()|.Where())*`. Объединенный запрос может начинаться с необязательного запроса `SelectMany`, за которым идет несколько операторов `Select` или `Where`.

**Лямбда-выражение LINQ**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**Лямбда-выражение LINQ**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**Лямбда-выражение LINQ**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**Лямбда-выражение LINQ**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>Вложенные операторы
синтаксис Hello `input.SelectMany(x=>x.Q())` где Q является `Select`, `SelectMany`, или `Where` оператор.

Во вложенном запросе внутренний запрос hello является элементом примененных tooeach hello внешней коллекции. Один является важной функцией, hello внутренний запрос может ссылаться поля toohello элементов hello hello внешней коллекции как самосоединения.

**Лямбда-выражение LINQ**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**Лямбда-выражение LINQ**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**Лямбда-выражение LINQ**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>Выполнение SQL-запросов
Cosmos DB предоставляет ресурсы через REST API, который можно вызвать с помощью любого языка, позволяющего отправлять запросы HTTP или HTTPS. Кроме того, Cosmos DB предлагает программные библиотеки для некоторых популярных языков программирования, таких как NET, Node.js, JavaScript и Python. Hello REST API и hello различных библиотеках все поддержку запросов через SQL. Hello .NET SDK поддерживает LINQ, кроме запросов tooSQL.

Здравствуйте, в следующих примерах показано, как toocreate запрос и отправить его с учетной записью Cosmos DB базы данных.

### <a id="RestAPI"></a>REST API
Cosmos DB предлагает простую и открытую модель программирования RESTful поверх HTTP. Учетные записи баз данных могут быть подготовлены с использованием подписки Azure. модель ресурсов Cosmos DB Hello состоит из набора ресурсов под учетной записью базы данных, каждый из которых можно с помощью логического и стабильный URI. Набор ресурсов — ссылка tooas канала в этом документе. Учетная запись базы данных может состоять из набора баз данных, каждая из которых содержит несколько коллекций, каждая из которых, в свою очередь, содержит хранимые процедуры, триггеры, определяемые пользователем функции, документы и соответствующие вложения.

модель Hello основные взаимодействия с этими ресурсами выполняется с помощью команд hello HTTP GET, PUT, POST и DELETE с их стандартных интерпретацию. Hello команды POST используется для создания нового ресурса, выполнение хранимой процедуры или при выдаче запроса Cosmos DB. Запросы всегда включают только операции чтения без побочных эффектов.

Hello следующих примерах POST для запроса DocumentDB API к коллекцию, содержащую два образца документов hello, когда мы рассмотрели к текущему моменту. запрос Hello имеет простой фильтр для имени свойства hello JSON. Обратите внимание на использование hello hello `x-ms-documentdb-isquery` и Content-Type: `application/query+json` toodenote заголовки, hello операции — это запрос.

**Запрос**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**Результаты**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


Во втором примере Hello показывает более сложный запрос, возвращающий несколько результатов из соединения hello.

**Запрос**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**Результаты**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


Если результаты запроса не может поместиться на одной странице результатов, а затем hello API-интерфейса REST возвращает токен продолжения через hello `x-ms-continuation-token` заголовок ответа. Клиенты может разбивать на страницы результатов, включив заголовок hello в последующие результаты. Hello количество результатов на странице также можно управлять с помощью hello `x-ms-max-item-count` номера заголовка. Если указанный запрос hello в статистической функции, такие как `COUNT`, то страница hello запроса может возвращать частично статистические значения по hello страницы результатов. Hello клиентов необходимо выполнять статистическую второго уровня через эти результаты tooproduce hello окончательные результаты, например, суммирования hello счетчики возвращаются в hello отдельных страниц tooreturn hello общее число объектов.

политика согласованности данных hello toomanage для запросов, используйте hello `x-ms-consistency-level` заголовок, как и все запросы REST API. Для согласованности сеанса это hello echo tooalso требуется последняя версия `x-ms-session-token` заголовка файла Cookie в запросе hello. Hello политика индексирования запрашиваемые коллекции может также повлиять на hello согласованности результатов запроса. Параметры политики индексирования по умолчанию hello, для коллекций hello индекс всегда является содержимого документа hello и результатов, удовлетворяющих согласованности hello, выбранного для данных запросов. Если политика индексирования hello ослабленной tooLazy, запросы могут возвращать устаревших результаты. Дополнительные сведения см. в статье [Настраиваемые уровни согласованности данных в Azure Cosmos DB][consistency-levels].

Если политика индексирования hello настроен на коллекцию hello не поддерживает указанный запрос hello, hello Azure Cosmos DB сервер возвращает 400 «Ошибочный запрос». Он возвращается для запросов к путям, сконфигурированным для поиска по значениям хэшей (равенство), а также к путям, явно исключенным из индексации. Hello `x-ms-documentdb-query-enable-scan` заголовок может быть указанного tooallow hello запроса tooperform проверку, если индекс недоступен.

Можно получить подробные метрики на выполнение запроса, задав `x-ms-documentdb-populatequerymetrics` заголовок слишком`True`. Дополнительные сведения см. в статье [Tuning query performance with Azure Cosmos DB](documentdb-sql-query-metrics.md) (Настройка производительности запросов с помощью Azure Cosmos DB).

### <a id="DotNetSdk"></a>Пакет SDK для C# (.NET)
Hello .NET SDK поддерживает LINQ и SQL запрос. Hello следующем примере показано, как tooperform hello простого фильтра запроса, представленные ранее в этом документе.

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Этот пример сравнивает два свойства на равенство в каждом документе и использует анонимные проекции. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Следующий пример Hello показывает соединения, выраженных через LINQ SelectMany.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



клиент .NET Hello автоматически выполняет итерацию всех страниц hello результатов запроса в блоках foreach hello, как показано выше. запрос Hello, параметры, представленные в hello раздел REST API также доступны в hello .NET SDK, с помощью hello `FeedOptions` и `FeedResponse` классов в метод CreateDocumentQuery hello. Hello количество страниц, можно управлять с помощью hello `MaxItemCount` параметр. 

Можно также явно контроль разбиения на страницы, создав `IDocumentQueryable` с помощью hello `IQueryable` объекта, затем путем чтения` ResponseContinuationToken` значения и их передача в качестве `RequestContinuationToken` в `FeedOptions`. `EnableScanInQuery`может быть просмотров tooenable набор, если запрос hello не поддерживаются hello настроена политика индексирования. Для секционированных коллекций можно использовать `PartitionKey` toorun hello запрос к одной секции (хотя Cosmos DB автоматически этот можно извлечь из текста hello запроса), и `EnableCrossPartitionQuery` toorun запросы, которые может потребоваться toobe выполняться несколько секций. 

См. слишком[примеры Azure Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net) дополнительные образцы, содержащий запросы. 

### <a id="JavaScriptServerSideApi"></a>Интерфейс API для серверного JavaScript
Cosmos DB предоставляет модель программирования для выполнения логики приложения на основе JavaScript непосредственно на hello коллекций, с помощью хранимых процедур и триггеров. Hello логику JavaScript, зарегистрированных на уровне коллекции, затем может выдавать операции базы данных в операции hello в документах hello hello, Получает коллекцию. Эти операции оборачиваются транзакциями ACID.

Hello следующем примере показано, как запросы toouse queryDocuments hello в toomake hello API сервера JavaScript внутри хранимых процедур и триггеров.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>Справочные материалы
1. [Введение tooAzure Cosmos DB][introduction]
2. [DocumentDB SQL Syntax](http://go.microsoft.com/fwlink/p/?LinkID=510612) (Синтаксис SQL в DocumentDB)
3. [Примеры .NET для Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net)
4. [Настраиваемые уровни согласованности данных в Azure Cosmos DB][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON — [http://json.org/](http://json.org/)
7. Спецификация JavaScript — [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. Методика вычисления запросов для больших баз данных — [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Обработка запросов в параллельных реляционных СУБД (Query Processing in Parallel Relational Database Systems), IEEE Computer Society Press, 1994
11. Lu, Ooi, Tan, Обработка запросов в параллельных реляционных СУБД (Query Processing in Parallel Relational Database Systems), IEEE Computer Society Press, 1994
12. Кристофер Олстон (Christopher Olston), Бенджамин Рид (Benjamin Reed), Аткарш Сривастава (Utkarsh Srivastava), Рави Камар (Ravi Kumar), Эндрю Томкинс (Andrew Tomkins): Язык Pig. Не такой уж и незнакомый язык для обработки данных (Pig Latin: A Not-So-Foreign Language for Data Processing), SIGMOD 2008 г.
13. Ж. Графе (G. Graefe). Hello каскадные платформа для оптимизации запросов. IEEE Data Eng. Bull., 18(3): 1995 г.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md