---
title: "метрики хранилища aaaEnabling в hello портал Azure | Документы Microsoft"
description: "Как tooenable метрик хранилища для hello служб больших двоичных объектов, очередей, таблицы и файла"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a>Включение метрик хранилища Azure и просмотр данных метрик
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Обзор
Метрики хранилища включаются по умолчанию при создании учетной записи хранения. Вы можете настроить отслеживание посредством hello [портал Azure](https://portal.azure.com) или Windows PowerShell или программно через одну из клиентских библиотек хранилища hello.

Можно настроить срок хранения данных метрик hello: этот период определяет срок хранения hello служба поддерживает метрики hello и расходов для hello пространство необходимые toostore их. Как правило следует использовать короткий срок хранения для ежеминутных метрик, нежели для часовых метрик из-за hello Требую значительно большего пространства для минутных метрик. Таким образом, чтобы иметь достаточно времени tooanalyze hello данных и загрузку метрик, нужно tookeep локально для анализа или составления следует выбрать период хранения. Помните, что за скачивание данных метрик из учетной записи хранения также взимается плата.

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a>Как с помощью метрики tooenable hello портал Azure
Выполните эти шаги метрики tooenable hello [портал Azure](https://portal.azure.com):

1. Перейдите tooyour учетной записи хранилища.
1. Выберите **диагностики** на hello **меню** колонку
1. Убедитесь, что **состояние** задано слишком**на**.
1. Выберите hello метрики для hello служб, который следует toomonitor.
1. Укажите политику хранения tooindicate продолжительность tooretain метрики и журнала данных.
1. Щелкните **Сохранить**.

Обратите внимание, что hello [портал Azure](https://portal.azure.com) не включает в настоящее время вы tooconfigure минутные показатели вашей учетной записи хранилища; необходимо включить ежеминутные метрики с помощью PowerShell или программно.

## <a name="how-tooenable-metrics-using-powershell"></a>Как tooenable метрик, с помощью PowerShell
Можно использовать PowerShell на ваш локальный компьютер tooconfigure метрик хранилища в вашей учетной записи хранилища с помощью hello Azure PowerShell командлет Get-AzureStorageServiceMetricsProperty tooretrieve hello текущие параметры и hello командлета SET-AzureStorageServiceMetricsProperty toochange hello текущие параметры.

Hello командлеты, позволяющие управлять метриками хранилища используйте hello следующие параметры:

* Возможными значениями MetricsType являются Hour и Minute.
* Возможными значениями ServiceType являются Blob, Queue и Table.
* Возможными значениями MetricsLevel являются None, Service и ServiceAndApi.

Например, hello следующая команда включает минуту метрики для службы BLOB-объектов hello в вашей учетной записи хранения по умолчанию с периодом хранения hello значение toofive дней:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

Hello следующая команда извлекает hello текущего почасовых метрик уровня и хранения дней для hello BLOB-объектов в учетной записи по умолчанию:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

Сведения о toowork tooconfigure hello Azure PowerShell командлеты с подпиской Azure и как tooselect hello хранилища по умолчанию учетной записи toouse см: [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>Как tooenable метрик хранилища программным способом
Привет, следующий фрагмент кода C# показано, как tooenable метрик и ведения журнала для службы BLOB-объектов hello с помощью hello клиентской библиотеки хранилища для .NET.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>Просмотр метрик хранилища
После настройки учетной записи хранения toomonitor метрики аналитики хранилища аналитики хранилища записывает hello метрики в набор известных таблиц в учетной записи хранилища. Часовые показатели tooview диаграммы можно настроить в hello [портал Azure](https://portal.azure.com):

1. Перейдите tooyour учетной записи хранилища в hello [портал Azure](https://portal.azure.com).
1. Выберите **метрики** в hello **меню** колонке hello службы которого метрик требуется tooview.
1. Выберите **изменить** на диаграмме hello требуется tooconfigure.
1. В hello **изменить диаграмму** колонки, выберите hello **диапазон времени**, **тип диаграммы**и hello метрик, которые необходимо отобразить на диаграмме hello.
1. Нажмите кнопку **ОК**.

Если требуется, чтобы toodownload hello метрики для долгосрочного хранения или tooanalyze их локально, необходимо:

* Используйте это средство, которое учитывает эти таблицы позволяют tooview и загрузить их.
* Написать пользовательские приложения или сценария tooread и хранить hello таблицы.

Многие средства обзора хранилища сторонних учитывать эти таблицы и позволяют tooview их напрямую.
Список доступных инструментов указан в разделе [Клиентские инструменты службы хранилища Azure](storage-explorers.md).

> [!NOTE]
> Начиная с версии 0.8.0 hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), можно просматривать и загружать таблицы метрик аналитики hello.
> 
> 

В порядке tooaccess hello analytics таблиц программными средствами, обратите внимание, что hello analytics таблицы не отображаются, если список всех таблиц hello в вашей учетной записи хранилища. Можно получить доступ к их напрямую по имени, или использовать hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) в hello библиотеки клиента .NET tooquery имена таблиц hello.

### <a name="hourly-metrics"></a>Часовые метрики
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Минутные метрики
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Емкость
* $MetricsCapacityBlob

Для этих таблиц можно найти подробные сведения о схемах hello [схема таблицы метрик аналитики хранилища](https://msdn.microsoft.com/library/azure/hh343264.aspx). Hello примере строк ниже показывают только подмножество доступных столбцов hello, но иллюстрируют некоторые важные функции hello способ метрик хранилища сохраняет эти показатели:

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Доступность | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |user;All |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |user;QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |user;QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |user;UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

В этом примере данных минутной метрики для ключа раздела hello используется hello время с минутным разрешением. Hello ключ строки определяет тип информации, хранящейся в строке приветствия hello и состоит из двух фрагментов информации, типом доступа hello и тип запроса hello:

* Тип доступа Hello — пользователя или системы, где пользователь относится tooall пользователь запросов toohello хранилища службы, а система — toorequests, выполненные средством аналитики хранилища.
* Тип запроса Hello — в этом случае это строка сводки, либо он определяет hello определенный интерфейс API, например QueryEntity или UpdateEntity.

пример Hello данных передачи, которые все hello записывает за одну минуту (начиная с 11:00 по тихоокеанскому времени), поэтому hello число QueryEntities запросов, а также hello число QueryEntity запросов, а также hello число запросов UpdateEntity сложить tooseven, которой является hello Общее показан на Строка Hello user: All. Аналогичным образом, можно создать производные hello среднее конца в конец задержку 104.4286 в строке приветствия user: All, вычисляя ((143.8 * 5) + 3 + 9) / 7.

## <a name="metrics-alerts"></a>Оповещения метрик
Настройка оповещений в hello следует [портал Azure](https://portal.azure.com) , метрик хранилища могут автоматически получать уведомления о важных изменениях в поведении hello устройств хранения. Если вы используете toodownload средства обозревателя хранилища данные метрик в формате с разделителями, можно использовать Microsoft Excel tooanalyze hello данных. Список доступных инструментов Storage Explorer см. в разделе [Клиентские инструменты службы хранилища Azure](storage-explorers.md). Можно настроить оповещения в hello **предупреждения правила** колонке доступен в рамках **мониторинг** в колонке меню учетной записи хранилища hello.

> [!IMPORTANT]
> Возможна задержка между событием хранилища и при записи hello соответствующие данные метрик каждый час или раз в минуту. В случае hello минутных метрик данные за несколько минут на запись одновременно. Это может привести tootransactions из более ранних минут статистически в транзакцию hello для hello текущую минуту. В этом случае hello предупреждение, что служба не может иметь все данные метрик, доступных для hello настроить оповещения интервал, который может вызвать срабатывание неожиданно tooalerts.
>

## <a name="accessing-metrics-data-programmatically"></a>Программный доступ к данным метрик
Hello ниже приведен пример кода C#, обращается к hello минутным метрикам для диапазона минут и отображает результаты hello в окне консоли. Она использует hello библиотека хранилища Azure версии 4, включающая hello CloudAnalyticsClient класс, который упрощает доступ к таблицам метрик hello в хранилище.

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>Какова стоимость включения метрик хранилища?
Напишите запросы сущностей таблицы toocreate для метрик взимается плата в операции хранилища Azure применимо tooall стандартные тарифы hello.

Чтение и удаление запросов по toometrics данных клиента, также применяются стандартные тарифы. Если вы настроили политику хранения данных, за удаление старых данных метрик хранилищем Azure плата не взимается. Однако при удалении данных аналитики, учетной записи взимается для операций delete hello.

Hello мощность, используемая hello таблицах метрик, также тарифицируется: можно использовать следующие tooestimate hello объем пространства, используемый для хранения данных метрик hello:

* Если каждый час служба использует каждый API в каждой службе, примерно 148 КБ данных сохраняется каждый час в таблицах транзакций метрик hello при включении службы и уровне API сводки.
* Если каждый час служба использует каждый API в каждой службе, примерно 12 КБ данных сохраняется каждый час в таблицах транзакций метрик hello при наличии только уровень службы сводки.
* Hello таблице емкости BLOB-объектов имеет две строки, добавленные в день (если пользователь выбрал использование журналов): это означает, что каждый день hello размер этой таблицы увеличивается на копирование tooapproximately 300 байт.

## <a name="next-steps"></a>Дальнейшие действия
[Включение ведения журнала и доступа к данным журнала хранилища](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
