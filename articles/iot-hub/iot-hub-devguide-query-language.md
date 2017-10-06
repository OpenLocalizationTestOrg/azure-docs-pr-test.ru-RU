---
title: "hello aaaUnderstand язык запросов центр IoT Azure | Документы Microsoft"
description: "Руководство разработчика по - описание языка запросов SQL-подобного центра IoT hello используется tooretrieve сведения об устройстве близнецы и заданиях из вашего центра IoT."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Справочник — язык запросов Центра Интернета вещей для двойников устройств, заданий и маршрутизации сообщений

Центр IoT сведения tooretrieve мощный язык SQL-подобного в отношении [близнецы устройства] [ lnk-twins] и [заданий][lnk-jobs]и [Маршрутизация сообщений][lnk-devguide-messaging-routes]. В этой статье представлены:

* Введение toohello основные функции hello центра IoT язык запросов, и
* Hello подробное описание языка hello.

## <a name="get-started-with-device-twin-queries"></a>Начало работы с запросами двойника устройства
[Двойники устройств][lnk-twins] могут содержать произвольные объекты JSON в качестве тегов и свойств. Центр IoT позволяет близнецы tooquery устройства как единый документ JSON, содержащий все сведения об устройстве двойных.
Предполагается, для экземпляра, что ваш близнецы устройство концентратора IoT hello следующие структуры:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

Центр IoT предоставляет близнецы устройства hello в виде документа коллекцию с именем **устройств**.
Поэтому приветствия при следующем запросе извлекает hello весь набор близнецы устройства:

```sql
SELECT * FROM devices
```

> [!NOTE]
> [Пакеты SDK для Azure IoT][lnk-hub-sdks] поддерживают разбивку на страницы объемных результатов.

Центр IoT позволяет близнецы устройства tooretrieve произвольный условиям фильтрации. Например,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

Извлекает hello близнецы устройства с hello **location.region** пара тегов слишком**США**.
Кроме того, поддерживаются логические операторы и арифметические сравнения. Например,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

Извлекает все устройства близнецы, расположенный в hello нам настроен toosend телеметрии меньше часто каждую минуту. Для удобства можно также константы массива возможных toouse с hello **в** и **NIN** операторы (не в). Например,

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

извлекает все двойники устройств, сообщившие о подключении по Wi-Fi или проводной сети. Он является зачастую необходимо tooidentify все близнецы устройств, содержащих определенное свойство. Центр IoT поддерживает функции hello `is_defined()` для этой цели. Например,

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

получить все близнецы устройств, определяющие hello `connectivity` сообщил свойство. См. toohello [предложение WHERE] [ lnk-query-where] раздел для полной ссылки hello hello возможности фильтрации.

Кроме того, поддерживаются группирование и агрегаты. Например,

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Возвращает состояние конфигурации каждого телеметрии hello число устройств hello.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Hello предыдущий пример иллюстрирует ситуацию, где три устройства подтверждать успешной настройки двух применение конфигурации hello и один сообщил об ошибке.

