---
title: "Поддержка Cosmos DB Gremlin aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello язык Gremlin из TinkerPop Apache, который функции и действия и доступен в базе данных Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Поддержка графа Gremlin в базе данных Azure Cosmos DB
Azure Cosmos DB поддерживает [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps) — язык обхода графов [Apache TinkerpPop](http://tinkerpop.apache.org), предназначенный для создания сущностей графа и выполнения операций запросов графов Graph API. Можно использовать hello Gremlin языка toocreate графа сущностей (вершин и границы), изменения свойств в этих сущностей, выполнения запросов и обходов и удаление сущностей. 

Azure Cosmos DB добавляет функции предприятиях toograph баз данных. Эти возможности включают глобальное распределение, независимое масштабирование хранилища и пропускной способности, прогнозируемую задержку операций менее 10 миллисекунд, автоматическое индексирование и гарантированный уровень производительности в 99,99 % случаях согласно соглашениям об уровне обслуживания. Поскольку Azure Cosmos DB поддерживает TinkerPop/Gremlin, можно легко перенести приложения, написанные с использованием другой диаграммы базы данных без необходимости изменения кода toomake. Кроме того, благодаря поддержке языка Gremlin база данных Azure Cosmos DB быстро и эффективно интегрируется с платформами аналитики, совместимыми с TinkerPop, например с [Apache Spark GraphX](http://spark.apache.org/graphx/). 

В этой статье мы укажите краткое описание Gremlin и перечислить hello Gremlin функции и действия, которые поддерживаются в режиме предварительного просмотра hello поддержки Graph API.

## <a name="gremlin-by-example"></a>Обзор Gremlin на примере
Используем образец toounderstand графа, каким образом запросы могут быть выражены в Gremlin. Hello на этом рисунке показано бизнес-приложения, который управляет данными о пользователях, интересы и устройств в форме hello графа.  

![Пример базы данных, в котором показаны люди, их интересы и устройства](./media/gremlin-support/sample-graph.png) 

На этом графике имеет следующие типы вершин (называемых «метка» в Gremlin) hello.

- Люди: hello граф состоит из трех пользователей, циклический перебор, Томас и Бен
- Интересы: должным образом, в этом примере hello игру футбольной
- Устройств: hello устройства, пользователи применяют
- Операционные системы: hello операционных систем hello устройств, работающих на

Мы представляют Привет связей между этими сущностями через следующие типы/метки краев hello.

- Знакомства. Например, "Томас знает Робин".
- Интерес: hello toorepresent интересы, hello людей в нашей диаграмме, например, «Бен заинтересована в футбольной»
- RunsOS: Ноутбук выполняется ОС Windows hello
- Использует: toorepresent использует какое устройство a человека. Например, Робин использует телефон Motorola с серийным номером 77.

Давайте выполнения некоторых операций с это с помощью hello граф [Gremlin консоли](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console). Можно также выполнить эти операции с использованием драйверов Gremlin hello платформы по вашему выбору (Java, Node.js, Python или .NET).  Прежде чем мы рассмотрим поддерживаемые функции в базе данных Azure Cosmos, давайте рассмотрим несколько примеров tooget знакомы с синтаксисом hello.

Сначала рассмотрим операции CRUD (создание, чтение, обновление и удаление). Hello следующие Gremlin инструкция вставляет hello «Thomas» вершин в hello graph:

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

Далее hello, следующем за инструкцией Gremlin вставляет «знает» границей между Thomas и циклический перебор.

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

Hello следующий запрос возвращает вершины «person» hello в порядке убывания их имена:
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

Где блеска диаграмм — при необходимости tooanswer вопросы, например «какие операционные системы дружественными Thomas используют?». Этот простой tooget обхода Gremlin эту информацию можно запустить из графа hello:

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
А теперь давайте рассмотрим, какие возможности предоставляет база данных Azure Cosmos DB разработчикам Gremlin.

## <a name="gremlin-features"></a>Функции Gremlin
TinkerPop — это стандартная платформа, которая охватывает широкий ряд технологий графа. Таким образом он имеет Стандартные термины toodescribe какие возможности предоставляются поставщиком графа. База данных Azure Cosmos DB обеспечивает временную базу данных графа с высокой степенью параллелизма и возможностью записи, которую можно разделить на секции на нескольких серверах или кластерах. 

Hello следующей таблице перечислены функции TinkerPop hello, реализованные в Azure Cosmos DB. 

| Категория | Реализация базы данных Azure Cosmos DB |  Примечания | 
| --- | --- | --- |
| Функции графа | В предварительной версии обеспечивается сохраняемость и одновременный доступ. Спроектированный toosupport транзакции | Методы компьютера может осуществляться через соединитель Spark hello. |
| Функции переменной | Поддерживаются такие типы значений: логическое значение, целое число, байт, двойное число с плавающей точкой, число с плавающей точкой, целое число со знаком, полная дата, строка. | Поддерживаются несложные типы. Совместимы со сложными типами через модель данных. |
| Функции вершины | Поддерживаются RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty.  | Поддерживается создание, изменение и удаление вершин. |
| Функции свойств вершины | Поддерживаются StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues. | Поддерживается создание, изменение и удаление свойств вершины. |
| Функции ребра | Поддерживаются RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty. | Поддерживается создание, изменение и удаление ребра. |
| Функции свойств ребра | Поддерживаются типы Properties, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues. | Поддерживается создание, изменение и удаление свойств ребра. |

## <a name="gremlin-wire-format-graphson"></a>Формат подключения Gremlin: GraphSON

Azure Cosmos DB использует hello [GraphSON формат](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) при возврате результатов от Gremlin операций. GraphSON — hello Gremlin стандартного формата для представления вершин, границ и свойства (одной или несколькими значениями) с помощью JSON. 

К примеру, hello следующий фрагмент кода показывает GraphSON представление вершина *возвращается toohello клиента* из базы данных Azure Cosmos. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

hello следующие имеют свойства Hello, используемые GraphSON для вершин:

| Свойство | Описание |
| --- | --- |
| id | Идентификатор Hello hello вершин. Должно быть уникальным (в сочетании со значением hello _partition, если применимо) |
| label | Метка Hello hello вершины. Это тип сущности необязательными и используются toodescribe hello. |
| type | Используется toodistinguish вершин из документов не графа |
| properties | В контейнере пользовательских свойств, связанных с вершины hello. Каждое свойство может иметь несколько значений. |
| _partition (настраиваемое) | ключ раздела Hello hello вершины. Может быть используется tooscale out графы toomultiple серверов |
| outE | Содержит список внешних ребер вершины. Хранение сведений о соседство hello с вершины позволяет для быстрого выполнения обходы. Ребра сгруппированы на основе меток. |

И hello edge содержит следующие сведения toohelp с частями tooother навигации графа hello hello.

| Свойство | Описание |
| --- | --- |
| id | Идентификатор Hello hello edge. Должно быть уникальным (в сочетании со значением hello _partition, если применимо) |
| label | Метка Hello края hello. Это свойство имеет тип связи необязательными и используются toodescribe hello. |
| inV | Содержит список вершин для ребра. Хранение сведений о соседство hello границу hello позволяет для быстрого выполнения обходы. Вершины сгруппированы на основе меток. |
| properties | В контейнере пользовательских свойств, связанных с hello edge. Каждое свойство может иметь несколько значений. |

Каждое свойство может хранить несколько значений в массиве. 

| Свойство | Описание |
| --- | --- |
| value | значение свойства hello Hello

## <a name="gremlin-partitioning"></a>Секционирование Gremlin

В базе данных Azure Cosmos DB графы хранятся в контейнерах, которые можно независимо масштабировать по отношению к пропускной способности и хранилищу (выражено в нормализованных запросах в секунду). Каждый контейнер должен определять необязательное, но все же рекомендуемое свойство ключа секции, указывающее логическую границу секции для связанных данных. Каждая вершина и ребро должны содержать свойство `id`, которое является уникальным для сущностей в этом значении ключа секции. Hello подробности описаны в [секционирования в базе данных Azure Cosmos](partition-data.md).

Операции Gremlin быстро и эффективно выполняются с данными графа, охватывающими несколько секций в базе данных Azure Cosmos DB. Тем не менее, рекомендуется toochoose ключа секции для диаграммы, часто используемых в качестве фильтра в запросах, имеет много уникальных значений и аналогичные частоту доступа эти значения. 

## <a name="gremlin-steps"></a>Шаги Gremlin
Теперь давайте рассмотрим hello Gremlin действия, поддерживаемые Azure Cosmos DB. Дополнительные сведения о Gremlin см. в [руководстве по TinkerPop](http://tinkerpop.apache.org/docs/current/reference).

| Шаг | Описание | Руководство по TinkerPop 3.2 | Примечания |
| --- | --- | --- | --- |
| `addE` | Добавляет ребро между двумя вершинами. | [Шаг addE](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | Добавляет граф toohello вершин | [Шаг addV](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest, что все обходы hello возвращать значение | [Шаг and](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | Tooassign модулятор шаг переменной toohello выходные данные шага | [Шаг as](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | Модулятор шага, используемый с `group` и `order`. | [Шаг by](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | Возвращает первый обхода hello, который возвращает результат | [Шаг coalesce](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | Возвращает постоянное значение. Используется с `coalesce`.| [Шаг constant](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Возвращает число hello из обхода hello | [Шаг count](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | Возвращает hello значений с удаленными повторениями hello | [Шаг dedup](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | Удаляет hello значения (вершин и границы) | [Шаг drop](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | Действует как ограничитель, вычисляющий hello статистической обработки результатов| [Шаг fold](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | Здравствуйте, групп значений на основании указанного метки hello| [Шаг group](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Использовать toofilter свойства, вершин и границ. Поддерживает варианты `hasLabel`, `hasId`, `hasNot` и `has`. | [Шаг has](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | Вставляет значения в поток.| [Шаг inject](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Использовать tooperform фильтра с помощью логического выражения | [Шаг is](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | Использовать toolimit количество элементов в обход hello| [Шаг limit](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | Заключает в оболочку локальной раздел tooa обхода, аналогично вложенный запрос | [Шаг local](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | Использовать отрицание hello tooproduce фильтра | [Шаг not](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | Здравствуйте, возвращает результат указан hello обход, если он дает результат else, он возвращает hello вызывающего элемента | [Шаг optional](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Гарантирует, что по крайней мере один из обходов hello возвращает значение | [Шаг or](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | Возвращает результаты в hello указан порядок сортировки | [Шаг order](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Полный путь возвращает hello обхода hello | [Шаг path](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | Свойства проектов hello виде карты | [Шаг project](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Возвращает свойства hello для hello указан метки | [Шаг properties](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | Фильтры toohello указан диапазон значений| [Шаг range](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Шаг hello повторяется для hello заданное число раз. Используется для циклов. | [Шаг repeat](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Использовать результаты toosample обхода hello | [Шаг sample](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Использовать результаты tooproject обхода hello |  [Шаг select](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Используется для статистических выражений, без блокировки из обхода hello | [Шаг store](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | Выполняет статистическое вычисление путей из вершины в дерево. | [Шаг tree](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | Развертывает итератор.| [Шаг unfold](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | Объединяет результаты из нескольких обходов.| [Шаг union](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Включает в себя hello действия, необходимые для обходов между краями и вершин `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, и `otherV` для | [Шаги vertex](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Использовать результаты toofilter hello обхода. Поддерживает операторы `eq`, `neq`, `lt`, `lte`, `gt`, `gte` и `between`.  | [Шаг where](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

Оптимизированный для операций записи обработчик базы данных Azure Cosmos DB по умолчанию поддерживает автоматическое индексирование всех свойств вершин и ребер. Таким образом, запросы с фильтрами, диапазон запросов, сортировка, или статистические выражения для любого свойства обработки из индекса hello и эффективно обслуживать. Дополнительные сведения о выполнении индексирования в базе данных Azure Cosmos DB см. в руководстве об [индексировании без использования схем](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).

## <a name="next-steps"></a>Дальнейшие действия
* Создайте приложение графа [с использованием пакетов SDK](create-graph-dotnet.md). 
* Ознакомьтесь с [поддержкой графов в базе данных Azure Cosmos DB](graph-introduction.md).
