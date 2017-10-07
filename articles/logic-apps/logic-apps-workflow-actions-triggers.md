---
title: "aaaWorkflow действия и триггеры — логика приложения Azure | Документы Microsoft"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Действия и триггеры рабочих процессов в Azure Logic Apps

Приложения логики состоят из триггеров и действий. Существует шесть типов триггеров. У каждого из них свой интерфейс и разное поведение. Также можно узнать о других сведений, просмотрев сведения hello объекта hello [язык определения рабочих процессов](logic-apps-workflow-definition-language.md).  
  
Прочитано toolearn Дополнительные сведения о триггеров, действий и использования их toobuild логику приложения tooimprove бизнес-процессов и рабочих процессов.  
  
### <a name="triggers"></a>триггеры;  

Триггер задает hello вызовов, которые можно инициировать запуск рабочего процесса логику приложения. Ниже приведены два разных способа hello tooinitiate выполнения рабочего процесса.  
  
-   с помощью опрашивающего триггера;  

-   Триггер push - по вызывающему Привет [API REST службы рабочего процесса](https://docs.microsoft.com/rest/api/logic/workflows)  
  
Все триггеры содержат следующие элементы верхнего уровня:  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Типы триггеров и их входные данные  

Можно использовать такие типы триггеров:
  
-   **Запрос** \- делает приложение hello логику конечную точку для вас toocall  
  
-   **Триггер повторения** (recurrence) — активируется на основе определенного расписания.  
  
-   **HTTP-триггер** — опрашивает конечную веб-точку HTTP. Hello HTTP конечной точки должны соответствовать определенным контрактом запускающее tooa \- либо с помощью 202\-асинхронный шаблон, или, возвращая массив  
  
-   **ApiConnection** \- активировать опросы как hello HTTP, однако она использует преимущества hello [API-интерфейсы, управляемая корпорацией Майкрософт](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- открывает конечной точки, аналогичные toohello триггер запуска вручную, однако он также вызывает tooa указан URL-адрес tooregister и отмены регистрации  
  
-   **ApiConnectionWebhook** \- работает как hello HTTPWebhook триггер, используя преимущества hello API-интерфейсы, управляемая корпорацией Майкрософт       
    Каждый тип триггера имеет разный набор **входных данных**, определяющий его поведение.  
  
## <a name="request-trigger"></a>Триггер запросов  

Этот триггер служит в качестве конечной точки, которые можно вызвать через HTTP-запроса tooinvoke логику приложения. Триггер запроса выглядит следующим образом:  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

Имеется также необязательное свойство, которое называется **schema**.  
  
|Имя элемента|Обязательно|Описание|  
|----------------|------------|---------------|  
|schema|Нет|Схема JSON, которая проверяет hello входящего запроса. Это полезно для помогает знать, какие свойства tooreference действия последующих рабочих процессов.|

tooinvoke этой конечной точки требуется toocall hello *listCallbackUrl* API. См. сведения в статье [Рабочие процессы](https://docs.microsoft.com/rest/api/logic/workflows).  
  
## <a name="recurrence-trigger"></a>Триггер повторения  

Триггер recurrence — это триггер, который выполняется на основе заданного расписания. Такой триггер может выглядеть следующим образом:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Как видите, это простой способ toorun рабочего процесса.  
  
|Имя элемента|Обязательно|Описание|  
|----------------|------------|---------------|  
|frequency|Да|Как часто hello триггер выполняет. Используйте только одно из этих значений: Second, Minute, Hour, Day, Week, Month или Year.|  
|interval|Да|Интервал hello заданных частоту повторения hello|  
|startTime|Нет|Используется, если для свойства startTime указано значение без смещения от UTC.|  
|timeZone|Нет|Используется, если для свойства startTime указано значение без смещения от UTC.|  
  
Можно также запланировать триггеров toostart, выполняющихся в определенный момент в будущем hello. Например если требуется toostart еженедельную отчета каждый понедельник можно запланировать hello логику приложения toostart каждый понедельник, создав hello, следующий триггер:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>Триггер HTTP  

Триггеры HTTP опроса указанной конечной точкой и проверьте наличие toodetermine ответа hello hello рабочего процесса должны быть выполнены. Hello объекта входных данных принимает набор hello tooconstruct необходимые параметры вызов HTTP:  
  
|Имя элемента|Обязательно|Описание|Тип|  
|----------------|------------|---------------|--------|  
|метод|Да|Может принимать одно из hello следующие методы HTTP: GET, POST, PUT, DELETE, HEAD или ИСПРАВЛЕНИЯ|Строка|  
|uri|Да|Здравствуйте, конечная точка http или https, вызывается. Не более 2 КБ.|string|  
|Запросы|Нет|Объект, представляющий URL-адрес hello запроса параметров tooadd toohello. Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.|Объект|  
|headers|Нет|Объект, представляющий каждый заголовков hello, отправляет запрос toohello. Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Объект|  
|текст|Нет|Объект, представляющий полезные данные hello, отсылаемые toohello конечной точки.|Объект|  
|retryPolicy|Нет|Объект, позволяющий настраивать поведение повтора hello 4xx или 5xx ошибок.|Объект|  
|authentication|Нет|Представляет метод hello, который hello запроса должен пройти проверку подлинности. Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Помимо планировщика, имеется еще одно поддерживаемое свойство: `authority`. По умолчанию его значение равно `https://login.windows.net`, если не указано другое. Также можно использовать другое значение, например `https://login.windows\-ppe.net`.|Объект|  
  
триггер Hello HTTP необходимо tooconform hello HTTP API с toowork конкретному шаблону в логике приложения. Он требует hello следующие поля:  
  
|Ответ|Описание|  
|------------|---------------|  
|Код состояния|Код состояния 200 \(ОК\) toocause запуска. Другие коды состояния не вызывают запуск.|  
|Заголовок Retry\-After|Число секунд, пока приложение hello логику снова опрашивает hello конечной точки.|  
|Заголовок Location|Hello toocall URL-адрес в следующем интервале опроса hello. Если не указан, используется hello исходный URL-адрес.|  
  
Ниже приведены некоторые примеры различных поведений для различных типов запросов.  
  
|Код ответа|Retry\-After|Поведение|  
|-----------------|----------------|------------|  
|200|\(Нет\)|Не допустимый триггер, повторите попытку\-After используется engine требуется, в противном случае hello никогда не опрашивает hello следующего запроса.|  
|202|60|Не вызывать hello рабочего процесса. Hello при следующей попытке происходит через одну минуту.|  
|200|10|Запуск рабочего процесса hello и еще раз проверить больше содержимого в течение 10 секунд.|  
|400|\(Нет\)|Ошибочный запрос, не запускайте hello рабочего процесса. При наличии не **политика повтора** определено, то используется политика по умолчанию hello. После достижения hello число повторных попыток hello триггер больше не является допустимым.|  
|500|\(Нет\)|Ошибка сервера, не запускайте hello рабочего процесса.  При наличии не **политика повтора** определено, то используется политика по умолчанию hello. После достижения hello число повторных попыток hello триггер больше не является допустимым.|  
  
выходы Hello триггера HTTP будет выглядеть как в следующем примере:  
  
|Имя элемента|Описание|Тип|  
|----------------|---------------|--------|  
|headers|заголовки HTTP-ответа hello Hello.|Объект|  
|текст|текст Hello hello HTTP-ответа.|Объект|  
  
## <a name="api-connection-trigger"></a>Триггер подключения API  

триггер подключения Hello API — аналогичные триггера toohello HTTP в своей функциональности. Однако параметры hello для идентификации действия hello отличаются. Пример:  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|Имя элемента|Обязательно|Тип|Описание|  
|----------------|------------|--------|---------------|  
|host|Да||Hello ApiApp размещается шлюза и идентификатор.|  
|метод|Да|Строка|Может принимать одно из hello следующие методы HTTP: **получить**, **POST**, **ПОМЕСТИТЬ**, **удаление**, **PATCH**, или  **HEAD**|  
|Запросы|Нет|Объект|Представляет hello запроса параметров toobe добавлен toohello URL-адрес. Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.|  
|headers|Нет|Объект|Представляет каждый заголовков hello, отправляет запрос toohello. Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|текст|Нет|Объект|Представляет полезные данные hello, отправляемое toohello конечной точки.|  
|retryPolicy|Нет|Объект|Позволяет toocustomize характер повторения hello 4xx или 5xx ошибок.|  
|authentication|Нет|Объект|Представляет метод hello, который hello запроса должен пройти проверку подлинности. Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).|  
  
являются следующие свойства Hello для узла.  
  
|Имя элемента|Обязательно|Описание|  
|----------------|------------|---------------|  
|api runtimeUrl|Да|Конечная точка Hello hello управляемый API.|  
|connection name||Должен быть вызван ссылочного параметра tooa `$connection` и hello имя подключения hello управляемых API, которое hello использует рабочего процесса.|
  
результаты Hello триггера API подключения являются:
  
|Имя элемента|Тип|Описание|  
|----------------|--------|---------------|  
|headers|Объект|заголовки HTTP-ответа hello Hello.|  
|текст|Объект|текст Hello hello HTTP-ответа.|  
  
## <a name="httpwebhook-trigger"></a>Триггер httpWebhook  

Hello HTTPWebhook триггер открывает конечную точку, аналогичные toohello триггер запуска вручную, но hello HTTPWebhook триггер также вызова tooa указан URL-адрес tooregister и отменять регистрацию. Триггер httpWebhook может выглядеть следующим образом:  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

Многие из этих разделов являются необязательными, и поведение hello hello веб-перехватчика зависит от того, какие разделы предоставленные или опущен.  
свойства веб-перехватчика Hello выглядят следующим образом:  
  
|Имя элемента|Обязательно|Описание|  
|----------------|------------|---------------|  
|subscribe|Нет|Здравствуйте, исходящий запрос, который вызывается, когда триггер hello создается и выполняет hello первоначальной регистрации.|  
|unsubscribe|Нет|Здравствуйте, исходящего сообщения запроса, при удалении триггера hello.|  
  
-   **Подписка** hello исходящего вызова, от которого поступил прослушивания tooevents toostart. Этот вызов начинается с hello выполните одинаковый набор параметров, которые hello обычные действия HTTP. Исходящих вызове любой hello время изменения рабочего процесса каким-либо образом, например, каждый раз, когда учетные данные hello учитываются или триггер hello входных параметров изменений.
  
    toosupport этот вызов, новые функции: `@listCallbackUrl()`. Эта функция возвращает уникальный URL-адрес для конкретного триггера в этом рабочем процессе. Он представляет уникальный идентификатор hello hello конечные точки, использующие hello службы REST.  
  
-   **unsubscribe** вызывается, когда операция делает этот триггер недействительным, например в результате таких действий:  
  
    -   Удаление или отключение триггера hello  
  
    -   Удаление или отключение hello рабочего процесса  
  
    -   Удаление или отключение подписки hello  
  
    приложения логики Hello автоматически вызывает hello действие отмены подписки. Параметры Hello, функция toothis hello таким же как триггер hello HTTP.  
  
    Hello выходы триггера HTTPWebhook hello представляют Привет содержимое hello входящего запроса:  
  
|Имя элемента|Тип|Описание|  
|-----------------|--------|---------------|  
|headers|Объект|заголовки Hello hello HTTP-запроса.|  
|текст|Объект|текст Hello hello HTTP-запроса.|  

Ограничения на действия веб-перехватчик может быть указано в hello так же, как [ограничения асинхронный HTTP](#asynchronous-limits).
  

## <a name="conditions"></a>Условия  

Для любого триггера можно использовать один или несколько условий toodetermine ли должен выполняться рабочий процесс hello, или нет. Например:  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

В этом случае hello только триггеры отчета во время рабочего процесса hello `sendReports` параметр имеет значение tootrue. Наконец условий может ссылаться на код состояния hello hello триггера. Например, можно настроить так, чтобы рабочий процесс запускался только в том случае, если веб-сайт возвращает код состояния 500:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Когда любое выражение ссылается на код состояния hello триггера hello \(каким-либо образом\), поведение по умолчанию hello \(триггер только на 200 \(ОК\) \) заменяется. Например, если требуется tootrigger на код состояния 200 и код состояния 201 имеется tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` как условие.  
  
## <a name="start-multiple-runs-for-a-request"></a>Запуск нескольких выполнений запроса

tookick отключение нескольких тестовых запусков для отдельного запроса `splitOn` может быть полезным, например, при необходимости toopoll конечную точку, которая может иметь несколько новых элементов между интервалами опроса.
  
С `splitOn`, можно указать свойство hello внутри hello полезные данные ответа, содержащий hello массив элементов, каждый из которых требуется toouse toostart выполнения триггера hello. Например предположим, что у вас есть API, который возвращает hello следующий ответ:  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
Логика приложения требуется только содержимое строк hello, можно создать триггер как в следующем примере:  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
Затем в hello определения рабочего процесса, `@triggerBody().name` возвращает `mycoolrow` для первого запуска hello и `another row` hello второго тестового запуска. Hello вид триггера выходные данные как в следующем примере:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Таким образом, если вы используете `SplitOn`, не удалось получить свойства hello, которые находятся за пределами массива hello в этом случае hello `Status` поля.  
  
> [!NOTE]  
> В этом примере мы используем hello `?` tooavoid сбой, если hello может toobe оператор `Rows` свойство отсутствует. 
  
## <a name="single-run-instance"></a>Экземпляр однократного выполнения

Вы можете настроить триггеры, если завершены все активные запуски пожар tooonly свойство повторения. В случае запланированного повторения при выполняющегося теста триггер hello пропускает и ждет, пока hello Далее повторения запланированного интервала toocheck еще раз.

Этот параметр через параметры hello операции:

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>Типы и входные данные  

Существует много типов действий, каждое из которых имеет уникальное поведение. Действия коллекций могут содержать множество вложенных действий.

### <a name="standard-actions"></a>Стандартные действия  

-   **http** — это действие вызывает конечную веб-точку HTTP.  
  
-   **ApiConnection** \- это действие ведет себя как hello действия HTTP, но использует hello API-интерфейсы, управляемая корпорацией Майкрософт.  
  
-   **ApiConnectionWebhook** \- как HTTPWebhook, но hello использует API-интерфейсы, управляемая корпорацией Майкрософт.  
  
-   **response** — это действие определяет ответ для входящего вызова.  
  
-   **wait** — это простое действие ожидает фиксированное количество времени или до определенного времени.  
  
-   **workflow** — это действие представляет вложенный рабочий процесс.  

-   **Function** \- — это действие представляет функцию Azure.

### <a name="collection-actions"></a>Действия коллекций

-   **scope** — это действие является логическим объединением других действий.

-   **Условие** \- это действие, вычисляет выражение и выполняет соответствующую ветвь результат hello.

-   **foreach** — это циклическое действие выполняет итерацию по массиву и внутренние действия для каждого элемента.

-   **Пока** \- этого цикла действия выполняет внутреннее действий, пока условие приводит tootrue.
  
Каждый тип действия имеет разный набор **входных данных**, определяющих его поведение.  
  
## <a name="http-action"></a>Действие HTTP  

Действия HTTP вызова заданной конечной точки и проверьте наличие toodetermine hello ответ должен выполняться рабочий процесс hello. Hello **входов** объект принимает набор hello вызовов hello HTTP tooconstruct необходимые параметры:  
  
|Имя элемента|Обязательно|Тип|Описание|  
|----------------|------------|--------|---------------|  
|метод|Да|Строка|Может принимать одно из hello следующие методы HTTP: **получить**, **POST**, **ПОМЕСТИТЬ**, **удаление**, **PATCH**, или  **HEAD**|  
|uri|Да|Строка|Здравствуйте, конечная точка http или https, вызывается. Не более 2 КБ.|  
|Запросы|Нет|Объект|Представляет URL-адрес hello запроса параметров tooadd toohello. Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.|  
|headers|Нет|Объект|Представляет каждый заголовков hello, отправляет запрос toohello. Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|текст|Нет|Объект|Представляет полезные данные hello, отправляемое toohello конечной точки.|  
|retryPolicy|Нет|Объект|Позволяет настраивать поведение повтора hello 4xx или 5xx ошибок.|  
|operationsOptions|Нет|Строка|Определяет набор hello toooverride специальные поведения.|  
|authentication|Нет|Объект|Представляет метод hello, который hello запроса должен пройти проверку подлинности. Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Помимо планировщика, имеется еще одно поддерживаемое свойство: `authority`. По умолчанию его значение равно `https://login.windows.net`, если не указано другое. Также можно использовать другое значение, например `https://login.windows\-ppe.net`.|  
  
Действия HTTP и \(действия API подключения\) поддерживают политики повтора. Политику повтора применяет toointermittent сбои, характеризуется как код состояния HTTP коды 408 429 и 5xx в исключения при подключении tooany сложения. Эта политика описываются с помощью hello *retryPolicy* объекта, определенного как показано ниже:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
Интервал повтора Hello указывается в формате ISO 8601 hello. Этот интервал имеет по умолчанию и минимальное значение 20 секунд, а hello максимальное значение составляет один час. Hello по умолчанию и максимальное число повторных попыток составляет четыре часа. Если не указано определение политики "Повторить" hello, `fixed` стратегия используется со значениями счетчика и интервала повторных попыток по умолчанию. политика повтора toodisable hello, задайте для него тип слишком`None`.  
  
Например hello следующее действие повторных попыток извлечение последние новости hello два раза, если временной ошибкой для всех трех выполнений, с 30-секундная задержка между попытками:  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>Модель асинхронных операций

По умолчанию все действия на основе HTTP поддерживают hello шаблон Стандартная асинхронной операции. Поэтому если удаленный сервер hello указывает этот запрос hello принимается для обработки с 202 \(принято\) ответа, hello Logic Apps ядра отслеживает опроса hello URL-адрес, указанный в заголовок расположения hello ответа до достижения терминала состояние \(не является\-ответа 202\).  
  
toodisable hello работы в асинхронном режиме описанные, заданные ранее `DisableAsyncPattern` параметр во входных параметрах действие hello. В этом случае hello выходные данные действия hello зависит от первоначального hello 202 ответа от сервера hello.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>Ограничения асинхронных операций

Асинхронная модель может быть ограничена его длительность tooa определенного интервала времени.  Если hello прошествии времени без достижения конечного состояния, помечается состояние hello действие hello `Cancelled` с кодом `ActionTimedOut`.  время ожидания Hello предел задается в формате ISO 8601.  Ограничения могут быть заданы с hello, используя синтаксис:

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>API подключения  

API подключения — это действие, которое ссылается на соединитель, управляемый Майкрософт.
Это действие требует допустимое соединение tooa ссылки и сведения об hello API и параметров, необходимых.

|Имя элемента|Обязательно|Тип|Описание|  
|----------------|------------|--------|---------------|  
|host|Да|Объект|Представляет hello соединителя сведения, такие как hello runtimeUrl и ссылка toohello объект подключения|
|метод|Да|Строка|Может принимать одно из hello следующие методы HTTP: **получить**, **POST**, **ПОМЕСТИТЬ**, **удаление**, **PATCH**, или  **HEAD**|  
|path|Да|Строка|путь Hello hello API-операции.|  
|Запросы|Нет|Объект|Представляет URL-адрес hello запроса параметров tooadd toohello. Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.|  
|headers|Нет|Объект|Представляет каждый заголовков hello, отправляет запрос toohello. Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|текст|Нет|Объект|Представляет полезные данные hello, отправляемое toohello конечной точки.|  
|retryPolicy|Нет|Объект|Позволяет настраивать поведение повтора hello 4xx или 5xx ошибок.|  
|operationsOptions|Нет|Строка|Определяет набор hello toooverride специальные поведения.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>Действие webhook API подключения

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Ограничения на действия веб-перехватчик может быть указано в hello так же, как [ограничения асинхронный HTTP](#asynchronous-limits).
  
## <a name="response-action"></a>Действие ответа  

Этот тип действия содержит полезные данные ответа hello из HTTP-запроса и включает statusCode, тело и заголовки:  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
Hello ответное действие имеет специальные ограничения, которые неприменимы tooother действия. В частности:  
  
-   Ответные меры не может быть параллельной в определении, поскольку toohello входящего запроса детерминированным ответа является обязательным.  
  
-   Ответное действие при достижении после hello входящий запрос после получения действие hello считается сбой \(конфликт\), и в результате выполнения hello `Failed`.  
  
-   Рабочий процесс с действиями ответа не может содержать `splitOn` в своем триггере, так как один вызов запускает несколько выполнений. В результате это должны проверяться, когда поток hello PUT и причина неверный запрос.  
  
## <a name="wait-action"></a>Действие wait  

Hello `wait` действие приостанавливает выполнение рабочего процесса в течение указанного интервала hello. Например, toowait 15 минут можно использовать этот фрагмент кода:  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
Кроме того, toowait до определенный момент времени, можно использовать в этом примере:  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> Длительность ожидания Hello можно задать либо с помощью hello **интервал** объекта или hello **до** объекта, но не оба.  
  
|Имя|Обязательно|Тип|Описание|  
|--------|------------|--------|---------------|  
|interval|Нет|Объект|длительность, в зависимости от времени ожидания Hello.|  
|interval unit|Да|Строка|Одна из таких единиц времени: second, minute, hour, day, week, month, year.|  
|interval count|Да|Строка|Длительность основании hello данных внутренних единицах измерения.|  
|until|Нет|Объект|длительность, основано на точке на времени ожидания Hello.|  
|until timestamp|Да|Строка|Строка &#124; hello моменту времени в формате UTC, когда hello ожидания истечения срока действия.|  

## <a name="query-action"></a>Действие запроса

Hello `query` действие позволяет фильтровать массив на основе условия. Например номера tooselect больше 2, можно использовать:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

Здравствуйте, выходные данные hello `query` действие — массив, содержащий элементы из входного массива hello, удовлетворяющие условию hello.

> [!NOTE]
> Если значения не удовлетворяют hello `where` условия, hello результат — пустой массив.

|Имя|Обязательно|Тип|Описание|
|--------|------------|--------|---------------|
|from|Да|Массив,|Hello исходного массива.|
|где:|Да|Строка|Hello условие tooapply tooeach элемент hello исходного массива.|

## <a name="select-action"></a>Выбор действия

Hello `select` действие позволяет проект в новое значение каждого элемента массива.
Например, tooconvert массив чисел в массив объектов, можно использовать:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

Здравствуйте, выходные данные hello `select` действие — массив, содержащий hello того же количества элементов как hello входного массива, при этом каждый элемент, преобразованные в определенный по hello `select` свойство. Если входные данные hello пустой массив, hello выводится также пустой массив.

|Имя|Обязательно|Тип|Описание|
|--------|------------|--------|---------------|
|from|Да|Массив,|Hello исходного массива.|
|select|Да|Любой|Hello проекции tooapply tooeach элемент hello исходного массива.|

## <a name="terminate-action"></a>Действие terminate

Действие прерывания Hello останавливает выполнение hello рабочего процесса, прерывание каких-либо незавершенных действий и пропускает все оставшиеся действия. Например, tooterminate выполнения со статусом **сбой**, можно использовать следующий фрагмент кода hello:

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> Действия уже выполнены не подвержены hello завершить действие.

|Имя|Обязательно|Тип|Описание|
|--------|------------|--------|---------------|
|runStatus|Да|Строка|целевой объект Hello состояние выполнения. **Failed** или **Cancelled**.|
|runError|Нет|Объект|сведения об ошибке Hello. Если поддерживается только **runStatus** задано слишком**сбой**.|
|runError code|Нет|Строка|Здравствуйте, запустите код ошибки.|
|runError message|Нет|Строка|Здравствуйте, запустите сообщение об ошибке.|

## <a name="compose-action"></a>Действие compose

Создать действие Hello дает возможность создавать произвольный объект. выходные данные Hello hello составления действие является результатом вычисления входами hello. Например, можно использовать hello составления выходов toomerge действие из нескольких действий:

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> Hello **составление** действие может быть используется tooconstruct выходные данные, включая объекты, массивы и любого другого типа, изначально поддерживаемых логики приложения, как XML и двоичный файл.

## <a name="table-action"></a>Действие таблицы

Hello `table` позволяет tooconvert массив элементов в **CSV** или **HTML** таблицы.

Предположим, что @triggerBody() выглядит следующим образом:

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

И позволяют определить как действие hello

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

Hello выше приведет к получению

<table><thead><tr><th>id</th><th>name</th></tr></thead><tbody><tr><td>0</td><td>apples</td></tr><tr><td>1</td><td>oranges</td></tr></tbody></table>"

В таблице hello toocustomize заказа можно задать столбцы hello явным образом. Например:

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

Hello выше приведет к получению

<table><thead><tr><th>Код результата</th><th>Описание</th></tr></thead><tbody><tr><td>0</td><td>fresh apples</td></tr><tr><td>1</td><td>fresh oranges</td></tr></tbody></table>"

Если hello `from` значение свойства — пустой массив, hello результатом является пустая таблица.

|Имя|Обязательно|Тип|Описание|
|--------|------------|--------|---------------|
|from|Да|Массив,|Hello исходного массива.|
|свойства|Да|Строка|Здравствуйте, формат, либо **CSV** или **HTML**.|
|columns|Нет|Массив,|столбцы Hello. Позволяет toooverride фигуры по умолчанию hello hello таблицы.|
|column header|Нет|Строка|заголовок столбца hello Hello.|
|column value|Да|Строка|значение столбца hello Hello.|

## <a name="workflow-action"></a>Действие workflow   

|Имя|Обязательно|Тип|Описание|  
|--------|------------|--------|---------------|  
|host id|Да|Строка|Идентификатор ресурса Hello hello рабочего процесса, которые должны toocall.|  
|host triggerName|Да|Строка|Имя триггера hello, что требуется tooinvoke Hello.|  
|Запросы|Нет|Объект|Представляет URL-адрес hello запроса параметров tooadd toohello. Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.|  
|headers|Нет|Объект|Представляет каждый заголовков hello, отправляет запрос toohello. Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|текст|Нет|Объект|Представляет hello полезные данные, отправленные toohello конечной точки.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Проверку доступа, внесенные в рабочий процесс hello \(точнее, триггер hello\), то есть вы должны получить доступ к toohello рабочего процесса.  
  
Выводит Hello из hello `workflow` действия основаны на определенный hello `response` действия в рабочем процессе дочерних hello. Если вы не определили любой `response` действие, а затем выходы hello пусты.  

## <a name="function-action"></a>Действие функции   

|Имя|Обязательно|Тип|Описание|  
|--------|------------|--------|---------------|  
|ИД функции|Да|Строка|Идентификатор ресурса, которые должны tooinvoke функции hello Hello.|  
|метод|Нет|Строка|метод HTTP Hello используется tooinvoke функции hello. Если не указан, по умолчанию используется `POST`.|  
|Запросы|Нет|Объект|Представляет URL-адрес hello запроса параметров tooadd toohello. Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.|  
|headers|Нет|Объект|Представляет каждый заголовков hello, отправляет запрос toohello. Например, tooset hello язык и тип запроса в: `"headers" : { "Accept-Language": "en-us" }`.|  
|текст|Нет|Объект|Представляет hello полезные данные, отправленные toohello конечной точки.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

При сохранении логику приложения hello, мы выполняет ряд проверок на hello ссылка на функцию:
-   Требуется функция toohello toohave доступа.
-   Допускается только стандартный триггер HTTP или универсальный триггер webhook в формате JSON.
-   В ней не должен быть определен какой-либо маршрут.
-   Допускаются только авторизация с помощью функции и анонимная авторизация.

URL-адрес триггера Hello извлекается, кэшируются и используются во время выполнения. Поэтому если любая операция делает недействительными кэшированные hello URL-адрес, действие hello завершается ошибкой во время выполнения. toowork возникновения этой проблемы, сохранения hello логику приложения еще раз, что будет привести tooretrieve логику приложения и кэшировать URL-адрес триггера hello еще раз.

## <a name="collection-actions-scopes-and-loops"></a>Действия коллекций (области и циклы)

Действия некоторых типов могут содержать вложенные действия. Ссылка действия в пределах коллекции можно ссылаться непосредственно за пределами коллекции hello. Если вы определили `http` в области, `@body('http')` действительно в любой точке рабочего процесса. Действия в пределах коллекции могут `runAfter` Здравствуйте, другие действия в одной коллекции.

## <a name="scope-action"></a>Действие scope

Hello `scope` действие позволяет логически группы действий в рабочем процессе.

|Имя|Обязательно|Тип|Описание|  
|--------|------------|--------|---------------|  
|actions|Да|Объект|Tooexecute внутреннего действия в пределах области hello|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>Действие foreach

Это циклическое действие выполняет итерацию по массиву и внутренние действия для каждого элемента. По умолчанию hello цикл выполняется в параллельном режиме (20 выполнений параллельно одновременно). Можно задать выполнение правила с помощью hello `operationOptions` параметра.

|Имя|Обязательно|Тип|Описание|  
|--------|------------|--------|---------------|  
|actions|Да|Объект|Tooexecute внутреннего действия в цикле hello|
|foreach|Да|string|Hello tooiterate массива по|
|operationOptions|Нет|строка|Любые параметры операции для определения поведения. В настоящее время поддерживает только `sequential` tooexecute итераций последовательно (поведение по умолчанию — параллельных)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Действие Until

Это действие цикла выполняет внутреннее действия, пока приводит tootrue.

|Имя|Обязательно|Тип|Описание|  
|--------|------------|--------|---------------|  
|actions|Да|Объект|Tooexecute внутреннего действия в цикле hello|
|expression|Да|string|tooevaluate выражение Hello после каждой итерации|
|limit|Да|Объект|должен быть определен Hello ограничения для hello цикл - по крайней мере один нижний предел|
|count|Нет|int|Hello ограничение toohello числа итераций, которые могут быть выполнены|
|timeout|Нет|string|Здравствуйте, как долго следует цикла время ожидания.  (в формате ISO 8601).|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>Условия. Действие If

Hello `If` действия позволяет вычислить условие и выполнение ветви, в зависимости от того, является ли выражение hello имеет слишком`true`.

|Имя|Обязательно|Тип|Описание|  
|--------|------------|--------|---------------|  
|actions|Да|Объект|Tooexecute внутреннего действия, когда выражение имеет слишком`true`|
|expression|Да|string|выражение tooevaluate Hello|
|else|Нет|Объект|Tooexecute внутреннего действия, когда выражение имеет слишком`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
Hello следующей таблице приведены примеры того, как условия можно использовать выражения в действии:  
  
|Значение JSON|Результат|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Любое значение, которое будет возвращаться tootrue вызывает toopass этого условия. Поддерживаются только логические выражения. tooconvert других типов tooBoolean, используйте функции `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Поддерживаются функции сравнения. Здесь пример hello действие hello только выполняется, когда выходные данные hello act1 превышает пороговое значение hello.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Функции логики, также поддерживаемые toocreate вложенных выражений типа Boolean. В этом случае hello действие выполняется, когда выходные данные hello act1 выше порогового значения hello или ниже 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Функции toocheck массива можно использовать, если массив имеет какие-либо элементы. В этом случае hello действие выполняется, когда hello ошибки массив является пустым.| 
|`"expression": "parameters('hasSpecialAction')"`|Ошибка является недопустимым условием, поскольку для условия требуется @.|  
  
Если условие не выполняется успешно, условие hello помечается как `Succeeded`. Действия в пределах либо hello `actions` или `else` объектов оценки слишком`Succeeded` при выполнении и успешно выполнен, `Failed` при выполнении и сбой, или `Skipped` при выполнении этой ветви не.

## <a name="next-steps"></a>Дальнейшие действия

[REST API службы рабочих процессов](https://docs.microsoft.com/rest/api/logic/workflows)
