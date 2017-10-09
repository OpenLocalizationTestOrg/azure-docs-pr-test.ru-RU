---
title: "Управление aaaConcurrency и рабочей нагрузки в хранилище данных SQL | Документы Microsoft"
description: "Общие сведения управлении параллелизмом и рабочей нагрузкой в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL
toodeliver прогнозируемую производительность в масштабе, хранилище данных SQL Microsoft Azure помогает управлять уровней параллелизма и распределение ресурсов, таких как память и определения приоритетов ЦП. В этой статье понятия вы toohello управление параллелизмом и рабочей нагрузки, объясняется, как обе эти функции были реализованы и как ими можно было управлять в хранилище данных. Управление рабочими нагрузками хранилище данных SQL — предполагаемого toohelp поддержки многопользовательских средах. но не поддерживает мультитенантные рабочие нагрузки.

## <a name="concurrency-limits"></a>Пределы параллелизма
Хранилище данных SQL позволяет вверх too1 024 одновременных подключений. Все эти подключения могут одновременно отправлять запросы. Однако toooptimize пропускной способности, хранилище данных SQL может поставить в очередь tooensure некоторые запросы, что каждый запрос получает инструкции grant минимальный объем памяти. Постановка в очередь происходит во время выполнения запроса. По очереди запросов при параллелизма заполнится до предела, хранилище данных SQL можно увеличить общая пропускная способность за счет того, активных запросов get доступа toocritically необходимые ресурсы памяти.  

Предельные границы параллелизма в хранилище данных SQL зависят от двух значений: *количества одновременных запросов* и *количества слотов выдачи*. Для tooexecute запроса она должна выполняться в рамках hello предельное число параллелизма и выделение слота hello параллелизма.

