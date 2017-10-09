---
title: "aaaFind данных с помощью поиска журналов в службе анализа журналов Azure | Документы Microsoft"
description: "Поиск по журналам позволяют toocombine и сопоставлять данные компьютеров из нескольких источников в существующей среде."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Поиск данных по журналам в Log Analytics

>[!NOTE]
> В этой статье описывается использование hello текущий язык запроса в службе анализа журналов запросов поиска журналов.  Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то вы должны обращаться слишком[основные сведения о журнале ищет в службе анализа журналов (новый)](log-analytics-log-search-new.md).


В основе hello аналитики журналов является функция поиска журналов hello, позволяющий toocombine и сопоставлять данные компьютеров из нескольких источников в существующей среде. Решения также берутся из журнала поиска toobring сведенных вы показатели по определенной проблемной области.

На странице поиска hello можно создать запрос и затем при поиске, можно фильтровать результаты hello с помощью элементов управления аспектами. Также можно создать сложные запросы tootransform, фильтрации и отчетов результатов.

Общие запросы поиска журналов отображаются на большинстве страниц решений. В консоли hello OMS можно щелкать плитки или детализировать элементы tooother tooview сведения об элементе hello с помощью функции поиска журналов.

В этом учебнике мы рассмотрим примеры toocover все основы hello при использовании поиска журналов.

Мы начинаться с простых практических примеров и затем разовьем их, чтобы получить представление о способе toouse hello синтаксис tooextract hello аналитики из данных hello реальных вариантах.

После ознакомления с методиками поиска можно просмотреть hello [Справочник поиска журнала анализа журналов](log-analytics-search-reference.md).

## <a name="use-basic-filters"></a>использование базовых фильтров;
Hello первое, что tooknow — что hello первая часть запрос поиска перед любым» | «символ вертикальной черты, всегда *фильтра*. Его можно рассматривать как предложение WHERE в TSQL, он определяет *что* подмножество toopull данные из хранилища данных OMS hello. Поиск в хранилище данных hello главным образом заключается указания характеристики hello hello данных необходимо tooextract, поэтому логично, что запрос будет начинаться с предложения WHERE hello.

Hello самый простой из доступных фильтров являются *ключевые слова*, такие как «ошибка», «время ожидания» или имя компьютера. Эти типы простых запросов обычно возвращают различные формы данных в рамках hello же результирующего набора. Так как служба аналитики журналов содержит различные *типы* данных в системе hello.

