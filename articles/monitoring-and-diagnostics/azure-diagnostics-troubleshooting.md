---
title: "aaaTroubleshooting диагностики Azure | Документы Microsoft"
description: "Устранение неполадок при использовании системы диагностики Azure на виртуальных машинах, в Service Fabric или в облачных службах."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: robb
ms.openlocfilehash: daaf9fa4c40982eb9ba04030d7e8ea1ad9fe085b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-troubleshooting"></a>Устранение неполадок с помощью системы диагностики Azure
Устранение неполадок toousing соответствующие сведения диагностики Azure. Дополнительные сведения о системе диагностики Azure см. в [обзоре системы диагностики Azure](azure-diagnostics.md).

## <a name="logical-components"></a>Логические компоненты
**Запуск диагностики подключаемого модуля (DiagnosticsPluginLauncher.exe)**: запускает hello расширения диагностики Azure. Служит в качестве входа hello точки процесса.

**Подключаемый модуль диагностики (DiagnosticsPlugin.exe)**: основной процесс, который запускается путем запуска hello выше и настраивает hello Monitoring Agent, запустившая его управляет времени его существования. 

**Агент наблюдения (агента наблюдения\*процессы .exe)**: эти процессы hello большая часть работы hello; т. е. мониторинг, сбора и передачи hello диагностические данные.  

## <a name="logartifact-paths"></a>Пути к журналам и артефактам
Ниже приведены важные журналы hello пути toosome и артефакты. Мы хранить ссылки toothese во всей остальной hello hello документа:
### <a name="cloud-services"></a>Облачные службы
| Артефакт | Путь |
| --- | --- |
| **Файл конфигурации системы диагностики Azure** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<версия>\Config.txt |
| **Файлы журналов** | C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<версия>\ |
| **Локальное хранилище данных диагностики** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Tables |
| **Файл конфигурации агента мониторинга** | C:\Resources\Directory\<CloudServiceDeploymentID>.\<RoleName>.DiagnosticStore\WAD0107\Configuration\MaConfig.xml |
| **Пакет расширений системы диагностики Azure** | %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<версия> |
| **Путь к служебной программе сбора журналов** | %SystemDrive%\Packages\GuestAgent\ |
| **Файл журнала MonAgentHost** | C:\Resources\Directory\<ИД_разверт._облачн._службы>.\<имя_роли>.DiagnosticStore\WAD0107\Configuration\MonAgentHost.<текущ._номер>.log |

### <a name="virtual-machines"></a>Виртуальные машины
| Артефакт | Путь |
| --- | --- |
| **Файл конфигурации системы диагностики Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<версия>\RuntimeSettings |
| **Файлы журналов** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<версия>\Logs\ |
| **Локальное хранилище данных диагностики** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<версия_системы_диагностики>\WAD0107\Tables |
| **Файл конфигурации агента мониторинга** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<версия_системы_диагностики>\WAD0107\Configuration\MaConfig.xml |
| **Состояние файла** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<версия>\Status |
| **Пакет расширений системы диагностики Azure** | C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<версия_системы_диагностики>|
| **Путь к служебной программе сбора журналов** | C:\WindowsAzure\Packages |
| **Файл журнала MonAgentHost** | C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<версия_системы_диагностики>\WAD0107\Configuration\MonAgentHost.<текущ._номер>.log |

## <a name="metric-data-doesnt-show-in-azure-portal"></a>Данные метрики не отображаются на портале Azure
Система диагностики Azure предоставляет ряд данных метрики, которые можно отобразить на портале Azure. При наличии проблем с просмотра этих данных в портале учетной записи хранения диагностики hello check -> WADMetrics\* таблица toosee, если существуют соответствующие записи метрики hello. Здесь hello PartitionKey таблицы hello hello идентификатор ресурса виртуальной машины или набора масштабирования виртуальных машин, который hello RowKey имя метрики hello т. е. имя счетчика производительности.

Если неверный идентификатор ресурса hello, проверьте конфигурацию диагностики -> метрики -> ResourceId toosee, если идентификатор ресурса hello задано правильно.

