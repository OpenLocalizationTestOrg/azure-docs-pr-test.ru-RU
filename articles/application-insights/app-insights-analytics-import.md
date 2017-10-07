---
title: "aaaImport вашей tooAnalytics данные в Azure Application Insights | Документы Microsoft"
description: "При импорте toojoin статические данные с телеметрии приложения или импорт tooquery потока данных с помощью аналитики."
services: application-insights
keywords: "открытие схемы, импорт данных"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>Импорт данных в инструмент аналитики

Импорт табличных данных в [Analytics](app-insights-analytics.md), либо toojoin его с [Application Insights](app-insights-overview.md) телеметрии из приложения, или можно проанализировать в отдельном потоке. Аналитика является потоки запросами языка хорошо подходит tooanalyzing отметку времени крупномасштабных телеметрии.

Вы можете импортировать данные в инструмент аналитики, используя собственную схему. Это не обязательно toouse hello Стандартная Application Insights схем, таких как запрос или трассировки.

Можно импортировать файлы в формате JSON или DSV (значения с разделителями — запятыми, точками с запятой или знаками табуляции).

Существует три ситуации, когда полезно Импорт tooAnalytics:

* **Объединение с данными телеметрии приложения.** Например можно импортировать таблицу, которая сопоставляет URL-адреса из заголовков для чтения страниц toomore вашего веб-сайта. В аналитике можно создать панель мониторинга отчета с диаграммой, показывающий hello десяти наиболее популярных страниц веб-сайта. Он может отображать hello названия страниц вместо hello URL-адреса.
* **Сопоставление данных телеметрии приложения** с другими источниками, например с отчетом о сетевом трафике, данными сервера или файлами журнала CDN.
* **Примените Analytics tooa отдельный поток данных.** Аналитика Application Insights — мощный инструмент, который хорошо работает с разреженным потоками с метками времени. Во многих случаях этот инструмент намного эффективнее, чем SQL. С помощью аналитики вы можете проанализировать такой поток из другого источника.

Отправка данных tooyour источник данных можно легко. 

1. (Один раз) Определите схему hello данных в «источник данных».
2. (Периодически) Отправка tooAzure хранилище данных и вызывать API-интерфейса REST toonotify hello нас, новые данные ожидает приема. В течение нескольких минут hello данных доступна для запросов в аналитике.

Hello частоту передачи hello определяется пользователем и как быстро хотите, чтобы ваш toobe данных, доступных для запросов. Это более эффективно tooupload данные большими частями, но не более 1 ГБ.

