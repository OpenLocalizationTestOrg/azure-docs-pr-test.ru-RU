---
title: "API-Интерфейс сборщика данных HTTP Analytics aaaLog | Документы Microsoft"
description: "Можно использовать hello API сборщика данных HTTP аналитики журналов tooadd POST JSON данных toohello анализа журналов репозиторий из любого клиента, который можно вызвать hello REST API. В этой статье описывается toouse hello API и содержит примеры toopublish данных с использованием различных языков программирования."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Отправка данных tooLog аналитика с hello HTTP API-Интерфейс сборщика данных
В этой статье показано, как toouse hello tooLog данных API-Интерфейс сборщика данных HTTP toosend Analytics из клиента REST API.  Он описывает, как tooformat данными, собранными сценарий или приложение, включить его в запросе и иметь этот запрос авторизован службой аналитики журналов.  В этой статье приведены примеры для PowerShell, C# и Python.

## <a name="concepts"></a>Основные понятия
Можно использовать toosend данных API-Интерфейс сборщика данных HTTP hello tooLog Analytics из любого клиента, который может вызывать API-интерфейса REST.  Это может быть runbook в автоматизации Azure, которая собирает управления данные из Azure или другой облака или он может быть системой альтернативного управления, которая использует tooconsolidate анализа журналов и анализа данных.

Все данные в репозитории hello анализа журналов хранятся как запись с записей типа.  Формат вашего toohello toosend данных HTTP API-Интерфейс сборщика данных нескольких записей в формате JSON.  При отправке данных hello отдельную запись создается в репозитории hello для каждой записи в полезных данных запроса hello.