### <a name="tooconduct-a-simple-search"></a>tooconduct простого поиска
1. На портале OMS hello щелкните **поиска журналов**.  
    ![плитка поиска](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. Введите в поле запроса hello `error` и нажмите кнопку **поиска**.  
    ![ошибка поиска](./media/log-analytics-log-searches/oms-search-error.png)  
    Например, запрос hello для `error` hello следующем рисунке возвратил 100 000 **событий** записей (собранных функцией управления журналами), 18 **ConfigurationAlert** записей (созданных в ходе настройки Оценка) и 12 **ConfigurationChange** записей (полученных функцией отслеживания изменений hello).   
    ![результаты поиска](./media/log-analytics-log-searches/oms-search-results01.png)  

Эти фильтры на самом деле не являются классами и типами объектов. *Тип* просто тег, или свойство или строка/имя/категория, присоединенные tooa части данных. Некоторые документы в системе hello помечены как **Type: ConfigurationAlert** и другие помечены как **типа: производительности**, или **Type: Event**, и т. д. Каждый результат поиска, документ, записи или запись отображает все общие свойства hello и их значения для каждого из этих фрагментов данных, а также можно использовать эти toospecify имена полей в фильтре hello при необходимости tooretrieve только записи hello где hello поле имеет заданное значение.

*Type* — это просто поле, которое имеет все записи, оно ничем не отличается от любого другого поля. Это было установлено на основе значения hello поля типа hello. Эта запись будет иметь другую форму. Кстати **тип = Perf**, или **тип события =** также является hello синтаксиса, что toolearn tooquery событий или данных о производительности.

Двоеточие (:) или знак равенства (=) можно использовать после имени поля hello и перед значением hello. **Type: Event** и **тип события =** являются одинаковое значение, можно выбрать hello стиль, который вы предпочитаете.

Поэтому, если hello введите = Perf записи имеют поле с именем «CounterName», а затем можно написать запрос наподобие `Type=Perf CounterName="% Processor Time"`.

Это позволит получить только данные о производительности hello где hello счетчик производительности имеет имя «% Processor Time».

### <a name="toosearch-for-processor-time-performance-data"></a>toosearch для данных производительности по загруженности процессора
* Введите в поле запроса поиска hello`Type=Perf CounterName="% Processor Time"`

Можно также указать значение более точно и использовать **InstanceName = _ 'Total'** в запросе hello, который представляет собой счетчик производительности Windows. Можно также выбрать другой аспект и другую пару **поле:значение**. Hello фильтр автоматически добавляется tooyour фильтра панели запроса hello. Это можно увидеть в hello после изображения. Показано, где tooclick tooadd **InstanceName: '_Total'** toohello запроса, не вводя никакого текста.

![аспект поиска](./media/log-analytics-log-searches/oms-search-facet.png)

Ваш запрос превращается в `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

В этом примере нет toospecify **тип = Perf** tooget toothis результат. Так как hello поля CounterName и InstanceName существуют только для записей Type = Perf hello запроса является достаточно точным, tooreturn hello такие же результаты, как hello и предыдущий более длинный:

```
CounterName="% Processor Time" InstanceName="_Total"
```

Это, поскольку все фильтры hello в запросе hello вычисляются как если бы *AND* друг с другом. По сути, hello дополнительные поля, добавить критерии toohello, вы получаете менее точные и детальные результаты.

Например, запрос hello `Type=Event EventLog="Windows PowerShell"` идентичен слишком`Type=Event AND EventLog="Windows PowerShell"`. Он возвращает все события, которые были зарегистрированы и собраны из журнала событий Windows PowerShell hello. Если вы добавляете фильтр несколько раз, выбрав приветствия же аспект, затем hello проблема является совершенно формальной — он может загромождать панель поиска hello, но она по-прежнему возвращает hello же результаты, так как hello неявный оператор и всегда присутствует несколько раз.

Вы можете легко обратить неявный оператор и hello с помощью явного оператора NOT. Например:

`Type:Event NOT(EventLog:"Windows PowerShell")`или его эквивалент `Type=Event EventLog!="Windows PowerShell"` возвращают все события из всех журналов, которые не являются журналами Windows PowerShell hello.

Либо можно использовать другой логический оператор, такой как ИЛИ (OR). Hello следующий запрос возвращает записи, для которых hello EventLog имеет значение Application или System.

```
EventLog=Application OR EventLog=System
```

С помощью hello выше запрос, вы получаете записи для обоих журналов в hello же результирующего набора.

Однако при удалении hello или, оставив неявный hello и на месте, то hello следующий запрос не даст никаких результатов, так как запись журнала событий, к которому относится tooBOTH журналы, не существует. Каждая запись журнала событий была записана tooonly один из двух журналов hello.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>использование дополнительных фильтров;
Hello следующий запрос возвращает записи для 2 журналов событий для всех компьютеров hello, которые отправляли данные.

```
EventLog=Application OR EventLog=System
```

![результаты поиска](./media/log-analytics-log-searches/oms-search-results03.png)

При выборе одного из полей hello или фильтры, можно провести hello запроса tooa конкретного компьютера, исключив все остальные. Hello результирующий запрос будет выглядеть следующим образом следующие hello.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Это следующие эквивалентные toohello из-за hello неявного оператора и.

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

Каждый запрос вычисляется в явной последовательностью hello. Примечание hello скобки.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Так же, как hello полем журнала событий, можно извлечь данные только для набора определенных компьютеров путем добавления или. Например:

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

Аналогичным образом, этот hello следующих запроса возвращают **% времени ЦП** hello выбранного только двух компьютеров.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>Типы полей
При создании фильтров, следует учитывать hello различия в работе с различными типами полей, возвращаемых из запросов поиска журналов.

**Поля, доступные для поиска,** выделены синим цветом в результатах.  Можно использовать для поиска полей в поля конкретного toohello условия поиска, например hello следующие:

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

**Поля с возможностью поиска произвольного текста** выделены серым цветом в результатах поиска.  Они не может использоваться с поле toohello конкретных условий поиска, как поля поиска.  Осуществляется только при выполнении запроса для всех полей, например следующих hello.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>Логические операторы
С помощью полей даты и времени и числовых полей можно выполнить поиск значений с помощью операторов *больше*, *меньше* и *меньше или равно*. Можно использовать простые операторы, такие как >, <>, =, < =,! = в строке поиска hello запроса.

Можно запросить журнал событий за конкретный период времени. Например hello последние 24 часа выражается с hello следующее мнемоническое выражение.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>с помощью логического оператора toosearch
* Введите в поле запроса поиска hello`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![поиск с логическими операторами](./media/log-analytics-log-searches/oms-search-boolean.png)

Несмотря на то, что можно управлять графически hello интервал времени, а большая часть времени может потребоваться toodo, что существуют преимущества tooincluding фильтра времени непосредственно в запрос hello. Например, это прекрасно работает с панелями мониторинга, где можно переопределить время hello для каждой плитки независимо от hello *глобальной* селектора времени на странице панели мониторинга hello. Дополнительные сведения см. в статье [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/) (Аспекты использования времени на панели мониторинга).

При фильтрации по времени, имейте в виду, что можно получить результаты для hello *пересечение* из hello двух периодов: hello, указанному в hello портал OMS (S1) и Здравствуйте, указанному в запросе hello (S2).

![пересечению](./media/log-analytics-log-searches/oms-search-intersection.png)

Это означает, что если hello периоды не пересекаются, например на портале OMS hello, где выбрано **на этой неделе** и в запросе hello, где определена **прошлой неделе**, то нет пересечение отсутствует, и вы не Получите никаких результатов.

Операторы сравнения, используемые для поля TimeGenerated hello можно также в других ситуациях. Например, для числовых полей.

К примеру Предположим, что оповещения оценки конфигурации имеют следующие уровни серьезности hello:

* 0 = информационный
* 1 = предупреждение
* 2 = критический

Можно запросить предупреждения и критические оповещения, а также исключить информационные оповещения с приветствия при следующем запросе:

```
Type=ConfigurationAlert  Severity>=1
```


Можно также использовать запросы в диапазоне. Это означает, что может предоставить hello начало и конец диапазона значений в последовательности. Например, если события из журнала событий Operations Manager hello там, где hello EventID — больше или равно too2100, но не больше 2199, а затем приветствия при следующем запросе позволит получить их.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> необходимо использовать синтаксис диапазона Hello — hello двоеточие (:): значение поля и *не* hello знак равенства (=). Заключите hello нижнюю и верхнюю границу диапазона hello в квадратные скобки, разделив их двумя точками (..).
>
>

## <a name="manipulate-search-results"></a>работа с результатами поиска;
При поиске данных вам требуется toorefine запрос поиска и наличие высокого уровня контроля над hello результаты. При извлечении результатов можно применять команды tootransform их.

Команды в поиске анализа журналов *должен* следовать после символа hello вертикальной черты (|). Фильтр должен всегда быть hello первой части строки запроса. Он определяет набор данных hello, с которыми работает, а затем» направляет эти результаты в команду. Затем можно использовать дополнительные команды hello канала tooadd. Это приблизительно конвейера toohello Windows PowerShell.

В общем случае язык поиска аналитики журналов hello пытается toomake стилю и правилам PowerShell toofollow ИТ аналогичные toohello ИТ-специалисты и tooease hello обучения.

Команды имеют форму глаголов, чтобы можно было легко понять, что именно они делают.  

### <a name="sort"></a>Сортировать
Команда sort Hello позволяет hello toodefine сортировку по одному или нескольким полям. Даже если вы не используете ее, по умолчанию применяется сортировка по времени в порядке убывания. Hello самые новые результаты всегда находятся в hello верхней части результатов поиска. Это означает, что при выполнении поиска с учетом `Type=Event EventID=1234` реально выполняется следующее:

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

Это, так как он является типом hello возможности, знакомые с в журналах. Например в hello в окне просмотра событий Windows.

Можно использовать результаты toochange hello способ сортировки. Hello следующих примерах показано, как это работает.

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


Hello простые примеры выше показывают работу команды: они изменяют форму hello hello результатов, фильтр вернул hello.

### <a name="limit-and-top"></a>Limit и top
Другой менее известной командой является LIMIT. Эта команда похожа на команды PowerShell. Предел — идентичных по функциональности toohello команде TOP. Hello следующие запросы возвращают hello одинаковые результаты.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>toosearch с помощью предложения top
* Введите в поле запроса поиска hello`Type=Event EventID=600 | Top 1`   
    ![поиск лучших результатов](./media/log-analytics-log-searches/oms-search-top.png)

Hello рисунке выше, 358 тысяч записей с EventID = 600. Здравствуйте, поля, аспекты и фильтры для hello слева всегда отображаются сведения о hello результаты, возвращаемые *частью фильтра hello* запросе hello, которая входит в состав hello до знака вертикальной черты. Hello **результатов** возвращает только самые последние 1 hello результат, так как команда в примере hello форму результатов и преобразовала hello.

### <a name="select"></a>Выберите пункт
Hello команда SELECT похожа на команду Select-Object в PowerShell. Она возвращает отфильтрованные результаты, имеющие не все свои первоначальные свойства. Вместо этого она выбирает только hello вами свойства.

#### <a name="toorun-a-search-using-hello-select-command"></a>toorun поиска с использованием команды select hello
1. В поле поиска введите `Type=Event` и нажмите кнопку **Поиск**.
2. Нажмите кнопку **+ Дополнительно** в одном tooview результаты hello, имеют все свойства hello, hello результаты.
3. Выберите некоторые из них явным образом и hello изменения запроса слишком`Type=Event | Select Computer,EventID,RenderedDescription`.  
    ![поиск с помощью select](./media/log-analytics-log-searches/oms-search-select.png)

Эта команда особенно полезен, если необходимо toocontrol выходными данными поиска и отбирать только hello фрагменты данных, которые важны для проводимого исследования, а не полный спектр записей hello. Это также полезно, когда записи различных типов имеют *несколько* общих свойств, но не *все* их свойства являются общими. , Можно сформировать выходные данные, более естественным образом выглядит как таблицу или удобны для экспорта tooa CSV-файл и последующей обработки в Excel.

## <a name="use-hello-measure-command"></a>Использование команды measure hello
MEASURE является одной из hello наиболее универсальных команд в поиске анализа журналов. Оно позволяет tooapply статистические *функции* tooyour данным и агрегировать результаты, сгруппированные по заданному полю. Существует несколько статистических функций, поддерживаемых командой Measure.

### <a name="measure-count"></a>Measure count()
Hello первой статистической функцией toowork с, и один из простой toounderstand hello hello *count()* функции.

Результатов любого поискового запроса, например `Type=Event`, отображаются фильтры, которые также называются аспектами на hello левая сторона результатов поиска. Hello фильтры показывают распределение значений по заданному полю для hello результатов выполненного поиска hello.

![поиск с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

Например, в hello изображения выше вы увидите hello **компьютера** поле и он показывает, что в пределах hello почти 739 тысячи событий в результатах hello 68 уникальных значений для hello **компьютер** поле в этих записях. Hello плитке отображаются только hello пяти, hello наиболее распространенные значений, которые записаны в hello **компьютера** полей), с сортировкой по hello количество документов, содержащих это конкретное значение в этом поле. В образ hello, вы увидите, что среди почти 369 тысячи событий 90 тысяч поступают с компьютера OpsInsights04.contoso.com hello, 83 тысячи — с компьютера DB03.contoso.com hello и т. д.

Что делать, если требуется toosee всех значений, поскольку hello плитке отображаются только только hello пяти?

Вот какие меры hello команды можно сделать с помощью функции count() hello. Эта функция не использует никаких параметров. Просто укажите поле hello, по которому требуется toogroup, — hello **компьютера** в данном случае:

`Type=Event | Measure count() by Computer`

![поиск с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

Однако **Computer** — это просто поле, используемое *в* каждом фрагменте данных. Нет никаких реляционных баз данных и никакого отдельного объекта **Computer**. Просто hello значения *в* hello данных могут описывать, какая сущность создала их, а также ряд других характеристик и аспектов данных hello, поэтому hello термин *аспекта*. Однако вы точно так же можете выполнять группировку по другим полям. Поскольку исходные результаты почти 739 тысячи событий, которые передаются в команду measure hello hello, также имеют поле с именем **EventID**, можно применить hello же методика toogroup по этому полю и получить количество событий по EventID:

```
Type=Event | Measure count() by EventID
```

Если вас не интересует hello реальное число записей, содержащих определенное значение, но вместо этого требуется только список hello значения самостоятельно, можно добавить *выберите* команду в конце hello и просто выберите hello первый столбец:

```
Type=Event | Measure count() by EventID | Select EventID
```

Затем можно усложнить и предварительно отсортировать результаты hello в запросе hello, или можно просто щелкнуть столбцы hello в сетке hello слишком.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>toosearch с использованием measure count
* Введите в поле запроса поиска hello`Type=Event | Measure count() by EventID`
* Добавление `| Select EventID` toohello конец запроса hello.
* Наконец, добавьте `| Sort EventID asc` toohello конец запроса hello.

Существует несколько важных моментов toonotice внимание:

Во-первых, отображаемые результаты hello не являются исходными необработанными результатами hello больше. Вместо этого они являются агрегированными результатами, то есть группами результатов. Это не проблема, однако следует понимать, что взаимодействие осуществляется с очень иной формой данных, которая отличается от hello исходной необработанной формы, который создается на лету hello в результате статистической обработки или применения статистической функции hello.

Во-вторых, **мер числа** в настоящее время возвращает только hello первых 100 различных результатов. Это ограничение не применяется toohello другим статистическим функциям. Таким образом обычно необходимо toouse точнее toosearch первый фильтр для определенных элементов, перед применением measure count().

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Использование функций hello max и min с командой measure hello
Существуют различные сценарии, где использование **Measure Max()** и **Measure Min()** имеет смысл. Однако поскольку каждая функция является противоположностью другой, мы опишем Max(), а с Min() вы сможете поэкспериментировать самостоятельно.

При запросе событий системы безопасности они имеют свойство **Level**, которое может изменяться. Например:

```
Type=SecurityEvent
```

![начало поиска с помощью measure count](./media/log-analytics-log-searches/oms-search-measure-max01.png)

Если требуется tooview hello наибольшее значение для всех безопасности hello события назначено общее поле Computer, hello группировкой по полю, можно использовать

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![поиск с помощью measure max по computer](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Он покажет, hello компьютеров с **уровень** записи, большинство из них имеют по крайней мере 8, на уровне многих уровень 16.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![поиск с помощью measure max для времени создания по computer](./media/log-analytics-log-searches/oms-search-measure-max03.png)

Эта функция хорошо работает с числами, однако она также работает с полями типа DateTime. Это полезно toocheck для hello последней или наиболее поздним штампом времени для любого фрагмента данных, индексируемых для каждого компьютера. Например: Если hello последнего события безопасности сообщалось для каждого компьютера?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>Использование функции avg hello с командой measure hello
Hello статистическая функция Avg(), используемая с командой measure можно toocalculate hello среднее значение для некоторого поля, а результаты группируются по hello того же или другому полю. Это оказывается полезным в самых различных случаях, например в случае с данными о производительности.

Мы начнем с данных о производительности. Обратите внимание, что OMS в настоящее время собирает счетчики производительности для машин Windows и Linux.

toosearch для *все* — самый простой запрос hello данных о производительности:

```
Type=Perf
```

![начало поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg01.png)

Hello первое, что вы заметите, — что анализа журналов показано три перспективы: список, в котором отображается которой показаны фактические записи hello за hello диаграмм; Таблица, которая показывает табличное представление данных счетчиков производительности; и метрик, которые отображаются графики для hello счетчики производительности.

В выше рисунке hello существует два набора поля, помеченные, указывающие hello следующее:

* Hello первый набор определяет имя счетчика производительности Windows, имя объекта и имя экземпляра в фильтре запроса hello. Это hello поля, которые, вероятно, наиболее часто используется в качестве аспектов и фильтров
* **Значения counterValue** — hello фактическое значение счетчика "hello". В этом примере значение hello — *75*.
* **TimeGenerated** имеет значение 12:51 в 24-часовом формате.

Здесь показано представление hello метрик на графике.

![начало поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg02.png)

После чтения сведений о записи фигуры hello производительности и ознакомления другими методиками поиска можно использовать measure Avg() tooaggregate этот тип числовых данных.

Ниже приведен простой пример.

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![поиска с помощью avg по samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

В этом примере выберите счетчик производительности hello общее время ЦП и среднее по компьютерам. Если вы хотите toonarrow работу вашей hello tooonly результаты последние 6 часов, можно использовать элемент управления фильтром времени hello или укажите в запросе следующим образом:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>Использование функции avg hello с командой measure hello toosearch
* Введите в поле запроса поиска hello `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.

Можно объединять и сопоставлять данные *по* разным компьютерам. Например предположим, что имеется набор узлов в некоторой ферме, где каждый узел является равно tooany других и заполним требуется грубая Балансировка одного типа рабочих и загрузка всех приветствия. Можно получить собрать счетчики за один проход с hello ниже запрос и получить средние значения для всей фермы hello. Для начала можно выбрать компьютеры hello с hello в следующем примере:

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Теперь, когда у вас есть компьютеры hello, также требуется только tooselect две ключевые показатели эффективности (KPI): % ЦП и % свободного места на диске. Таким образом эту часть запроса hello выглядит следующим образом:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

Теперь можно добавить компьютеры и счетчики с hello в следующем примере:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Здравствуйте, так как у вас есть выбору конкретных элементов, **измерения Avg()** позволяет возвратить среднее значение hello не для компьютера, а для всей фермы hello путем группирования по CounterName. Например:

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

Это позволяет получить удобное компактное представление с парой ключевых показателей эффективности вашей среды.

![группировка поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg04.png)

Можно легко использовать запрос поиска hello в панели мониторинга. Например, можно сохранить запрос поиска hello и создания панели мониторинга из него с именем *ключевые показатели эффективности фермы Web*. toolearn Дополнительные сведения об использовании панелей мониторинга, в разделе [создания настраиваемой панели мониторинга в службе анализа журналов](log-analytics-dashboards.md).

![панель мониторинга поиска с помощью avg](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>Использование функции hello sum с командой measure hello
функция sum Hello — функции, подобные tooother hello мер команды. Вы увидите пример как toouse hello функции sum с [поиск журналов IIS W3C в Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).

Функции Max() и Min() можно использовать с числами, датой и временем, а также с текстовыми строками. Текстовые строки сортируются в алфавитном порядке, и вы получаете первую и последнюю сроку.

Однако функцию Sum() можно использовать только с числовыми полями. Это также применимо tooAvg().

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Использование функции процентиля hello с командой measure hello
функция вычисления процентиля Hello является аналогичные tooAvg() и Sum(), его можно использовать только для числовых полей. Можно использовать любой процентиля между 1 too99 на числовое поле. Можно использовать оба варианта команды: **percentile** и **pct**. Рассмотрим несколько примеров.  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>Использовать hello, где команды
Hello команда работает как фильтр, когда он может быть применен фильтр toofurther конвейера hello статистическая обработка результатов, полученных с помощью команды Measure как противоположность tooraw результатов, которые фильтруются в начале hello запроса.

Например:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

Можно добавить другой канал» | «символьных и hello, где tooonly команды получить которых средняя загрузка ЦП превышает 80%, с компьютеров hello в следующем примере:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Если вы знакомы с Microsoft System Center Operations Manager, контролирующий hello там, где в терминах пакета управления. Если пример hello правило, первая часть запроса hello hello будет hello источника данных и hello где команда будет выглядеть определение условия hello.

Hello запрос можно использовать в качестве плитки в **Моя панель мониторинга**, как отслеживать, toosee при чрезмерную загрузку ЦП компьютера. toolearn Дополнительные сведения о панели мониторинга, в разделе [создания настраиваемой панели мониторинга в службе анализа журналов](log-analytics-dashboards.md). Можно также создать и использовать панели мониторинга с помощью мобильного приложения hello. Дополнительные сведения вы найдете в описании [мобильного приложения OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865). В двух нижних плитках hello hello после изображения, вы увидите hello монитор, отображающий список и число. По существу всегда требуется номер toobe hello ноль и hello toobe список пустой. Иное состояние указывает на наличие условия предупреждения. При необходимости, его можно использовать tootake взглянуть на какие компьютеры находятся в условиях нехватки.

![панель мониторинга на мобильном устройстве](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Используйте оператор in hello
Hello *в* оператор, вместе с *NOT IN* позволяет toouse вложенные поиски, которые являются поисками, включающими другой поиск в качестве аргумента. Такой поисковый запрос заключается в фигурные скобки {} внутри другого поискового запроса, который называется *основным* или *внешним*. Результат вложенного поиска, часто это список уникальных результатов Hello затем используется как аргумент в его основном поиске.

Можно использовать вложенные поиски применяются toomatch подмножества данных, которые нельзя описать непосредственно в выражении поиска, но которые могут быть созданы из поиска. Например, если вы хотите использовать один поиск toofind все события из *компьютерах отсутствуют обновления безопасности*, то вы должны toodesign вложенный поиск, который сначала определяет, что *компьютерах отсутствуют обновления безопасности*  поиск события принадлежность toothose узлов.

Таким образом, вы выражаете *компьютеры на которых сейчас отсутствуют необходимые обновления для системы безопасности* с приветствия при следующем запросе:

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

После получения списка hello hello поиск можно использовать в качестве внутреннего поиска toofeed hello списка компьютеров во внешний (основной) поиск, который будет искать события для этих компьютеров. Для этого внутренний поиск hello в фигурные скобки, а его результаты передаются как возможные значения для поля или фильтра во внешний поиск hello, с помощью оператора hello in.. Hello запрос будет выглядеть следующим образом:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

Также Обратите внимание hello оценка системных обновлений hello фильтр, используемый в hello внутреннего поиска, так как время моментальный снимок всех компьютеров каждые 24 часа. Hello внутренний запрос можно сделать более простым и точным счет поиска только за день. Hello внешний поиск использует Выбор времени hello в пользовательском интерфейсе hello, получая события за последние 7 дней hello. Подробные сведения об операторах времени см. в разделе [Логические операторы](#boolean-operators).

Так как вы только использовать hello результаты внутреннего поиска hello как значение фильтра для Здравствуйте внешнего, можно по-прежнему применять команды в hello внешнего поиска. Например можно по-прежнему hello группы выше события с помощью другой команды measure:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![пример поиска с оператором IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

Обычно следует вашего внутреннего запроса tooexecute быстро за время ожидания на стороне службы анализа журналов и также tooreturn небольшое количество результатов. Если hello внутренний запрос возвращает больше результатов, hello список результатов усекается, что может привести tooreturn внешнего поиска hello неверные результаты.

Другое правило заключается в этом hello сейчас внутренний поиск должен tooprovide *агрегированных* результаты. Другими словами, в нем должна содержаться команда *measure*. Необработанные результаты пока нельзя передавать во внешний поиск.

Кроме того может существовать только один оператор IN, и он должен быть последним фильтром hello в запросе hello. Несколько операторов IN не может быть либо — это предотвращает запуск нескольких вложенных поисков: важно происходит, только один вложенный или внутренний поиск hello возможна для каждого внешнего поиска.

Даже при наличии этих ограничений IN позволяет множество видов коррелированных поисков и вы toodefine содержать что-нибудь подобное toogroups, таких как компьютеры, пользователей или файлы, независимо от hello полей данных. Ниже приведены некоторые примеры.

**Все обновления, отсутствующие на компьютерах, где отключен параметр автоматического обновления.**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**Все события ошибок для компьютеров, на которых работает SQL Server (то есть тех, где выполнялась оценка SQL).**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**Все события безопасности для компьютеров, являющихся контроллерами домена (то есть тех, где выполнялась оценка AD).**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**Какие другие учетные записи входили на toohello же компьютеры, в которых учетная запись BACONLAND\jochan?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Использование команды distinct hello
Как hello названия, эта команда предоставляет список уникальных значений для поля. Несмотря на простоту команды, она весьма полезна. Здравствуйте, же может осуществляться с помощью команды measure count() также, как показано ниже.

```
Type=Event | Measure count() by Computer
```

![пример команды поиска DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

Однако если вас интересует только список уникальных значений, а не hello число документов, что значения, затем DISTINCT может предоставить tooread более понятные и удобочитаемые выходные данные и более короткий синтаксис, как показано ниже.

```
Type=Event | Distinct Computer
```
![пример команды поиска DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Функция countdistinct hello с командой measure hello
функция countdistinct Hello подсчитывает hello число различающихся значений в каждой группе. Например, это может быть использован toocount hello количество уникальных компьютеров, создание отчетов для каждого типа:

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Используйте команду интервал измерения hello
Log Analytics собирает данные практически в режиме реального времени, что позволяет собирать и наглядно отображать почти любой счетчик производительности. Просто введите запрос hello **типа: производительности** вернет тысячи метрики диаграмм на основе hello числа счетчиков и серверов в вашей среде анализа журналов. С метрики статистической обработки по требованию, можно взглянуть на hello общую метрики в вашей среде на высоком уровне и глубокое погружение в более подробных данных, необходимого для.

Предположим, что требуется tooknow Какова средняя загрузка ЦП hello на всех компьютерах. Просмотрев hello средняя загрузка ЦП для каждого компьютера, может оказаться полезным так как результаты могут получить сглажены. toolook Дополнительные сведения о можно собрать ваши результаты в меньшее время окна фрагментами и найти в временных рядов по разным измерениям. Например нужно выполнить hello почасовой среднее использование ЦП на всех компьютерах следующим образом.

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![measure average interval](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

По умолчанию эти результаты будут отображаться в виде интерактивного графика с несколькими рядами данных.  Этот график поддерживает переключение рядов (с масштабированием по оси y), масштабирование и подсказки при наведении указателя мыши.  параметр отображения таблицы Hello по-прежнему доступен для просмотра hello необработанных данных, при необходимости.

Также можно сгруппировать результаты по другим полям. В этом примере просматриваю все счетчики % hello для одного конкретного компьютера и требуется tooknow возможности hello каждый час 70 процентилем каждого счетчика.

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
Один toonote вещь: эти запросы не, ограниченный tooperformance счетчики. Можно применить их tooany метрику. В этом примере выполняется просмотр журналов W3C IIS. Я хочу tooknow возможности hello максимальное время, затрачиваемое на 5-минутный интервал для обработки каждого запроса:

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>Использование нескольких статистических выражений в одном запросе
Для команды measure можно указать несколько статистических выражений.  Каждому из них можно присвоить отдельный псевдоним.  Если не задан, возникающие hello псевдоним именем поля будет hello агрегатной функции, который был использован (т. е. «avg(CounterValue)» для avg(CounterValue)).

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

Вот еще один пример:

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о поиске по журналам можно получить в следующих статьях.

* Используйте [настраиваемые поля в службе анализа журналов](log-analytics-custom-fields.md) tooextend запросов поиска журналов.
* Просмотрите hello [Справочник поиска журнала анализа журналов](log-analytics-search-reference.md) tooview все hello поиск поля и аспекты, доступных в службе анализа журналов.
