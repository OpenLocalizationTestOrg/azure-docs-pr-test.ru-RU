---
title: "Счетчики производительности в Azure Diagnostics aaaUse | Документы Microsoft"
description: "Использование счетчиков производительности в облачных служб Azure или узкие места toofind виртуальных машин и настройки производительности."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Создание и использование счетчиков производительности в приложении Azure
В этой статье описываются преимущества hello и как счетчики производительности tooput в приложение Azure. Можно использовать их данные toocollect, обнаруживать узкие места и настройки производительности системы и приложений.

Счетчики производительности, доступные для Windows Server, IIS и ASP.NET можно также собирать и использовать toodetermine работоспособности hello Azure веб-ролей, рабочих ролей и виртуальных машин. Вы также можете создавать и использовать настраиваемые счетчики производительности.  

Вы можете проверить данные счетчиков производительности.

1. Непосредственно на узле приложения hello с hello системный монитор получить доступ с помощью удаленного рабочего стола
2. Здравствуйте, пакет управления Azure с помощью System Center Operations Manager
3. Другие средства мониторинга, которые обращаются к hello tooAzure хранилища переданных диагностических данных. Дополнительные сведения см. в статье [Хранение и просмотр диагностических данных в службе хранилища Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx).  

Дополнительные сведения о наблюдении за производительностью hello приложения hello [портал Azure](http://portal.azure.com/), в разделе [как tooMonitor облачных служб](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Дополнительные подробные рекомендации по методам ведения журнала и трассировки, а также использованию диагностики и других проблем tootroubleshoot методы и оптимизации приложений Azure см. в разделе [Устранение неполадок советы и рекомендации по разработке Azure Приложения](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Включение мониторинга счетчиков производительности
Счетчики производительности по умолчанию отключены. Приложение или задача запуска необходимо изменить диагностики по умолчанию hello агента tooinclude hello конкретных счетчиков производительности для конфигурации обратиться в toomonitor для каждого экземпляра роли.

### <a name="performance-counters-available-for-microsoft-azure"></a>Счетчики производительности, доступные в Microsoft Azure
Azure предоставляет подмножество hello счетчики производительности, доступные для Windows Server, IIS и стека ASP.NET hello. Hello следующей таблице перечислены некоторые счетчики производительности hello особый интерес для приложения Azure.

| Категория счетчика: объект (экземпляр) | Имя счетчика | Справочные материалы |
| --- | --- | --- |
| Исключения .NET CLR (*глобально*) |Число исключений/с |Счетчики производительности исключений |
| Память .NET CLR (*глобально*) |Время на сборку мусора, % |Счетчики производительности памяти |
| ASP.NET: |Перезапуски приложения |Счетчики производительности для ASP.NET |
| ASP.NET: |Время выполнения запроса |Счетчики производительности для ASP.NET |
| ASP.NET: |Прерванные запросы |Счетчики производительности для ASP.NET |
| ASP.NET: |Перезапуски рабочего процесса |Счетчики производительности для ASP.NET |
| Приложения ASP.NET (**всего**) |Общее число запросов |Счетчики производительности для ASP.NET |
| Приложения ASP.NET (**всего**) |Число запросов в секунду |Счетчики производительности для ASP.NET |
| ASP.NET v4.0.30319 |Время выполнения запроса |Счетчики производительности для ASP.NET |
| ASP.NET v4.0.30319 |Время ожидания запроса |Счетчики производительности для ASP.NET |
| ASP.NET v4.0.30319 |Текущие запросы |Счетчики производительности для ASP.NET |
| ASP.NET v4.0.30319 |Запросы в очереди |Счетчики производительности для ASP.NET |
| ASP.NET v4.0.30319 |Отклоненные запросы |Счетчики производительности для ASP.NET |
| Память |Доступный объем в МБ |Счетчики производительности памяти |
| Память |Число байтов выделенной памяти |Счетчики производительности памяти |
| Процессор(_всего) |% загруженности процессора |Счетчики производительности для ASP.NET |
| TCPv4 |Ошибки подключения |Объект TCP |
| TCPv4 |Установлено подключений |Объект TCP |
| TCPv4 |Сбросов подключений |Объект TCP |
| TCPv4 |Отправлено сегментов/с |Объект TCP |
| Сетевой интерфейс (*) |Полученных байтов/с |Объект сетевого интерфейса |
| Сетевой интерфейс (*) |Отправленных байтов/с |Объект сетевого интерфейса |
| Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2) |Полученных байтов/с |Объект сетевого интерфейса |
| Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2) |Отправленных байтов/с |Объект сетевого интерфейса |
| Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2) |Всего байтов/с |Объект сетевого интерфейса |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Создание и добавление приложения tooyour счетчики производительности
Azure имеет toocreate поддержки и изменять пользовательские счетчики производительности для веб-ролей и рабочих ролей. счетчики Hello возможно, используется монитор и tootrack поведения приложения. Вы можете создавать пользовательские категории и описатели счетчиков производительности для задачи при запуске, веб-роли или рабочей роли с повышенными разрешениями, а также удалять их.