![Обзор сборщика данных HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Создание запроса
API сборщик данных toouse hello HTTP, создайте запрос POST, включающий toosend данных hello в JavaScript Object Notation (JSON).  Здравствуйте, атрибуты hello списка следующих трех таблиц, необходимых для каждого запроса. Описаны более подробно далее в статье hello каждого атрибута.

### <a name="request-uri"></a>URI запроса
| Атрибут | Свойство |
|:--- |:--- |
| Метод |ПУБЛИКАЦИЯ |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Тип содержимого |приложение/json |

### <a name="request-uri-parameters"></a>Параметры URI запроса
| Параметр | Описание |
|:--- |:--- |
| CustomerID |Уникальный идентификатор Hello для рабочей области Microsoft Operations Management Suite hello. |
| Ресурс |Имя ресурса Hello API: / api/logs. |
| Версия API |версия Hello toouse hello API с этим запросом. В настоящее время это версия 2016-04-01. |

### <a name="request-headers"></a>Заголовки запросов
| Заголовок | Описание |
|:--- |:--- |
| Авторизация |подпись авторизации Hello. Далее в статье hello вы найдете сведения о том, как заголовок toocreate HMAC-SHA256. |
| Log-Type |Укажите тип записи hello hello отправляемых данных. В настоящее время тип журнала hello поддерживает только текстовые символы. Цифры и специальные символы не поддерживаются. |
| x-ms-date |Дата Hello обработки этого запроса hello, в формате RFC 1123. |
| time-generated-field |Имя поля данных hello, содержащей timestamp hello элемента данных hello Hello. Если вы укажете здесь поле, его содержимое будет использоваться как значение параметра **TimeGenerated**. Если это поле не указано, по умолчанию для Здравствуйте, **TimeGenerated** — время hello, hello полученный является сообщение. содержимое поля сообщения hello Hello следовать hello ISO 8601 формат гггг-мм-: Ssz. |

## <a name="authorization"></a>Авторизация
Любой запрос toohello API сборщика данных HTTP аналитики журналов должен включать заголовок авторизации. tooauthenticate запроса, необходимо подписать запрос hello с hello первичный или вторичный ключ hello hello рабочей области, которая делает запрос hello. Затем передайте подпись в составе запроса hello.   

Вот hello формат для заголовка авторизации hello.

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*ИД рабочей области* — уникальный идентификатор рабочей области Operations Management Suite hello hello. *Подпись* — [хэш-проверки подлинности сообщения код (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) , создается из запроса hello и затем вычисляется с помощью hello [алгоритм SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Затем его можно закодировать с помощью кодировки Base64.

Используйте этот формат tooencode hello **SharedKey** строки подписи:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Вот пример строки подписи:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

При наличии строки подписи hello, кодировать их с помощью hello алгоритм HMAC-SHA256 на hello строку в кодировке UTF-8 и затем кодирует hello результат в Base64. Используйте следующий формат:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

Примеры Hello в следующих разделах hello имеют toohelp кода образца, создайте заголовок авторизации.

## <a name="request-body"></a>Тело запроса
тело Hello приветственное сообщение должно быть в формате JSON. Она должна включать один или несколько записей с пар имен и значений свойств hello в следующем формате:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

Позволяет выполнять пакетные несколько записей вместе в одном запросе с помощью hello следующая формата. Все записи hello должно быть hello таким же типом записи.

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a>Тип и свойства записи
Определить тип пользовательских записей, при передаче данных с помощью hello API сборщика данных HTTP аналитики журналов. В настоящее время не удается записать данные tooexisting типы записей, которые были созданы в другие типы данных и решениях. Служба аналитики журналов считывает hello входящих данных, а затем создает свойства, которые соответствуют типам данных hello значений Привет вводимых.

Каждый запрос toohello, необходимо включить API аналитики журналов **тип журнала** заголовок с именем hello hello типа записи. суффикс Hello **_CL** — имя автоматически добавленных toohello введите toodistinguish его из других журналов типы как пользовательского журнала. Например, если ввести имя hello **MyNewRecordType**, аналитика журналов создается запись с типом hello **MyNewRecordType_CL**. Это помогает избежать конфликтов между именами типов, создаваемыми пользователями, и готовыми именами существующих или будущих решений Microsoft.

Тип данных свойства tooidentify, аналитика журналов добавляет суффикс toohello имя свойства. Если свойство содержит значение null, свойство hello не включено в этой записи. В этой таблице перечислены тип данных свойства hello и соответствующего суффикса.

| Тип данных свойства | Суффикс |
|:--- |:--- |
| Строка |_s |
| Логический |_b |
| Double |_d |
| Дата и время |_t |
| GUID |_g |

Hello тип данных, который использует служба аналитики журналов для каждого свойства зависит от типа записи hello для новой записи hello, существуют ли уже.

* Если тип записи hello не существует, аналитика журналов создает новую. Служба аналитики журналов использует hello JSON вывод toodetermine hello тип данных для каждого свойства для новой записи hello.
* Если существует тип записи hello, аналитика журналов попыток toocreate новой записи на основе существующих свойств. Если hello тип данных для свойства в новой записи hello не соответствуют и не может быть преобразованный toohello существующий тип или если hello запись содержит свойство, которое не существует, аналитика журналов создает новое свойство с соответствующей суффикс hello.

Например, при отправке следующих данных создается запись с тремя свойствами: **number_d**, **boolean_b** и **string_s**:

![Пример записи 1](media/log-analytics-data-collector-api/record-01.png)

Если введен этот следующей записи со всеми значениями в строковом формате hello свойства не будут изменяться. Эти значения могут быть tooexisting преобразованные типы данных:

![Пример записи 2](media/log-analytics-data-collector-api/record-02.png)

Но при внесении следующего Отправка анализа журналов приведет hello новые свойства **boolean_d** и **string_d**. Преобразовать эти значения нельзя:

![Пример записи 3](media/log-analytics-data-collector-api/record-03.png)

Если введен hello следующие записи, перед созданием тип записи hello анализа журналов создать запись с тремя свойствами **указанного**, **boolean_s**, и **string_s**. В этой операции каждый начальные значения hello форматируется как строка:

![Пример записи 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Ограничения данных
Существуют некоторые ограничения вокруг hello данные, отправленные toohello сбора данных аналитики журналов API.

* Не более 30 МБ на tooLog post Analytics API-Интерфейс сборщика данных. Это ограничение размера для одной публикации. Если hello данных из одной записи, размер которой превышает 30 МБ, следует разбить hello фрагментами данных вверх toosmaller размера, а затем отправить их одновременно.
* Не более 32 КБ для значений полей. Если значение поля hello превышает 32 КБ, hello данные будут усечены.
* Рекомендуемое максимальное количество полей для данного типа — 50. Это ограничение введено для удобства поиска и использования.  

## <a name="return-codes"></a>Коды возврата
Код состояния HTTP 200 Hello означает, что для обработки был получен этот запрос hello. Это означает, что hello, операция выполнена успешно.

В этой таблице перечислены hello полный набор кодов состояний, которые могут возвращать hello службы.

| Код | Состояние | Код ошибки | Описание |
|:--- |:--- |:--- |:--- |
| 200 |ОК | |успешно принят запрос Hello. |
| 400 |Недопустимый запрос |InactiveCustomer |Рабочая область Hello был закрыт. |
| 400 |Недопустимый запрос |InvalidApiVersion |Hello API версии, указанной службой hello не распознана. |
| 400 |Недопустимый запрос |InvalidCustomerId |указан недопустимый ИД рабочей области Hello. |
| 400 |Недопустимый запрос |InvalidDataFormat |Отправлены недопустимые данные JSON. текст Hello ответа может содержать дополнительные сведения о как tooresolve hello ошибки. |
| 400 |Недопустимый запрос |InvalidLogType |Тип журнала Hello указан автономной специальные символы и цифры. |
| 400 |Недопустимый запрос |MissingApiVersion |версия API Hello не был указан. |
| 400 |Недопустимый запрос |MissingContentType |Тип содержимого Hello не был указан. |
| 400 |Недопустимый запрос |MissingLogType |Hello требуется значение тип журнала не был указан. |
| 400 |Недопустимый запрос |UnsupportedContentType |Тип содержимого Hello не было задано слишком**приложение/json**. |
| 403 |Запрещено |InvalidAuthorization |Hello службы не удалось выполнить запрос tooauthenticate hello. Проверьте ключ рабочей области, hello идентификатор и подключения являются допустимыми. |
| 404 |Не найдено | | Возможно, неверно указан URL-адрес hello или hello запроса слишком велик. |
| 429 |Слишком много запросов | | Hello служба столкнулась с большим объемом данных из вашей учетной записи. Повторите попытку запроса hello позже. |
| 500 |Внутренняя ошибка сервера |UnspecifiedError |Внутренняя ошибка службы Hello. Запрос hello. Повторите попытку. |
| 503 |Служба недоступна |ServiceUnavailable |Служба Hello в настоящее время является недоступным tooreceive запросов. Повторите запрос. |

## <a name="query-data"></a>Запрос данных
tooquery данные, зафиксированные hello API сборщика данных HTTP аналитики журналов, поиска записей в режиме **тип** , равно toohello **LogType** с добавлением указанным вами значением **_CL**. Например, если вы использовали значение **MyCustomLog**, будут возвращены все записи, содержащие текст **Type=MyCustomLog_CL**.

>[!NOTE]
> Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запрос изменится toohello следующее.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Примеры запросов
В следующих разделах hello, вы найдете примеры данных toosubmit toohello API сборщика данных HTTP аналитики журналов с помощью различных языков программирования.

Для каждого образца выполните указанные ниже действия tooset hello переменных для заголовка авторизации hello:

1. На портале Operations Management Suite hello, выберите hello **параметры** плитку, а затем выберите hello **подключенные источники** вкладки.
2. toohello справа от **идентификатор рабочей области**, выберите значок копирования hello, а затем вставьте идентификатор hello в качестве значения hello hello **Customer ID** переменной.
3. toohello справа от **первичного ключа**, выберите значок копирования hello, а затем вставьте идентификатор hello в качестве значения hello hello **Shared Key** переменной.

Кроме того можно изменить hello переменных типа hello журнала и данных JSON.

### <a name="powershell-sample"></a>Пример для PowerShell
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a>Пример на языке C#
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a>Пример на языке Python
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a>Дальнейшие действия
- Используйте hello [API поиска журналов](log-analytics-log-search-api.md) tooretrieve данными из репозитория анализа журналов hello.