* Параллельных запросов являются запросами hello, выполнению в hello же время. Хранилище данных SQL поддерживает до too32 параллельных запросов на больших размеров DWU hello.
* Слоты выдачи выделяются на основе DWU. Каждые 100 DWU обеспечивают 4 слота. Например, для DW100 выделяется 4 слота, а для DW1000 — 40 слотов. Каждый запрос использует один или несколько параллелизма разъемов, зависящее от hello [класс ресурсов](#resource-classes) hello запроса. Запросы, выполняемые в классе ресурса smallrc hello используют один слот параллелизма. Запросы, выполняемые с более высоким классом ресурсов, будут использовать больше слотов выдачи.

Hello следующей таблице описываются ограничения hello для параллельных запросов и слотов параллелизма в hello различных размеров DWU.

### <a name="concurrency-limits"></a>Пределы параллелизма
| DWU | Максимальное число одновременных запросов | Число выделенных слотов выдачи |
|:--- |:---:|:---:|
| DW100 |4. |4. |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

При достижении одного из этих пороговых значений, новые запросы помещаются в очередь и выполняются в порядке поступления.  Завершения запросов и число запросов и слоты hello упадет ниже ограничения hello, освобождаются в очереди запросов. 

> [!NOTE]  
> *Выберите* запросов, выполняющихся исключительно на динамические административные представления (DMV) или каким-либо ограничения параллелизма hello не определены представления каталога. Вы можете отслеживать hello системы независимо от hello число запросов, выполняющихся на нем.
> 
> 

## <a name="resource-classes"></a>Классы ресурсов
Ресурс классов помогают контролировать выделения памяти и ЦП с данным запросом tooa. Можно назначить два вида ресурсов классы tooa пользователя в форме hello ролей базы данных. Существуют следующие два типа ресурсов классов Hello.
1. Классы динамических ресурсов (**smallrc mediumrc, largerc xlargerc**) выделить переменный объем памяти в зависимости от hello текущей DWU. Это означает, что при вертикальном масштабировании tooa больше DWU запросы, автоматически получают больший объем памяти. 
2. Статические классы ресурсов (**staticrc10 staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) выделить hello такого же объема памяти, вне зависимости от hello текущей DWU (при условии, что hello DWU сам располагает достаточным объемом памяти). Это означает, что при большем значении DWU, можно выполнить дополнительные запросы в каждом классе ресурсов одновременно.

Для пользователей, использующих класс ресурсов **smallrc** и **staticrc10**, выделяется меньший объем памяти, и предоставляются большие возможности параллелизма. Напротив, пользователям назначены слишком**xlargerc** или **staticrc80** получают большой объем памяти, и поэтому меньше их запросы могут выполняться параллельно.

По умолчанию каждый пользователь является членом класса hello небольшой ресурсов **smallrc**. Здравствуйте, процедура `sp_addrolemember` — используется класс ресурса со tooincrease hello и `sp_droprolemember` — используется класс ресурсов toodecrease hello. Например, эта команда увеличивает класс ресурсов hello объекта loaduser слишком**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>Запросы, которые не учитывают классы ресурсов

Существует несколько типов запросов, которые не смогут воспользоваться преимуществами большего выделения памяти. Hello система игнорирует их класс выделения ресурсов и всегда вместо выполнения этих запросов в классе hello мало ресурсов. Если эти запросы всегда выполняются в классе мало ресурсов hello, они могут выполняться, когда ячеек с параллелизмом, при недостатке свободной и они не будет использовать дополнительные слоты, чем требуется. Дополнительные сведения см. в разделе [Исключения для запросов в отношении ограничений параллелизма](#query-exceptions-to-concurrency-limits).

## <a name="details-on-resource-class-assignment"></a>Дополнительные сведения о назначении классов ресурсов


Ниже приведены дополнительные сведения о классах ресурсов.

* *Изменение роли* требуется разрешение toochange hello ресурсов класса пользователя.
* Несмотря на то, что можно добавить tooone пользователя или более высокие классы ресурсов hello, динамический ресурс классы имеют приоритет над классы статический ресурс. То есть если пользователю назначено tooboth **mediumrc**(динамически) и **staticrc80**(статический), **mediumrc** — класс ресурсов hello, учитывается.
 * При назначении пользователю toomore, чем класс один ресурс в типе класса конкретный ресурс (более одного класса динамический ресурс или несколько классов статический ресурс), принимается класс ресурсов наибольший hello. То есть если пользователю назначено tooboth mediumrc и largerc, учитывается выше hello класс ресурсов (largerc). И, если пользователю назначено tooboth **staticrc20** и **statirc80**, **staticrc80** обрабатывается.
* Класс ресурсов Hello hello системы администрирования пользователя нельзя.

Подробное описание примера см. в разделе [Пример изменения класса ресурсов пользователя](#changing-user-resource-class-example).

## <a name="memory-allocation"></a>Выделение памяти
Существуют преимущества и недостатки tooincreasing класс ресурса пользователя. Увеличение класс ресурсов для пользователя, предоставляет их запросы доступа toomore памяти, что может означать, что запросы выполняются быстрее.  Однако классы более высокого ресурсов также уменьшить hello числа параллельных запросов, которые могут выполняться. Это hello компромисса между выделения больших объемов памяти tooa одного запроса или разрешить другие запросы, которые также должны распределения памяти, toorun одновременно. Если один пользователь имеет высокий уровень выделение памяти для запроса, другие пользователи не получат доступ toothat же toorun памяти запроса.

в следующей таблице Hello сопоставляет hello память, выделенную распространения tooeach DWU и ресурсов класса.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>Выделение памяти на распределение для классов динамических ресурсов (в МБ)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1 600 |
| DW500 |100 |400 |800 |1 600 |
| DW600 |100 |400 |800 |1 600 |
| DW1000 |100 |800 |1 600 |3200 |
| DW1200 |100 |800 |1 600 |3200 |
| DW1500 |100 |800 |1 600 |3200 |
| DW2000 |100 |1 600 |3200 |6400 |
| DW3000 |100 |1 600 |3200 |6400 |
| DW6000 |100 |3200 |6400 |12 800 |

в следующей таблице Hello сопоставляет hello память, выделенную распространения tooeach DWU и класс статический ресурс. Обратите внимание, что классы более высокого ресурсов hello их память сокращение ограничения глобальных DWU toohonor hello.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>Выделение памяти на распределение для классов статических ресурсов (в МБ)
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1 600 |1 600 |1 600 |1 600 |
| DW500 |100 |200 |400 |800 |1 600 |1 600 |1 600 |1 600 |
| DW600 |100 |200 |400 |800 |1 600 |1 600 |1 600 |1 600 |
| DW1000 |100 |200 |400 |800 |1 600 |3200 |3200 |3200 |
| DW1200 |100 |200 |400 |800 |1 600 |3200 |3200 |3200 |
| DW1500 |100 |200 |400 |800 |1 600 |3200 |3200 |3200 |
| DW2000 |100 |200 |400 |800 |1 600 |3200 |6400 |6400 |
| DW3000 |100 |200 |400 |800 |1 600 |3200 |6400 |6400 |
| DW6000 |100 |200 |400 |800 |1 600 |3200 |6400 |12 800 |

Из hello предшествующей таблице, можно видеть, что запрос на DW2000 в hello **xlargerc** класс ресурсов будет иметь доступ too6, 400 МБ памяти в пределах каждой hello 60 распределенных баз данных.  В хранилище данных SQL используется 60 распределений. Таким образом toocalculate hello общая память, выделенная для запроса в классе данного ресурса, hello выше значения необходимо будет умножено на 60.

### <a name="memory-allocations-system-wide-gb"></a>Выделение памяти для всей системы (ГБ)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

Из этой таблицы распределения памяти во всей системе, можно увидеть, что запрос на DW2000 в классе ресурса xlargerc hello выделена общий 375 ГБ памяти (распределения 6 400 МБ * 60 / 1024 tooconvert tooGB) на время всего hello хранилище данных SQL.

Hello же применяется вычисление классов toostatic ресурсов.
 
## <a name="concurrency-slot-consumption"></a>Использование слотов выдачи  
Хранилище данных SQL предоставляет дополнительные tooqueries памяти, работающих в более высоких классов ресурса. Память — фиксированный ресурс.  Таким образом hello выделена дополнительная память каждого запроса, hello, которые можно выполнять меньшее число параллельных запросов. Hello следующей таблице reiterates все предыдущие принципы hello в одном представлении, показывающая количество hello параллелизма слоты, имеющиеся по DWU и слоты hello, потребляемых каждого класса ресурсов.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>Выделение и использование слотов параллельности для классов динамических ресурсов  
| DWU | Максимальное число одновременных запросов | Число выделенных слотов выдачи | Слоты, используемые smallrc | Слоты, используемые mediumrc | Слоты, используемые largerc | Слоты, используемые xlargerc |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4. |4. |1 |1 |2 |4. |
| DW200 |8 |8 |1 |2 |4. |8 |
| DW300 |12 |12 |1 |2 |4. |8 |
| DW400 |16 |16 |1 |4. |8 |16 |
| DW500 |20 |20 |1 |4. |8 |16 |
| DW600 |24 |24 |1 |4. |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>Выделение и использование слотов выдачи для классов статических ресурсов  
| DWU | Максимальное число одновременных запросов | Число выделенных слотов выдачи |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4. |4. |1 |2 |4. |4. |4. |4. |4. |4. |
| DW200 |8 |8 |1 |2 |4. |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4. |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4. |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4.| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4.| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4.| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4.| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4.| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4.| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4.| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4.| 8| 16| 32| 64| 128|

В этих таблицах можно увидеть, что хранилище данных SQL при использовании DW1000 обрабатывает до 32 параллельных запросов и может выделить 40 слотов выдачи. Если все пользователи работают с классом smallrc, то будет разрешено выполнять 32 параллельных запроса, так как каждый запрос использует 1 слот выдачи. Если всем пользователям DW1000 были запущены в mediumrc, каждый запрос должен размещаться 800 МБ на распространение для выделения общей памяти 47 ГБ каждого запроса и параллелизма бы пользователям ограниченный too5 (40 слоты параллелизма 8 слотов на mediumrc пользователя и).

## <a name="selecting-proper-resource-class"></a>Выбор правильного класса ресурсов  
Рекомендуется назначить пользователей toopermanently tooa-класс ресурсов, вместо изменения их классов ресурсов. Например таблиц columnstore tooclustered загружает создавать индексы более высокого качества, при выделении памяти. tooensure загружает памяти toohigher доступа, создайте пользователя специально для загрузки данных и назначить этого пользователя tooa выше ресурсов класса без возможности восстановления.
Существует несколько лучшие методики toofollow здесь. Как упоминалось выше, хранилище данных SQL поддерживает два вида типов классов ресурсов: классы статических ресурсов и классы динамических ресурсов.
### <a name="loading-best-practices"></a>Рекомендации по загрузкам
1.  Если ожиданиям hello загрузок с помощью обычных объем данных, класс статический ресурс является хорошим выбором. Позже при масштабировании tooget дополнительные вычислительные возможности, хранилище данных hello, смогут toorun несколько параллельных запрашивает out-of--box, как пользователь нагрузки hello не больше памяти.
2.  Если полная загружает ожиданиям hello в некоторых случаях, класс динамический ресурс является хорошим выбором. Позже, при вертикальном масштабировании tooget большей вычислительной мощности, hello нагрузки пользователь получит несколько памяти out-of--box, таким образом позволяя tooperform нагрузки hello быстрее.

Hello загружает tooprocess объем памяти, необходимый эффективно зависит от природы hello загрузить таблицу hello и hello объем обработки данных. Для экземпляра загрузка данных в таблицы CCI требуются некоторые rowgroups CCI toolet памяти достичь оптимальность. Дополнительные сведения см. в разделе индексы Columnstore hello - руководство загрузки данных.

Как правило, мы рекомендуем toouse менее 200 МБ памяти для загрузки.

### <a name="querying-best-practices"></a>Рекомендации по выполнению запросов
Запросы имеют различные требования в зависимости от их сложности. Увеличить объем памяти для запроса или увеличение параллелизма hello являются оба tooaugment допустимые способы общую пропускную способность, в зависимости от потребностей hello запроса.
1.  Если hello ожидания обычных, сложные запросы (например, toogenerate ежедневно и еженедельно отчеты) и не обязательно tootake преимуществами параллелизма, класс динамический ресурс является хорошим выбором. Если системе hello tooprocess дополнительные данные, масштабирование hello хранилище данных таким образом автоматически предоставят дополнительные памяти toohello пользователь, выполняющий запрос hello.
2.  Если hello ожиданиям, переменной или diurnal паралеллизма (для экземпляра Если hello базы данных запрашивается через веб-интерфейса широко доступны), класс статический ресурс является хорошим выбором. Позже, при масштабировании хранилища toodata hello пользователя, связанного с классом hello статический ресурс будет автоматически быть может toorun несколько параллельных запросов.

Выбор правильного память, в зависимости от необходимости hello запроса не так просто, как он зависит от многих факторов, таких как hello объем данных, запрошенных, hello характер hello схем таблиц и различных соединения, выбора и предикаты группы. С точки зрения Общие, выделить больше памяти, позволит toocomplete запросов быстрее, но уменьшится hello общую параллелизма. Если низкий уровень параллелизма не является проблемой, чрезмерное выделение памяти не нанесет вреда. может потребоваться toofine настройки пропускной способности при различных конфигурациях ресурсов классов.

Можно использовать следующие hello хранимой процедуры toofigure out grant параллелизма и памяти на каждый класс ресурсов на заданной цели уровня Обслуживания и hello ближайший наиболее ресурсов класс для операций служб с интенсивными вычислениями CCI памяти для несекционированной таблицы CCI на класс данного ресурса:

#### <a name="description"></a>Описание:  
Вот hello цель этой хранимой процедуры.  
1. toohelp закончится пользователя grant параллелизма и памяти на каждый класс ресурсов на заданной цели. Пользователь должен tooprovide значение NULL для схемы и tablename для этого, как показано в приведенном ниже примере hello.  
2. пользователь toohelp понять, hello ближайший наиболее класс ресурсов для hello памяти intensed CCI операций (нагрузки Копировать таблиц перестроения индекса, т. д.) не секционированной таблицы CCI на класс данного ресурса. Hello хранимой процедуры используется toofind схемы таблицы out grant hello требуемый объем памяти для этого.

#### <a name="dependencies--restrictions"></a>Зависимости и ограничения
- Данная хранимая процедура не спроектированных toocalculate требования к памяти для таблицы секционированы cci.    
- Данная хранимая процедура не принимает требования к памяти в учетную запись для hello части SELECT CTAS/INSERT-Выбор и предполагает, что он toobe простой запрос SELECT.
- Данная хранимая процедура использует временную таблицу, чтобы это можно было использовать в сеансе hello которой был создан этот хранимая процедура.    
- Данная хранимая процедура зависит от текущего предложения hello (например, конфигурации оборудования, DMS конфигурации) и при изменении любого из, затем данная хранимая процедура не будет работать правильно.  
- Данная хранимая процедура зависит от существующего предлагаемого ограничения параллелизма, и если он изменится, то данная хранимая процедура будет работать неправильно.  
- Данная хранимая процедура зависит от существующих предложений класса ресурсов, и если они изменится, то данная хранимая процедура будет работать неправильно.  

>  [!NOTE]  
>  Если вы не получаете выходные данные после выполнения хранимой процедуры с предоставленными параметрами, тогда возможны два варианта. <br />1. Один из параметров хранилища данных содержит недопустимое значение SLO. <br />2. Отсутствует соответствующий класс ресурсов для операции CCI, если было указано имя таблицы. <br />Например в DW100, наибольший предоставления памяти составляет 400 МБ и если таблица имеет схему широкий достаточно toocross hello требование 400 МБ.
      
#### <a name="usage-example"></a>Пример использования
Синтаксис:  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Укажите параметр NULL tooextract hello текущей DWU из hello базе данных Хранилища данных или укажите любой поддерживаемый DWU в форме «DW100» hello
2. @SCHEMA_NAME:Введите имя схемы таблицы hello
3. @TABLE_NAME:Введите имя таблицы, представляющие интерес hello

Примеры выполнения этой хранимой процедуры.  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

Table1, используемых в hello выше примеры можно рассматривать как показано ниже:  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Вот определение hello хранимой процедуры.
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>Приоритет при выполнении запросов
Классы ресурсов в хранилище данных SQL реализованы с помощью групп рабочей нагрузки. Существует всего восемь группы рабочей нагрузки, которые управляют поведением hello hello ресурсов классов через hello различных размеров DWU. Для любого DWU хранилище данных SQL используется только четыре из восьми групп рабочей нагрузки hello. Это разумно, так как каждая группа рабочей нагрузки назначен tooone четыре ресурсов классов: smallrc mediumrc, largerc, или xlargerc. Hello важность понимания hello группы рабочей нагрузки, что некоторые из этих групп рабочей нагрузки набора toohigher *важность*. Значение приоритета используется при планировании распределения ресурсов ЦП. Запросы, которым назначен высокий приоритет, получают в три раза больше циклов ЦП, чем запросы со средним приоритетом. Поэтому сопоставление слотов выдачи также определяет приоритет ЦП. Если для выполнения запроса используется 16 или больше слотов, он помечается как запрос с высоким приоритетом.

Hello Следующая таблица показывает сопоставления hello важность для каждой группы рабочей нагрузки.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>Слоты tooconcurrency сопоставления группы рабочей нагрузки и важности
| Группы рабочей нагрузки | Сопоставление слотов выдачи | МБ/распределение | Приоритет |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |Средний |
| SloDWGroupC01 |2 |200 |Средний |
| SloDWGroupC02 |4. |400 |Средний |
| SloDWGroupC03 |8 |800 |Средний |
| SloDWGroupC04 |16 |1 600 |Высокий |
| SloDWGroupC05 |32 |3200 |Высокий |
| SloDWGroupC06 |64 |6400 |Высокий |
| SloDWGroupC07 |128 |12 800 |Высокий |

Из hello **распределения и потребления слотов параллелизма** диаграммы, можно увидеть, что DW500 используется 1, 4, 8 или 16 параллелизма слотов для smallrc, mediumrc, largerc и xlargerc, соответственно. Эти значения можно искать в hello предшествующий важность hello toofind диаграммы для каждого класса ресурсов.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>Сопоставление DW500 tooimportance классы ресурсов
| Класс ресурсов | Группа рабочей нагрузки | Число используемых слотов выдачи | МБ/распределение | приоритет |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |Средний |
| mediumrc |SloDWGroupC02 |4. |400 |Средний |
| largerc |SloDWGroupC03 |8 |800 |Средний |
| xlargerc |SloDWGroupC04 |16 |1 600 |Высокий |
| staticrc10 |SloDWGroupC00 |1 |100 |Средний |
| staticrc20 |SloDWGroupC01 |2 |200 |Средний |
| staticrc30 |SloDWGroupC02 |4. |400 |Средний |
| staticrc40 |SloDWGroupC03 |8 |800 |Средний |
| staticrc50 |SloDWGroupC03 |16 |1 600 |Высокий |
| staticrc60 |SloDWGroupC03 |16 |1 600 |Высокий |
| staticrc70 |SloDWGroupC03 |16 |1 600 |Высокий |
| staticrc80 |SloDWGroupC03 |16 |1 600 |Высокий |

Можно использовать при устранении неполадок следующие toolook запрос динамического административного Представления в hello различия в выделении ресурсов памяти подробно с точки зрения hello hello регулятора ресурсов или tooanalyze active и за прошедший период использования групп рабочей нагрузки hello hello.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>Запросы, учитывающие пределы параллелизма
Большинство запросов управляются классами ресурсов. Эти запросы должен лежать в пределах параллельных запросов hello и пороговые значения слота параллелизма. Пользователь нельзя выбрать tooexclude запроса из модели слот hello параллелизма.

tooreiterate, hello следующие инструкции выполнять классов ресурсов.

* INSERT SELECT
* UPDATE
* УДАЛИТЬ
* SELECT (при запросе таблиц пользователя)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* ALTER TABLE REBUILD
* CREATE INDEX
* CREATE CLUSTERED COLUMNSTORE INDEX
* CREATE TABLE AS SELECT (CTAS)
* Загрузка данных
* Операции перемещения данных, осуществляемые hello службы перемещения данных (DMS)

## <a name="query-exceptions-tooconcurrency-limits"></a>Запрос исключений tooconcurrency ограничения
Некоторые запросы не учитывают hello ресурсов класса toowhich hello пользователю назначается. Ограничения параллелизма toohello эти исключения при внесении hello ресурсов памяти, необходимый для определенной команды низкое значение, часто из-за hello команда — это операция метаданных. Цель Hello эти исключения — tooavoid больше операций выделения памяти для запросов, которые никогда не должны их. В таких случаях по умолчанию hello мало ресурсов класса (smallrc) всегда используется независимо от того, класс фактический ресурс hello назначенный пользователь toohello. Например, `CREATE LOGIN` всегда будет работать с классом smallrc. Hello toofulfill ресурсы, необходимые этой операции являются очень мало, поэтому не вносит в него смысле tooinclude hello запроса в модели слот параллелизма hello.  Эти запросы также не ограничивается предел параллелизма пользователя hello 32, неограниченное число таких запросов можно запустить копирование ограничение сеансов toohello 1 024 сеансов.

Привет, следующие инструкции, не учитывают классов ресурсов:

* CREATE или DROP TABLE;
* ALTER TABLE ... SWITCH, SPLIT или MERGE PARTITION;
* ALTER INDEX DISABLE
* DROP INDEX
* CREATE, UPDATE или DROP STATISTICS;
* TRUNCATE TABLE
* ALTER AUTHORIZATION
* CREATE LOGIN
* CREATE, ALTER или DROP USER;
* CREATE, ALTER или DROP PROCEDURE;
* CREATE или DROP VIEW;
* INSERT VALUES
* SELECT (из системных представлений и динамических административных представлений);
* EXPLAIN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a> Пример изменения класса ресурсов пользователя
1. **Создайте имя входа:** откройте tooyour подключения **master** базы данных на hello SQL server для размещения базы данных хранилища данных SQL и выполните следующие команды hello.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > Это разумно toocreate пользователя в базе данных master hello для пользователей в хранилище данных SQL Azure. Создание пользователя в базе данных master позволяет toologin пользователя, с помощью таких средств, как среда SSMS без указания имени базы данных.  Он также позволяет им toouse hello объекта обозревателя tooview все базы данных на SQL server.  Дополнительные сведения о создании пользователей и управлении ими см. в статье [Защита базы данных в хранилище данных SQL][Secure a database in SQL Data Warehouse].
   > 
   > 
2. **Создание пользователя в хранилище данных SQL:** откройте toohello подключения **хранилище данных SQL** базы данных и выполните следующую команду hello.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **Предоставление разрешений:** hello следующий пример предоставляет `CONTROL` на hello **хранилище данных SQL** базы данных. `CONTROL`в hello уровень базы данных является Здравствуйте, эквивалентные роли db_owner в SQL Server.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **Увеличить класс ресурсов:** используйте hello следующий запрос tooadd tooa выше рабочей нагрузки управления роли пользователя.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **Уменьшить класс ресурсов:** используйте hello следующий запрос tooremove пользователя из роли управления рабочей нагрузки.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > Это не возможные tooremove пользователь из smallrc.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>Представление, используемое для определения запросов, поставленных в очередь, и другие динамические административные представления
Можно использовать hello `sys.dm_pdw_exec_requests` запросы динамического административного Представления tooidentify, ожидающих в очереди с параллелизмом. Запросы, ожидающие выделения слота выдачи, будет находиться в **приостановленном**состоянии.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

Чтобы просмотреть роли управления рабочей нагрузкой, можно использовать представление `sys.database_principals`.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

приветствия при следующем запросе показано, какие роли назначается каждому пользователю.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

Хранилище данных SQL имеет следующие hello типах ожидания.

* **LocalQueriesConcurrencyResourceType**: запросы, которые находятся за пределами framework слот hello параллелизма. В качестве примеров таких запросов можно привести запросы и системные функции динамических административных представлений, такие как `SELECT @@VERSION` .
* **UserConcurrencyResourceType**: запросы, которые находятся внутри framework слот hello параллелизма. В качестве примеров использования этого типа ресурсов можно привести запросы к таблицам пользователя.
* **DmsConcurrencyResourceType**относится к ожиданиям, связанным с операциями перемещения данных.
* **BackupConcurrencyResourceType**может использоваться при создании резервной копии базы данных. Hello максимальное значение для этого типа ресурса равно 1. Если несколько операций резервного копирования были запрошены на hello то же время, другим пользователям в очередь hello.

Hello `sys.dm_pdw_waits` динамического административного Представления можно использовать toosee, какие ресурсы запрос ожидает.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

Hello `sys.dm_pdw_resource_waits` динамическое административное Представление показывает только ожидания hello ресурсов, потребляемых данного запроса. Время ожидания ресурса только измеряет hello времени ожидания ресурсов toobe указано, как противоположность toosignal ожидания времени, которое hello время, необходимое для hello базовый запрос hello tooschedule серверы SQL на ЦП hello.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

Hello `sys.dm_pdw_wait_stats` динамического административного Представления можно использовать для анализа исторических тенденций ожиданий.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об управлении пользователями и безопасностью базы данных см. в статье [Защита базы данных в хранилище данных SQL][Secure a database in SQL Data Warehouse]. Дополнительные сведения о классах большие ресурсов может повысить качество кластеризованный индекс, см. в разделе [перестроение индексов tooimprove сегмент качество].

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[перестроение индексов tooimprove сегмент качество]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