### <a name="c-example"></a>Пример C#
функции запросов Hello предоставляется hello [службу C# SDK] [ lnk-hub-sdks] в hello **RegistryManager** класса.
Ниже приведен пример простого запроса:

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Обратите внимание, каким образом hello **запроса** создается с размер страницы (вверх too1000) и затем можно получить несколько страниц с вызывающему Привет **GetNextAsTwinAsync** методы несколько раз.
Примечание hello объекта запроса предоставляет доступ к нескольким **Далее\***, в зависимости от предусмотренного hello запроса, таких как объекты устройств двойных или задания параметр десериализации hello или обычный toobe JSON при использовании проекций.

### <a name="nodejs-example"></a>Пример для Node.js
функции запросов Hello предоставляется hello [службы Azure IoT SDK для Node.js] [ lnk-hub-sdks] в hello **реестра** объекта.
Ниже приведен пример простого запроса:

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Обратите внимание, каким образом hello **запроса** создается с размер страницы (вверх too1000) и затем можно получить несколько страниц с вызывающему Привет **nextAsTwin** методы несколько раз.
Примечание hello объекта запроса предоставляет доступ к нескольким **Далее\***, в зависимости от предусмотренного hello запроса, таких как объекты устройств двойных или задания параметр десериализации hello или обычный toobe JSON при использовании проекций.

### <a name="limitations"></a>Ограничения
> [!IMPORTANT]
> Результаты запроса могут иметь несколько минут задержки с учетом toohello последние значения в близнецы устройства. Если запросы к близнецы отдельное устройство по идентификатору, его всегда является предпочтительным toouse hello извлечения устройства двойных API, который всегда содержит последние значения hello и имеет выше регулирование пределы.

В настоящее время сравнения поддерживаются только между типами-примитивами (не объектами), например, `... WHERE properties.desired.config = properties.reported.config` поддерживается только в том случае, если эти свойства имеют примитивные значения.

## <a name="get-started-with-jobs-queries"></a>Начало работы с запросами заданий
[Задания] [ lnk-jobs] предоставляют tooexecute способом операции на наборы устройств. Каждый двойных устройства сведениями hello hello заданий, из которых он входит в коллекцию с именем **задания**.
Логически получается следующее:

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

В настоящее время эта коллекция поддерживает запросы как **devices.jobs** в hello центра IoT язык запросов.

> [!IMPORTANT]
> В настоящее время hello свойства задания никогда не возвращается при запросе близнецы устройства (запросы, содержащих «с устройств»). Доступ к нему можно получить только непосредственно с помощью запросов, использующих `FROM devices.jobs`.
>
>

Например, tooget все задания (последние и запланированные), влияющих на отдельном устройстве, можно использовать приветствия при следующем запросе:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Обратите внимание на то, как этот запрос предоставляет hello конкретного устройства состояние каждого задания возвращается (и, возможно hello прямой метод ответа).
Это также возможно toofilter с произвольной логических условий для всех свойств объекта в hello **devices.jobs** коллекции.
Например hello следующий запрос:

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

получает список всех завершенных заданий обновления двойников устройств для устройства **myDeviceId**, созданных после сентября 2016 года.

Это также tooretrieve возможные результаты на устройство hello одним заданием.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Ограничения
В настоящее время запросы к **devices.jobs** не поддерживают следующие элементы:

* проекции, поэтому можно использовать только `SELECT *`;
* Условия, которые ссылаются двойных toohello устройства в свойствах toojob сложения (см. раздел hello предшествующий раздела).
* выполняемые агрегаты, например count, avg, group by.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Начало работы с выражениями запросов по маршрутам сообщений, отправляемых с устройства в облако

С помощью [маршруты устройства в облако][lnk-devguide-messaging-routes], можно настроить центр IoT toodispatch устройства в облако сообщений toodifferent конечные точки на основе выражений, оцениваются на отдельных сообщений.

маршрут Hello [условие] [ lnk-query-expressions] использует hello же язык запросов центр IoT в качестве условий в запросах двойных и задания. Маршрут условий в заголовки сообщений hello и текст. Маршрутизации запроса выражение может включать только заголовки сообщений, но только тела сообщения hello, или заголовки сообщения и тело сообщения. Центр IoT предполагается определенной схеме hello заголовки и текст сообщения в порядке tooroute сообщений и hello в следующих разделах описываются требования для центра IoT tooproperly маршрута:

### <a name="routing-on-message-headers"></a>Маршрутизация по заголовкам сообщений

Центр IoT предполагается следующий JSON-представление заголовков сообщений для маршрутизации сообщений hello.

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

Системные свойства сообщения имеют префикс hello `'$'` символов.
Доступ к пользовательским свойствам всегда осуществляется с использованием их имен. Если имя свойства пользователя происходит toocoincide с системного свойства (такие как `$to`), свойство hello пользователя будут извлечены с hello `$to` выражение.
Вы всегда можете открыть Свойства системы hello квадратными скобками `{}`: например, можно использовать выражение hello `{$to}` tooaccess hello системное свойство `to`. Имена свойств в квадратных скобках всегда получают hello соответствующего свойства системы.

Не забывайте, что в именах свойств не учитывается регистр.

> [!NOTE]
> Все свойства сообщения являются строками. Системные свойства, как описано в hello [руководстве разработчика][lnk-devguide-messaging-format], в настоящий момент не доступны toouse в запросах.
>

Например, если вы используете `messageType` свойства, может потребоваться tooroute все данные телеметрии tooone и все оповещения tooanother конечная. Можно написать следующие выражения tooroute hello телеметрии hello:

```sql
messageType = 'telemetry'
```

И hello следующие выражения tooroute hello предупреждающих сообщений.

```sql
messageType = 'alert'
```

Также поддерживаются логические выражения и функции. Эта функция позволяет toodistinguish между уровень серьезности, например:

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

См. toohello [выражений и условий] [ lnk-query-expressions] раздел hello полный список поддерживаемых операторов и функций.

### <a name="routing-on-message-bodies"></a>Маршрутизация по тексту сообщений

Центр IoT только маршрутизацию на основе тела сообщения содержимое, если текст сообщения hello правильно сформированный JSON в кодировке UTF-8, UTF-16 или UTF-32. Необходимо задать тип содержимого hello приветственное сообщение слишком`application/json` и hello содержимого кодировки tooone hello поддерживается кодировки UTF в tooallow заголовки сообщений hello, центр IoT tooroute приветственное сообщение в зависимости от содержимого текста hello. Если один из заголовков hello не указан, центр IoT не будет tooevaluate любое выражение запроса, включающие текст hello от приветственное сообщение. Если сообщение не является сообщением JSON или приветственное сообщение не указывает тип содержимого hello и кодировку содержимого, по-прежнему может использовать сообщение hello tooroute на основании заголовков сообщений hello Маршрутизация сообщений.

Можно использовать `$body` в сообщение hello tooroute выражение запроса hello. Простой текст ссылки, ссылка на массив текст или несколько ссылок на текст можно использовать в выражении запроса hello. В выражении запроса можно также указывать сочетание ссылки на текст со ссылкой на заголовок сообщения. Например hello ниже приведены допустимые выражения.

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>Основные сведения о запросе Центра Интернета вещей
Каждый запрос Центра Интернета вещей состоит из предложений SELECT и FROM, а также необязательных предложений WHERE и GROUP BY. Каждый запрос выполняется для коллекции документов JSON, например двойников устройств. Hello предложение FROM указывает hello документа коллекции toobe итерация на (**устройств** или **devices.jobs**). Затем hello hello, ГДЕ применяется предложение фильтра. С агрегаты, а результаты этого шага hello группируются как hello указано в предложении GROUP BY, и для каждой группы формируется строку как указано в предложении SELECT hello.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>Предложение FROM
Hello **из < from_specification >** предложение можно предположить только два значения: **с устройств**, близнецы tooquery устройство, или **из devices.jobs**, tooquery задания на устройство Подробные сведения.

## <a name="where-clause"></a>Предложение WHERE
Hello **ГДЕ < filter_condition >** предложение является необязательным. Указывает одно или несколько условий, которым hello документов JSON в коллекции hello FROM должны удовлетворять toobe включается как часть результата hello. Любой документ JSON должно быть указано hello условия слишком «true» toobe включается в результат hello.

Допускается Hello условия, описанные в разделе [выражений и условий][lnk-query-expressions].

## <a name="select-clause"></a>Предложение SELECT
предложение SELECT Hello (**ВЫБЕРИТЕ < select_list >**) является обязательным и указывает, какие значения извлекаются из запроса hello. Он указывает toobe значения JSON hello toogenerate новых объектов JSON.
Для каждого элемента Здравствуйте отфильтрованные (и при необходимости сгруппированные) подмножеством hello FROM коллекции, этап отображения hello создает новый объект JSON, созданные с помощью hello значения, указанные в предложении SELECT hello.

Ниже приведен hello грамматики hello предложения SELECT.

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

где **attribute_name** ссылается свойство tooany документа JSON hello в коллекции hello FROM. Некоторые примеры предложения SELECT можно найти в hello [Приступая к работе с запросами двойных устройства] [ lnk-query-getstarted] раздела.

В настоящее время предложения для осуществления выбора, отличные от **SELECT \***, поддерживаются только в статистических запросах к двойникам устройств.

## <a name="group-by-clause"></a>Предложение GROUP BY
Hello **GROUP BY < group_specification >** предложение является необязательным элементом, могут быть выполнены после фильтр hello, указан в hello предложение WHERE и перед hello проекции, указанной в hello выбрать. Он группирует документов на основании hello значение атрибута. Эти группы представлены используемые toogenerate суммарный значения, указанные в предложении SELECT hello.

Ниже представлен пример запроса с использованием предложения GROUP BY:

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Hello формальных для GROUP BY используется синтаксис:

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

где **attribute_name** ссылается свойство tooany документа JSON hello в коллекции hello FROM.

В настоящее время hello предложения GROUP BY поддерживается только при запросе близнецы устройства.

## <a name="expressions-and-conditions"></a>Выражения и условия
В общем *выражение*:

* Результатом является tooan экземпляр типа JSON (например, логическое значение, число, строка, массив или объект.), и
* Определяется путем обработки данных, поступающих из документа JSON устройства hello и константы, с помощью встроенных операторов и функций.

*Условия* , выражений, которые оценивают tooa логическое значение. Любой другой константой, отличный от Boolean **true** считается **false** (включая **null**, **не определено**, любой экземпляр объекта или массива все строки и четко hello логическое значение **false**).

Hello для выражения используется синтаксис:

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

Описание:

| Знак | Определение |
| --- | --- |
| attribute_name | Любое свойство документа JSON hello в hello **FROM** коллекции. |
| binary_operator | Любого бинарного оператора, перечисленные в hello [операторы](#operators) раздела. |
| function_name| Любая функция, перечисленные в hello [функции](#functions) раздела. |
| decimal_literal |Число с плавающей запятой в десятичном представлении. |
| hexadecimal_literal |Число выражен строкой hello, "0 x», за которым следует строка шестнадцатеричных цифр. |
| string_literal |Строковые литералы — это строки Юникода, представленные в виде последовательности из нуля или более знаков Юникода или escape-последовательностей. Строковые литералы заключаются в одинарные кавычки (апостроф — ') или двойные кавычки (кавычки — "). В знаках Юникода, определяемых 4 шестнадцатеричными цифрами, разрешено использовать escape-символы `\'`, `\"`, `\\` и `\uXXXX`. |

### <a name="operators"></a>Операторы
поддерживаются следующие операторы Hello:

| Семейство | Операторы |
| --- | --- |
| Арифметические |+,-,*,/,% |
| Логические |AND, OR, NOT |
| Сравнение |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>Функции
При выполнении запроса задания и близнецы hello поддерживается только функция является:

| Функция | Описание |
| -------- | ----------- |
| IS_DEFINED(Свойство) | Возвращает логическое значение, указывающее, если свойство hello назначено значение (включая `null`). |

В условиях маршруты поддерживаются следующие математические функции hello.

| Функция | Описание |
| -------- | ----------- |
| ABS(x) | Возвращает hello абсолютное (положительное) значение hello указанного числового выражения. |
| EXP(x) | Возвращает значение экспоненты hello объекта hello указанного числового выражения (e ^ x). |
| POWER(x,y) | Здравствуйте, возвращает значение указанного hello toohello выражения указанная степень (x ^ y).|
| SQUARE(x) | Квадратный из hello hello возвращает указанное числовое значение. |
| CEILING(x) | Возвращает hello наименьшее целочисленное значение больше или равно, hello указанного числового выражения. |
| FLOOR(x) | Возвращает наибольшее целое число hello меньше или равно toohello указанного числового выражения. |
| SIGN(x) | Здравствуйте, возвращает положительное (+ 1), ноль (0) или отрицательный знак (-1) hello указанного числового выражения.|
| SQRT(x) | Квадратный из hello hello возвращает указанное числовое значение. |

В условиях маршруты hello после типа, проверка и приведение функции поддерживаются:

| Функция | Описание |
| -------- | ----------- |
| AS_NUMBER | Преобразует число tooa hello входной строки. Возвращает `noop`, если аргумент является числом, или `Undefined`, если строка не представляет число.|
| IS_ARRAY | Возвращает логическое значение, указывающее, если тип hello hello задать выражение является массивом. |
| IS_BOOL | Возвращает логическое значение, указывающее, если тип hello hello задать выражение является логическим. |
| IS_DEFINED | Возвращает логическое значение, указывающее, если свойство hello назначено значение. |
| IS_NULL | Возвращает логическое значение, указывающее, если тип hello hello задать выражение имеет значение null. |
| IS_NUMBER | Возвращает логическое значение, указывающее, если тип hello hello задать выражение является числом. |
| IS_OBJECT | Возвращает логическое значение, указывающее, если тип hello hello задать выражение, объект JSON. |
| IS_PRIMITIVE | Возвращает логическое значение, указывающее, если тип hello hello задать выражение является примитивом (строка, логическое значение, числовое или `null`). |
| IS_STRING | Возвращает логическое значение, указывающее, если тип hello hello выражения является строка. |

В условиях маршруты поддерживаются следующие строковые функции hello.

| Функция | Описание |
| -------- | ----------- |
| CONCAT(x, …) | Возвращает строку, являющуюся результатом объединения двух или более строковых значений hello. |
| LENGTH(x) | Количество символов для hello hello возвращает указанного строкового выражения.|
| LOWER(x) | Возвращает строковое выражение после преобразования данных toolowercase символ верхнего регистра. |
| UPPER(x) | Возвращает строковое выражение после преобразования данных toouppercase строчные буквы. |
| SUBSTRING(строка, начало[, длина]) | Возвращает часть строкового выражения, начиная с hello указан символ Отсчитываемая от нуля позиция и продолжает toohello указывается длина или toohello конца строки hello. |
| INDEX_OF(строка, фрагмент) | Возвращает hello, начальная позиция первого вхождения hello hello второго строкового выражения внутри первого указанного строкового выражения hello, или значение -1, если строка hello не найдена.|
| STARTS_WITH(x, y) | Возвращает логическое значение, указывающее, является ли первое строковое выражение hello начинается с hello во-вторых. |
| ENDS_WITH(x, y) | Возвращает логическое значение, указывающее, было ли первое строковое выражение hello заканчивается hello второй. |
| CONTAINS(x,y) | Возвращает логическое значение, указывающее, является ли hello первое строковое выражение содержит hello второй. |

## <a name="next-steps"></a>Дальнейшие действия
Узнайте, как tooexecute запросы в приложения с помощью [пакеты SDK Azure IoT][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
