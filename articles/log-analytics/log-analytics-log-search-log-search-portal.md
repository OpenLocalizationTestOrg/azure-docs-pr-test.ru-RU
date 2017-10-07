---
title: "портал поиска журналов aaaUsing hello в службе анализа журналов Azure | Документы Microsoft"
description: "Эта статья содержит учебник, в котором описано, как toocreate входа поиск и анализировать данные, хранящиеся в рабочей области аналитики журналов с помощью портала hello поиска журналов.  Hello учебник включает выполнение некоторых простых запросов tooreturn различные типы данных и анализ результатов."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Создание запросов поиска журналов в Azure Log Analytics с помощью портала hello поиска журналов

> [!NOTE]
> В этой статье описывается hello портала поиска журналов в Azure Log Analytics с помощью hello новый язык запросов.  Можно узнать больше о новом языке hello и получить tooupgrade процедуры hello в рабочей области [обновление поиск журнала toonew рабочей области Azure Log Analytics](log-analytics-log-search-upgrade.md).  
>
> Если в рабочей области не был обновленного toohello новый язык запросов, вы должны обращаться слишком[найти данные с помощью запросов поиска журналов в службе анализа журналов](log-analytics-log-searches.md) сведения о текущей версии hello hello портала поиска журналов.

Эта статья содержит учебник, в котором описано, как toocreate входа поиск и анализировать данные, хранящиеся в рабочей области аналитики журналов с помощью портала hello поиска журналов.  Hello учебник включает выполнение некоторых простых запросов tooreturn различные типы данных и анализ результатов.  Этот раздел посвящен функции hello портала поиска журналов для изменения запроса hello, а не непосредственное изменение.  Для непосредственного редактирования запросов hello подробнее hello [Справочник по языку запросов](https://go.microsoft.com/fwlink/?linkid=856079).

Поиск toocreate hello портале Advanced Analytics вместо hello портала поиска журналов, в разделе [Приступая к работе с портала службы анализа hello](https://go.microsoft.com/fwlink/?linkid=856587).  Использовать оба порталы hello tooaccess языка hello и тех же данных в рабочей области аналитики журналов hello того же запроса.

## <a name="prerequisites"></a>Предварительные требования
Предполагается наличие рабочей области аналитики журналов с по крайней мере одного подключенного источника, формирует данные для запросов tooanalyze hello.  

- Если у вас нет рабочей области, можно создать бесплатно с помощью процедуры hello на [приступить к работе с рабочей областью аналитики журналов](log-analytics-get-started.md).
- Подключитесь по крайней мере одну [агент Windows](log-analytics-windows-agents.md) или один [агент Linux](log-analytics-linux-agents.md) toohello рабочей области.  

## <a name="open-hello-log-search-portal"></a>Привет открыть портал поиска журналов
Сначала откройте портал hello поиска журналов.  Его можно использовать в hello портал Azure или портал OMS hello.

1. Здравствуйте, откройте портал Azure.
2. TooLog аналитика перейдите и выберите рабочую область.
3. Выберите **поиска журналов** toostay в hello Azure portal или запустите hello портал OMS, выбрав **портал OMS** и затем нажать кнопку поиска журналов hello.

![Кнопка поиска по журналу](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>Создание простого поиска
самый быстрый способ tooretrieve Hello toowork некоторых данных с является простой запрос, который возвращает все записи в таблице.  Если у вас есть любой рабочей tooyour подключенных клиентов Windows или Linux, вы получите данные в либо hello событий (Windows) или таблицу Syslog (Linux).

Введите один hello, следующие запросы в поле поиска hello и нажмите кнопку поиска hello.  

```
Event
```
```
Syslog
```

Данные возвращаются в виде списка по умолчанию hello и можно увидеть количество записей, были возвращены.

![Простой запрос](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

Только hello первый несколькими свойствами каждой записи отображаются.  Нажмите кнопку **Показать больше** toodisplay все свойства для конкретной записи.

![Сведения о записи](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Настройка области времени hello
Каждая запись, собранные службой аналитики журналов имеет **TimeGenerated** свойство, которое содержит hello дату и время создания этой записи hello.  Запрос поиска журналов портале hello возвращает только записи с **TimeGenerated** в пределах области hello времени, отображаемого на hello слева от оператора экран приветствия.  

Можно изменить фильтр времени hello, выбрав раскрывающийся список hello или изменив ползунок hello.  Hello ползунка выводится Гистограмма, показывающая hello относительное количество записей для каждого сегмента времени в пределах диапазона hello.  Этот сегмент будет зависеть от диапазона hello.

область времени по умолчанию Hello — **1 день**.  Измените это значение слишком**7 дней**, и общее количество записей hello следует увеличить.

![Промежуток времени создания данных](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Фильтровать результаты запроса hello
На hello левой стороны экрана приветствия — панель фильтра hello, позволяющий tooadd фильтрации запроса toohello без непосредственное изменение.  Несколько свойств, возвращаемых записей hello отображаются вместе со значениями десять top с числом записей.

При работе с **событий**, выберите hello флажок и далее слишком**ошибка** под **EVENTLEVELNAME**.   При работе с **Syslog**, выберите hello флажок и далее слишком**err** под **УРОВЕНЬ_СЕРЬЕЗНОСТИ_ОШИБКИ**.  При этом изменяется запрос hello tooone из следующих toolimit hello hello результаты tooerror события.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Фильтр](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

Добавить свойства toohello фильтр области, выбрав **добавить toofilters** hello свойства меню на одной из записей hello.

![Добавить toofilter меню](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

Можно задать hello же отфильтровать, выбрав **фильтра** меню свойств hello запись со значением hello требуется toofilter.  

Только у вас есть hello **фильтра** параметр для свойства с их именами синим цветом.  Это *доступные для поиска* поля, индексируемые для условий поиска.  Поля серым цветом, *произвольный текст для поиска* поля, имеющие только hello **Показать ссылки** параметр.  Этот параметр возвращает записи, имеющие это значение в любом свойстве.

![Меню фильтра](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

Результаты hello на одном свойстве можно сгруппировать, нажав кнопку hello **Group by** в меню записи hello.  При этом будет добавлено [суммировать](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) запрос tooyour оператор, который отображает результаты hello в диаграмме.  Можно сгруппировать в несколько свойств, но потребовалось бы tooedit hello запроса напрямую.  Выберите hello записей меню Далее hello hello **компьютера** свойство и выберите **Group by «Компьютер»**.  

![Группировка по компьютеру](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>Работа с результатами
портал поиска журналов Hello имеет множество функций для работы с hello результатов запроса.  Можно сортировать, фильтр и группирование результатов tooanalyze hello данных без изменения настоящего запроса hello.  По умолчанию результаты запроса не сортируются.

tooview hello данных в виде таблицы, которая предоставляет дополнительные параметры для фильтрации и сортировки, щелкните **таблицы**.  

![Табличное представление](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

Нажмите стрелку hello характеристики hello записей tooview для этой записи.

![Сортировка результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

Выполните сортировку по любому полю, щелкнув заголовок соответствующего столбца.

![Сортировка результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Фильтровать результаты hello на конкретное значение в столбце hello, нажав кнопку "Фильтр" hello и предоставляя условие фильтра.

![Фильтрация результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Группировать по столбцу, перетащив его столбца заголовок toohello вверху hello результаты.  Можно группировать по нескольким полям, перетащив верхней toohello несколько столбцов.

![Группирование результатов](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>Работа с данными о производительности
Данные о производительности для Windows и Linux агенты хранится в рабочей области аналитики журналов hello hello **производительности** таблицы.  Записи о производительности выглядят как любые другие записи. Мы можем создать простой запрос, который возвращает все записи о производительности, а также события.

```
Perf
```

![Данные о производительности](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

Возвращать миллионы записей для всех объектов и счетчиков производительности не очень полезно.  Запрашивать такие же методы, используемые выше toofilter hello данных или просто ввести следующие hello hello можно использовать непосредственно в поле поиска журнала hello.  В результате будут возвращены только записи использования процессора для компьютеров Windows и Linux.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Использование процессора](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

Это ограничивает hello данных tooa определенного счетчика, но она по-прежнему не поместить его в форму, которая особенно полезна.  Можно отобразить данные hello в виде графика, но сначала необходимо toogroup его по компьютеру и TimeGenerated.  toogroup по нескольким полям необходимо toomodify hello запроса напрямую, поэтому изменение hello запроса toohello следующие.  В этом случае используется hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) функции hello **значения CounterValue** среднее значение свойства toocalculate hello за каждый час.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Диаграмма данных о производительности](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Теперь, когда данные hello подходящим образом группируются, можно отобразить его в visual диаграммы путем добавления hello [визуализации](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) оператор.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![График](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о языке запросов анализа журналов hello в [Приступая к работе с портала службы анализа hello](https://go.microsoft.com/fwlink/?linkid=856079).
- Перемещайтесь учебника при помощи hello [Advanced Analytics портала](https://go.microsoft.com/fwlink/?linkid=856587) позволяющее toorun hello же запросы и доступа hello и тех же данных как портал hello поиска журналов.
