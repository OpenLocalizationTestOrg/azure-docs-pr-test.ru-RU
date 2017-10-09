---
title: "aaaCapacity и производительность решения в службе анализа журналов Azure | Документы Microsoft"
description: "Используйте hello емкости и производительности решений в toohelp аналитики журналов понять hello ресурсы серверов Hyper-V."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Планирование емкости виртуальной машины Hyper-V с hello емкости и производительности решений (Предварительная версия)

![Символ "Емкость и производительность"](./media/log-analytics-capacity/capacity-solution.png)

Можно использовать hello емкости и производительности решений в toohelp анализа журналов, которые вы понимаете hello ресурсы серверов Hyper-V. решение Hello предоставляет подробные сведения о среде Hyper-V, отображая hello общее использование узлов hello (ЦП, памяти и диска) и hello виртуальных машин, запущенных на этих узлах Hyper-V. Показатели собираются для Процессора, памяти и дисках между узлами и hello виртуальных машин, работающих на них.

решение Hello.

-   показывает узлы с максимальным и минимальным использованием памяти и ресурсов ЦП;
-   показывает виртуальные машины с максимальным и минимальным использованием памяти и ресурсов ЦП;
-   показывает виртуальные машины с максимальным и минимальным использованием пропускной способности и числом операций ввода-вывода в секунду;
-   показывает, какие виртуальные машины запущены на конкретных узлах;
-   Показывает hello top диски с высокой пропускной способностью операций ввода-ВЫВОДА, и задержки в кластере Общие тома
- Позволяет вам toocustomize и фильтр на основе групп

> [!NOTE]
> Hello предыдущей версии hello емкости и производительности решения с именем управления емкостью требуется System Center Operations Manager и System Center Virtual Machine Manager. В обновленном решении эти зависимости не применяются.


## <a name="connected-sources"></a>Подключенные источники

Привет, в следующей таблице описываются hello подключенных источников, которые поддерживаются в этом решении.

| Подключенный источник | Поддержка | Описание |
|---|---|---|
| [Агенты Windows](log-analytics-windows-agents.md) | Да | решение Hello собирает сведения данных емкости и производительности от агентов Windows. |
| [Агенты Linux](log-analytics-linux-agents.md) | Нет    | решение Hello не собирает сведения данных емкости и производительности от агентов прямой Linux.|
| [Группы управления SCOM](log-analytics-om-agents.md) | Да |решение Hello собирает данные емкости и производительности от агентов в подключенной группе управления SCOM. Прямое подключение от tooOMS агент SCOM hello не является обязательным. Данные будут отправлены из репозитория OMS toohello группы управления hello.|
| [Учетная запись хранения Azure](log-analytics-azure-storage.md) | Нет | Служба хранилища Azure не содержит сведения о емкости и производительности.|

## <a name="prerequisites"></a>Предварительные требования

- Агенты Windows или Operations Manager должны быть установлены на узлах Hyper-V под управлением Windows Server 2012 (или более поздней версии), а не на виртуальных машинах.


## <a name="configuration"></a>Конфигурация

Выполните следующий шаг tooadd hello емкости и производительности tooyour рабочая область решения hello.

- Добавить hello емкости и производительности решений tooyour рабочую область OMS процесса hello, описанных в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Пакеты управления

Если группы управления SCOM к рабочей области OMS подключенных tooyour, затем hello следующие пакеты управления будут установлены в SCOM при добавлении этого решения. Никакая настройка или обслуживание для этих пакетов управления не требуются.

- Microsoft.IntelligencePacks.CapacityPerformance

событие 1201 Hello выглядит так:


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

При обновлении hello емкости и производительности решений hello номер версии изменится.

