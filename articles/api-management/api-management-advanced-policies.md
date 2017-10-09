---
title: "Дополнительные политики управления API aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello Дополнительные политики, доступные для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a>Расширенные политики в службе управления API
Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AdvancedPolicies"></a> Расширенные политики  
  
-   [Поток управления](api-management-advanced-policies.md#choose) — условно применяет операторы политики на основе результатов вычисления логических hello hello [выражений](api-management-policy-expressions.md).  
  
-   [Прямой запрос](#ForwardRequest) -пересылает hello запроса toohello внутренней службы.

-   [Ограничения параллелизма](#LimitConcurrency) -предотвращает заключены политики из более чем hello указанное число запросов во время выполнения.
  
-   [Журнал tooEvent концентратора](#log-to-eventhub) -отправляет сообщения в hello указан формат tooan концентратора событий определяются сущности средства ведения журнала. 

-   [Макета ответа](#mock-response) -прерываний конвейера выполнения и возвращает ответ на сгенерированные непосредственно toohello вызывающего объекта.
  
-   [Повторите](#Retry) -повторных попыток выполнения hello заключены операторы политики, если и пока не будет выполнено условие hello. Выполнение будет сквозные hello определенные промежутки времени и копирование toohello указанное число повторных попыток.  
  
-   [Вернуть ответ](#ReturnResponse) -конвейера прерывания выполнения и возвращает hello указанного ответа непосредственно toohello вызывающего объекта. 
  
-   [Отправка запроса на один из способов](#SendOneWayRequest) -отправляет toohello запроса указан URL-адрес без ожидания ответа.  
  
-   [Отправка запроса](#SendRequest) -отправляет toohello запроса указан URL-адрес.  

-   [Задайте прокси-сервер HTTP](#SetHttpProxy) -позволяет tooroute пересылать запросы через прокси-сервер HTTP.  

-   [Установка метода запроса](#SetRequestMethod) -позволяет toochange метод hello HTTP для запроса.  
  
-   [Задать код состояния](#SetStatus) -toohello код состояния hello HTTP изменения заданного значения.  
  
-   [Задание переменной](api-management-advanced-policies.md#set-variable) — сохраняет значение в именованной переменной [контекста](api-management-policy-expressions.md#ContextVariables) для последующего использования.  

-   [Трассировки](#Trace) -добавляет строку в hello [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) выходных данных.  
  
-   [Подождите](#Wait) -ожидает заключены [запрос на отправку](api-management-advanced-policies.md#SendRequest), [получить значение из кэша](api-management-caching-policies.md#GetFromCacheByKey), или [поток управления](api-management-advanced-policies.md#choose) toocomplete политики, прежде чем продолжить.  
  
##  <a name="choose"></a> Управление потоками  
 Hello `choose` политики применяются встраиваемые правила, операторы в зависимости от результата вычисления логических выражений, аналогичные tooan if-then-else или коммутатор hello конструкции в языке программирования.  
  
###  <a name="ChoosePolicyStatement"></a> Правило политики  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 Hello политика потока управления должен содержать по крайней мере один `<when/>` элемента. Hello `<otherwise/>` элемент является необязательным. Условия в `<when/>` элементы оцениваются в порядке их следования в политике hello. Правила политики, включенные в hello сначала `<when/>` элемент с атрибутом условия, равным `true` будут применены. Политики, заключенный в hello `<otherwise/>` элемент, если он имеется, будут применяться, если все из hello `<when/>` являются атрибуты условий для элемента `false`.  
  
### <a name="examples"></a>Примеры  
  
####  <a name="ChooseExample"></a> Пример  
 Hello ниже приведен пример [set-variable](api-management-advanced-policies.md#set-variable) политики и две политики потока управления.  
  
 политика задания переменной в Hello находится в разделе "Входящие" Здравствуйте и создает `isMobile` логическое [контекста](api-management-policy-expressions.md#ContextVariables) переменной, которая имеет значение tootrue, если hello `User-Agent` заголовок запроса содержит текст hello `iPad` или `iPhone`.  
  
 Первая политика потока управления Hello также находится в разделе "Входящие" Здравствуйте и определяет условное применение одной из двух [параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) политики в зависимости от значения hello hello `isMobile` переменной контекста.  
  
 Hello Вторая политика потока управления находится в разделе "Исходящие" hello и условно применяет hello [tooJSON преобразование XML](api-management-transformation-policies.md#ConvertXMLtoJSON) политики при `isMobile` задано слишком`true`.  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a>Пример  
 В этом примере показано, как tooperform фильтрация содержимого, удалив элементы данных из ответа hello получил от службы внутренних hello при использовании hello `Starter` продукта. Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too34:30 Перемотка вперед. Начинаются с 31:50 toosee Обзор [hello темной API прогноз Sky](https://developer.forecast.io/) для этой демонстрации.  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|choose|Корневой элемент.|Да|  
|when|Здравствуйте, toouse условие для hello `if` или `ifelse` части hello `choose` политики. Если hello `choose` политика содержит несколько `when` разделы, они вычисляются последовательно. Здравствуйте, один раз `condition` when элемент оценивается как слишком`true`, последующие `when` оценки условий.|Да|  
|otherwise|Содержит фрагмент toobe hello политики, используется, если ни один из hello `when` условия соблюдаются слишком`true`.|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|  
|---------------|-----------------|--------------|  
|condition="Логическое выражение &#124; Логическая константа"|Логическое выражение или константа tooevaluated при Здравствуйте, содержащий Hello `when` вычисляется правила политики.|Да|  
  
###  <a name="ChooseUsage"></a> Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  
  
##  <a name="ForwardRequest"></a> Перенаправляющий запрос  
 Hello `forward-request` политика направляет hello входящего запроса toohello серверной службе указанный в запросе hello [контекста](api-management-policy-expressions.md#ContextVariables). Hello URL-адрес внутренней службы задается в hello API [параметры](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) и может быть изменено с помощью hello [задать серверной службы](api-management-transformation-policies.md) политики.  
  
> [!NOTE]
>  Удаление результатов этой политики в запросе hello не направляются toohello серверной службы hello политики и в разделе "Исходящие" hello вычисляются сразу после успешного завершения hello политик hello в hello входящих раздела.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="example"></a>Пример  
 Hello следующую политику уровня API направляет все запросы toohello серверной службы с интервалом 60 секунд времени ожидания.  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Пример  
 Этот уровень политики операция использует hello `base` элемент tooinherit hello серверной политики из hello родительской API уровня области.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Пример  
 Эта политика уровня операции явным образом направляет все запросы toohello серверной службы с временем ожидания 120 и не наследует родительский hello API уровня политики.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Пример  
 Этот уровень политики операции не перенаправляет запросы toohello внутренней службы.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|forward-request|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|timeout="целое число"|Hello интервал времени ожидания в секундах перед сбоем hello вызовов toohello внутренней службы.|Нет|Время ожидания отсутствует|  
|follow-redirects="true &#124; false"|Указывает, следуют hello шлюза или возвращаемый вызывающий объект toohello перенаправлений с серверной службе hello.|Нет|нет|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** backend.  
  
-   **Области политики:** все области.  
  
##  <a name="LimitConcurrency"></a> Ограничение параллелизма  
 Hello `limit-concurrency` политика запрещает заключенными политики выполнения более чем hello заданного количества запросов в определенный момент времени. После превышения порогового значения hello, новые запросы добавляются tooa очереди, пока не удастся hello максимум длины очереди. Когда очередь заполнится, новые запросы немедленно завершатся ошибкой.
  
###  <a name="LimitConcurrencyStatement"></a> Правило политики  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>Примеры  
  
####  <a name="ChooseExample"></a> Пример  
 Hello следующем примере показано, как toolimit число запросов, пересылаемые tooa серверной части, на основе значения hello переменной контекста.
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|    
|limit-concurrency|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|--------------|  
|key|Строка. Допустимое выражение. Указывает область hello параллелизма. Используется несколькими политиками.|Да|Недоступно|  
|max-count|Целое число. Указывает максимальное число запросов, разрешенных политикой tooenter hello.|Да|Недоступно|  
|timeout|Целое число. Допустимое выражение. Указывает количество секунд, запрос будет ожидать tooenter области до появления в hello «403 слишком много запросов»|Нет|Infinity|  
|max-queue-length|Целое число. Допустимое выражение. Указывает hello максимум длины очереди. Входящие запросы попытки tooenter эта политика будет остановлен с «403 слишком много запросов» немедленно при исчерпании hello очереди.|Нет|Infinity|  
  
###  <a name="ChooseUsage"></a> Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  

##  <a name="log-to-eventhub"></a>Журнал tooEvent концентратора  
 Hello `log-to-eventhub` политики отправляет сообщения в hello указан формат tooan концентратора событий, определяемые сущности средства ведения журнала. Как и предполагает его имя, hello политика используется для сохранения выбранного запроса или ответа сведения о контексте для анализа сети или вне сети.  
  
> [!NOTE]
>  Пошаговое руководство по настройке концентратора событий и ведение журнала событий, в разделе [как события управления API toolog концентраторов событий Azure с](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>Пример  
 Любая строка может использоваться как toobe значение hello в концентраторы событий в журнал. В этом примере hello даты и времени, имя развертывания службы, код запроса, IP-адрес и имя операции для всех входящих звонков, средства ведения журнала зарегистрирована hello концентратора событий регистрируется toohello `contoso-logger` идентификатор.  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|log-to-eventhub|Корневой элемент. Hello значение этого элемента — концентратора событий tooyour toolog строку hello.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|  
|---------------|-----------------|--------------|  
|logger-id|Идентификатор Hello hello средства ведения журнала зарегистрированные в службе управления API.|Да|  
|partition-id|Указывает индекс hello hello раздела, куда должны отправляться сообщения.|необязательный параметр. Этот атрибут не может использоваться, если используется `partition-key`.|  
|partition-key|Задает значение hello, используемое для назначения раздела при отправке сообщений.|необязательный параметр. Этот атрибут не может использоваться, если используется `partition-id`.|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  

##  <a name="mock-response"></a> Макетирование ответа  
Hello `mock-response`, как имя hello подразумевает, — использовать toomock интерфейсы API и операции. Он прерывает выполнение обычный конвейер и возвращает вызывающему объекту toohello макеты ответа. политика Hello всегда пытается tooreturn отклики наилучшее качество. При возможности, она предпочитает примеры содержимого ответа. Она создает примеры ответов из схем, если схемы указаны, а примеры — нет. Если не найдены ни примеры, ни схемы, возвращаются ответы без содержимого.
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>Примеры  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|mock-response|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|--------------|  
|status-code|Указывает код состояния ответа и соответствующий пример используется tooselect или схемы.|Нет|200|  
|content-type|Указывает `Content-Type` значение заголовка ответа и соответствующий пример используется tooselect или схемы.|Нет|None|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, on-error.  
  
-   **Области политики:** все области.

##  <a name="Retry"></a> Повтор  
 Hello `retry` политики один раз выполняет свои дочерние политики, а затем повторяет их выполнение до попытки hello `condition` становится `false` или повторите `count` израсходована.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a>Пример  
 Копирование tooten раз, используя алгоритм повторения экспоненциального следующий пример запроса forewarding повторяется в hello. Поскольку `first-fast-retry` задано toofalse, все повторных попыток, алгоритм повторного exponsntial toohello субъекта.  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|retry|Корневой элемент. Может содержать любые другие политики в качестве дочерних элементов.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|condition|Логический литерал или [выражение](api-management-policy-expressions.md), указывающее, что нужно сделать: прекратить повторные попытки (`false`) или продолжить (`true`).|Да|Недоступно|  
|count|Положительное число, указывающее максимальное число повторных попыток tooattempt hello.|Да|Недоступно|  
|interval|Положительное число, в секундах, указав hello интервал ожидания между попытками повтора hello.|Да|Недоступно|  
|max-interval|Положительное число, в секундах, указав hello интервал ожидания между попытками повтора hello. Это используется tooimplement алгоритм экспоненциального повторных попыток.|Нет|Недоступно|  
|delta|Положительное число, в секундах, указав приращения интервал ожидания hello. Это алгоритмы линейной и экспоненциальный повторных попыток используется tooimplement hello.|Нет|Недоступно|  
|first-fast-retry|Если задать слишком `true` , первой попытки повтора hello вступает в силу немедленно.|Нет|`false`|  
  
> [!NOTE]
>  Если только hello `interval` указано, **фиксированной** выполняются интервал повторных попыток.  
>  Если только hello `interval` и `delta` указаны, **линейной** используется алгоритм интервал повторения, где время ожидания между повторными попытками вычисляемые соответствующим hello следующую формулу - `interval + (count - 1)*delta`.  
>  Здравствуйте, когда `interval`, `max-interval` и `delta` указаны, **экспоненциального** применяется алгоритм интервал повторения, где hello время ожидания между повторными попытками hello растут по экспоненте значению hello `interval`значение toohello `max-interval` toohello ниже в соответствии с forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) . Обратите внимание, что эта политика наследует ограничения использования дочерних политик.  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  
  
##  <a name="ReturnResponse"></a> Возврат ответа  
 Hello `return-response` политики прерывает выполнение конвейера и возвращает пользовательский ответ toohello вызывающего или по умолчанию. По умолчанию возвращается код `200 OK` без текста. Можно указать настраиваемый ответ с помощью переменной контекста или правил политики. Если указаны оба hello содержащихся в переменной контекста hello изменении ответа посредством инструкции политики hello перед возвращением toohello вызывающего объекта.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|return-response|Корневой элемент.|Да|  
|set-header|Правило политики [set-header](api-management-transformation-policies.md#SetHTTPheader).|Нет|  
|set-body|Правило политики [set-body](api-management-transformation-policies.md#SetBody).|Нет|  
|set-status|Правило политики [set-status](api-management-advanced-policies.md#SetStatus).|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|  
|---------------|-----------------|--------------|  
|response-variable-name|Hello переменной контекста hello ссылка на имя, например, вышестоящим [запрос на отправку](api-management-advanced-policies.md#SendRequest) политики и содержащий `Response` объекта|необязательный параметр.|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  
  
##  <a name="SendOneWayRequest"></a> Отправка одностороннего запроса  
 Hello `send-one-way-request` политики отправляет hello предоставленный toohello URL-адрес указан без ожидания ответа.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>Пример  
 Эта политика образец показывает пример использования hello `send-one-way-request` toosend политики сообщение tooa резерв чата Если hello код ответа HTTP больше или равно too500. Дополнительные сведения об этом образце см. в разделе [с помощью внешних служб из hello службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|send-one-way-request|Корневой элемент.|Да|  
|url|URL-адрес Hello hello запроса.|Нет, если mode=copy. В противном случае да.|  
|метод|Здравствуйте, метод HTTP для запроса hello.|Нет, если mode=copy. В противном случае да.|  
|Верхний колонтитул|Заголовок запроса. Используйте несколько элементов заголовка для нескольких заголовков запросов.|Нет|  
|текст|текст запроса Hello.|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|mode="строка"|Определяет, является ли новый запрос или копию hello текущего запроса. В режиме исходящие режим = копирования не инициализирует hello текст запроса.|Нет|Создать|  
|name|Указывает имя набора toobe заголовок hello hello.|Да|Недоступно|  
|exists-action|Задает tootake какие действия при hello заголовок уже задан. Этот атрибут должен иметь одно из последующих значений hello.<br /><br /> -Переопределите - значение hello заменяет существующий заголовок hello.<br />-skip — не заменяет существующее значение заголовка hello.<br />-Добавить - добавляет значение существующего заголовка hello значение toohello.<br />-delete — удаляет hello заголовок из запроса hello.<br /><br /> Если задано слишком`override` перечислении нескольких записей с hello одинаковые имена, результаты в заголовке hello, соответствующим tooall записей о наборах (которые будут указаны несколько раз); в результате hello устанавливается только значения из списка.|Нет|override|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  
  
##  <a name="SendRequest"></a> Отправка запроса  
 Hello `send-request` политики отправляет toohello указан URL-адрес, больше не ожидания не hello задавать значение времени ожидания запроса указано hello.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>Пример  
 Этот пример одним из способов tooverify маркер ссылки с сервера авторизации. Дополнительные сведения об этом образце см. в разделе [с помощью внешних служб из hello службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|send-request|Корневой элемент.|Да|  
|url|URL-адрес Hello hello запроса.|Нет, если mode=copy. В противном случае да.|  
|метод|Здравствуйте, метод HTTP для запроса hello.|Нет, если mode=copy. В противном случае да.|  
|Верхний колонтитул|Заголовок запроса. Используйте несколько элементов заголовка для нескольких заголовков запросов.|Нет|  
|текст|текст запроса Hello.|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|mode="строка"|Определяет, является ли новый запрос или копию hello текущего запроса. В режиме исходящие режим = копирования не инициализирует hello текст запроса.|Нет|Создать|  
|response-variable-name="строка"|Если не указано, используется `context.Response`.|Нет|Недоступно|  
|timeout="целое число"|Hello интервал времени ожидания в секундах перед вызовом hello toohello URL-адрес завершается ошибкой.|Нет|60|  
|ignore-error|Если значение true, а hello запрос приведет к ошибке:<br /><br /> если response-variable-name указано, он будет содержать значение null;<br />если response-variable-name не указано, контекст запроса не будет обновлен.|Нет|нет|  
|name|Указывает имя набора toobe заголовок hello hello.|Да|Недоступно|  
|exists-action|Задает tootake какие действия при hello заголовок уже задан. Этот атрибут должен иметь одно из последующих значений hello.<br /><br /> -Переопределите - значение hello заменяет существующий заголовок hello.<br />-skip — не заменяет существующее значение заголовка hello.<br />-Добавить - добавляет значение существующего заголовка hello значение toohello.<br />-delete — удаляет hello заголовок из запроса hello.<br /><br /> Если задано слишком`override` перечислении нескольких записей с hello одинаковые имена, результаты в заголовке hello, соответствующим tooall записей о наборах (которые будут указаны несколько раз); в результате hello устанавливается только значения из списка.|Нет|override|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  
  
##  <a name="SetHttpProxy"></a> Установка прокси-сервера HTTP  
 Hello `proxy` политика позволяет tooroute toobackends пересылки запросов через прокси-сервер HTTP. Между шлюзом hello и прокси-сервера hello поддерживается только HTTP (не HTTPS). Используются только базовая проверка подлинности и проверка подлинности NTLM.
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>Пример  
Обратите внимание на использование hello [свойства](api-management-howto-properties.md) как значения hello имя пользователя и пароль tooavoid, хранение конфиденциальных сведений в документе политики hello.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|proxy|Корневой элемент|Да|  

### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|url="string"|URL-адрес прокси-сервера в виде hello. http://Host: Port.|Да|Недоступно|  
|username="string"|Toobe имя пользователя, используемый для проверки подлинности с прокси-сервером hello.|Нет|Недоступно|  
|password="string"|Toobe пароль, используемый для проверки подлинности с прокси-сервером hello.|Нет|Недоступно|  

### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** все области.  

##  <a name="SetRequestMethod"></a> Задание метода запроса  
 Hello `set-method` политика позволяет toochange метод запроса hello HTTP для запроса.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>Пример  
 Пример политики, которая использует hello `set-method` политики показан пример отправки сообщения tooa резерв чата, если hello код ответа HTTP больше или равно too500. Дополнительные сведения об этом образце см. в разделе [с помощью внешних служб из hello службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|set-method|Корневой элемент. значение Hello элемента hello задает метод HTTP hello.|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, on-error.  
  
-   **Области политики:** все области.  
  
##  <a name="SetStatus"></a> Задание кода состояния  
 Hello `set-status` политики наборов hello HTTP состояние кода toohello заданное значение.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>Пример  
 В этом примере показано, как tooreturn ответ 401, если маркер авторизации hello является недопустимым. Дополнительные сведения см. в разделе [с помощью внешних служб из hello службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|set-status|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|code="целое число"|tooreturn код состояния Hello HTTP.|Да|Недоступно|  
|reason="строка"|Описание hello причину для возврата hello код состояния.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** outbound, backend, on-error.  
  
-   **Области политики:** все области.  

##  <a name="set-variable"></a> Задание переменной  
 Hello `set-variable` объявляет политики [контекста](api-management-policy-expressions.md#ContextVariables) переменной и присвоение ей значения, указанного с помощью [выражение](api-management-policy-expressions.md) или строковым литералом. Если hello выражение содержит литерал, он будет преобразован тип string и hello tooa hello значения будет `System.String`.  
  
###  <a name="set-variablePolicyStatement"></a> Правило политики  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a> Пример  
 Hello ниже приведен пример политика задания переменной в hello входящих раздела. Эта политика задания переменной создает `isMobile` логическое [контекста](api-management-policy-expressions.md#ContextVariables) переменной, которая имеет значение tootrue, если hello `User-Agent` заголовок запроса содержит текст hello `iPad` или `iPhone`.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|set-variable|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|  
|---------------|-----------------|--------------|  
|name|Имя переменной hello Hello.|Да|  
|value|значение переменной hello Hello. Это может быть выражение или литеральное значение.|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  
  
###  <a name="set-variableAllowedTypes"></a> Допустимые типы  
 Выражения, используемые в hello `set-variable` политики должен возвращать hello следующие базовые типы.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a> Трассировка  
 Hello `trace` политики добавляет строку в hello [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) выходных данных. Hello политики будет выполняться только если трассировка инициируется, т. е. `Ocp-Apim-Trace` заголовок запроса представить и задать слишком`true` и `Ocp-Apim-Subscription-Key` заголовок запроса присутствует и имеет допустимый ключ, связанный с учетной записью администратора hello.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|trace|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|источник|Строка литерала может применяться toohello trace viewer и указав источник приветственное сообщение hello.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** все области.  
  
##  <a name="Wait"></a> Ожидание  
 Hello `wait` политики выполняет его непосредственных дочерних политик в параллельном режиме и ожидает либо все, либо один из его непосредственных дочерних политик toocomplete, до ее завершения. Hello политики ожидания могут иметь в качестве его непосредственных дочерних политик [запрос на отправку](api-management-advanced-policies.md#SendRequest), [получить значение из кэша](api-management-caching-policies.md#GetFromCacheByKey), и [поток управления](api-management-advanced-policies.md#choose) политики.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>Пример  
 В следующий пример hello есть два `choose` политик в качестве непосредственных дочерних политики hello `wait` политики. Каждая из этих политик `choose` выполняется в параллельном режиме. Каждый `choose` политики пытается tooretrieve кэшированное значение. В случае пропуска кэша серверная служба называется значением tooprovide hello. В этом примере hello `wait` политики для завершения всех ее непосредственных дочерних политик завершить, так как hello `for` атрибута задано слишком`all`.   В этот примере hello контекста переменных (`execute-branch-one`, `value-one`, `execute-branch-two`, и `value-two`) объявлены вне области hello этот пример политики.  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|wait|Корневой элемент. Может содержать в качестве дочерних элементов только политики `send-request`, `cache-lookup-value` и `choose`.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|for|Определяет, является ли hello `wait` политики ожидает все toobe политики непосредственных дочерних завершена или только один. Допустимые значения:<br /><br /> -   `all`-ожидания для всех toocomplete непосредственных дочерних политик<br />-любое - ожидания любой toocomplete политики непосредственных дочерних. После завершения первой политики непосредственных дочерних hello hello `wait` политики завершается, и любые другие политики непосредственных дочерних выполнение завершается.|Нет|все|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend.  
  
-   **Области политики:** все области.  
  
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в следующих статьях:
-   [Политики в управлении API](api-management-howto-policies.md) 
-   [Выражения политики](api-management-policy-expressions.md)