Если нет данных для конкретного показателя hello, проверьте конфигурацию диагностики -> PerformanceCounter toosee, если метрика hello (счетчик производительности) включен. Мы можем добавить следующие счетчики по умолчанию hello.
- \Processor(_Total)\% Загруженность процессора
- \Память\доступные байты
- \ASP.NET Applications(__Total__)\Requests/Sec
- \ASP.NET Applications(__Total__)\Errors Total/Sec
- \ASP.NET\Requests Queued
- \ASP.NET\Requests Rejected
- \Processor(w3wp)\% Processor Time
- \Process(w3wp)\Private Bytes
- \Process(WaIISHost)\% Processor Time
- \Process(WaIISHost)\Private Bytes
- \Process(WaWorkerHost)\% Processor Time
- \Process(WaWorkerHost)\Private Bytes
- \Memory\Page Faults/sec
- \.NET CLR Memory(_Global_)\% Time in GC
- \LogicalDisk(C:)\Disk Write Bytes/sec
- \LogicalDisk(C:)\Disk Read Bytes/sec
- \LogicalDisk(D:)\Disk Write Bytes/sec
- \LogicalDisk(D:)\Disk Read Bytes/sec

Если hello конфигурации задано правильно, но все равно не отображаются данные метрик hello, следуйте правилам hello ниже hello дальнейшего исследования.


## <a name="azure-diagnostics-is-not-starting"></a>Система диагностики Azure не запускается
Посмотрите на **DiagnosticsPluginLauncher.log** и **DiagnosticsPlugin.log** файлы из места hello hello файлы журналов, предоставляемых выше сведения о том, почему диагностики сбой toostart. 

Если эти журналы указывают `Monitoring Agent not reporting success after launch`, это означает, что произошел сбой запуска MonAgentHost.exe. Найдите в журналах hello, в hello местоположение, указанное для `MonAgentHost log file` hello выше в разделе.

