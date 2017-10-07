---
title: "aaaAzure метрик мониторинга - поддерживаемых показателей каждого типа ресурсов | Документы Microsoft"
description: "Список метрик, доступных для каждого типа ресурса в Azure Monitor."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Метрики, поддерживаемые Azure Monitor
Монитор Azure предоставляет несколько способов toointeract показателей, включая создание диаграмм их на портале hello, доступа к ним через API-Интерфейс REST hello или запрос их с помощью PowerShell или интерфейс командной строки. Ниже приведен полный список метрик, доступных в настоящее время в конвейере метрик Azure Monitor.

> [!NOTE]
> Другие показатели, могут быть доступны на портале hello или с помощью предыдущих версий API. Этот список включает только доступно при использовании общедоступной предварительной версии hello консолидированные hello Azure монитор метрики конвейера метрики общедоступной предварительной версии.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|qpu_metric|QPU|Count|Средняя|QPU. Диапазоны: 0–100 для S1, 0–200 для S2 и 0–400 для S4.|
|memory_metric|Память|Байты|Средняя|Память. Диапазоны: 0–25 ГБ для S1, 0–50 ГБ для S2 и 0–100 ГБ для S4.|
|TotalConnectionRequests|Общее число запросов на подключение|Count|Средняя|Общее число запросов на подключение. Поступившие запросы.|
|SuccessfullConnectionsPerSec|Число успешных подключений в секунду|Число/с|Средняя|Частота успешных установок подключений.|
|TotalConnectionFailures|Общее число неудачных подключений|Count|Средняя|Общее число неудачных попыток подключения.|
|CurrentUserSessions|Текущие пользовательские сеансы|Count|Средняя|Текущее число установленных пользовательских сеансов.|
|QueryPoolBusyThreads|Занятые потоки в пуле запросов|Count|Средняя|Число занятых потоков в пуле потоков запросов hello.|
|CommandPoolJobQueueLength|Длина очереди заданий пула команд|Count|Средняя|Число заданий в очереди пула потоков команд hello hello.|
|ProcessingPoolJobQueueLength|Длина очереди заданий пула обработки|Count|Средняя|Количество заданий не ввода-вывода в очереди пула потоков обработки hello hello.|
|CurrentConnections|Подключение: текущие подключения|Count|Средняя|Текущее число установленных клиентских подключений.|
|CleanerCurrentPrice|Память: текущая цена очистки|Count|Средняя|Текущая цена памяти, $/ байт/время, нормализованная too1000.|
|CleanerMemoryShrinkable|Память: сжимаемая память очистки|Байты|Средняя|Объем памяти в байтах, toopurging субъекта по hello фоновой очистки.|
|CleanerMemoryNonshrinkable|Память: несжимаемая память очистки|Байты|Средняя|Объем памяти в байтах, не toopurging субъекта по hello фоновой очистки.|
|MemoryUsage|Память: использование памяти|Байты|Средняя|Использование hello процессом сервера согласно расчетам стоимости очистки памяти в памяти. Равно toocounter Process\PrivateBytes плюс размер hello размещенный в памяти данных без учета памяти, сопоставленной или выделенной с помощью hello в памяти xVelocity (VertiPaq) сверх подсистемы xVelocity hello предельный объем памяти.|
|MemoryLimitHard|Память: твердый лимит памяти|Байты|Средняя|Твердый лимит памяти, из файла конфигурации.|
|MemoryLimitHigh|Память: верхний предел памяти|Байты|Средняя|Верхняя граница объема памяти, из файла конфигурации.|
|MemoryLimitLow|Память: нижний предел памяти|Байты|Средняя|Нижняя граница объема памяти, из файла конфигурации.|
|MemoryLimitVertiPaq|Память: ограничение памяти VertiPaq|Байты|Средняя|Ограничение памяти, из файла конфигурации.|
|Quota|Память: квота|Байты|Средняя|Текущая квота памяти, в байтах. Квота памяти также называется выделением или резервированием памяти.|
|QuotaBlocked|Память: заблокировано квот|Count|Средняя|Текущее число запросов на квоту, заблокированных до высвобождения других квот памяти.|
|VertiPaqNonpaged|Память: размер нестраничных данных VertiPaq|Байты|Средняя|Байт памяти заблокирован в hello рабочий набор для использования в памяти подсистемой hello.|
|VertiPaqPaged|Память: размер страничных данных VertiPaq|Байты|Средняя|Размер памяти (в байтах), занятой страничными данными в памяти.|
|RowsReadPerSec|Обработка: считано строк в секунду|Число/с|Средняя|Интенсивность считывания строк из всех реляционных баз данных.|
|RowsConvertedPerSec|Обработка: преобразовано строк в секунду|Число/с|Средняя|Интенсивность преобразованных в ходе обработки строк.|
|RowsWrittenPerSec|Обработка: записано строк в секунду|Число/с|Средняя|Интенсивность записанных в ходе обработки строк.|
|CommandPoolBusyThreads|Потоки: занятые потоки в пуле команд|Count|Средняя|Число занятых потоков в пуле потоков команд hello.|
|CommandPoolIdleThreads|Потоки: бездействующие потоки в пуле команд|Count|Средняя|Число бездействующих потоков в пуле потоков команд hello.|
|LongParsingBusyThreads|Потоки: занятые потоки продолжительного анализа|Count|Средняя|Число занятых потоков в hello продолжительный анализ пула потоков.|
|LongParsingIdleThreads|Потоки: бездействующие потоки продолжительного анализа|Count|Средняя|Число бездействующих потоков в hello продолжительный анализ пула потоков.|
|LongParsingJobQueueLength|Потоки: длина очереди заданий продолжительного анализа|Count|Средняя|Число заданий в очереди hello hello продолжительный анализ пула потоков.|
|ProcessingPoolBusyIOJobThreads|Потоки: занятые потоки ввода-вывода в пуле обработки заданий|Count|Средняя|Количество потоков, выполняющих задания ввода-вывода в hello в пуле потоков обработки.|
|ProcessingPoolBusyNonIOThreads|Потоки: занятые потоки в пуле обработки, не связанные с вводом-выводом|Count|Средняя|Количество потоков, выполняющих задания без ввода-вывода в hello в пуле потоков обработки.|
|ProcessingPoolIOJobQueueLength|Потоки: длина очереди заданий ввода-вывода пула обработки|Count|Средняя|Количество заданий ввода-вывода в очереди пула потоков обработки hello hello.|
|ProcessingPoolIdleIOJobThreads|Потоки: бездействующие потоки ввода-вывода в пуле обработки заданий|Count|Средняя|Число бездействующих потоков заданий ввода-вывода в hello в пуле потоков обработки.|
|ProcessingPoolIdleNonIOThreads|Потоки: бездействующие потоки в пуле обработки, не связанные с вводом-выводом|Count|Средняя|Число бездействующих потоков в пул потоков обработки hello выделенные задания toonon с вводом выводом.|
|QueryPoolIdleThreads|Потоки: бездействующие потоки в пуле запросов|Count|Средняя|Число бездействующих потоков заданий ввода-вывода в hello в пуле потоков обработки.|
|QueryPoolJobQueueLength|Потоки: длина очереди заданий пула запросов|Count|Средняя|Число заданий в очереди пула потоков запросов hello hello.|
|ShortParsingBusyThreads|Потоки: занятые потоки быстрого анализа|Count|Средняя|Число занятых потоков в hello короткий пулом потоков синтаксического анализа.|
|ShortParsingIdleThreads|Потоки: бездействующие потоки быстрого анализа|Count|Средняя|Число бездействующих потоков в hello короткий пулом потоков синтаксического анализа.|
|ShortParsingJobQueueLength|Потоки: длина очереди заданий быстрого анализа|Count|Средняя|Число заданий в очереди hello hello короткий пулом потоков синтаксического анализа.|
|memory_thrashing_metric|Пробуксовка памяти|Процент|Средняя|Среднее значение пробуксовки памяти.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|TotalRequests|Total Gateway Requests|Count|Всего|Число запросов к шлюзу|
|SuccessfulRequests|Successful Gateway Requests|Count|Всего|Число успешных запросов к шлюзу|
|UnauthorizedRequests|Неавторизованные запросы к шлюзу|Count|Всего|Число неавторизованных запросов к шлюзу|
|FailedRequests|Failed Gateway Requests|Count|Всего|Количество сбоев при обработке запросов к шлюзу.|
|OtherRequests|Другие запросы к шлюзу|Count|Всего|Количество других запросов к шлюзу|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|CoreCount|Dedicated Core Count|Count|Всего|Общее число выделенных ядер в учетной записи пакетной hello|
|TotalNodeCount|Dedicated Node Count|Count|Всего|Общее число выделенных узлов в учетной записи пакетной hello|
|LowPriorityCoreCount|LowPriority Core Count|Count|Всего|Общее число ядер низким приоритетом в учетной записи пакетной hello|
|TotalLowPriorityNodeCount|Low-Priority Node Count|Count|Всего|Общее число узлов низким приоритетом в учетной записи пакетной hello|
|CreatingNodeCount|Creating Node Count|Count|Всего|Количество создаваемых узлов.|
|StartingNodeCount|Starting Node Count|Count|Всего|Число узлов, которые запускаются.|
|WaitingForStartTaskNodeCount|Waiting For Start Task Node Count|Count|Всего|Количество узлов, Ожидание toocomplete запустить задачу hello|
|StartTaskFailedNodeCount|Start Task Failed Node Count|Count|Всего|Количество узлов, где не удалось запустить задачу hello|
|IdleNodeCount|Idle Node Count|Count|Всего|Количество узлов в неактивном состоянии.|
|OfflineNodeCount|Offline Node Count|Count|Всего|Количество узлов не в сети.|
|RebootingNodeCount|Rebooting Node Count|Count|Всего|Количество перезапускаемых узлов.|
|ReimagingNodeCount|Reimaging Node Count|Count|Всего|Число узлов, для которых пересоздается образ.|
|RunningNodeCount|Running Node Count|Count|Всего|Число работающих узлов.|
|LeavingPoolNodeCount|Leaving Pool Node Count|Count|Всего|Количество узлов, оставляя hello пула|
|UnusableNodeCount|Unusable Node Count|Count|Всего|Число узлов, непригодных для использования.|
|PreemptedNodeCount|Preempted Node Count|Count|Всего|Количество замещенных узлов.|
|TaskStartEvent|Task Start Events|Count|Всего|Общее число запущенных задач.|
|TaskCompleteEvent|Task Complete Events|Count|Всего|Общее число завершенных задач.|
|TaskFailEvent|Task Fail Events|Count|Всего|Общее число задач, завершившихся сбоем.|
|PoolCreateEvent|Pool Create Events|Count|Всего|Общее число созданных пулов.|
|PoolResizeStartEvent|Pool Resize Start Events|Count|Всего|Общее число запущенных задач изменения размера пула.|
|PoolResizeCompleteEvent|Pool Resize Complete Events|Count|Всего|Общее число завершенных задач изменения размера пула.|
|PoolDeleteStartEvent|Pool Delete Start Events|Count|Всего|Общее число запущенных задач удаления пула.|
|PoolDeleteCompleteEvent|Pool Delete Complete Events|Count|Всего|Общее число завершенных задач удаления пула.|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|connectedclients|Подключенные клиенты|Count|Максимальная||
|totalcommandsprocessed|Всего операций|Count|Всего||
|cachehits|Попаданий в кэш|Count|Всего||
|cachemisses|Промахов в кэше|Count|Всего||
|getcommands|Операций считывания|Count|Всего||
|setcommands|Операций записи|Count|Всего||
|evictedkeys|Исключенные ключи|Count|Всего||
|totalkeys|Всего ключей|Count|Максимальная||
|expiredkeys|Ключи с истекшим сроком действия|Count|Всего||
|usedmemory|Используемая память|Байты|Максимальная||
|usedmemoryRss|RSS используемой памяти|Байты|Максимальная||
|serverLoad|Загрузка сервера|Процент|Максимальная||
|cacheWrite|Запись в кэш|Байт/с|Максимальная||
|cacheRead|Чтение из кэша|Байт/с|Максимальная||
|percentProcessorTime|ЦП|Процент|Максимальная||
|connectedclients0|Connected Clients (Shard 0)|Count|Максимальная||
|totalcommandsprocessed0|Total Operations (Shard 0)|Count|Всего||
|cachehits0|Cache Hits (Shard 0)|Count|Всего||
|cachemisses0|Cache Misses (Shard 0)|Count|Всего||
|getcommands0|Gets (Shard 0)|Count|Всего||
|setcommands0|Sets (Shard 0)|Count|Всего||
|evictedkeys0|Evicted Keys (Shard 0)|Count|Всего||
|totalkeys0|Total Keys (Shard 0)|Count|Максимальная||
|expiredkeys0|Expired Keys (Shard 0)|Count|Всего||
|usedmemory0|Used Memory (Shard 0)|Байты|Максимальная||
|usedmemoryRss0|Used Memory RSS (Shard 0)|Байты|Максимальная||
|serverLoad0|Server Load (Shard 0)|Процент|Максимальная||
|cacheWrite0|Cache Write (Shard 0)|Байт/с|Максимальная||
|cacheRead0|Cache Read (Shard 0)|Байт/с|Максимальная||
|percentProcessorTime0|CPU (Shard 0)|Процент|Максимальная||
|connectedclients1|Connected Clients (Shard 1)|Count|Максимальная||
|totalcommandsprocessed1|Total Operations (Shard 1)|Count|Всего||
|cachehits1|Cache Hits (Shard 1)|Count|Всего||
|cachemisses1|Cache Misses (Shard 1)|Count|Всего||
|getcommands1|Gets (Shard 1)|Count|Всего||
|getcommands1|Sets (Shard 1)|Count|Всего||
|evictedkeys1|Evicted Keys (Shard 1)|Count|Всего||
|totalkeys1|Total Keys (Shard 1)|Count|Максимальная||
|expiredkeys1|Expired Keys (Shard 1)|Count|Всего||
|usedmemory1|Used Memory (Shard 1)|Байты|Максимальная||
|usedmemoryRss1|Used Memory RSS (Shard 1)|Байты|Максимальная||
|serverLoad1|Server Load (Shard 1)|Процент|Максимальная||
|cacheWrite1|Cache Write (Shard 1)|Байт/с|Максимальная||
|cacheRead1|Cache Read (Shard 1)|Байт/с|Максимальная||
|percentProcessorTime1|CPU (Shard 1)|Процент|Максимальная||
|connectedclients2|Connected Clients (Shard 2)|Count|Максимальная||
|totalcommandsprocessed2|Total Operations (Shard 2)|Count|Всего||
|cachehits2|Cache Hits (Shard 2)|Count|Всего||
|cachemisses2|Cache Misses (Shard 2)|Count|Всего||
|getcommands2|Gets (Shard 2)|Count|Всего||
|getcommands2|Sets (Shard 2)|Count|Всего||
|evictedkeys2|Evicted Keys (Shard 2)|Count|Всего||
|totalkeys2|Total Keys (Shard 2)|Count|Максимальная||
|expiredkeys2|Expired Keys (Shard 2)|Count|Всего||
|usedmemory2|Used Memory (Shard 2)|Байты|Максимальная||
|usedmemoryRss2|Used Memory RSS (Shard 2)|Байты|Максимальная||
|serverLoad2|Server Load (Shard 2)|Процент|Максимальная||
|cacheWrite2|Cache Write (Shard 2)|Байт/с|Максимальная||
|cacheRead2|Cache Read (Shard 2)|Байт/с|Максимальная||
|percentProcessorTime2|CPU (Shard 2)|Процент|Максимальная||
|connectedclients3|Connected Clients (Shard 3)|Count|Максимальная||
|totalcommandsprocessed3|Total Operations (Shard 3)|Count|Всего||
|cachehits3|Cache Hits (Shard 3)|Count|Всего||
|cachemisses3|Cache Misses (Shard 3)|Count|Всего||
|getcommands3|Gets (Shard 3)|Count|Всего||
|setcommands3|Sets (Shard 3)|Count|Всего||
|evictedkeys3|Evicted Keys (Shard 3)|Count|Всего||
|totalkeys3|Total Keys (Shard 3)|Count|Максимальная||
|expiredkeys3|Expired Keys (Shard 3)|Count|Всего||
|usedmemory3|Used Memory (Shard 3)|Байты|Максимальная||
|usedmemoryRss3|Used Memory RSS (Shard 3)|Байты|Максимальная||
|serverLoad3|Server Load (Shard 3)|Процент|Максимальная||
|cacheWrite3|Cache Write (Shard 3)|Байт/с|Максимальная||
|cacheRead3|Cache Read (Shard 3)|Байт/с|Максимальная||
|percentProcessorTime3|CPU (Shard 3)|Процент|Максимальная||
|connectedclients4|Connected Clients (Shard 4)|Count|Максимальная||
|totalcommandsprocessed4|Total Operations (Shard 4)|Count|Всего||
|cachehits4|Cache Hits (Shard 4)|Count|Всего||
|cachemisses4|Cache Misses (Shard 4)|Count|Всего||
|getcommands4|Gets (Shard 4)|Count|Всего||
|setcommands4|Sets (Shard 4)|Count|Всего||
|evictedkeys4|Evicted Keys (Shard 4)|Count|Всего||
|totalkeys4|Total Keys (Shard 4)|Count|Максимальная||
|expiredkeys4|Expired Keys (Shard 4)|Count|Всего||
|usedmemory4|Used Memory (Shard 4)|Байты|Максимальная||
|usedmemoryRss4|Used Memory RSS (Shard 4)|Байты|Максимальная||
|serverLoad4|Server Load (Shard 4)|Процент|Максимальная||
|cacheWrite4|Cache Write (Shard 4)|Байт/с|Максимальная||
|cacheRead4|Cache Read (Shard 4)|Байт/с|Максимальная||
|percentProcessorTime4|CPU (Shard 4)|Процент|Максимальная||
|connectedclients5|Connected Clients (Shard 5)|Count|Максимальная||
|totalcommandsprocessed5|Total Operations (Shard 5)|Count|Всего||
|cachehits5|Cache Hits (Shard 5)|Count|Всего||
|cachemisses5|Cache Misses (Shard 5)|Count|Всего||
|getcommands5|Gets (Shard 5)|Count|Всего||
|getcommands5|Sets (Shard 5)|Count|Всего||
|evictedkeys5|Evicted Keys (Shard 5)|Count|Всего||
|totalkeys5|Total Keys (Shard 5)|Count|Максимальная||
|expiredkeys5|Expired Keys (Shard 5)|Count|Всего||
|usedmemory5|Used Memory (Shard 5)|Байты|Максимальная||
|usedmemoryRss5|Used Memory RSS (Shard 5)|Байты|Максимальная||
|serverLoad5|Server Load (Shard 5)|Процент|Максимальная||
|cacheWrite5|Cache Write (Shard 5)|Байт/с|Максимальная||
|cacheRead5|Cache Read (Shard 5)|Байт/с|Максимальная||
|percentProcessorTime5|CPU (Shard 5)|Процент|Максимальная||
|connectedclients6|Connected Clients (Shard 6)|Count|Максимальная||
|totalcommandsprocessed6|Total Operations (Shard 6)|Count|Всего||
|cachehits6|Cache Hits (Shard 6)|Count|Всего||
|cachemisses6|Cache Misses (Shard 6)|Count|Всего||
|getcommands6|Gets (Shard 6)|Count|Всего||
|setcommands6|Sets (Shard 6)|Count|Всего||
|evictedkeys6|Evicted Keys (Shard 6)|Count|Всего||
|totalkeys6|Total Keys (Shard 6)|Count|Максимальная||
|expiredkeys6|Expired Keys (Shard 6)|Count|Всего||
|usedmemory6|Used Memory (Shard 6)|Байты|Максимальная||
|usedmemoryRss6|Used Memory RSS (Shard 6)|Байты|Максимальная||
|serverLoad6|Server Load (Shard 6)|Процент|Максимальная||
|cacheWrite6|Cache Write (Shard 6)|Байт/с|Максимальная||
|cacheRead6|Cache Read (Shard 6)|Байт/с|Максимальная||
|percentProcessorTime6|CPU (Shard 6)|Процент|Максимальная||
|connectedclients7|Connected Clients (Shard 7)|Count|Максимальная||
|totalcommandsprocessed7|Total Operations (Shard 7)|Count|Всего||
|cachehits7|Cache Hits (Shard 7)|Count|Всего||
|cachemisses7|Cache Misses (Shard 7)|Count|Всего||
|getcommands7|Gets (Shard 7)|Count|Всего||
|setcommands7|Sets (Shard 7)|Count|Всего||
|evictedkeys7|Evicted Keys (Shard 7)|Count|Всего||
|totalkeys7|Total Keys (Shard 7)|Count|Максимальная||
|expiredkeys7|Expired Keys (Shard 7)|Count|Всего||
|usedmemory7|Used Memory (Shard 7)|Байты|Максимальная||
|usedmemoryRss7|Used Memory RSS (Shard 7)|Байты|Максимальная||
|serverLoad7|Server Load (Shard 7)|Процент|Максимальная||
|cacheWrite7|Cache Write (Shard 7)|Байт/с|Максимальная||
|cacheRead7|Cache Read (Shard 7)|Байт/с|Максимальная||
|percentProcessorTime7|CPU (Shard 7)|Процент|Максимальная||
|connectedclients8|Connected Clients (Shard 8)|Count|Максимальная||
|totalcommandsprocessed8|Total Operations (Shard 8)|Count|Всего||
|cachehits8|Cache Hits (Shard 8)|Count|Всего||
|cachemisses8|Cache Misses (Shard 8)|Count|Всего||
|getcommands8|Gets (Shard 8)|Count|Всего||
|setcommands8|Sets (Shard 8)|Count|Всего||
|evictedkeys8|Evicted Keys (Shard 8)|Count|Всего||
|totalkeys8|Total Keys (Shard 8)|Count|Максимальная||
|expiredkeys8|Expired Keys (Shard 8)|Count|Всего||
|usedmemory8|Used Memory (Shard 8)|Байты|Максимальная||
|usedmemoryRss8|Used Memory RSS (Shard 8)|Байты|Максимальная||
|serverLoad8|Server Load (Shard 8)|Процент|Максимальная||
|cacheWrite8|Cache Write (Shard 8)|Байт/с|Максимальная||
|cacheRead8|Cache Read (Shard 8)|Байт/с|Максимальная||
|percentProcessorTime8|CPU (Shard 8)|Процент|Максимальная||
|connectedclients9|Connected Clients (Shard 9)|Count|Максимальная||
|totalcommandsprocessed9|Total Operations (Shard 9)|Count|Всего||
|cachehits9|Cache Hits (Shard 9)|Count|Всего||
|cachemisses9|Cache Misses (Shard 9)|Count|Всего||
|getcommands9|Gets (Shard 9)|Count|Всего||
|setcommands9|Sets (Shard 9)|Count|Всего||
|evictedkeys9|Evicted Keys (Shard 9)|Count|Всего||
|totalkeys9|Total Keys (Shard 9)|Count|Максимальная||
|expiredkeys9|Expired Keys (Shard 9)|Count|Всего||
|usedmemory9|Used Memory (Shard 9)|Байты|Максимальная||
|usedmemoryRss9|Used Memory RSS (Shard 9)|Байты|Максимальная||
|serverLoad9|Server Load (Shard 9)|Процент|Максимальная||
|cacheWrite9|Cache Write (Shard 9)|Байт/с|Максимальная||
|cacheRead9|Cache Read (Shard 9)|Байт/с|Максимальная||
|percentProcessorTime9|CPU (Shard 9)|Процент|Максимальная||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|TotalCalls|Total Calls|Count|Всего|Общее число вызовов.|
|SuccessfulCalls|Successful Calls|Count|Всего|Число успешных вызовов.|
|TotalErrors|Total Errors|Count|Всего|Общее число вызовов, вернувших сообщение об ошибке (код ответа HTTP 4xx или 5xx).|
|BlockedCalls|Blocked Calls|Count|Всего|Число вызовов, превысивших ограничение скорости или квоты.|
|ServerErrors|Server Errors|Count|Всего|Число вызовов, приведших к внутренней ошибке сервера (код ответа HTTP 5xx).|
|ClientErrors|Client Errors|Count|Всего|Число вызовов, приведших к ошибке на стороне клиента (код ответа HTTP 4xx).|
|DataIn|Входящие данные:|Байты|Всего|Размер входящих данных в байтах.|
|DataOut|Выходные данные|Байты|Всего|Размер исходящих данных в байтах.|
|Latency|Задержка|MilliSeconds|Средняя|Время задержки в миллисекундах.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|Percentage CPU|Загрузка ЦП|Процент|Средняя|Процент Hello выделенных вычислительных единиц, которые в настоящее время используется hello виртуальные машины|
|Сеть (входящий трафик)|Сеть (входящий трафик)|Байты|Всего|Hello число байтов, полученных по всем сетевым интерфейсам hello виртуальных машин (входящий трафик)|
|Сеть (исходящий трафик)|Сеть (исходящий трафик)|Байты|Всего|Hello число байтов out во всех сетевых интерфейсах, hello виртуальных машин (исходящий трафик)|
|Скорость чтения с диска|Скорость чтения с диска|Байты|Всего|Общее число байтов, считанных с диска за период мониторинга.|
|Disk Write Bytes|Скорость записи на диск|Байты|Всего|Общее число байтов, записанных в ходе наблюдения за период toodisk|
|Disk Read Operations/Sec|Чтение с дисков (операций/с)|Число/с|Средняя|Количество операций вода-вывода в секунду при чтении с диска.|
|Disk Write Operations/Sec|Запись на диски (операций/с)|Число/с|Средняя|Количество операций вода-вывода в секунду при записи на диск.|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets;

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|Percentage CPU|Загрузка ЦП|Процент|Средняя|Процент Hello выделенных вычислительных единиц, которые в настоящее время используется hello виртуальные машины|
|Сеть (входящий трафик)|Сеть (входящий трафик)|Байты|Всего|Hello число байтов, полученных по всем сетевым интерфейсам hello виртуальных машин (входящий трафик)|
|Сеть (исходящий трафик)|Сеть (исходящий трафик)|Байты|Всего|Hello число байтов out во всех сетевых интерфейсах, hello виртуальных машин (исходящий трафик)|
|Скорость чтения с диска|Скорость чтения с диска|Байты|Всего|Общее число байтов, считанных с диска за период мониторинга.|
|Disk Write Bytes|Скорость записи на диск|Байты|Всего|Общее число байтов, записанных в ходе наблюдения за период toodisk|
|Disk Read Operations/Sec|Чтение с дисков (операций/с)|Число/с|Средняя|Количество операций вода-вывода в секунду при чтении с диска.|
|Disk Write Operations/Sec|Запись на диски (операций/с)|Число/с|Средняя|Количество операций вода-вывода в секунду при записи на диск.|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|Percentage CPU|Загрузка ЦП|Процент|Средняя|Процент Hello выделенных вычислительных единиц, которые в настоящее время используется hello виртуальные машины|
|Сеть (входящий трафик)|Сеть (входящий трафик)|Байты|Всего|Hello число байтов, полученных по всем сетевым интерфейсам hello виртуальных машин (входящий трафик)|
|Сеть (исходящий трафик)|Сеть (исходящий трафик)|Байты|Всего|Hello число байтов out во всех сетевых интерфейсах, hello виртуальных машин (исходящий трафик)|
|Скорость чтения с диска|Скорость чтения с диска|Байты|Всего|Общее число байтов, считанных с диска за период мониторинга.|
|Disk Write Bytes|Скорость записи на диск|Байты|Всего|Общее число байтов, записанных в ходе наблюдения за период toodisk|
|Disk Read Operations/Sec|Чтение с дисков (операций/с)|Число/с|Средняя|Количество операций вода-вывода в секунду при чтении с диска.|
|Disk Write Operations/Sec|Запись на диски (операций/с)|Число/с|Средняя|Количество операций вода-вывода в секунду при записи на диск.|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|DCIApiCalls|Customer Insights API Calls|Count|Всего||
|DCIMappingImportOperationSuccessfulLines|Mapping Import Operation Successful Lines|Count|Всего||
|DCIMappingImportOperationFailedLines|Mapping Import Operation Failed Lines|Count|Всего||
|DCIMappingImportOperationTotalLines|Mapping Import Operation Total Lines|Count|Всего||
|DCIMappingImportOperationRuntimeInSeconds|Mapping Import Operation Runtime In Seconds|Секунды|Всего||
|DCIOutboundProfileExportSucceeded|Outbound Profile Export Succeeded|Count|Всего||
|DCIOutboundProfileExportFailed|Outbound Profile Export Failed|Count|Всего||
|DCIOutboundProfileExportDuration|Outbound Profile Export Duration|Секунды|Всего||
|DCIOutboundKpiExportSucceeded|Outbound Kpi Export Succeeded|Count|Всего||
|DCIOutboundKpiExportFailed|Outbound Kpi Export Failed|Count|Всего||
|DCIOutboundKpiExportDuration|Outbound Kpi Export Duration|Секунды|Всего||
|DCIOutboundKpiExportStarted|Outbound Kpi Export Started|Секунды|Всего||
|DCIOutboundKpiRecordCount|Outbound Kpi Record Count|Секунды|Всего||
|DCIOutboundProfileExportCount|Outbound Profile Export Count|Секунды|Всего||
|DCIOutboundInitialProfileExportFailed|Outbound Initial Profile Export Failed|Секунды|Всего||
|DCIOutboundInitialProfileExportSucceeded|Outbound Initial Profile Export Succeeded|Секунды|Всего||
|DCIOutboundInitialKpiExportFailed|Outbound Initial Kpi Export Failed|Секунды|Всего||
|DCIOutboundInitialKpiExportSucceeded|Outbound Initial Kpi Export Succeeded|Секунды|Всего||
|DCIOutboundInitialProfileExportDurationInSeconds|Outbound Initial Profile Export Duration In Seconds|Секунды|Всего||
|AdlaJobForStandardKpiFailed|Adla Job For Standard Kpi Failed In Seconds|Секунды|Всего||
|AdlaJobForStandardKpiTimeOut|Adla Job For Standard Kpi TimeOut In Seconds|Секунды|Всего||
|AdlaJobForStandardKpiCompleted|Adla Job For Standard Kpi Completed In Seconds|Секунды|Всего||
|ImportASAValuesFailed|Import ASA Values Failed Count|Count|Всего||
|ImportASAValuesSucceeded|Import ASA Values Succeeded Count|Count|Всего||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|JobEndedSuccess|Successful Jobs|Count|Всего|Количество успешно выполненных заданий.|
|JobEndedFailure|Failed Jobs|Count|Всего|Количество невыполненных заданий.|
|JobEndedCancelled|Cancelled Jobs|Count|Всего|Количество отмененных заданий.|
|JobAUEndedSuccess|Successful AU Time|Секунды|Всего|Общее время AU успешно выполненных заданий.|
|JobAUEndedFailure|Failed AU Time|Секунды|Всего|Общее время AU невыполненных заданий.|
|JobAUEndedCancelled|Cancelled AU Time|Секунды|Всего|Общее время AU отмененных заданий.|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|cpu_percent|Нагрузка ЦП|Процент|Средняя|Нагрузка ЦП|
|compute_limit|Ограничение на единицы вычислений|Count|Средняя|Ограничение на единицы вычислений|
|compute_consumption_percent|Процент использования единиц вычислений|Процент|Средняя|Процент использования единиц вычислений|
|memory_percent|Процент памяти|Процент|Средняя|Процент памяти|
|io_consumption_percent|Процент ввода-вывода данных|Процент|Средняя|Процент ввода-вывода данных|
|storage_percent|Storage percentage|Процент|Средняя|Storage percentage|
|storage_used|Storage used|Байты|Средняя|Storage used|
|storage_limit|Storage limit|Байты|Средняя|Storage limit|
|active_connections|Общее количество активных подключений|Count|Средняя|Общее количество активных подключений|
|connections_failed|Общее количество неудачных подключений|Count|Средняя|Общее количество неудачных подключений|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|cpu_percent|Нагрузка ЦП|Процент|Средняя|Нагрузка ЦП|
|compute_limit|Ограничение на единицы вычислений|Count|Средняя|Ограничение на единицы вычислений|
|compute_consumption_percent|Процент использования единиц вычислений|Процент|Средняя|Процент использования единиц вычислений|
|memory_percent|Процент памяти|Процент|Средняя|Процент памяти|
|io_consumption_percent|Процент ввода-вывода данных|Процент|Средняя|Процент ввода-вывода данных|
|storage_percent|Storage percentage|Процент|Средняя|Storage percentage|
|storage_used|Storage used|Байты|Средняя|Storage used|
|storage_limit|Storage limit|Байты|Средняя|Storage limit|
|active_connections|Общее количество активных подключений|Count|Средняя|Общее количество активных подключений|
|connections_failed|Общее количество неудачных подключений|Count|Средняя|Общее количество неудачных подключений|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Число предпринятых попыток отправки сообщений телеметрии.|Count|Всего|Число попыток toobe устройства в облако телеметрии сообщений отправленных tooyour центра IoT|
|d2c.telemetry.ingress.success|Число отправленных сообщений телеметрии.|Count|Всего|Число сообщений телеметрии устройства в облако успешно отправленных tooyour центра IoT|
|c2d.commands.egress.complete.success|Завершенные команды.|Count|Всего|Количество успешно выполненных устройства hello команд облака на устройство|
|c2d.commands.egress.abandon.success|Прерванные команды.|Count|Всего|Количество команд облака на устройство, прерваны hello устройства|
|c2d.commands.egress.reject.success|Отклоненные команды.|Count|Всего|Количество отклоненных устройства hello команд облака на устройство|
|devices.totalDevices|Общее число устройств.|Count|Всего|Число устройств, зарегистрированных tooyour центра IoT|
|devices.connectedDevices.allProtocol|Подключенные устройства|Count|Всего|Количество устройств, подключенных tooyour центра IoT|
|d2c.telemetry.egress.success|Telemetry messages delivered|Count|Всего|Количество раз, когда сообщения были успешно записаны tooendpoints (всего)|
|d2c.telemetry.egress.dropped|Удаленные сообщения.|Count|Всего|Количество сообщений, отброшенных из-за исчезновения конечную доставки hello|
|d2c.telemetry.egress.orphaned|Потерянные сообщения.|Count|Всего|число Hello сообщения, которые не соответствуют все маршруты, включая hello резервной маршрута|
|d2c.telemetry.egress.invalid|Недопустимые сообщения.|Count|Всего|Hello количество сообщений не доставлено из-за tooincompatibility с конечной точкой hello|
|d2c.telemetry.egress.fallback|Сообщения, соответствующие условиям для резервной конечной точки.|Count|Всего|Количество сообщений, записываемых toohello резервной конечной точки|
|d2c.endpoints.egress.eventHubs|Доставлено сообщений tooEvent конечные точки центра|Count|Всего|Количество раз, когда сообщения были успешно письменного tooEvent конечные точки центра|
|d2c.endpoints.latency.eventHubs|Message latency for Event Hub endpoints|Миллисекунды|Средняя|Hello среднее время задержки между центра IoT toohello входящих сообщений и входящих сообщений в концентратор событий конечную точку, в миллисекундах|
|d2c.endpoints.egress.serviceBusQueues|Доставлено сообщений tooService конечные точки очередей шины|Count|Всего|Количество раз, когда сообщения были конечные точки очередей шины успешно письменного tooService|
|d2c.endpoints.latency.serviceBusQueues|Message latency for Service Bus Queue endpoints|Миллисекунды|Средняя|Hello среднее время задержки между центра IoT toohello входящих сообщений и входящих сообщений в конечную очередь Service Bus в миллисекундах|
|d2c.endpoints.egress.serviceBusTopics|Доставлено сообщений tooService раздел шины конечных точек|Count|Всего|Количество раз, когда сообщения были конечные точки успешно письменного tooService раздел шины|
|d2c.endpoints.latency.serviceBusTopics|Message latency for Service Bus Topic endpoints|Миллисекунды|Средняя|Hello среднее время задержки между центра IoT toohello входящих сообщений и входящих сообщений в конечную точку шины обслуживания, в миллисекундах|
|d2c.endpoints.egress.builtIn.events|Сообщения, доставленные встроенных конечной точки toohello (сообщения и события)|Count|Всего|Количество раз, когда сообщения были встроенных конечной точки успешно письменного toohello (сообщения и события)|
|d2c.endpoints.latency.builtIn.events|Задержка сообщений для конечной точки встроенных hello (сообщения и события)|Миллисекунды|Средняя|Hello среднее время задержки между центра IoT toohello входящих сообщений и входящих сообщений в hello встроенных конечную точку (сообщения и события), в миллисекундах |
|d2c.twin.read.success|Успешные операции чтения с двойников, инициированные устройством.|Count|Всего|Считывает Hello количество всех успешных двойных инициированные устройства.|
|d2c.twin.read.failure|Неудачные операции чтения с двойников, инициированные устройством.|Count|Всего|Hello количество всех ошибок двойных инициированные устройства чтения.|
|d2c.twin.read.size|Размер ответа операций чтения с двойников, инициированных устройством.|Байты|Средняя|двойных среднее Hello, min и max все успешные инициированные устройства чтения.|
|d2c.twin.update.success|Успешные обновления двойников, инициированные устройством.|Count|Всего|количество всех успешных обновлений инициированные устройства двойных Hello.|
|d2c.twin.update.failure|Неудачные обновления двойников, инициированные устройством.|Count|Всего|Hello количество всех сбой обновления двойных инициированные устройства.|
|d2c.twin.update.size|Размер обновлений двойников, инициированных устройством.|Байты|Средняя|Hello average, min и максимальный размер всех успешных инициированные устройства двойных обновлений.|
|c2d.methods.success|Успешные вызовы прямых методов.|Count|Всего|количество всех успешных прямых вызовов Hello.|
|c2d.methods.failure|Неудачные вызовы прямых методов.|Count|Всего|Hello количество всех сбой прямых вызовов.|
|c2d.methods.requestSize|Размер запроса вызовов прямых методов.|Байты|Средняя|Hello average, min и max все успешные направлять запросы, метод.|
|c2d.methods.responseSize|Размер ответа вызовов прямых методов.|Байты|Средняя|Среднее Hello, min и max всех ответов успешно прямой метод.|
|c2d.twin.read.success|Успешные операции чтения с двойников, инициированные из серверной части.|Count|Всего|количество всех успешных операций чтения назад окончания инициировал двойных Hello.|
|c2d.twin.read.failure|Неудачные операции чтения с двойников, инициированные из серверной части.|Count|Всего|Hello количество всех ошибок чтения двойных назад инициировано конечным.|
|c2d.twin.read.size|Размер ответа операций чтения с двойников, инициированных из серверной части.|Байты|Средняя|Среднее Hello, min и max все успешные назад окончания инициировал две операции чтения.|
|c2d.twin.update.success|Успешные обновления двойников, инициированные из серверной части.|Count|Всего|количество всех успешных обновления обратно окончания инициировал двойных Hello.|
|c2d.twin.update.failure|Неудачные обновления двойников, инициированные из серверной части.|Count|Всего|Hello количество всех сбой двойных инициировал назад окончания обновления.|
|c2d.twin.update.size|Размер обновлений двойников, инициированных из серверной части.|Байты|Средняя|двойных Hello average, min и максимальный размер всех успешных инициировал назад окончания обновления.|
|twinQueries.success|Успешные запросы двойников.|Count|Всего|количество всех запросов успешно двойных Hello.|
|twinQueries.failure|Неудачные запросы двойников.|Count|Всего|количество всех неудачных двойных запросов Hello.|
|twinQueries.resultSize|Размер результатов запросов двойников.|Байты|Средняя|Среднее Hello, min и max hello результат размера всех двойных успешных запросов.|
|jobs.createTwinUpdateJob.success|Успешные операции создания заданий обновления двойников.|Count|Всего|количество всех успешного создания задания обновления двойных Hello.|
|jobs.createTwinUpdateJob.failure|Неудачные операции создания заданий обновления двойников.|Count|Всего|количество всех сбоя создания заданий обновления двойных Hello.|
|jobs.createDirectMethodJob.success|Успешные операции создания заданий вызова методов.|Count|Всего|количество всех успешного создания задания прямой метод вызова Hello.|
|jobs.createDirectMethodJob.failure|Неудачные операции создания заданий вызова методов.|Count|Всего|количество всех сбоя создания прямой метод вызова задания Hello.|
|jobs.listJobs.success|Успешных вызовов toolist заданий|Count|Всего|количество всех заданий toolist успешных вызовов Hello.|
|jobs.listJobs.failure|Неудачные вызовы toolist заданий|Count|Всего|Счетчик Hello все неудачные вызовы toolist задания.|
|jobs.cancelJob.success|Успешные отмены заданий.|Count|Всего|Hello количество всех успешных вызовов toocancel задания.|
|jobs.cancelJob.failure|Неудачные отмены заданий.|Count|Всего|Счетчик Hello все неудачные вызовы toocancel задания.|
|jobs.queryJobs.success|Успешные запросы заданий.|Count|Всего|количество всех заданий tooquery успешных вызовов Hello.|
|jobs.queryJobs.failure|Неудачные запросы заданий.|Count|Всего|Счетчик Hello все неудачные вызовы tooquery задания.|
|jobs.completed|Завершенные задания|Count|Всего|Счетчик Hello все завершенные задания.|
|jobs.failed|Неудачные задания.|Count|Всего|Счетчик Hello все невыполненные задания.|
|d2c.telemetry.ingress.sendThrottle|Количество ошибок регулирования|Count|Всего|Количество ошибок регулирования из-за регулирования пропускной способности toodevice|
|dailyMessageQuotaUsed|Общее количество используемых сообщений|Count|Средняя|Количество сообщений, использованных сегодня|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|INREQS|Входящие запросы отправки|Count|Всего|Общее количество входящих запросов отправки для концентратора уведомлений|
|SUCCREQ|Выполненные запросы|Count|Всего|Общее количество успешных запросов для пространства имен|
|FAILREQ|Невыполненные запросы|Count|Всего|Общее количество неудачных запросов для пространства имен|
|SVRBSY|Ошибки из-за занятости сервера|Count|Всего|Общее количество ошибок из-за занятости сервера для пространства имен|
|INTERR|Внутренние ошибки сервера|Count|Всего|Общее количество внутренних ошибок сервера для пространства имен|
|MISCERR|Другие ошибки|Count|Всего|Общее количество неудачных запросов для пространства имен|
|INMSGS|Входящие сообщения|Count|Всего|Общее количество входящих сообщений для пространства имен|
|OUTMSGS|Исходящие сообщения|Count|Всего|Общее количество исходящих сообщений для пространства имен|
|EHINMBS|Входящие байты|Байты|Всего|Пропускная способность входящих сообщений концентратора событий для пространства имен|
|EHOUTMBS|Исходящие байты|Байты|Всего|Общее количество исходящих сообщений для пространства имен|
|EHABL|Archive backlog messages|Count|Всего|Архивные сообщения концентратора событий в списке невыполненных работ для пространства имен|
|EHAMSGS|Archive messages|Count|Всего|Архивные сообщения концентратора событий в пространстве имен|
|EHAMBS|Archive message throughput|Байты|Всего|Пропускная способность архивных сообщений концентратора событий в пространстве имен|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|RunsStarted|Runs Started|Count|Всего|Число запущенных выполнений рабочего процесса.|
|RunsCompleted|Runs Completed|Count|Всего|Число завершенных выполнений рабочего процесса.|
|RunsSucceeded|Runs Succeeded|Count|Всего|Число успешно завершенных выполнений рабочего процесса.|
|RunsFailed|Runs Failed|Count|Всего|Число выполнений рабочего процесса, завершившихся сбоем.|
|RunsCancelled|Runs Cancelled|Count|Всего|Число отмененных выполнений рабочего процесса.|
|RunLatency|Run Latency|Секунды|Средняя|Задержка завершенных выполнений рабочего процесса.|
|RunSuccessLatency|Run Success Latency|Секунды|Средняя|Задержка успешно завершенных выполнений рабочего процесса.|
|RunThrottledEvents|Run Throttled Events|Count|Всего|Число событий регулирования действия или триггера рабочего процесса.|
|RunFailurePercentage|Run Failure Percentage|Процент|Всего|Процент выполнений рабочего процесса, завершившихся сбоем.|
|ActionsStarted|Actions Started |Count|Всего|Число запущенных действий рабочего процесса.|
|ActionsCompleted|Actions Completed |Count|Всего|Число завершенных действий рабочего процесса.|
|ActionsSucceeded|Actions Succeeded |Count|Всего|Число успешно выполненных действий рабочего процесса.|
|ActionsFailed|Actions Failed|Count|Всего|Число действий рабочего процесса, завершившихся сбоем.|
|ActionsSkipped|Actions Skipped |Count|Всего|Число пропущенных действий рабочего процесса.|
|ActionLatency|Action Latency |Секунды|Средняя|Задержка завершенных действий рабочего процесса.|
|ActionSuccessLatency|Action Success Latency |Секунды|Средняя|Задержка успешно выполненных действий рабочего процесса.|
|ActionThrottledEvents|Action Throttled Events|Count|Всего|Число событий регулирования действия рабочего процесса.|
|TriggersStarted|Triggers Started |Count|Всего|Число запущенных триггеров рабочего процесса.|
|TriggersCompleted|Triggers Completed |Count|Всего|Число завершенных триггеров рабочего процесса.|
|TriggersSucceeded|Triggers Succeeded |Count|Всего|Число успешно выполненных триггеров рабочего процесса.|
|TriggersFailed|Triggers Failed |Count|Всего|Число триггеров рабочего процесса, завершившихся со сбоем.|
|TriggersSkipped|Triggers Skipped|Count|Всего|Число пропущенных триггеров рабочего процесса.|
|TriggersFired|Triggers Fired |Count|Всего|Число активированных триггеров рабочего процесса.|
|TriggerLatency|Trigger Latency |Секунды|Средняя|Задержка завершенных триггеров рабочего процесса.|
|TriggerFireLatency|Trigger Fire Latency |Секунды|Средняя|Задержка активированных триггеров рабочего процесса.|
|TriggerSuccessLatency|Trigger Success Latency |Секунды|Средняя|Задержка успешно выполненных триггеров рабочего процесса.|
|TriggerThrottledEvents|Trigger Throttled Events|Count|Всего|Число событий регулирования триггера рабочего процесса.|
|BillableActionExecutions|Billable Action Executions|Count|Всего|Число выполненных действий рабочего процесса, за которые выставляется счет.|
|BillableTriggerExecutions|Billable Trigger Executions|Count|Всего|Число выполненных триггеров рабочего процесса, за которые выставляется счет.|
|TotalBillableExecutions|Total Billable Executions|Count|Всего|Число выполнений рабочего процесса, за которые выставляется счет.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|Throughput|Пропускная способность|Байт/с|Средняя||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|BytesIn|BytesIn|Count|Всего||
|BytesOut|BytesOut|Count|Всего||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|registration.all|Операции регистрации|Count|Всего|Счетчик Hello всех успешных операций регистрации (запросы обновления операции создания и удаления). |
|registration.create|Операции создания регистрации|Count|Всего|Счетчик Hello все операции создания успешной регистрации.|
|registration.update|Операции обновления регистрации|Count|Всего|количество всех обновлений успешной регистрации Hello.|
|registration.get|Операции чтения регистрации|Count|Всего|количество всех запросов успешной регистрации Hello.|
|registration.delete|Операции удаления регистрации|Count|Всего|Счетчик Hello все операции удаления успешной регистрации.|
|incoming|Входящие сообщения|Count|Всего|Hello количество всех успешных отправки вызовов API. |
|incoming.scheduled|Отправлено запланированных push-уведомлений|Count|Всего|Отменено запланированных push-уведомлений|
|incoming.scheduled.cancel|Отменено запланированных push-уведомлений|Count|Всего|Отменено запланированных push-уведомлений|
|scheduled.pending|Запланированных уведомлений в состоянии ожидания|Count|Всего|Запланированных уведомлений в состоянии ожидания|
|installation.all|Операции управления установкой|Count|Всего|Операции управления установкой|
|installation.get|Операции получения установки|Count|Всего|Операции получения установки|
|installation.upsert|Операции создания или обновления установки|Count|Всего|Операции создания или обновления установки|
|installation.patch|Операции исправления установки|Count|Всего|Операции исправления установки|
|installation.delete|Операции удаления установки|Count|Всего|Операции удаления установки|
|outgoing.allpns.success|Успешные уведомления|Count|Всего|Счетчик Hello все успешные уведомления.|
|outgoing.allpns.invalidpayload|Ошибки полезных данных|Count|Всего|Счетчик Hello Push-уведомлений, не удалась, поскольку hello PNS вернул ошибку неправильный полезных данных.|
|outgoing.allpns.pnserror|Ошибки внешней системы уведомлений|Count|Всего|Счетчик Hello Push-уведомлений, которые не удалось из-за ошибки связи со hello PNS (исключает проблемы с проверкой подлинности).|
|outgoing.allpns.channelerror|Ошибки канала|Count|Всего|число Hello помещает в котором произошел сбой, поскольку канал hello недопустимы, не связанные с hello правильный приложения регулирование или истек срок действия.|
|outgoing.allpns.badorexpiredchannel|Ошибки из-за поврежденного или просроченного канала|Count|Всего|число Hello, завершилась ошибкой, поскольку hello канала или токен или registrationId регистрации hello в недействителен или Push-уведомлений.|
|outgoing.wns.success|Успешные уведомления WNS|Count|Всего|Счетчик Hello все успешные уведомления.|
|outgoing.wns.invalidcredentials|Ошибки авторизации WNS (недопустимые учетные данные)|Count|Всего|число Hello помещает, сбой, так как hello PNS не приняла hello, если учетные данные или hello блокируются. (Windows Live не распознает hello учетные данные).|
|outgoing.wns.badchannel|Ошибка из-за поврежденного канала WNS|Count|Всего|Здравствуйте, количество Push-уведомлений, которые не удалась, поскольку не распознано hello ChannelURI регистрации hello в (состояние WNS: 404 не найдено).|
|outgoing.wns.expiredchannel|Ошибка из-за просроченного канала WNS|Count|Всего|Здравствуйте, количество отправок, сбой, так как hello ChannelURI истек срок действия (состояние WNS: 410 останова).|
|outgoing.wns.throttled|Регулируемые уведомления WNS|Count|Всего|количество отправок, сбой, так как WNS регулирует это приложение Hello (состояние WNS: 406 неприемлемо).|
|outgoing.wns.tokenproviderunreachable|Ошибки авторизации WNS (нет доступа)|Count|Всего|Windows Live недоступна.|
|outgoing.wns.invalidtoken|Ошибки авторизации WNS (недопустимый маркер)|Count|Всего|Hello токена, предоставляемого tooWNS является недопустимым (WNS состояние: ошибка проверки подлинности 401).|
|outgoing.wns.wrongtoken|Ошибки авторизации WNS (неправильный маркер)|Count|Всего|Здравствуйте маркера, предоставляемых tooWNS является допустимым, но для другого приложения (состояние WNS: 403 запрещено). Это может произойти, если hello ChannelURI регистрации hello в связан с другим приложением. Проверьте, что клиентское приложение hello связан с hello одного приложения, чьи учетные данные будут в концентраторе уведомлений hello.|
|outgoing.wns.invalidnotificationformat|Недопустимый формат уведомления WNS|Count|Всего|Недопустимый формат уведомления hello Hello (состояние WNS: 400). Обратите внимание, что WNS не отклоняет все недопустимые полезные данные.|
|outgoing.wns.invalidnotificationsize|Ошибка из-за недопустимого размера уведомления WNS|Count|Всего|полезные данные уведомления Hello слишком велик (состояние WNS: 413).|
|outgoing.wns.channelthrottled|Канал WNS регулируется|Count|Всего|уведомления Hello было удалено, так как регулируется hello ChannelURI регистрации hello в (заголовок ответа WNS: X-WNS-NotificationStatus:channelThrottled).|
|outgoing.wns.channeldisconnected|Канал WNS отсоединен|Count|Всего|уведомления Hello было удалено, так как регулируется hello ChannelURI регистрации hello в (заголовок ответа WNS: X-WNS-DeviceConnectionStatus: отключен).|
|outgoing.wns.dropped|Пропущенные уведомления WNS|Count|Всего|уведомления Hello было удалено, так как регулируется hello ChannelURI регистрации hello в (X-WNS-NotificationStatus: удаленный, но не X-WNS-DeviceConnectionStatus: отключен).|
|outgoing.wns.pnserror|Ошибки WNS|Count|Всего|Уведомление не доставлено из-за ошибок связи с WNS.|
|outgoing.wns.authenticationerror|Ошибки проверки подлинности WNS|Count|Всего|Уведомление не доставлено из-за ошибок связи Windows Live с использованием недопустимых учетных данных или неправильного маркера.|
|outgoing.apns.success|Успешные уведомления APNS|Count|Всего|Счетчик Hello все успешные уведомления.|
|outgoing.apns.invalidcredentials|Ошибки авторизации APNS|Count|Всего|число Hello помещает, сбой, так как hello PNS не приняла hello, если учетные данные или hello блокируются.|
|outgoing.apns.badchannel|Ошибка из-за поврежденного канала APNS|Count|Всего|Здравствуйте, количество Push-уведомлений, которые не удалось из-за недопустимого токена hello (код состояния APNS: 8).|
|outgoing.apns.expiredchannel|Ошибка из-за просроченного канала APNS|Count|Всего|Счетчик Hello маркер, который были признаны недействительными по каналу обратной связи APNS hello.|
|outgoing.apns.invalidnotificationsize|Ошибка из-за недопустимого размера уведомления APNS|Count|Всего|Здравствуйте, количество Push-уведомлений, которые не удалось, так как имеет слишком большой объем полезных данных hello (код состояния APNS: 7).|
|outgoing.apns.pnserror|Ошибки APNS|Count|Всего|число Hello помещает, сбой из-за ошибок связи с APNS.|
|outgoing.gcm.success|Успешные уведомления GCM|Count|Всего|Счетчик Hello все успешные уведомления.|
|outgoing.gcm.invalidcredentials|Ошибки авторизации GCM (недопустимые учетные данные)|Count|Всего|число Hello помещает, сбой, так как hello PNS не приняла hello, если учетные данные или hello блокируются.|
|outgoing.gcm.badchannel|Ошибка из-за поврежденного канала GCM|Count|Всего|Здравствуйте, количество Push-уведомлений, которые не удалась, поскольку не распознан registrationId hello регистрации hello в (GCM результат: недопустимая регистрация).|
|outgoing.gcm.expiredchannel|Ошибка из-за просроченного канала GCM|Count|Всего|Здравствуйте, количество Push-уведомлений, которые не удалась, поскольку истек срок действия registrationId hello регистрации hello в (GCM результат: NotRegistered).|
|outgoing.gcm.throttled|Регулируемые уведомления GCM|Count|Всего|количество отправок, сбой, так как GCM регулированию это приложение Hello (код состояния GCM: 501-599 или результат: недоступен).|
|outgoing.gcm.invalidnotificationformat|Недопустимый формат уведомления GCM|Count|Всего|Здравствуйте, количество Push-уведомлений, не прошедшие из-за неправильно форматирован hello полезных данных (результат GCM: InvalidDataKey или InvalidTtl).|
|outgoing.gcm.invalidnotificationsize|Ошибка из-за недопустимого размера уведомления GCM|Count|Всего|Здравствуйте, количество Push-уведомлений, которые не удалось, так как имеет слишком большой объем полезных данных hello (GCM результат: MessageTooBig).|
|outgoing.gcm.wrongchannel|Ошибка из-за неправильного канала GCM|Count|Всего|число Hello Push-уведомлений, сбой из-за registrationId hello регистрации hello в связанных toohello текущее приложение (GCM результат: InvalidPackageName).|
|outgoing.gcm.pnserror|Ошибки GCM|Count|Всего|число Hello помещает, сбой из-за ошибок связи с GCM.|
|outgoing.gcm.authenticationerror|Ошибки проверки подлинности GCM|Count|Всего|Здравствуйте, количество Push-уведомлений, которые не удалась, поскольку hello PNS не приняла hello предоставленных учетных данных учетные данные hello заблокированы или hello SenderId настроена неправильно в приложение hello (GCM результат: MismatchedSenderId).|
|outgoing.mpns.success|Успешные уведомления MPNS|Count|Всего|Счетчик Hello все успешные уведомления.|
|outgoing.mpns.invalidcredentials|Недопустимые учетные данные MPNS|Count|Всего|число Hello помещает, сбой, так как hello PNS не приняла hello, если учетные данные или hello блокируются.|
|outgoing.mpns.badchannel|Ошибка из-за поврежденного канала MPNS|Count|Всего|Здравствуйте, количество Push-уведомлений, которые не удалась, поскольку не распознано hello ChannelURI регистрации hello в (состояние MPNS: 404 не найдено).|
|outgoing.mpns.throttled|Регулируемые уведомления MPNS|Count|Всего|количество отправок, сбой, так как MPNS регулирует это приложение Hello (WNS MPNS: 406 неприемлемо).|
|outgoing.mpns.invalidnotificationformat|Недопустимый формат уведомления MPNS|Count|Всего|число Hello помещает, сбой, так как имеет слишком большой объем полезных данных hello hello уведомления.|
|outgoing.mpns.channeldisconnected|Канал MPNS отсоединен|Count|Всего|Hello количество Push-уведомлений, которые не удалась, поскольку был отключен hello ChannelURI регистрации hello в (состояние MPNS: не удалось найти 412).|
|outgoing.mpns.dropped|Пропущенные уведомления MPNS|Count|Всего|Здравствуйте, количество отправок удаленных MPNS (заголовок ответа MPNS: X NotificationStatus: QueueFull или Suppressed).|
|outgoing.mpns.pnserror|Ошибки MPNS|Count|Всего|число Hello помещает, сбой из-за ошибок связи с MPNS.|
|outgoing.mpns.authenticationerror|Ошибки проверки подлинности MPNS|Count|Всего|число Hello помещает, сбой, так как hello PNS не приняла hello, если учетные данные или hello блокируются.|
|notificationhub.pushes|Все исходящие уведомления|Count|Всего|Все исходящих уведомлений hello концентратора уведомлений|
|incoming.all.requests|Все входящие запросы|Count|Всего|Общее количество входящих запросов для концентратора уведомлений|
|Incoming.all.failedrequests|Все неудачные входящие запросы|Count|Всего|Общее количество неудачных входящих запросов для концентратора уведомлений|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|qpu_metric|QPU|Count|Средняя|QPU. Диапазоны: 0–100 для S1, 0–200 для S2 и 0–400 для S4.|
|memory_metric|Память|Байты|Средняя|Память. Диапазоны: 0–25 ГБ для S1, 0–50 ГБ для S2 и 0–100 ГБ для S4.|
|TotalConnectionRequests|Общее число запросов на подключение|Count|Средняя|Общее число запросов на подключение. Поступившие запросы.|
|SuccessfullConnectionsPerSec|Число успешных подключений в секунду|Число/с|Средняя|Частота успешных установок подключений.|
|TotalConnectionFailures|Общее число неудачных подключений|Count|Средняя|Общее число неудачных попыток подключения.|
|CurrentUserSessions|Текущие пользовательские сеансы|Count|Средняя|Текущее число установленных пользовательских сеансов.|
|QueryPoolBusyThreads|Занятые потоки в пуле запросов|Count|Средняя|Число занятых потоков в пуле потоков запросов hello.|
|CommandPoolJobQueueLength|Длина очереди заданий пула команд|Count|Средняя|Число заданий в очереди пула потоков команд hello hello.|
|ProcessingPoolJobQueueLength|Длина очереди заданий пула обработки|Count|Средняя|Количество заданий не ввода-вывода в очереди пула потоков обработки hello hello.|
|CurrentConnections|Подключение: текущие подключения|Count|Средняя|Текущее число установленных клиентских подключений.|
|CleanerCurrentPrice|Память: текущая цена очистки|Count|Средняя|Текущая цена памяти, $/ байт/время, нормализованная too1000.|
|CleanerMemoryShrinkable|Память: сжимаемая память очистки|Байты|Средняя|Объем памяти в байтах, toopurging субъекта по hello фоновой очистки.|
|CleanerMemoryNonshrinkable|Память: несжимаемая память очистки|Байты|Средняя|Объем памяти в байтах, не toopurging субъекта по hello фоновой очистки.|
|MemoryUsage|Память: использование памяти|Байты|Средняя|Использование hello процессом сервера согласно расчетам стоимости очистки памяти в памяти. Равно toocounter Process\PrivateBytes плюс размер hello размещенный в памяти данных без учета памяти, сопоставленной или выделенной с помощью hello в памяти xVelocity (VertiPaq) сверх подсистемы xVelocity hello предельный объем памяти.|
|MemoryLimitHard|Память: твердый лимит памяти|Байты|Средняя|Твердый лимит памяти, из файла конфигурации.|
|MemoryLimitHigh|Память: верхний предел памяти|Байты|Средняя|Верхняя граница объема памяти, из файла конфигурации.|
|MemoryLimitLow|Память: нижний предел памяти|Байты|Средняя|Нижняя граница объема памяти, из файла конфигурации.|
|MemoryLimitVertiPaq|Память: ограничение памяти VertiPaq|Байты|Средняя|Ограничение памяти, из файла конфигурации.|
|Quota|Память: квота|Байты|Средняя|Текущая квота памяти, в байтах. Квота памяти также называется выделением или резервированием памяти.|
|QuotaBlocked|Память: заблокировано квот|Count|Средняя|Текущее число запросов на квоту, заблокированных до высвобождения других квот памяти.|
|VertiPaqNonpaged|Память: размер нестраничных данных VertiPaq|Байты|Средняя|Байт памяти заблокирован в hello рабочий набор для использования в памяти подсистемой hello.|
|VertiPaqPaged|Память: размер страничных данных VertiPaq|Байты|Средняя|Размер памяти (в байтах), занятой страничными данными в памяти.|
|RowsReadPerSec|Обработка: считано строк в секунду|Число/с|Средняя|Интенсивность считывания строк из всех реляционных баз данных.|
|RowsConvertedPerSec|Обработка: преобразовано строк в секунду|Число/с|Средняя|Интенсивность преобразованных в ходе обработки строк.|
|RowsWrittenPerSec|Обработка: записано строк в секунду|Число/с|Средняя|Интенсивность записанных в ходе обработки строк.|
|CommandPoolBusyThreads|Потоки: занятые потоки в пуле команд|Count|Средняя|Число занятых потоков в пуле потоков команд hello.|
|CommandPoolIdleThreads|Потоки: бездействующие потоки в пуле команд|Count|Средняя|Число бездействующих потоков в пуле потоков команд hello.|
|LongParsingBusyThreads|Потоки: занятые потоки продолжительного анализа|Count|Средняя|Число занятых потоков в hello продолжительный анализ пула потоков.|
|LongParsingIdleThreads|Потоки: бездействующие потоки продолжительного анализа|Count|Средняя|Число бездействующих потоков в hello продолжительный анализ пула потоков.|
|LongParsingJobQueueLength|Потоки: длина очереди заданий продолжительного анализа|Count|Средняя|Число заданий в очереди hello hello продолжительный анализ пула потоков.|
|ProcessingPoolBusyIOJobThreads|Потоки: занятые потоки ввода-вывода в пуле обработки заданий|Count|Средняя|Количество потоков, выполняющих задания ввода-вывода в hello в пуле потоков обработки.|
|ProcessingPoolBusyNonIOThreads|Потоки: занятые потоки в пуле обработки, не связанные с вводом-выводом|Count|Средняя|Количество потоков, выполняющих задания без ввода-вывода в hello в пуле потоков обработки.|
|ProcessingPoolIOJobQueueLength|Потоки: длина очереди заданий ввода-вывода пула обработки|Count|Средняя|Количество заданий ввода-вывода в очереди пула потоков обработки hello hello.|
|ProcessingPoolIdleIOJobThreads|Потоки: бездействующие потоки ввода-вывода в пуле обработки заданий|Count|Средняя|Число бездействующих потоков заданий ввода-вывода в hello в пуле потоков обработки.|
|ProcessingPoolIdleNonIOThreads|Потоки: бездействующие потоки в пуле обработки, не связанные с вводом-выводом|Count|Средняя|Число бездействующих потоков в пул потоков обработки hello выделенные задания toonon с вводом выводом.|
|QueryPoolIdleThreads|Потоки: бездействующие потоки в пуле запросов|Count|Средняя|Число бездействующих потоков заданий ввода-вывода в hello в пуле потоков обработки.|
|QueryPoolJobQueueLength|Потоки: длина очереди заданий пула запросов|Count|Средняя|Число заданий в очереди пула потоков запросов hello hello.|
|ShortParsingBusyThreads|Потоки: занятые потоки быстрого анализа|Count|Средняя|Число занятых потоков в hello короткий пулом потоков синтаксического анализа.|
|ShortParsingIdleThreads|Потоки: бездействующие потоки быстрого анализа|Count|Средняя|Число бездействующих потоков в hello короткий пулом потоков синтаксического анализа.|
|ShortParsingJobQueueLength|Потоки: длина очереди заданий быстрого анализа|Count|Средняя|Число заданий в очереди hello hello короткий пулом потоков синтаксического анализа.|
|memory_thrashing_metric|Пробуксовка памяти|Процент|Средняя|Среднее значение пробуксовки памяти.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Description (Описание)|
|---|---|---|---|---|
|SearchLatency|Search Latency|Секунды|Средняя|Задержка среднее поиска для службы поиска hello|
|SearchQueriesPerSecond|Search queries per second|Число/с|Средняя|Поисковые запросы в секунду для службы поиска hello|
|ThrottledSearchQueriesPercentage|Throttled search queries percentage|Процент|Средняя|Процент запросов поиска, которые были регулирование для службы поиска hello|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|CPUXNS|CPU usage per namespace|Процент|Максимальная|Метрика использования ЦП пространства имен служебной шины для премиум-обслуживания|
|WSXNS|Memory size usage per namespace|Процент|Максимальная|Метрика использования памяти пространства имен служебной шины для премиум-обслуживания|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|cpu_percent|Процент использования ЦП|Процент|Средняя|Процент использования ЦП|
|physical_data_read_percent|Процент операций ввода/вывода данных|Процент|Средняя|Процент операций ввода/вывода данных|
|log_write_percent|Log IO percentage|Процент|Средняя|Log IO percentage|
|dtu_consumption_percent|Процент использования DTU|Процент|Средняя|Процент использования DTU|
|storage|Total database size|Байты|Максимальная|Total database size|
|connection_successful|Успешные подключения|Count|Всего|Успешные подключения|
|connection_failed|Неудачные подключения|Count|Всего|Неудачные подключения|
|blocked_by_firewall|Заблокировано брандмауэром|Count|Всего|Заблокировано брандмауэром|
|deadlock|Взаимоблокировки|Count|Всего|Взаимоблокировки.|
|storage_percent|Размер базы данных в процентах|Процент|Максимальная|Размер базы данных в процентах|
|xtp_storage_percent|Процент хранилища выполняющейся в памяти OLTP|Процент|Средняя|Процент хранилища выполняющейся в памяти OLTP|
|workers_percent|Workers percentage|Процент|Средняя|Workers percentage|
|sessions_percent|Процент использования сеансов|Процент|Средняя|Процент использования сеансов|
|dtu_limit|Лимит DTU|Count|Средняя|Лимит DTU|
|dtu_used|DTU used|Count|Средняя|DTU used|
|dwu_limit|Лимит DWU|Count|Максимальная|Лимит DWU|
|dwu_consumption_percent|DWU percentage|Процент|Максимальная|DWU percentage|
|dwu_used|DWU used|Count|Максимальная|DWU used|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|cpu_percent|Процент использования ЦП|Процент|Средняя|Процент использования ЦП|
|database_cpu_percent|Процент использования ЦП|Процент|Средняя|Процент использования ЦП|
|physical_data_read_percent|Процент операций ввода/вывода данных|Процент|Средняя|Процент операций ввода/вывода данных|
|database_physical_data_read_percent|Процент операций ввода/вывода данных|Процент|Средняя|Процент операций ввода/вывода данных|
|log_write_percent|Log IO percentage|Процент|Средняя|Log IO percentage|
|database_log_write_percent|Log IO percentage|Процент|Средняя|Log IO percentage|
|dtu_consumption_percent|Процент использования DTU|Процент|Средняя|Процент использования DTU|
|database_dtu_consumption_percent|Процент использования DTU|Процент|Средняя|Процент использования DTU|
|storage_percent|Storage percentage|Процент|Средняя|Storage percentage|
|workers_percent|Workers percentage|Процент|Средняя|Workers percentage|
|database_workers_percent|Workers percentage|Процент|Средняя|Workers percentage|
|sessions_percent|Процент использования сеансов|Процент|Средняя|Процент использования сеансов|
|database_sessions_percent|Процент использования сеансов|Процент|Средняя|Процент использования сеансов|
|eDTU_limit|eDTU limit|Count|Средняя|eDTU limit|
|storage_limit|Storage limit|Байты|Средняя|Storage limit|
|eDTU_used|eDTU used|Count|Средняя|eDTU used|
|storage_used|Storage used|Байты|Средняя|Storage used|
|database_storage_used|Storage used|Байты|Средняя|Storage used|
|xtp_storage_percent|Процент хранилища выполняющейся в памяти OLTP|Процент|Средняя|Процент хранилища выполняющейся в памяти OLTP|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|dtu_consumption_percent|Процент использования DTU|Процент|Средняя|Процент использования DTU|
|database_dtu_consumption_percent|Процент использования DTU|Процент|Средняя|Процент использования DTU|
|storage_used|Storage used|Байты|Средняя|Storage used|
|database_storage_used|Storage used|Байты|Средняя|Storage used|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|ResourceUtilization|Использование единиц потоковой передачи (%)|Процент|Максимальная|Использование единиц потоковой передачи (%)|
|InputEvents|Входные события|Count|Всего|Входные события|
|InputEventBytes|Байты входного события|Байты|Всего|Байты входного события|
|LateInputEvents|События позднего ввода|Count|Всего|События позднего ввода|
|OutputEvents|Выходные события|Count|Всего|Выходные события|
|ConversionErrors|Ошибки преобразования данных|Count|Всего|Ошибки преобразования данных|
|Errors|Ошибки среды выполнения|Count|Всего|Ошибки среды выполнения|
|DroppedOrAdjustedEvents|Неупорядоченные события|Count|Всего|Неупорядоченные события|
|AMLCalloutRequests|Запросы функций|Count|Всего|Запросы функций|
|AMLCalloutFailedRequests|Неудачные запросы функций|Count|Всего|Неудачные запросы функций|
|AMLCalloutInputEvents|События функций|Count|Всего|События функций|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|CpuPercentage|Процент использования ЦП|Процент|Средняя|Процент использования ЦП|
|MemoryPercentage|Процент использования памяти|Процент|Средняя|Процент использования памяти|
|DiskQueueLength|Длина дисковой очереди|Count|Всего|Длина дисковой очереди|
|HttpQueueLength|Длина очереди HTTP:|Count|Всего|Длина очереди HTTP:|
|BytesReceived|Входящие данные:|Байты|Всего|Входящие данные:|
|BytesSent|Выходные данные|Байты|Всего|Выходные данные|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (за исключением функций)

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|CpuTime|Время ЦП:|Секунды|Всего|Время ЦП:|
|Requests|Запросы|Count|Всего|Запросы|
|BytesReceived|Входящие данные:|Байты|Всего|Входящие данные:|
|BytesSent|Выходные данные|Байты|Всего|Выходные данные|
|Http101|Http 101|Count|Всего|Http 101|
|Http2xx|HTTP 2xx|Count|Всего|HTTP 2xx|
|Http3xx|HTTP 3xx:|Count|Всего|HTTP 3xx:|
|Http401|HTTP 401:|Count|Всего|HTTP 401:|
|Http403|HTTP 403:|Count|Всего|HTTP 403:|
|Http404|HTTP 404:|Count|Всего|HTTP 404:|
|Http406|HTTP 406:|Count|Всего|HTTP 406:|
|Http4xx|HTTP 4xx:|Count|Всего|HTTP 4xx:|
|Http5xx|Ошибки HTTP-сервера:|Count|Всего|Ошибки HTTP-сервера:|
|MemoryWorkingSet|рабочий набор памяти;|Байты|Средняя|рабочий набор памяти;|
|AverageMemoryWorkingSet|средний размер рабочего набора памяти;|Байты|Средняя|средний размер рабочего набора памяти;|
|AverageResponseTime|Среднее время ответа:|Секунды|Средняя|Среднее время ответа:|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (функции)

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|BytesReceived|Входящие данные:|Байты|Всего|Входящие данные:|
|BytesSent|Выходные данные|Байты|Всего|Выходные данные|
|Http5xx|Ошибки HTTP-сервера:|Count|Всего|Ошибки HTTP-сервера:|
|MemoryWorkingSet|рабочий набор памяти;|Байты|Средняя|рабочий набор памяти;|
|AverageMemoryWorkingSet|средний размер рабочего набора памяти;|Байты|Средняя|средний размер рабочего набора памяти;|
|FunctionExecutionUnits|Function Execution Units|Count|Средняя|Единицы выполнения функции.|
|FunctionExecutionCount|Function Execution Count|Count|Средняя|Число выполнений функции.|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Метрика|Отображаемое имя метрики|Единица измерения|Тип статистической обработки|Описание|
|---|---|---|---|---|
|CpuTime|Время ЦП:|Секунды|Всего|Время ЦП:|
|Requests|Запросы|Count|Всего|Запросы|
|BytesReceived|Входящие данные:|Байты|Всего|Входящие данные:|
|BytesSent|Выходные данные|Байты|Всего|Выходные данные|
|Http101|Http 101|Count|Всего|Http 101|
|Http2xx|HTTP 2xx|Count|Всего|HTTP 2xx|
|Http3xx|HTTP 3xx:|Count|Всего|HTTP 3xx:|
|Http401|HTTP 401:|Count|Всего|HTTP 401:|
|Http403|HTTP 403:|Count|Всего|HTTP 403:|
|Http404|HTTP 404:|Count|Всего|HTTP 404:|
|Http406|HTTP 406:|Count|Всего|HTTP 406:|
|Http4xx|HTTP 4xx:|Count|Всего|HTTP 4xx:|
|Http5xx|Ошибки HTTP-сервера:|Count|Всего|Ошибки HTTP-сервера:|
|MemoryWorkingSet|рабочий набор памяти;|Байты|Средняя|рабочий набор памяти;|
|AverageMemoryWorkingSet|средний размер рабочего набора памяти;|Байты|Средняя|средний размер рабочего набора памяти;|
|AverageResponseTime|Среднее время ответа:|Секунды|Средняя|Среднее время ответа:|
|FunctionExecutionUnits|Function Execution Units|Count|Средняя|Единицы выполнения функции.|
|FunctionExecutionCount|Function Execution Count|Count|Средняя|Число выполнений функции.|

## <a name="next-steps"></a>Дальнейшие действия
* [Прочитайте о метриках в Azure Monitor](monitoring-overview-metrics.md)
* [Создайте оповещения на основе метрик](insights-receive-alert-notifications.md)
* [Экспорт toostorage метрики концентратора событий и анализа журналов](monitoring-overview-of-diagnostic-logs.md)