Дополнительные сведения об обновлении пакетов управления решения см. в разделе [tooLog подключение Operations Manager Analytics](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>С помощью решения hello

При добавлении hello емкости и производительности tooyour рабочая область решения hello емкости и производительности будет добавлен toohello Общие сведения о панели мониторинга. Эта Плитка счетчик hello количество активных узлов Hyper-V и hello количество активных виртуальных машин, которые были отслеживаются для выбранного периода времени hello.

![Плитка "Емкость и производительность"](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Просмотр сведений об использовании

Щелкните здесь, hello емкости и производительности плитки tooopen hello емкости и производительности панели мониторинга. панель мониторинга Hello, включает столбцы hello hello в следующей таблице. Каждый столбец содержит вверх tooten сузьте указан, критерий столбца hello области и временной диапазон. Можно выполнить поиск журнала, который возвращает все записи, нажав кнопку **все** внизу hello hello столбца или щелкнув заголовок столбца hello.

- **Узлы**
    - **Загрузка Процессора узла** показано графическое тенденций использования ЦП hello хост-компьютеров и список узлов, в зависимости от выбранного периода времени hello. Наведите указатель на сведения tooview диаграммы hello строки для определенной точки времени. Щелкните диаграмму tooview hello Дополнительные сведения на странице поиска журналов. Щелкните любой поиска журналов tooopen имя узла и просматривать данные счетчика ЦП для виртуальных машин, размещенных.
    - **Использование памяти узла** показывает графический тенденции использования памяти hello хост-компьютеров и список узлов, в зависимости от выбранного периода времени hello. Наведите указатель на сведения tooview диаграммы hello строки для определенной точки времени. Щелкните диаграмму tooview hello Дополнительные сведения на странице поиска журналов. Щелкните любой узел имя tooopen журнала поиска и просмотра памяти счетчик сведений для размещенных виртуальных машин.
- **Виртуальные машины**
    - **Использование ЦП виртуальной Машины** показано графическое тенденции использования hello ЦП виртуальных машин и список виртуальных машин, на базе hello указанного периода времени. Наведите указатель на сведения tooview диаграммы hello строки для определенной точки времени для hello первые три виртуальные машины. Щелкните диаграмму tooview hello Дополнительные сведения на странице поиска журналов. Щелкните любой поиска журналов tooopen имя виртуальной Машины и просмотрите статистические данные счетчика ЦП для hello виртуальной Машины.
    - **Использование памяти виртуальной Машины** показывает графический тенденции использования памяти hello виртуальных машин и список виртуальных машин, на базе hello указанного периода времени. Наведите указатель на сведения tooview диаграммы hello строки для определенной точки времени для hello первые три виртуальные машины. Щелкните диаграмму tooview hello Дополнительные сведения на странице поиска журналов. Щелкните любой поиска журналов tooopen имя виртуальной Машины и просмотрите памяти статистические данные счетчика для hello виртуальной Машины.
    - **Виртуальная машина общий диск операций ввода-ВЫВОДА** показано общее графический тренда hello операций ввода-ВЫВОДА для виртуальных машин и список виртуальных машин с hello операций ввода-ВЫВОДА для каждой из них, при использовании hello указанного периода времени. Наведите указатель на сведения tooview диаграммы hello строки для определенной точки времени для hello первые три виртуальные машины. Щелкните диаграмму tooview hello Дополнительные сведения на странице поиска журналов. Выберите любой поиска журналов tooopen имя виртуальной Машины и просмотрите, агрегированных диска IOPS счетчика сведения для hello виртуальной Машины.
    - **Общая пропускная способность диска виртуальной Машины** показано графическое тренда hello пропускная способность общего диска для виртуальных машин и список виртуальных машин с hello пропускная способность общего диска для каждого, на основе hello указанного периода времени. Наведите указатель на сведения tooview диаграммы hello строки для определенной точки времени для hello первые три виртуальные машины. Щелкните диаграмму tooview hello Дополнительные сведения на странице поиска журналов. Щелкните любой поиска журналов tooopen имя виртуальной Машины и просмотрите данные счетчика агрегированных дискового пропускную способность для hello виртуальной Машины.
- **Общие тома кластера**
    - **Общая пропускная способность** показывает сумму hello и чтения и записи на общие тома кластера.
    - **Общее число операций ввода-ВЫВОДА** показывает сумму hello операций ввода вывода в секунду на общие тома кластера.
    - **Общая задержка** показывает Общая задержка hello в общие тома кластера.
- **Плотность размещения** hello top отражает hello общее число доступных toohello решения узлов и виртуальных машин. Щелкните hello top tooview Дополнительные сведения о плитке в поиске по журналам. Также перечислены все узлы и количество виртуальных машин, размещенных в hello. Щелкните toodrill узла в результаты hello виртуальной Машины на странице поиска журналов.


![Колонка "Узлы" на панели мониторинга](./media/log-analytics-capacity/dashboard-hosts.png)

![Колонка "Виртуальные машины" на панели мониторинга](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Оценка производительности

Рабочих вычислительных сред, значительно отличаются от tooanother одной организации. Кроме того, емкость и производительность может зависеть от того, как запущены виртуальные машины, и от того, что вы считаете нормальным. Конкретные процедуры toohelp измерения производительности, возможно, не будут применяться tooyour среды. Поэтому более обобщенный предписания лучше подходит toohelp. Корпорация Майкрософт публикует различные из статьи toohelp предписания измерения производительности.

toosummarize, решение hello собирает данные о емкости и производительности из различных источников, включая счетчики производительности. Эти данные емкости и производительности, которые представлены в различных областей в решении hello и сравните вашего toothose результаты на hello [Оценка производительности в Hyper-V](https://msdn.microsoft.com/library/cc768535.aspx) статьи. Несмотря на то, что hello статья была опубликована некоторое время назад, показатели hello, рекомендации и инструкции, остаются действительными. статья Hello содержит полезные ресурсы tooother ссылки.


## <a name="sample-log-searches"></a>Пример поисков журналов

Привет, в следующей таблице предоставляет образец поиска журналов для емкости и производительности собираются и данных для вычисления, это решение.

| Запрос | Описание |
|---|---|
| Конфигурация памяти всех узлов | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Конфигурация памяти всех виртуальных машин | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Показатель общего числа дисковых операций ввода-вывода в секунду на всех виртуальных машинах | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Показатель общей пропускной способности дисков на всех виртуальных машинах | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Показатель общего числа операций ввода-вывода в секунду на всех общих томах кластера | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Показатель общей пропускной способности на всех общих томах кластера | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Показатель общей задержки на всех общих томах кластера | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Если рабочую область был обновленного toohello [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запросы будут изменены следующие toohello.

> | Запрос | Описание |
|:--- |:--- |
| Конфигурация памяти всех узлов | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "Host Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| Конфигурация памяти всех виртуальных машин | Perf &#124; where ObjectName == "Capacity and Performance" and CounterName == "VM Assigned Memory MB" &#124; summarize MB = avg(CounterValue) by InstanceName |
| Показатель общего числа дисковых операций ввода-вывода в секунду на всех виртуальных машинах | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Reads/s" or CounterName == "VHD Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Показатель общей пропускной способности дисков на всех виртуальных машинах | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "VHD Read MB/s" or CounterName == "VHD Write MB/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Показатель общего числа операций ввода-вывода в секунду на всех общих томах кластера | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Показатель общей пропускной способности на всех общих томах кластера | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Reads/s" or CounterName == "CSV Writes/s") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |
| Показатель общей задержки на всех общих томах кластера | Perf &#124; where ObjectName == "Capacity and Performance" and (CounterName == "CSV Read Latency" or CounterName == "CSV Write Latency") &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), CounterName, InstanceName |


## <a name="next-steps"></a>Дальнейшие действия
* Используйте [входа поиска аналитики журналов](log-analytics-log-searches.md) tooview подробные данные о емкости и производительности.