> [!NOTE]
> *У вас есть большое количество tooanalyze источники данных?* [*Рассмотрите возможность использования* logstash *tooship данные в Application Insights.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Перед началом работы

Вам необходимы:

1. Ресурс Application Insights в Microsoft Azure.

 * Если требуется tooanalyze данных отдельно от других телеметрии [создать новый ресурс Application Insights](app-insights-create-new-resource.md).
 * Если вы будете объединения или сравнения данных с помощью телеметрии из приложения, которое уже настроен с помощью Application Insights, hello ресурсов можно использовать для этого приложения.
 * Сотрудник или владелец ресурса toothat доступа.
 
2. хранилище Azure. Отправка tooAzure хранилища и аналитики получает данные из него. 

 * Рекомендуем создать отдельную учетную запись хранения для больших двоичных объектов. Если BLOB-объектов являются общими с другими процессами, он занимает больше времени для наших tooread процессы BLOB-объектов.


## <a name="define-your-schema"></a>Определение схемы

Прежде чем импортировать данные, необходимо определить *источника данных* указывает, hello схемы данных.
Можно создать до too50 источники данных в один ресурс Application Insights

1. Запустите мастер источников данных hello. Воспользуйтесь кнопкой Add new data source (Добавить новый источник данных). Кроме того, нажмите кнопку "Параметры" в правом верхнем углу и в раскрывающемся меню выберите "Источники данных".

    ![Добавление источника данных](./media/app-insights-analytics-import/add-new-data-source.png)

    Введите имя для нового источника данных.

2. Определение формата hello файлов, которые нужно будет загрузить.

    Можно вручную задать формат hello или загрузить образец файла.

    Если hello данные в формате CSV, первая строка hello образец hello может быть заголовки столбцов. Можно изменить имена полей hello в следующем шаге hello.

    Образец Hello должен включать по крайней мере 10 строк или записей данных.

    Имена столбцов или полей должны состоять из букв и цифр (без пробелов и знаков препинания).

    ![Передача примера файла](./media/app-insights-analytics-import/sample-data-file.png)


3. Есть схемы проверки hello, hello мастера. Если он выводимые типы hello из выборки, может потребоваться tooadjust hello вывести типы столбцов hello.

    ![Просмотр схемы вывести hello](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (Необязательно.) Отправьте определение схемы. В разделе hello в указанном ниже формате.

 * Выберите метку времени. Все данные в инструменте аналитики должны включать поле метки времени. Он должен иметь тип `datetime`, но он не имеет toobe с именем «timestamp». Если в данных есть столбец, содержащий дату и время в формате ISO, выберите этот как hello столбец отметки времени. В противном случае выберите «как данные поступили», и процесс импорта hello добавит поле метки времени.

5. Создайте источник данных hello.

### <a name="schema-definition-file-format"></a>Формат файла определения схемы

Вместо редактирования схемы hello в пользовательском Интерфейсе, можно загрузить из файла определения схемы hello. Hello схемы определения имеет следующий формат: 

Формат с разделителями 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

Формат JSON 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Каждый столбец идентифицируется hello расположение, имя и тип. 

* Расположение — формата файла с разделителями, он располагается hello hello сопоставить значения. Формат JSON это jpath hello hello сопоставлен ключа.
* Имя — hello отображается имя столбца hello.
* Тип — hello тип данных этого столбца.
 
В случае использовался в образце данных, а в качестве разделителя формат файла, определение схемы hello необходимо сопоставить все столбцы и добавить новые столбцы в конце hello. 

JSON допускает частичное сопоставление данных hello, поэтому hello определение схемы формат JSON не имеют toomap каждый ключ, который находится в образце данных. Также можно сопоставить столбцы, которые не являются частью hello образцов данных. 

## <a name="import-data"></a>Импорт данных

tooimport данных, передать его tooAzure хранилища, создать ключ доступа для него и затем вызвать API-интерфейса REST.

![Добавление источника данных](./media/app-insights-analytics-import/analytics-upload-process.png)

Можно выполнить вручную после процесса hello или настройка автоматизированной системы toodo его через регулярные интервалы. Вам требуется toofollow эти шаги для каждого блока данных требуется tooimport.

1. Передача данных hello слишком[хранилище больших двоичных объектов](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * Большие двоичные объекты могут быть любого размера вверх too1GB несжатых данных. С точки зрения производительности идеально использовать большие двоичные объекты размером несколько сотен мегабайт.
 * Он позволяет уменьшить время передачи tooimprove Gzip и задержки для toobe hello данных, доступных для запроса. Используйте hello `.gz` расширение имени файла.
 * Это наиболее toouse отдельную учетную запись хранилища для этой цели tooavoid вызовы от различных служб снижения производительности.
 * При отправке данных в высокой частотой, каждые несколько секунд, рекомендуется toouse больше, чем одну учетную запись хранения, для повышения производительности.

 
2. [Создайте ключ подписи общего доступа для большого двоичного объекта hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). ключ Hello должны иметь срок действия одного дня и предоставить доступ для чтения.
3. Сделайте toonotify вызов REST Application Insights, данных находится в состоянии ожидания.

 * Конечная точка: `https://dc.services.visualstudio.com/v2/track`
 * Метод HTTP: POST
 * Полезные данные:

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

Hello местозаполнителей являются:

* `Blob URI with Shared Access Key`: Вы получаете это из hello процедуры для создания ключа. Это конкретных toohello больших двоичных объектов.
* `Schema ID`: hello идентификатор схемы, созданные для определенной схемы. Hello данные этого большого двоичного объекта должны соответствовать схеме toohello.
* `DateTime`: hello времени, на какие hello отправляется запрос, UTC. Мы принимаем следующие форматы: ISO8601 (например, "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").
* `Instrumentation key` для ресурса Application Insights.

Hello становятся доступными в аналитике через несколько минут.

## <a name="error-responses"></a>Сообщения об ошибках

* **400 Ошибочный запрос**: указывает hello полезных данных запроса является недопустимым. Убедитесь, что:
 * указан правильный ключ инструментирования;
 * указано допустимое значение времени Оно должно быть время hello, теперь в формате UTC.
 * JSON hello события соответствует toohello схемы.
* **403 Запрещено**: hello больших двоичных объектов, отправленные вами недоступен. Убедитесь, что hello общий ключ доступа является допустимым и не истек.
* **404. Не найдено**:
 * Hello большого двоичного объекта не существует.
 * Неверный идентификатор sourceId Hello.

Более подробные сведения содержатся в hello ответа, сообщение об ошибке.


## <a name="sample-code"></a>Пример кода

Этот код использует hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) пакет NuGet.

### <a name="classes"></a>Классы

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>Прием данных

Используйте этот код для каждого большого двоичного объекта. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Дальнейшие действия

* [Обзор hello язык запросов для анализа журналов](app-insights-analytics-tour.md)
* [Используйте *Logstash* tooApplication toosend данных аналитики](https://github.com/Microsoft/logstash-output-application-insights)