Последняя строка Hello hello файлов журнала содержит код выхода hello.  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```
Если найти **отрицательное** код выхода, см. в toohello [выхода кодовой таблицы](#azure-diagnostics-plugin-exit-codes) в hello [ссылки](#references).

## <a name="diagnostics-data-is-not-logged-tooazure-storage"></a>Диагностические данные — не регистрируются tooAzure хранилища
Определите данные не отображаются или только некоторые из данных hello не отображаются.

### <a name="diagnostics-infrastructure-logs"></a>Журналы инфраструктуры диагностики
В журналах инфраструктуры диагностики записываются все ошибки системы диагностики Azure. Убедитесь, что вы включили ([как?](#how-to-check-diagnostics-extension-configuration)) записи журналов диагностики инфраструктуры в конфигурации и быстро найти соответствующие ошибки, которые отображаются в hello `DiagnosticInfrastructureLogsTable` таблицу в учетной записи хранения настроенных.

### <a name="no-data-is-showing-up"></a>Данные не отображаются
Наиболее распространенной причиной Hello полностью отсутствует данных события является хранилища неправильно определенные сведения об учетной записи.

Решение. Исправьте файл конфигурации системы диагностики и переустановите систему диагностики.

Учетная запись хранения hello правильно настроен, удаленного рабочего стола на компьютере hello и убедитесь, что DiagnosticsPlugin.exe MonAgentCore.exe, работают ли и. Если они не выполняются, следуйте сведениям в разделе [Система диагностики Azure не запускается](#azure-diagnostics-is-not-starting). При выполнении процессов hello перехода слишком[является получение локально собранные данные](#is-data-getting-captured-locally) и следуйте инструкциям в этом руководстве оттуда.

### <a name="part-of-hello-data-is-missing"></a>Отсутствует часть данных hello
В некоторых случаях вы можете получать не все данные. Это означает сбор данных hello / передача конвейера задано правильно. Выполните подразделах hello Вот toonarrow работу с какой проблемой hello:
#### <a name="is-collection-configured"></a>Проверка параметров сбора 
Конфигурация диагностики содержит hello часть, которая указывает, что для определенного типа данных toobe собраны. [Проверьте конфигурацию](#how-to-check-diagnostics-extension-configuration) toomake убедиться, что вам не нужны для данных вы не настроены для коллекции.
#### <a name="is-hello-host-generating-data"></a>Узел hello формирование данных:
- **Счетчики производительности**: откройте системный монитор и проверьте счетчик hello.
- **Журналы трассировки**: удаленного рабочего стола к hello ВМ и добавление файла конфигурации приложения toohello TextWriterTraceListener.  В разделе tooset http://msdn.microsoft.com/library/sk36c28t.aspx слушателя текст hello.  Убедитесь, что hello `<trace>` элемент имеет `<trace autoflush="true">`.<br />
Если журналы трассировки не создаются, см. сведения в разделе [Подробные сведения об отсутствии журналов трассировки](#more-about-trace-logs-missing).
- **Трассировки событий Windows**: удаленного рабочего стола в hello виртуальной Машины и установки PerfView.  Откройте средство PerfView и выберите "File (Файл) > User Command (Пользовательская команда) > Ожидать передачи данных", указав при этом необходимых поставщиков ETW (etwprovder1, etwprovider2 и т. д.).  Обратите внимание, что команды прослушивания hello учитывается регистр, не должно быть пробелов между hello запятыми список поставщиков трассировки событий Windows.  При сбое команды hello toorun, можно щелкнуть кнопку «Вход» hello в hello правой нижней части toosee инструмент Perfview hello, была попытка toorun и какие hello результат был.  При условии, что входные данные hello указано правильно, затем откроется новое окно вверх и через несколько секунд сначала просмотра трассировки событий Windows.
- **Журналы событий**: удаленного рабочего стола к hello виртуальной Машины. Откройте `Event Viewer` и обеспечить hello события отсутствуют.
#### <a name="is-data-getting-captured-locally"></a>Проверка локального сохранения данных
Затем убедитесь, что данные hello начало регистрируются локально.
Hello данные хранятся локально в `*.tsf` файлы в [hello локального хранилища для данных диагностики](#log-artifacts-path). Каждый тип журнала записывается в разные файлы `.tsf`. Hello называются имена аналогичные toohello таблица в хранилище azure. Например, показатели счетчиков `Performance Counters` производительности записываются в файл `PerformanceCountersTable.tsf`, а данные журналов событий — в файл `WindowsEventLogsTable.tsf`. Используйте инструкции hello в [извлечения локального журнала](#local-log-extraction) статьи tooopen hello локальный сбор файлов и убедитесь, что вы видите их получение, собранные на диске.

Если у вас см. в журналах начало собираются локально и уже проверена hello узла создание данных, скорее всего имеется ошибка конфигурации. Проверьте конфигурацию тщательно для hello соответствующий раздел. Также проверьте конфигурацию hello, созданный для MonitoringAgent [MaConfig.xml](#log-artifacts-path) и убедитесь, что некоторые разделе с описанием источника соответствующих hello и не теряются при переводе между конфигурации службы диагностики azure и конфигурация агента мониторинга.
#### <a name="is-data-getting-transferred"></a>Проверка передачи данных
Если вы проверили hello начало фиксируются локально, но вы по-прежнему не отображается в вашей учетной записи хранения: 
- Первое и самое главное убедитесь, что учетной записи хранения правильно указано, и что вы не изменили hello etc.for ключей заданного учетной записи хранилища. Иногда пользователи облачных служб не обновляют раздел `useDevelopmentStorage=true`.
- Если учетная запись хранения указана правильно, Убедитесь, что у вас некоторые ограничения сети, которые не допускают компоненты hello конечные точки tooreach открытом хранилище. Одним из способов toodo, tooremote рабочего стола к hello компьютера и повторите toowrite что-нибудь toohello учетной записи хранения самостоятельно.
- Наконец, вы можете просмотреть ошибки агента наблюдения. Агент мониторинга записывает его журналы в `maeventtable.tsf` в [hello локального хранилища для данных диагностики](#log-artifacts-path). Следуйте инструкциям в разделе [извлечения локального журнала](#local-log-extraction) статьи tooopen этот файл и повторите выяснить наличие `errors` , указывающее, сбои tooread локальные файлы или записи toostorage.

### <a name="capturing--archiving-logs"></a>Архивация и запись журналов
Пройдено hello выше действия, но не удалось определить необходимые неправильное и думать о обращения в службу поддержки. Hello первое, что вас могут попросить — toocollect журналы с компьютера. Вы можете сэкономить время, сделав это самостоятельно. Запустите hello `CollectGuestLogs.exe` программы [путь программа для сбора журналов](#log-artifacts-path) и создает ZIP-файл с все журналы azure в hello одной папке.

## <a name="diagnostics-data-tables-not-found"></a>Таблицы данных диагностики не найдены
Hello таблиц в хранилище Azure, содержащий события трассировки событий Windows именуются hello, следующий код:

```C#
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

