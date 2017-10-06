---
title: "политики преобразования при управлении API aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о политиках hello преобразования, доступные для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a>Политики преобразования службы управления API
Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a> Политики преобразования  
  
-   [Преобразование JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - преобразует запрос или текст ответа от JSON tooXML.  
  
-   [Преобразование XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - преобразует запрос, или из XML tooJSON текст ответа.  
  
-   [Поиск и замена строки в тексте](api-management-transformation-policies.md#Findandreplacestringinbody) – отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.  
  
-   [Маскировать URL-адреса в содержимом](api-management-transformation-policies.md#MaskURLSContent) -загрузочную запись (маскировка) ссылок в ответ hello текста, чтобы они указывали toohello равнозначными ссылками через шлюз hello.  
  
-   [Задать серверной службе](api-management-transformation-policies.md#SetBackendService) -изменяет hello серверную службу для входящего запроса.  
  
-   [Задайте текст](api-management-transformation-policies.md#SetBody) -задает текст сообщения hello для входящих и исходящих запросов.  
  
-   [Задание заголовка HTTP](api-management-transformation-policies.md#SetHTTPheader) - назначает значение tooan существующего ответа и/или заголовка запроса или Добавление нового заголовка ответа и/или запроса.  
  
-   [Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) - добавляет, заменяет значение или удаляет параметр строки запроса.  
  
-   [Замена URL-адреса](api-management-transformation-policies.md#RewriteURL) -преобразование URL-АДРЕСЕ запроса из общеупотребительной формы формы toohello ожидаемый hello веб-службы.  
  
-   [Преобразования XML с помощью XSLT](api-management-transformation-policies.md#XSLTransform) -применяется tooXML преобразование XSL в тексте запроса или ответа hello.  
  
##  <a name="ConvertJSONtoXML"></a>Преобразовать JSON tooXML  
 Hello `json-to-xml` политики преобразует тело запроса или ответа из JSON tooXML.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|json-to-xml|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|apply|Hello атрибут должен быть задан tooone из hello следующие значения.<br /><br /> always — всегда применять преобразование;<br />content-type-json — преобразовать только в том случае, если в заголовке ответа Content-Type указано наличие формата JSON.|Да|Недоступно|  
|consider-accept-header|Hello атрибут должен быть задан tooone из hello следующие значения.<br /><br /> true — применять преобразование, только если JSON запрашивается в заголовке запроса Accept;<br />false — всегда применять преобразование.|Нет|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, on-error.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="ConvertXMLtoJSON"></a>Преобразование XML tooJSON  
 Hello `xml-to-json` политики преобразует тело запроса или ответа из XML tooJSON. Эта политика может быть используется toomodernize API-интерфейсов на основании XML-только для внутренних веб-служб.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|xml-to-json|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|kind|Hello атрибут должен быть задан tooone из hello следующие значения.<br /><br /> -javascript friendly: hello преобразовать JSON имеет понятное tooJavaScript разработчиков формы.<br />-direct: hello преобразованный JSON отражает структуру hello исходного документа XML.|Да|Недоступно|  
|apply|Hello атрибут должен быть задан tooone из hello следующие значения.<br /><br /> always — всегда применять преобразование;<br />content-type-xml — преобразовать только в том случае, если в заголовке ответа Content-Type указано наличие формата XML.|Да|Недоступно|  
|consider-accept-header|Hello атрибут должен быть задан tooone из hello следующие значения.<br /><br /> true — применять преобразование, только если XML запрашивается в заголовке запроса Accept;<br />false — всегда применять преобразование.|Нет|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, on-error.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="Findandreplacestringinbody"></a> Поиск и замена строки в тексте  
 Hello `find-and-replace` политики поиск подстроки запроса или ответа и ее замена другой подстрокой.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|find-and-replace|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|from|toosearch строка Hello для.|Да|Недоступно|  
|значение|Строка замены Hello. Укажите строку нулевой длины замены строки tooremove hello поиска.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="MaskURLSContent"></a> Маскировка URL-адресов в содержимом  
 Hello `redirect-content-urls` политики загрузочную запись (маскировка) ссылок в тексте hello, чтобы они указывали toohello равнозначными ссылками через шлюз hello. Используйте в hello разделе "Исходящие" toore записи ответа текст ссылки toomake их toohello точки шлюза. Используйте в hello входящих раздел для получения противоположного результата.  
  
> [!NOTE]
>  Эта политика не изменяет значения заголовка, например заголовка `Location`. значения заголовка toochange, использовать hello [заголовка набора](api-management-transformation-policies.md#SetHTTPheader) политики.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|redirect-content-urls|Корневой элемент.|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetBackendService"></a> Задание внутренней службы  
 Используйте hello `set-backend-service` tooredirect политики входящее сообщение запроса другой внутренней tooa чем hello от указанного в параметрах hello API для этой операции. Этот параметр изменяет hello серверной службы базовый URL-адрес входящего запроса toohello hello, указанному в политике hello.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
В этом примере hello политика задания внутренней службы направляет запросы на основе значения версии hello, переданный hello запроса строки tooa другой внутренней службе чем hello один hello, указанный в API.
  
Изначально hello базовый URL-адрес внутренней службы является производным от параметров API hello. Здравствуйте, поэтому URL-адрес запроса `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` становится `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` где `http://contoso.com/api/10.4/` является hello внутренний URL-адрес службы указан в настройках hello API.  
  
Здравствуйте, когда [< выберите\> ](api-management-advanced-policies.md#choose) применяется инструкция политики hello серверной базовый URL-адрес службы может снова измениться слишком`http://contoso.com/api/8.2` или `http://contoso.com/api/9.1`, в зависимости от hello значение параметра запроса hello версии запроса. Например, если hello значение — `"2013-15"` hello последний запрос URL-адрес становится `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Если дальнейшее преобразование запроса hello не нужное, другие [политик преобразования](api-management-transformation-policies.md#TransformationPolicies) может использоваться. Например, tooremove hello версии запроса параметр теперь, когда hello запрос выполняется маршрутизация tooa версии конкретной серверной части, hello [параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) политики можно использовать tooremove hello параметре.  
  
### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
В этот примере hello политики маршруты hello запроса tooa службы структуры серверное приложение используя строку запроса userId hello в качестве ключа секции hello и hello основной реплики раздела hello.  

### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|set-backend-service|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|base-url|Новый базовый URL-адрес внутренней службы.|Нет|Недоступно|  
|backend-id|Идентификатор hello tooroute серверной части для.|Нет|Недоступно|  
|sf-partition-key|Применимо только для внутреннего hello — это служба Service Fabric и задается с помощью «идентификатор серверной». Использовать tooresolve определенный раздел из hello службы разрешения имен.|Нет|Недоступно|  
|sf-replica-type|Применимо только для внутреннего hello — это служба Service Fabric и задается с помощью «идентификатор серверной». Элементы управления, если запрос hello должен составлять toohello первичной или вторичной реплики секции. |Нет|Недоступно|    
|sf-resolve-condition|Применимо только для внутреннего hello — это служба Service Fabric. Определение условия hello вызовите tooService структуры внутренних наличия toobe, повторяющимся в новое решение.|Нет|Недоступно|    
|sf-service-instance-name|Применимо только для внутреннего hello — это служба Service Fabric. Позволяет toochange экземплярами служб во время выполнения. |Нет|Недоступно|    

### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, backend.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetBody"></a> Задание текста  
 Используйте hello `set-body` текст сообщения hello tooset политики для входящих и исходящих запросов. tooaccess hello тело сообщения можно использовать hello `context.Request.Body` свойства или hello `context.Response.Body`в зависимости от того, является ли политика hello в hello раздел входящих или исходящих подключений.  
  
> [!IMPORTANT]
>  Обратите внимание, что по умолчанию при доступе к hello тела сообщения с помощью `context.Request.Body` или `context.Response.Body`, исходное сообщение hello текст будет потерян, а также необходимо задать, возвращая текст hello обратно в выражении hello. текст hello toopreserve содержимого, задайте hello `preserveContent` параметр слишком`true` при доступе к приветственное сообщение. Если `preserveContent` задано слишком`true` и другой текст возвращается оператором выражения hello hello используется текст.  
>   
>  Имейте в виду следующие рекомендации при использовании hello hello `set-body` политики.  
>   
>  -   Если вы используете hello `set-body` tooreturn политики новый или обновленный текст, не требуется tooset `preserveContent` слишком`true` так, как вы явно указали hello новое содержимое тела.  
> -   Сохранение hello содержимого ответа в конвейер входящих hello не имеет смысла, так как еще нет ответа.  
> -   Сохранение содержимого hello запроса в конвейер исходящих hello не имеет смысла, так как hello запрос уже был отправлен toohello базы данных на этом этапе.  
> -   Если эта политика используется при отсутствии текста сообщения, например во входящем параметре GET, возникает исключение.  
  
 Дополнительные сведения см. в разделе hello `context.Request.Body`, `context.Response.Body`и hello `IMessage` подразделы hello [переменной контекста](api-management-policy-expressions.md#ContextVariables) таблицы.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="literal-text-example"></a>Пример литерального текста  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>Пример, доступ к телу hello в виде строки. Обратите внимание что мы сохранение hello исходный текст запроса, можно обратиться к его позже в конвейере hello.
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Пример, доступ к телу hello как JObject. Обратите внимание, что так как мы не резервировании hello исходного текста запроса, доступ к его позже в конвейере hello будет приведет к исключению.  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a>Фильтрация ответа в зависимости от продукта  
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

### <a name="using-liquid-templates-with-set-body"></a>Использование шаблонов Liquid с политикой set-body 
Hello `set-body` политики может быть hello настроенных toouse [жидкости](https://shopify.github.io/liquid/basics/introduction/) шаблонов языка tootransfom hello тело запроса или ответа. Это может быть очень эффективны, если вам требуется toocompletely изменения формы hello формат сообщения.

> [!IMPORTANT]
> Здравствуйте, реализация жидкости, используемых в hello `set-body` политика настроена в «режиме C#». Это особенно важно при выполнении действий, таких как фильтрация. Например, с помощью фильтра даты требует использования hello Pascal регистр и C# даты, например форматирования:
>
> {{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> В порядке toocorrectly привязки tooan текст XML с помощью шаблона жидкости hello, используйте `set-header` tooset Content-Type tooeither политики приложения/xml, text/xml (или любой тип, заканчивая + xml); для текст JSON, она должна иметь приложение/json, текста и json (или любой тип конца с + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>Преобразование с помощью шаблона жидкости tooSOAP JSON
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a>Преобразование JSON с помощью шаблона Liquid
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|set-body|Корневой элемент. Содержит текст hello или выражения, которые возвращает текст.|Да|  

### <a name="properties"></a>Свойства  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|шаблон|Используется toochange hello шаблонов режим, задать политику текст hello будет выполняться в. В настоящее время является hello поддерживается только значение:<br /><br />политика текст hello - жидкости - задания будет использовать модуль жидкости шаблонов hello |Нет|liquid|  

Для доступа к сведениям о hello запроса и ответа, hello жидкости шаблона можно привязать объект контекста tooa с hello следующие свойства: <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetHTTPheader"></a> Установка HTTP-заголовка  
 Hello `set-header` политики присваивает значение tooan существующего ответа и/или заголовка запроса или Добавление нового заголовка ответа и/или запроса.  
  
 Вставляет список HTTP-заголовков в HTTP-сообщение. При помещении в конвейер входящих сообщений эта политика задает hello заголовки HTTP для запроса hello, передаваемые toohello целевой службы. При помещении в конвейер исходящих сообщений эта политика задает hello заголовки HTTP для отправляемого клиент шлюза toohello hello ответа.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="example"></a>Пример  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Контекст сведения toohello серверная служба пересылки  
 В этом примере показано, как политика tooapply на hello API уровня toosupply контекста сведения toohello серверной службы. Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too10:30 Перемотка вперед. В 12:10 отсутствует Демонстрация вызова операции на портале разработчиков hello, где можно просмотреть политики hello на работе.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|set-header|Корневой элемент.|Да|  
|value|Указывает значение hello hello заголовок toobe набора. Для нескольких заголовков с hello таким же именем, добавьте дополнительные `value` элементов.|Да|  
  
### <a name="properties"></a>Свойства  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|exists-action|Задает tootake какие действия при hello заголовок уже задан. Этот атрибут должен иметь одно из последующих значений hello.<br /><br /> -Переопределите - значение hello заменяет существующий заголовок hello.<br />-skip — не заменяет существующее значение заголовка hello.<br />-Добавить - добавляет значение существующего заголовка hello значение toohello.<br />-delete — удаляет hello заголовок из запроса hello.<br /><br /> Если задано слишком`override` перечислении нескольких записей с hello одинаковые имена, результаты в заголовке hello, соответствующим tooall записей о наборах (которые будут указаны несколько раз); в результате hello устанавливается только значения из списка.|Нет|override|  
|name|Указывает имя набора toobe заголовок hello.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetQueryStringParameter"></a> Настройка параметра строки запроса  
 Hello `set-query-parameter` добавляет политики, заменяет значение, или удаляет запрос параметра строки запроса. Можно использовать toopass параметров запроса, ожидаемый hello серверной службы, которые являются необязательными, или никогда не присутствуют в запросе hello.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="example"></a>Пример  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Контекст сведения toohello серверная служба пересылки  
 В этом примере показано, как политика tooapply на hello API уровня toosupply контекста сведения toohello серверной службы. Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too10:30 Перемотка вперед. В 12:10 отсутствует Демонстрация вызова операции на портале разработчиков hello, где можно просмотреть политики hello на работе.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|set-query-parameter|Корневой элемент.|Да|  
|value|Указывает значение hello объекта набора toobe параметров запроса hello. Несколько параметров запроса с hello таким же именем, добавьте дополнительные `value` элементов.|Да|  
  
### <a name="properties"></a>Свойства  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|exists-action|Указывает tootake какие действия, если уже задан параметр запроса hello. Этот атрибут должен иметь одно из последующих значений hello.<br /><br /> -Переопределите - hello заменяет значение существующего параметра hello.<br />-skip — не заменяет hello значение существующего параметра запроса.<br />-Добавить - добавляет hello значение toohello значение существующего параметра запроса.<br />-delete — удаляет параметр запроса hello из запроса hello.<br /><br /> Если задано слишком`override` перечислении нескольких записей с hello одинаковые имена, результаты в параметр запроса hello, соответствующим tooall записей о наборах (которые будут указаны несколько раз); в результате hello устанавливается только значения из списка.|Нет|override|  
|name|Указывает имя набора toobe параметр запроса hello.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, backend.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="RewriteURL"></a> Перезапись URL-адреса  
 Hello `rewrite-uri` политики преобразование URL-АДРЕСЕ запроса из формы toohello общей формы ожидаемый hello веб-службы, как показано в следующий пример hello.  
  
-   Открытый URL — `http://api.example.com/storenumber/ordernumber`.  
  
-   URL-адрес запроса — `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`.  
  
 Эта политика может использоваться, когда отдела или со средствами браузера URL-адрес необходимо преобразовать в формат URL-адрес hello, ожидаемый hello веб-службы. Этот параметр требуется только при представлении альтернативный формат URL-адрес, например чистой URL-адреса, RESTful URL-адреса, удобный для восприятия человеком или Оптимизированных для поисковых систем URL-адресов, которые являются исключительно структурными URL-адреса, которые не содержат строку запроса, а состоят только hello путь hello toobe ресурс (после hello схемы и hello полномочий). Это часто делает в эстетических целях, для удобства и простоты использования или для оптимизации поисковых систем (SEO).  
  
> [!NOTE]
>  Можно добавлять только параметры строки запроса с помощью политики hello. Вы не может добавить дополнительные параметры шаблона пути в hello замена URL-адреса.  

### <a name="policy-statement"></a>Правило политики  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|rewrite-uri|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|Обязательно|значение по умолчанию|  
|---------------|-----------------|--------------|-------------|  
|шаблон|Hello фактический URL-адресу с все параметры строки запроса. При использовании выражений, hello всего значения должен быть выражением.|Да|Недоступно|  
|copy-unmatched-params|Указывает параметры запроса в hello входящего запроса не присутствует в hello исходного URL-адрес шаблона, добавляются ли URL-адрес toohello определяется hello обновленной версии шаблона|Нет|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** product, API, operation.  
  
##  <a name="XSLTransform"></a> Преобразование XML с помощью XSLT  
 Hello `Transform XML using an XSLT` tooXML преобразование XSL в тексте запроса или ответа hello применяется политика.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|xsl-transform|Корневой элемент.|Да|  
|Параметр|Используется toodefine переменные, используемые в преобразовании hello|Нет|  
|xsl:stylesheet|Корневой элемент таблицы стилей. Все элементы и атрибуты, определенные в стандарту hello [спецификацию XSLT](http://www.w3.org/TR/xslt)|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound.  
  
-   **Области политики:** global, product, API, operation.  
  
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  
