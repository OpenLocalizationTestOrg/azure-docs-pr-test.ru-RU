---
title: "aaaCollect и анализ счетчиков производительности в Azure Log Analytics | Документы Microsoft"
description: "По производительности tooanalyze анализа журналов счетчиков производительности собираются на агентах Windows и Linux.  В этой статье описывается, как агентов Windows и Linux, подробные сведения о них хранятся в репозитории OMS hello и как счетчиков производительности коллекцию tooconfigure tooanalyze их на портале OMS hello."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Источники данных о производительности Windows и Linux в Log Analytics
Счетчики производительности в Windows и Linux глубже понять hello производительности компонентов оборудования, операционных систем и приложений.  Служба аналитики журналов может собрать счетчики производительности более короткие интервалы для analysis рядом реального времени (NRT) в данные о производительности tooaggregating сложения для более термин анализа и отчетности.

![Счетчики производительности](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>Настройка счетчиков производительности
Настройка счетчиков производительности на портале OMS hello из hello [меню данные в параметры журнала аналитика](log-analytics-data-sources.md#configuring-data-sources).

При настройке Windows или счетчики производительности Linux для новой рабочей области OMS, можно выбрать параметр tooquickly hello создать несколько общие счетчики.  Они перечислены с tooeach следующий флажок.  Создать любой счетчиков, которые tooinitially проверяются и нажмите кнопку **hello добавить выбранные счетчики производительности**.

Для каждого счетчика производительности Windows можно выбрать конкретный экземпляр. Экземпляр hello каждого счетчика, выбранный для счетчиков производительности Linux, применяется tooall дочерним счетчикам родительского счетчика hello. Hello следующей таблице показаны распространенные экземпляров hello tooboth доступные счетчики производительности Linux и Windows.

| Имя экземпляра | Описание |
| --- | --- |
| \_Total |Общее количество всех экземпляров hello |
| \* |Все экземпляры |
| (/&#124;/var) |Сопоставление экземпляров с именем / или/var |

### <a name="windows-performance-counters"></a>Счетчики производительности Windows

![Настройка счетчиков производительности Windows](media/log-analytics-data-sources-performance-counters/configure-windows.png)

Следуйте этой процедуре tooadd новый toocollect счетчика производительности Windows.

1. Имя типа hello счетчика hello в текстовом поле hello в формате hello *\counter объекта (экземпляра)*.  По мере ввода вы увидите соответствующий список распространенных счетчиков.  Счетчик можно выбрать из списка hello или тип в одной из ваших собственных.  Кроме того, вы можете получить все экземпляры определенного счетчика, указав *объект\счетчик*.  

    При сборе данных счетчиков производительности SQL Server из именованных экземпляров, все именованные экземпляра счетчиков с *MSSQL$* и за которым следует имя hello hello экземпляра.  Например, toocollect hello Коэффициент попаданий в кэш журнала счетчиков для всех баз данных из hello объекта производительности баз данных для SQL именованного экземпляра INST2, указать `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`.

2. Нажмите кнопку  **+**  или нажмите клавишу **ввод** toohello tooadd hello счетчикам.
3. При добавлении счетчика необходимо используется по умолчанию hello 10 секунд для его **интервала выборки**.  Если требуется tooreduce требования к хранилищу hello hello собранных данных о производительности можно изменить этот tooa высокого значения вверх too1800 секунд (30 минут).
4. После завершения добавления счетчиков нажмите кнопку hello **Сохранить** кнопку вверху hello конфигурации hello toosave экран приветствия.

### <a name="linux-performance-counters"></a>Счетчики производительности Linux

![Настройка счетчиков производительности Linux](media/log-analytics-data-sources-performance-counters/configure-linux.png)

Следуйте этой процедуре tooadd новый toocollect счетчиков производительности Linux.

1. По умолчанию все изменения конфигурации автоматически размещаемых tooall агентов.  Агенты Linux файл конфигурации отправляется сборщик данных Fluentd toohello.  Если вы хотите toomodify этот файл вручную на каждом агенте Linux, затем снимите флажок hello *применить указанную ниже компьютеры Linux toomy конфигурации* и следуйте руководству, Привет приведенному ниже.
2. Имя типа hello счетчика hello в текстовом поле hello в формате hello *\counter объекта (экземпляра)*.  По мере ввода вы увидите соответствующий список распространенных счетчиков.  Счетчик можно выбрать из списка hello или тип в одной из ваших собственных.  
3. Нажмите кнопку  **+**  или нажмите клавишу **ввод** tooadd hello toohello по счетчикам других счетчиков для hello объекта.
4. Все счетчики для использования объекта hello же **интервала выборки**.  по умолчанию Hello равен 10 секундам.  При необходимости, чтобы tooreduce требования к хранилищу hello hello собранных данных о производительности изменить этот tooa высокого значения вверх too1800 секунд (30 минут).
5. После завершения добавления счетчиков нажмите кнопку hello **Сохранить** кнопку вверху hello конфигурации hello toosave экран приветствия.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>Настройка счетчиков производительности Linux в файле конфигурации
Вместо того чтобы настраивать счетчики производительности Linux с помощью портала OMS hello, предусмотрена возможность hello изменения файлов конфигурации на агенте Linux hello.  Toocollect метрики производительности определяются конфигурации hello в **/и т. д/opt/microsoft/omsagent/\<идентификатор рабочей области\>/conf/omsagent.conf**.

Каждый объект или категория toocollect метрик производительности должен быть определен в файле конфигурации hello как один `<source>` элемента. следующий синтаксис Hello hello шаблону ниже.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


в hello в следующей таблице описаны параметры Hello в этом элементе.

| Параметры | Описание |
|:--|:--|
| object\_name | Имя объекта для коллекции hello. |
| instance\_regex |  Объект *регулярное выражение* определение какие toocollect экземпляров. Здравствуйте, значение: `.*` указывает все экземпляры. toocollect метрик процессора только hello \_общий экземпляр можно указать `_Total`. только toocollect метрик процесса для hello экземпляров crond или sshd, можно указать: "(crond\|sshd). |
| counter\_name\_regex | Объект *регулярное выражение* определение toocollect какие счетчики (hello объекта). Укажите все счетчики объекта hello toocollect: `.*`. toocollect только данные счетчиков пространства подкачки hello объекта памяти, например, можно указать:`.+Swap.+` |
| interval | Частота, с которой hello собираются данные счетчиков объекта. |


Hello следующей таблице перечислены hello объекты и счетчики, которые можно задать в файле конфигурации hello.  Для определенных приложений доступны дополнительные счетчики, как описано в статье [Collect performance counters for Linux applications in Log Analytics](log-analytics-data-sources-linux-applications.md) (Сбор данных счетчиков производительности для приложений Linux в Log Analytics).

| Имя объекта | Имя счетчика |
|:--|:--|
| Логический диск | Процент свободных индексных дескрипторов |
| Логический диск | Процент свободного места |
| Логический диск | Процент используемых индексных дескрипторов |
| Логический диск | Процент используемого места |
| Логический диск | Скорость чтения с диска (байт/с)  |
| Логический диск | Операций чтения с диска в секунду  |
| Логический диск | Обращений к диску в секунду |
| Логический диск | Скорость записи на диск (байт/с) |
| Логический диск | Операций записи на диск в секунду |
| Логический диск | Свободно мегабайт |
| Логический диск | Скорость обмена с логическим диском (байт/с) |
| Память | Процент доступной памяти |
| Память | Процент доступной области подкачки |
| Память | Процент используемой памяти |
| Память | Процент используемой области подкачки |
| Память | Доступный объем памяти в МБ |
| Память | Доступный объем подкачки в МБ |
| Память | Операций чтения со страницы в секунду |
| Память | Операций записи на страницу в секунду |
| Память | Страниц в секунду |
| Память | Используемая области подкачки в МБ |
| Память | Используемый объем памяти в МБ |
| Сеть | Всего передано байт |
| Сеть | Всего получено байт |
| Сеть | Всего байт |
| Сеть | Всего передано пакетов |
| Сеть | Всего получено пакетов |
| Сеть | Всего ошибок Rx |
| Сеть | Всего ошибок Tx |
| Сеть | Всего конфликтов |
| Физический диск | Среднее время чтения с диска (с) |
| Физический диск | Среднее время обращения к диску (с) |
| Физический диск | Среднее время записи на диск (с) |
| Физический диск | Скорость обмена с физическим диском (байт/с) |
| Process | Процент времени работы в привилегированном режиме |
| Process | Процент времени пользователя |
| Process | Используемая память в КБ |
| Process | Виртуальная общая память |
| Процессор | Процент времени DPC |
| Процессор | Процент времени простоя |
| Процессор | Процент времени прерывания |
| Процессор | Процент времени ожидания ввода-вывода |
| Процессор | Процент времени работы с низким приоритетом |
| Процессор | Процент времени работы в привилегированном режиме |
| Процессор | % загруженности процессора |
| Процессор | Процент времени пользователя |
| системный; | Объем свободной физической памяти |
| системный; | Объем свободного места в файлах подкачки |
| системный; | Объем свободной виртуальной памяти |
| системный; | Процессы |
| системный; | Объем, сохраненный в файлах подкачки |
| системный; | Время доступности |
| системный; | Пользователи |


Ниже представлена конфигурация по умолчанию hello для метрики производительности.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>Сбор данных
Служба Log Analytics будет собирать данные со всех указанных счетчиков производительности с заданным для них интервалом выборки во всех агентах, в которых установлен счетчик.  Hello не собраны, и необработанные данные hello доступна во всех представлениях поиска журналов для hello промежуток времени, указанный по подписке OMS.

## <a name="performance-record-properties"></a>Свойства записи о производительности
Производительность записи имеют тип **производительности** и имеющих свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| Компьютер |Компьютер, hello события, собранные из. |
| CounterName |Имя счетчика производительности hello |
| CounterPath |Полный путь счетчика hello в форме hello \\ \\ \<компьютера >\\object(instance)\\счетчика. |
| CounterValue |Числовое значение счетчика "hello". |
| InstanceName |Имя экземпляра событий hello.  Если экземпляра нет, используется пустое значение. |
| ObjectName |Имя объекта производительности hello |
| SourceSystem |Тип данных hello агента были собраны. <br><br>OpsManager — агент Windows, подключенный напрямую или через SCOM <br> Linux — все агенты Linux  <br> AzureStorage – диагностика Azure |
| TimeGenerated |Дата и время hello данные были собраны. |

## <a name="sizing-estimates"></a>Оценки размера
 Сбор данных для одного счетчика с 10-секундным интервалом генерирует около 1 МБ данных в день на каждый экземпляр.  Можно оценить требования к хранилищу hello счетчика с hello следующую формулу.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>Поиск по журналам с записями о производительности
Hello следующей таблице приведены примеры различных запросов поиска журналов, получить производительность записи.

| Запрос | Описание |
|:--- |:--- |
| Type=Perf |Все данные о производительности. |
| Type=Perf Computer="MyComputer" |Все данные о производительности с определенного компьютера |
| Type=Perf CounterName="Current Disk Queue Length" |Все данные о производительности с определенного счетчика |
| Type=Perf (ObjectName=Processor) CounterName="% Processor Time" InstanceName=_Total &#124; measure Avg(Average) as AVGCPU by Computer |Средний объем использования ЦП на всех компьютерах |
| Type=Perf (CounterName="% Processor Time") &#124; measure max(Max) by Computer |Максимальный объем использования ЦП на всех компьютерах |
| Type=Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" &#124; measure Avg(Average) by InstanceName |Среднее для всех экземпляров данного компьютера hello текущая длина очереди диска |
| Type=Perf CounterName="DiskTransfers/sec" &#124; measure percentile95(Average) by Computer |95-й процентиль для обращений к диску/с на всех компьютерах |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total" &#124; measure avg(CounterValue) by Computer Interval 1HOUR |Средняя почасовая нагрузка на ЦП по всем компьютерам |
| Type=Perf Computer="MyComputer" CounterName=%* InstanceName=_Total &#124; measure percentile70(CounterValue) by CounterName Interval 1HOUR |Почасовые 70-е процентили по каждому процентному счетчику для конкретного компьютера |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total" (Computer="MyComputer") &#124; measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR |Почасовые средние, минимальные, максимальные значения и 75-е процентили по загрузке ЦП для конкретного компьютера |
| Type=Perf ObjectName="MSSQL$INST2:Databases" InstanceName=master | Все данные о производительности от производительности базы данных hello объекта для базы данных master hello из именованного экземпляра SQL Server INST2 hello.  

>[!NOTE]
> Если рабочую область был обновленного toohello [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запросы будут изменены следующие toohello.

> | Запрос | Описание |
|:--- |:--- |
| Perf |Все данные о производительности. |
| Perf &#124; where Computer == "MyComputer" |Все данные о производительности с определенного компьютера |
| Perf &#124; where CounterName == "Current Disk Queue Length" |Все данные о производительности с определенного счетчика |
| Perf &#124; where ObjectName == "Processor" and CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AVGCPU = avg(Average) by Computer |Средний объем использования ЦП на всех компьютерах |
| Perf &#124; where CounterName == "% Processor Time" &#124; summarize AggregatedValue = max(Max) by Computer |Максимальный объем использования ЦП на всех компьютерах |
| Perf &#124; where ObjectName == "LogicalDisk" and CounterName == "Current Disk Queue Length" and Computer == "MyComputerName" &#124; summarize AggregatedValue = avg(Average) by InstanceName |Среднее для всех экземпляров данного компьютера hello текущая длина очереди диска |
| Perf &#124; where CounterName == "DiskTransfers/sec" &#124; summarize AggregatedValue = percentile(Average, 95) by Computer |95-й процентиль для обращений к диску/с на всех компьютерах |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), Computer |Средняя почасовая нагрузка на ЦП по всем компьютерам |
| Perf &#124; where Computer == "MyComputer" and CounterName startswith_cs "%" and InstanceName == "_Total" &#124; summarize AggregatedValue = percentile(CounterValue, 70) by bin(TimeGenerated, 1h), CounterName | Почасовые 70-е процентили по каждому процентному счетчику для конкретного компьютера |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" and Computer == "MyComputer" &#124; summarize ["min(CounterValue)"] = min(CounterValue), ["avg(CounterValue)"] = avg(CounterValue), ["percentile75(CounterValue)"] = percentile(CounterValue, 75), ["max(CounterValue)"] = max(CounterValue) by bin(TimeGenerated, 1h), Computer |Почасовые средние, минимальные, максимальные значения и 75-е процентили по загрузке ЦП для конкретного компьютера |
| Perf &#124; where ObjectName == "MSSQL$INST2:Databases" and InstanceName == "master" | Все данные о производительности от производительности базы данных hello объекта для базы данных master hello из именованного экземпляра SQL Server INST2 hello.  

## <a name="viewing-performance-data"></a>Просмотр данных о производительности
При выполнении поиска журналов для данных производительности hello **списка** отображается представление по умолчанию.  tooview hello данных в графической форме, нажмите кнопку **метрики**.  Подробные графическое представление, щелкните hello  **+**  следующее tooa счетчика.  

![Свернутое представление метрик](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

tooaggregate данные о производительности на странице поиска журналов, в разделе [метрики статистической обработки по требованию и визуализации в OMS](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/).


## <a name="next-steps"></a>Дальнейшие действия
* [Сбор данных счетчиков производительности из приложений Linux](log-analytics-data-sources-linux-applications.md), включая MySQL и сервер HTTP Apache.
* Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений.  
* Экспортировать собранные данные слишком[Power BI](log-analytics-powerbi.md) дополнительные визуализации и анализа.