Пример:

```XML
        <EtwEventSourceProviderConfiguration provider="prov1">
          <Event id="1" />
          <Event id="2" eventDestination="dest1" />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider="prov2">
          <DefaultEvents eventDestination="dest2" />
        </EtwEventSourceProviderConfiguration>
```
```JSON
"EtwEventSourceProviderConfiguration": [
    {
        "provider": "prov1",
        "Event": [
            {
                "id": 1
            },
            {
                "id": 2,
                "eventDestination": "dest1"
            }
        ],
        "DefaultEvents": {
            "eventDestination": "DefaultEventDestination",
            "sinks": ""
        }
    },
    {
        "provider": "prov2",
        "DefaultEvents": {
            "eventDestination": "dest2"
        }
    }
]
```
Создается 4 таблицы:

| Событие | Имя таблицы |
| --- | --- |
| provider=”prov1” &lt;Event id=”1” /&gt; |WADEvent+MD5(“prov1”)+”1” |
| provider=”prov1” &lt;Event id=”2” eventDestination=”dest1” /&gt; |WADdest1 |
| provider=”prov1” &lt;DefaultEvents /&gt; |WADDefault+MD5(“prov1”) |
| provider=”prov2” &lt;DefaultEvents eventDestination=”dest2” /&gt; |WADdest2 |

## <a name="references"></a>Ссылки

### <a name="how-toocheck-diagnostics-extension-configuration"></a>Как toocheck конфигурацию расширения диагностики
Здравствуйте, наиболее простым способом toocheck конфигурацию расширения toonavigate toohttp://resources.azure.com, перейти toohello виртуальной машины или облачные службы на какие hello расширения системы диагностики Azure (IaaSDiagnostics / PaaDiagnostics) не гарантируется.