> [!NOTE]
> Код, который вносит изменения toocustom счетчики производительности должны быть повышенные разрешения toorun. Если код hello в веб-роли или рабочей роли, hello роль должна содержать тег hello <Runtime executionContext="elevated" /> в hello ServiceDefinition.csdef-файла для роли tooinitialize hello должным образом.
>
>

Можно отправлять с помощью агента диагностики hello tooAzure хранения производительности счетчиков данных.

Hello стандартные данные счетчиков производительности формируется hello, обрабатываемых в Azure. Данные пользовательских счетчиков производительности должны создаваться приложением веб-роли или рабочей роли. В разделе [типы счетчиков производительности](https://msdn.microsoft.com/library/z573042h.aspx) сведения о типах hello данных, которые могут храниться в пользовательские счетчики производительности. Пример создания и установки данных пользовательских счетчиков производительности в веб-роли см. в статье [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) (Пример PerformanceCounters).

## <a name="store-and-view-performance-counter-data"></a>Сохранение и просмотр данных счетчика производительности
Azure кэширует данные счетчиков производительности вместе с другими диагностическими сведениями. Эти данные доступны для удаленного мониторинга, пока экземпляр роли hello выполняется с помощью удаленного рабочего стола доступа tooview средства, такие как системный монитор. toopersist hello данных за пределами экземпляра роли hello, hello диагностики агента необходимо перенести hello данных tooAzure хранилища. Ограничение размера Hello hello кэшированных данных счетчиков производительности можно настроить в агент диагностики hello, или может быть настроен toobe часть общего ограничения для всех hello диагностических данных. Дополнительные сведения о размере буфера hello см. в разделе [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) и [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). В разделе [хранения и просмотра диагностических данных в хранилище Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) Общие сведения о настройке hello агента tootransfer данных tooa учетная запись хранения диагностики.

Каждый настроенный экземпляр счетчика производительности записывается с указанной частотой выборки и передаче данных выборки hello toohello учетной записи хранения плановым запросом передачи или запрос передачи по требованию. Автоматическую передачу можно запланировать с периодичностью раз в минуту. Данные счетчиков производительности, передаваемых агентом диагностики hello хранится в таблице WADPerformanceCountersTable, в учетной записи хранения hello. К этой таблице можно обращаться с помощью запросов в рамках стандартных методов API хранилища Azure. В разделе [пример PerformanceCounters Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) пример запроса и отображения данных счетчиков производительности из таблицы WADPerformanceCountersTable hello.

> [!NOTE]
> В зависимости от частоты передачи агент диагностики hello и задержки очереди hello самые последние данные счетчиков производительности в учетной записи хранилища hello может быть устаревшим в несколько минут.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Включение счетчиков производительности с помощью файла конфигурации диагностики
Используйте следующие счетчики производительности tooenable процедуры в приложении Azure hello.

## <a name="prerequisites"></a>Предварительные требования
В этом разделе предполагается, что были импортированы hello монитор диагностики в приложении и были добавлены hello диагностики конфигурации файла tooyour решения Visual Studio (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и более поздних версий). Дополнительные сведения отображены в шагах 1 и 2 статьи [Включение диагностики в облачных службах и виртуальных машинах Azure](cloud-services-dotnet-diagnostics.md).

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>Шаг 1. Сбор и хранение данных счетчиков производительности
После добавления диагностики hello файл решения Visual Studio tooyour можно настроить hello сбор и хранение данных счетчиков производительности в приложении Azure. Это делается путем добавления файла диагностики toohello счетчиков производительности. Данные диагностики, включая счетчики производительности, сначала собираются в экземпляре hello. Hello данные затем сохраненного toohello WADPerformanceCountersTable таблицу hello службы таблицы Azure, так вы также должны toospecify hello учетной записи хранения в приложении. При тестировании приложения локально в эмуляторе вычислений hello, можно также хранить данные диагностики локально в hello эмулятор хранилища. Перед сохранением диагностических данных, необходимо сначала перейти toohello [портал Azure](http://portal.azure.com/) и создать учетную запись классической хранилища. Рекомендуется toolocate вашей учетной записи хранения в hello географическому расположению, как приложения Azure. С сохранением hello Azure приложений и учетную запись хранения находятся в Здравствуйте географическому расположению, предотвратить дополнительные затраты на внешнюю полосу пропускания и уменьшить задержку.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Добавьте файл диагностики toohello счетчиков производительности
Вы можете использовать самые разные счетчики. Hello следующем примере показано несколько счетчиков производительности, которые рекомендуются для веб- и мониторинг рабочей роли.

Откройте файл диагностики hello (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и более поздних версий) и добавьте следующий элемент DiagnosticMonitorConfiguration toohello hello:

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

атрибут bufferQuotaInMB Hello, который указывает hello максимальный объем хранилища файловой системы, которая доступна для hello типа собираемых данных (журналы Azure, журналы IIS, и т. д.). Hello по умолчанию — 0. При достижении квоты hello старые данные hello удаляется по мере добавления новых данных. Hello сумма всех свойств bufferQuotaInMB hello должна быть больше, чем значение hello атрибута OverallQuotaInMB hello. Более подробное рассмотрение определения того, какой объем хранилища потребуется для hello сбор диагностических данных см. в разделе hello разделе настройки WAD [Устранение неполадок советы и рекомендации по разработке приложений Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

Hello scheduledTransferPeriod атрибут, который указывает hello интервал между запланированными передачами данных, округляется в сторону увеличения toohello ближайшего минуты. В следующих примерах hello задается tooPT30M (30 минут). Параметр hello передачи периода tooa малое значение, например 1 минуту, будет отрицательно влиять на производительность приложения в рабочей среде, но может быть полезным для просмотра диагностики быстрой работы при тестировании. Hello запланированный период передачи должен быть достаточно мал tooensure, что диагностических данных не будет перезаписан в экземпляре hello, но достаточно велик, что он не повлияет на производительность приложения hello.

атрибут counterSpecifier Hello указывает toocollect счетчика производительности hello. атрибут SampleRate содержит Hello указывает hello скорость, с которой счетчик производительности hello должны считываться, в данном случае 30 секунд.

После добавления счетчиков производительности для hello, которые должны toocollect, сохраните изменения toohello диагностики. Далее необходимо использовать учетную запись хранения toospecify hello, будут сохраняться данные диагностики hello.

### <a name="specify-hello-storage-account"></a>Укажите учетную запись хранения hello
toopersist вашей tooyour сведения диагностики хранилища Azure учетной записи, необходимо указать строку подключения в файле конфигурации (ServiceConfiguration.cscfg) службы.

Для Azure SDK 2.5 hello учетной записи хранилища можно задать в файле diagnostics.wadcfgx hello.

> [!NOTE]
> Эти инструкции применяются только tooAzure SDK 2.4 и ниже. Для Azure SDK 2.5 hello учетной записи хранилища можно задать в файле diagnostics.wadcfgx hello.
>
>

строки подключения hello tooset:

1. Откройте файл ServiceConfiguration.Cloud.cscfg hello, с помощью любого текстового редактора и строка подключения hello набор для хранилища. Hello *AccountName* и *AccountKey* значения находятся в hello портал Azure в мониторинга учетной записи хранения hello в списке ключей доступа.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Сохраните файл ServiceConfiguration.Cloud.cscfg hello.
3. Откройте файл ServiceConfiguration.Local.cscfg hello и убедитесь, что UseDevelopmentStorage tootrue.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Теперь, когда hello строки подключения заданы, приложение будет сохранять учетная запись хранения tooyour данных диагностики при развертывании приложения.
4. Сохраните и соберите свой проект, затем разверните приложение.

## <a name="step-2-optional-create-custom-performance-counters"></a>Шаг 2. (Необязательно) Создание пользовательских счетчиков производительности
В дополнение к этому toohello предварительно определенные счетчики производительности, можно добавить собственные пользовательские счетчики производительности toomonitor рабочих и веб-ролей. Пользовательские счетчики производительности могут быть используется монитор и tootrack поведения приложения и может быть создано или удалены в задаче запуска, веб-роли или рабочей роли с повышенными разрешениями.

агент диагностики Azure Hello обновляет hello конфигурации счетчиков производительности из файла .wadcfg hello одну минуту, после запуска.  Если создать пользовательские счетчики производительности в метод OnStart hello и задачи запуска выполняются дольше, чем tooexecute одну минуту, пользователем счетчиков производительности будет не были созданы при агент Azure Diagnostics hello tooload их.  В этом случае система диагностики Azure будет надлежащим образом собирать все данные диагностики — за исключением данных пользовательских счетчиков производительности.  tooresolve эту проблему, создайте hello счетчиков производительности в задачу запуска и перемещение метод OnStart toohello некоторые задачи запуска работать после создания hello счетчиков производительности.

Выполните следующие шаги toocreate простой пользовательский счетчик производительности с именем «\MyCustomCounterCategory\MyButton1Counter» hello.

1. Откройте файл определения hello службы (CSDEF) для вашего приложения.
2. Добавьте hello элемент toohello WebRole или WorkerRole элемент tooallow выполнения среды с повышенными привилегиями:

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Сохраните файл hello.
4. Откройте файл диагностики hello (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и более поздних версий) и добавьте следующие toohello DiagnosticMonitorConfiguration hello

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Сохраните файл hello.
6. Создайте hello пользовательскую категорию счетчиков производительности в метод OnStart hello своей роли перед вызовом базы. Метод OnStart. Hello следующий пример на C# создается пользовательская категория, если он еще не существует:

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Обновите счетчики hello внутри приложения. Следующий пример Hello обновляет пользовательский счетчик производительности для событий Button1_Click:

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Сохраните файл hello.  

Теперь данных пользовательских счетчиков производительности собираются монитором диагностики Azure hello.

## <a name="step-3-query-performance-counter-data"></a>Шаг 3. Запрос данных счетчика производительности
После развертывания приложения и запущена, монитор диагностики hello начнет сбор данных счетчиков производительности и сохранение этой tooAzure хранения данных. Используйте средства, такие как обозреватель серверов в Visual Studio [обозреватель хранилищ Azure](http://azurestorageexplorer.codeplex.com/), или [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) компании Cerebrata tooview hello данных счетчиков производительности в hello Таблица WADPerformanceCountersTable. Можно также программно использовать в запросах hello таблицы службы [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), или [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Hello следующий пример на C# показан базовый запрос к таблице WADPerformanceCountersTable hello и сохраняет hello диагностики данных tooa CSV-файла. После hello счетчики производительности сохранены tooa CSV-файл, можно использовать hello построения диаграмм возможностей в Microsoft Excel или другие средства toovisualize hello данными. Быть убедиться, что tooadd tooMicrosoft.WindowsAzure.Storage.dll ссылки, который входит в hello Azure SDK для .NET от октября 2012 или более поздней версии. сборка Hello — установленных toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ каталог.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

Сущности сопоставляют tooC # объектов с помощью пользовательского класса, производного от **TableEntity**. Hello следующий код определяет класс сущностей, который представляет собой счетчик производительности в hello **WADPerformanceCountersTable** таблицы.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Дальнейшие действия
[Просмотрите дополнительные статьи о системе диагностику Azure](../azure-diagnostics.md)