Кроме того, удаленного рабочего стола к машине hello и просмотрите файл конфигурации службы диагностики Azure hello, описанной в соответствующем разделе hello [здесь](#log-artifacts-path).

В обоих вариантов поиска **Microsoft.Azure.Diagnostics** затем для hello **xmlCfg** или **WadCfg** поля. 

В случае виртуальных машин Если присутствует поле WadCfg hello, это означает, что файл конфигурации hello, — в формате JSON. Если присутствует поле xmlCfg hello, значит hello конфигурации в формате XML и в кодировке base64. Требуется слишком[декодирования](http://www.bing.com/search?q=base64+decoder) toosee hello XML, который был загружен с помощью системы диагностики.

Для роли облачной службы, если вы выберете hello конфигурации с диска, hello данных имеет кодировку base64, вам потребуется слишком[декодирования](http://www.bing.com/search?q=base64+decoder) toosee hello XML, который был загружен с помощью системы диагностики.

### <a name="azure-diagnostics-plugin-exit-codes"></a>Коды выхода подключаемого модуля системы диагностики Azure
Подключаемый модуль Hello возвращает следующие коды выхода hello:

| Код выхода | Описание |
| --- | --- |
| 0 |Успешно. |
| -1 |Общая ошибка. |
| -2 |Не удается tooload hello rcf файл.<p>Это внутренняя ошибка должен произойти, только если hello гостевой агент подключаемый модуль запуска вручную вызове, неправильно, hello виртуальной Машины. |
| -3 |Не удалось загрузить файл конфигурации диагностики hello.<p><p>Решение. Это вызвано тем, что файл конфигурации не прошел проверку схемы. Hello решением является tooprovide файл конфигурации, который соответствует схеме hello. |
| -4 |Другой экземпляр hello мониторинг агента диагностики уже использует каталог локального ресурса hello.<p><p>Решение. Укажите другое значение для **LocalResourceDirectory**. |
| -6 |Hello гостевой агент подключаемый модуль запуска попытка toolaunch диагностики с недопустимой записью командной строки.<p><p>Это внутренняя ошибка должен произойти, только если hello гостевой агент подключаемый модуль запуска вручную вызове, неправильно, hello виртуальной Машины. |
| -10 |Подключаемый модуль диагностики Hello завершил работу с необработанным исключением. |
| -11 |Hello гостевого агента был процесса hello не удается toocreate отвечает за запуск и мониторинг hello, агент мониторинга.<p><p>Решение: Убедитесь, что достаточно ресурсов toolaunch доступны новые процессы.<p> |
| -101 |Недопустимые аргументы при вызове подключаемый модуль диагностики hello.<p><p>Это внутренняя ошибка должен произойти, только если hello гостевой агент подключаемый модуль запуска вручную вызове, неправильно, hello виртуальной Машины. |
| -102 |процесс Hello подключаемый модуль — не удается tooinitialize сам.<p><p>Решение: Убедитесь, что достаточно ресурсов toolaunch доступны новые процессы. |
| -103 |процесс Hello подключаемый модуль — не удается tooinitialize сам. Точнее, это объект средства ведения журнала не удается toocreate hello.<p><p>Решение: Убедитесь, что достаточно ресурсов toolaunch доступны новые процессы. |
| -104 |Не удается tooload hello rcf файл hello гостевого агента.<p><p>Это внутренняя ошибка должен произойти, только если hello гостевой агент подключаемый модуль запуска вручную вызове, неправильно, hello виртуальной Машины. |
| -105 |Подключаемый модуль диагностики Hello не удается открыть файл конфигурации диагностики hello.<p><p>Это внутренняя ошибка должен произойти, только если подключаемый модуль диагностики hello вручную вызове, неправильно, hello виртуальной Машины. |
| -106 |Не удалось прочитать файл конфигурации диагностики hello.<p><p>Решение. Это вызвано тем, что файл конфигурации не прошел проверку схемы. Поэтому hello решением является tooprovide файл конфигурации, который соответствует схеме hello. В разделе [как toocheck конфигурацию расширения диагностики](#how-to-check-diagnostics-extension-configuration). |
| -107 |Агент мониторинга проход toohello Hello ресурса каталога недопустим.<p><p>Это внутренняя ошибка должен произойти, только если агент наблюдения hello вручную вызове, неправильно, hello виртуальной Машины.</p> |
| -108 |Не удается tooconvert hello файла конфигурации диагностики в агент файлом конфигурации наблюдения за hello.<p><p>Это внутренняя ошибка должен произойти, только если подключаемый модуль диагностики hello вручную вызова используется недопустимый файл конфигурации. |
| -110 |Общая ошибка конфигурации системы диагностики.<p><p>Это внутренняя ошибка должен произойти, только если подключаемый модуль диагностики hello вручную вызова используется недопустимый файл конфигурации. |
| -111 |Не удается toostart hello агент мониторинга.<p><p>Решение. Убедитесь, что доступен достаточный объем системных ресурсов. |
| -112 |Общая ошибка |

### <a name="local-log-extraction"></a>Извлечение локального журнала
Привет, агент мониторинга собирает журналы и артефактам, как `.tsf` файлы. `.tsf` Файл TSF недоступен для чтения, но его можно преобразовать в формат CSV с помощью `.csv` следующей служебной программы: 

```
<Azure diagnostics extension package>\Monitor\x64\table2csv.exe <relevantLogFile>.tsf
```
Новый файл с именем `<relevantLogFile>.csv` будет создан в hello же пути, что и соответствующий hello `.tsf` файла.

**Примечание**: достаточно toorun этой программы с файлом основного tsf hello (например, PerformanceCountersTable.tsf). Hello, сопровождающие файлов (например, PerformanceCountersTables_\*\*001.tsf PerformanceCountersTables_\*\*002. tsf и т.д.) автоматически будут обрабатываться.

### <a name="more-about-trace-logs-missing"></a>Подробные сведения об отсутствии журналов трассировки

**Примечание:** это главным образом относится toocloud службы только в том случае, если вы настроили hello DiagnosticsMonitorTraceListener приложения, запущенного на ВМ IaaS. 

- Убедитесь, что в hello web.config или app.config настроен DiagnosticMonitorTraceListener приветствия.  Эта конфигурация используется по умолчанию в проектах облачных служб, но некоторые клиенты закомментируйте его out, что вызовет toonot операторы трассировки hello будут собираться средствами диагностики. 
- Если журналы не начало записываются из метода OnStart или выполнения hello убедитесь, что hello DiagnosticMonitorTraceListener находится в файле app.config hello.  По умолчанию он находится в файле web.config hello, но, применяется только toocode, запущенного в рамках w3wp.exe; Поэтому необходимо в трассировках toocapture app.config, запущенных в WaIISHost.exe.
- Убедитесь, что вы используете Diagnostics.Trace.TraceXXX, а не Diagnostics.Debug.WriteXXX.  Hello отладочные операторы будут удалены из выпуска.
- Убедитесь, что код компилируется hello фактически имеет hello Diagnostics.Trace строки (используйте Reflector, ildasm или ILSpy tooverify).  Diagnostics.Trace команды удаляются из hello скомпилированные двоичные, если не используется символ условной компиляции hello ТРАССИРОВКИ.  Если с помощью msbuild toobuild hello проекта это можно сделать общие проблемы toorun в.

## <a name="known-issues-and-mitigations"></a>Известные проблемы и устранения рисков
Ниже приведен список известных проблем и способы их устранения.

**1. Зависимость от .NET 4.5.**

Система диагностики Azure имеет зависимость среды выполнения на платформе .NET 4.5 или более поздней версии. Во время написания это hello всех машин, подготовленных для облачных служб, а также все официальный azure образы виртуальных машин базового .NET 4.5 или выше установлена. Это, однако по-прежнему возможно tooland в ситуации, где повторите toorun WAD на компьютере, где нет .NET 4.5 или более поздней версии. Например, если создаете виртуальную машину на основе старого образа (моментального снимка) или с помощью собственного диска.

В этом случае при запуске DiagnosticsPluginLauncher.exe возвращается код выхода **255**. Происходит сбой из-за toohello необработанное исключение: 
```
System.IO.FileLoadException: Could not load file or assembly 'System.Threading.Tasks, Version=1.5.11.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies
```

**Устранение.** Установите на виртуальной машине платформу .NET 4.5 или более поздней версии.

**2. Данные счетчиков производительности доступные в хранилище, но не отображаются на портале.**

На портале виртуальных машин данные определенных счетчиков производительности отображаются по умолчанию. Если вы не видите их и известно, что данные hello начало формируются, так как он доступен в хранилище. Убедитесь, что:
- Если имена счетчиков hello данных в хранилище на английском языке. Если имена счетчиков hello не на английском языке, портала метрики диаграммы не будет возможности toorecognize его.
- Если вы используете подстановочные знаки (\*) в именах счетчик производительности, hello портал не будет hello может toocorrelate настроен и собранных счетчиков.

**Устранение рисков**: изменение hello машины tooEnglish язык для системных учетных записей. Панель управления -> области Администрирование -> Копировать параметры -> снимите флажок «Приветствие экрана и системных учетных записей», чтобы пользовательский язык hello не применены toosystem учетной записи. Также убедитесь, что если требуется портала toobe работы основной потребления подстановочные знаки не используется.
