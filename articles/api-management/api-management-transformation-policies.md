---
title: "Политики преобразования службы управления API Azure | Документация Майкрософт"
description: "Сведения о политиках преобразования, доступных для использования в службе управления API Azure."
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
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a>Политики преобразования службы управления API
В этой статье рассматриваются приведенные ниже политики управления API. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a> Политики преобразования  
  
-   [Преобразование JSON в XML](api-management-transformation-policies.md#ConvertJSONtoXML) – преобразует текст запроса или ответа в формате JSON в формат XML.  
  
-   [Преобразование XML в JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) – преобразует текст запроса или ответа в формате XML в формат JSON.  
  
-   [Поиск и замена строки в тексте](api-management-transformation-policies.md#Findandreplacestringinbody) – отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.  
  
-   [Маскировка URL-адресов в содержимом](api-management-transformation-policies.md#MaskURLSContent) — перезаписывает (маскирует) ссылки в тексте ответа так, чтобы каждая из них указывала на эквивалентную ссылку через шлюз.  
  
-   [Задание внутренней службы](api-management-transformation-policies.md#SetBackendService) – изменяет внутреннюю службу для входящего запроса.  
  
-   [Задание текста](api-management-transformation-policies.md#SetBody) – задает текст сообщения для входящих и исходящих запросов.  
  
-   [Установка HTTP-заголовка](api-management-transformation-policies.md#SetHTTPheader) -– назначает значение существующему заголовку ответа и/или запроса или добавляет новый заголовок ответа и/или запроса.  
  
-   [Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) - добавляет, заменяет значение или удаляет параметр строки запроса.  
  
-   [Перезапись URL-адреса](api-management-transformation-policies.md#RewriteURL) – преобразует URL-адрес запроса из его общедоступной формы в форму, ожидаемую веб-службой.  
  
-   [Преобразование XML с помощью XSLT](api-management-transformation-policies.md#XSLTransform) — применяет преобразование данных в формате XSL в формат XML в тексте запроса или ответа.  
  
##  <a name="ConvertJSONtoXML"></a> Преобразование JSON в XML  
 Политика `json-to-xml` преобразует текст запроса или ответа в формате JSON в формат XML.  
  
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
|apply|Для атрибута нужно задать одно из следующих значений:<br /><br /> always — всегда применять преобразование;<br />content-type-json — преобразовать только в том случае, если в заголовке ответа Content-Type указано наличие формата JSON.|Да|Недоступно|  
|consider-accept-header|Для атрибута нужно задать одно из следующих значений:<br /><br /> true — применять преобразование, только если JSON запрашивается в заголовке запроса Accept;<br />false — всегда применять преобразование.|Нет|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, on-error.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="ConvertXMLtoJSON"></a> Преобразование XML в JSON  
 Политика `xml-to-json` преобразует текст запроса или ответа в формате XML в формат JSON. Эту политику можно использовать для модернизации интерфейсов API, основанных на серверных веб-службах (только XML).  
  
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
|kind|Для атрибута нужно задать одно из следующих значений:<br /><br /> javascript-friendly — преобразованный JSON имеет форму, понятную разработчикам JavaScript;<br />direct — преобразованный JSON отражает структуру исходного XML-документа.|Да|Недоступно|  
|apply|Для атрибута нужно задать одно из следующих значений:<br /><br /> always — всегда применять преобразование;<br />content-type-xml — преобразовать только в том случае, если в заголовке ответа Content-Type указано наличие формата XML.|Да|Недоступно|  
|consider-accept-header|Для атрибута нужно задать одно из следующих значений:<br /><br /> true — применять преобразование, только если XML запрашивается в заголовке запроса Accept;<br />false — всегда применять преобразование.|Нет|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, on-error.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="Findandreplacestringinbody"></a> Поиск и замена строки в тексте  
 Политика `find-and-replace` отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
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
|from|Строка, которую нужно найти.|Да|Недоступно|  
|значение|Строка замены. Укажите строку замены с нулевой длиной для удаления строки поиска.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="MaskURLSContent"></a> Маскировка URL-адресов в содержимом  
 Политика `redirect-content-urls` перезаписывает (маскирует) ссылки в тексте ответа так, чтобы каждая из них указывала на эквивалентную ссылку через шлюз. Используйте в разделе outbound, чтобы перезаписать ссылки текста ответа так, чтобы они указывали на шлюз. Используйте в разделе inbound для обратного эффекта.  
  
> [!NOTE]
>  Эта политика не изменяет значения заголовка, например заголовка `Location`. Чтобы изменить значения заголовка, используйте политику [set-header](api-management-transformation-policies.md#SetHTTPheader).  
  
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
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetBackendService"></a> Задание внутренней службы  
 Используйте политику `set-backend-service` для перенаправления входящего запроса во внутреннюю службу, отличную от указанной в параметрах API для этой операции. Эта политика изменяет базовый URL-адрес внутренней службы входящего запроса на URL-адрес, указанный в политике.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
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
В этом примере политика задания внутренней службы направляет запросы на основе значения версии, переданного в строке запроса во внутреннюю службу, отличную от указанной в API.
  
Изначально базовый URL-адрес внутренней службы является производным от параметров API. Поэтому URL-адрес запроса `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` становится `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef`, где `http://contoso.com/api/10.4/` — URL-адрес внутренней службы, указанной в параметрах API.  
  
Когда применяется правило политики [<choose\>](api-management-advanced-policies.md#choose), базовый URL-адрес внутренней службы может снова измениться на `http://contoso.com/api/8.2` или `http://contoso.com/api/9.1` в зависимости от значения параметра запроса версии. Например, если значение — `"2013-15"`, URL-адрес последнего запроса становится `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Если требуются дополнительные преобразования запроса, можно воспользоваться другими [политиками преобразования](api-management-transformation-policies.md#TransformationPolicies). Например, чтобы удалить параметр запроса версии после направления запроса в конкретную серверную часть версии, для удаления атрибута избыточной версии можно использовать политику [Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter).  
  
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
В этом примере политика направляет запрос к внутренней службе Service Fabric, используя строку запроса userId в качестве ключа секции и используя первичную реплику секции.  

### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|set-backend-service|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|base-url|Новый базовый URL-адрес внутренней службы.|Нет|Недоступно|  
|backend-id|Идентификатор серверной части для перенаправления.|Нет|Недоступно|  
|sf-partition-key|Применяется только, когда серверной частью является служба Service Fabric и она задана с помощью атрибута backend-id. Используется для разрешения определенной секции в имени службы разрешения имен.|Нет|Недоступно|  
|sf-replica-type|Применяется только, когда серверной частью является служба Service Fabric и она задана с помощью атрибута backend-id. Контролирует, куда должен отправляться запрос: в первичную или вторичную реплику секции. |Нет|Недоступно|    
|sf-resolve-condition|Применяется только, когда серверной частью является служба Service Fabric. Условие, определяющее, необходимо ли повторить вызов к серверной части Service Fabric с новым разрешением.|Нет|Недоступно|    
|sf-service-instance-name|Применяется только, когда серверной частью является служба Service Fabric. Разрешает изменение экземпляров службы в среде выполнения. |Нет|Недоступно|    

### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, backend.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetBody"></a> Задание текста  
 Используйте политику `set-body`, чтобы задать текст сообщения для входящих и исходящих запросов. Для доступа к тексту сообщения можно использовать свойство `context.Request.Body` или `context.Response.Body` в зависимости от того, где находится политика: в разделе inbound или outbound.  
  
> [!IMPORTANT]
>  Обратите внимание, что по умолчанию при доступе к тексту сообщения с помощью `context.Request.Body` или `context.Response.Body` исходный текст сообщения теряется и его необходимо задать, возвратив текст обратно в выражение. Чтобы сохранить содержимое текста, при доступе к сообщению присвойте параметру `preserveContent` значение `true`. Если для параметра `preserveContent` задано значение `true` и в выражении возвращается другой текст, используется возвращаемый текст.  
>   
>  Учтите следующие рекомендации при использовании политики `set-body`.  
>   
>  -   Если для возврата нового или обновленного текста используется политика `set-body`, для параметра `preserveContent` не требуется задавать значение `true`, так как вы явно указываете новое содержимое текста.  
> -   Сохранять содержимое ответа во входящем конвейере не имеет смысла, так как ответа еще нет.  
> -   Сохранять содержимое запроса в исходящем конвейере не имеет смысла, так как на этом этапе запрос уже был отправлен в серверную часть.  
> -   Если эта политика используется при отсутствии текста сообщения, например во входящем параметре GET, возникает исключение.  
  
 Дополнительные сведения см. в разделах `context.Request.Body`, `context.Response.Body` и `IMessage` в таблице [Переменная контекста](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="literal-text-example"></a>Пример литерального текста  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a>Пример доступа к тексту как к строке Обратите внимание, что мы сохраняем исходный текст запроса, чтобы позже можно было обратиться к нему в конвейере.
  
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
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a>Пример доступа к тексту как к объекту JObject Обратите внимание, что мы не резервировали исходный текст запроса, поэтому попытка получить к нему доступ позже в конвейере приведет к возникновению исключения.  
  
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
 В этом примере показано, как выполнить фильтрацию содержимого путем удаления элементов данных из ответа, полученного из внутренней службы при использовании продукта `Starter`. Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, эпизод 177: возможности управления API с Владом Виноградским) с отметки времени 34:30. Начните с отметки времени 31:50, чтобы узнать общие сведения о [прогнозном API Dark Sky](https://developer.forecast.io/), используемом для этого примера.  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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
В политике `set-body` можно настроить использование языка шаблонов [Liquid](https://shopify.github.io/liquid/basics/introduction/) для преобразования текста запроса или ответа. Это может быть очень эффективным, когда требуется полностью изменить формат сообщения.

> [!IMPORTANT]
> Реализация шаблонов Liquid, используемая в политике `set-body`, настраивается в режиме C#. Это особенно важно при выполнении действий, таких как фильтрация. Например, если применяется фильтр по дате, то необходимо использовать стиль Pascal и форматирование даты C#, как в следующем примере:
>
> {{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> Чтобы с помощью шаблона Liquid правильно выполнить привязку к тексту XML, используйте политику `set-header`. Задайте для Content-Type значение application/xml или text/xml (или любой другой тип, заканчивающийся на +xml). Для текста JSON значение должно быть application/json или text/json (или любой другой тип, заканчивающийся на +json).

#### <a name="convert-json-to-soap-using-a-liquid-template"></a>Преобразование JSON в SOAP с помощью шаблона Liquid
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
|set-body|Корневой элемент. Содержит текст или выражения, которые возвращают текст.|Да|  

### <a name="properties"></a>Свойства  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|шаблон|Используется для изменения режима шаблона, в котором будет выполняться политика set-body. В настоящее время поддерживается только одно значение:<br /><br />- liquid — политика set-body будет использовать подсистему шаблонов Liquid. |Нет|liquid|  

Для доступа к сведениям о запросе и ответе шаблон Liquid можно привязать к объекту context с помощью следующих свойств: <br />
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
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetHTTPheader"></a> Установка HTTP-заголовка  
 Политика `set-header` назначает значение имеющемуся заголовку ответа и/или запроса или добавляет новый заголовок ответа и/или запроса.  
  
 Вставляет список HTTP-заголовков в HTTP-сообщение. Если эта политика находится во входящем конвейере, она устанавливает HTTP-заголовки для запроса, передаваемого в целевую службу. Если эта политика находится в исходящем конвейере, она устанавливает HTTP-заголовки для ответа, отправляемого клиенту шлюза.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="example"></a>Пример  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a>Пересылка контекстных сведений во внутреннюю службу  
 В этом примере показано, как применить политику на уровне API для предоставления контекстных сведений внутренней службе. Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, эпизод 177: возможности управления API с Владом Виноградским) с отметки времени 10:30. На отметке времени 12:10 демонстрируется вызов операции на портале разработчика, где можно просмотреть политику в действии.  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
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
|значение|Указывает значение заголовка, которое должно быть установлено. Для нескольких заголовков с одним и тем же именем добавьте дополнительные элементы `value`.|Да|  
  
### <a name="properties"></a>Свойства  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|exists-action|Указывает действие, которое должно быть выполнено, когда заголовок уже задан. Атрибут должен иметь одно из следующих значений:<br /><br /> override — заменяет значение имеющегося заголовка;<br />skip — не заменяет значение имеющегося заголовка;<br />append — добавляет значение к значению имеющегося заголовка;<br />delete — удаляет заголовок из запроса.<br /><br /> Если установлено значение `override`, перечисление нескольких записей с одним и тем же именем будет приводить к тому, что заголовок будет устанавливаться в соответствии со всеми записями (будут перечисляться несколько раз). В результате будут установлены только перечисленные значения.|Нет|override|  
|name|Указывает имя заголовка, которое должно быть установлено.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetQueryStringParameter"></a> Настройка параметра строки запроса  
 Политика `set-query-parameter` добавляет, заменяет значение или удаляет параметр строки запроса. Можно использовать для передачи параметров запроса, ожидаемых внутренней службой, которые являются необязательными или никогда не присутствуют в запросе.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="example"></a>Пример  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a>Пересылка контекстных сведений во внутреннюю службу  
 В этом примере показано, как применить политику на уровне API для предоставления контекстных сведений внутренней службе. Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, эпизод 177: возможности управления API с Владом Виноградским) с отметки времени 10:30. На отметке времени 12:10 демонстрируется вызов операции на портале разработчика, где можно просмотреть политику в действии.  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|set-query-parameter|Корневой элемент.|Да|  
|значение|Указывает значение параметра запроса, которое должно быть установлено. Для нескольких параметров запроса с одним и тем же именем добавьте дополнительные элементы `value`.|Да|  
  
### <a name="properties"></a>Свойства  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|exists-action|Указывает действие, которое должно быть выполнено, когда параметр запроса уже задан. Атрибут должен иметь одно из следующих значений:<br /><br /> override — заменяет значение имеющегося параметра;<br />skip — не заменяет значение имеющегося параметра запроса;<br />append — добавляет значение к значению имеющегося параметра запроса;<br />delete — удаляет параметр запроса из запроса.<br /><br /> Если установлено значение `override`, перечисление нескольких записей с одним и тем же именем будет приводить к тому, что параметр запроса будет устанавливаться в соответствии со всеми записями (будут перечисляться несколько раз). В результате будут установлены только перечисленные значения.|Нет|override|  
|name|Указывает имя параметра запроса, которое должно быть установлено.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, backend.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="RewriteURL"></a> Перезапись URL-адреса  
 Политика `rewrite-uri` преобразовывает URL-адрес запроса из его общедоступной формы в форму, ожидаемую веб-службой, как показано в следующем примере.  
  
-   Открытый URL — `http://api.example.com/storenumber/ordernumber`.  
  
-   URL-адрес запроса — `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`.  
  
 Эту политику можно использовать, когда дружественный для пользователя и/или браузера URL-адрес должен быть преобразован в формат URL-адреса, ожидаемый веб-службой. Эту политику необходимо применять только при указании URL-адресов в другом формате, например "чистых" URL-адресов, URL-адресов типа RESTful, дружественных для пользователя URL-адресов или дружественных для SEO URL-адресов, которые представляют собой чисто структурные URL-адреса, не содержащие строку запроса. Вместо этого они содержат только путь к ресурсу (после схемы и полномочий). Это часто делает в эстетических целях, для удобства и простоты использования или для оптимизации поисковых систем (SEO).  
  
> [!NOTE]
>  Используя политику, можно добавлять только параметры строки запроса. Нельзя добавлять дополнительный параметр пути к шаблону в URL-адрес перезаписи.  

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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
|шаблон|Фактический URL-адрес веб-службы с любыми параметрами строки запроса. При использовании выражений все значение должно быть выражением.|Да|Недоступно|  
|copy-unmatched-params|Указывает, добавляются ли в определяемый шаблоном перезаписи URL-адрес параметры запроса во входящем запросе, отсутствующие в исходном шаблоне URL-адреса.|Нет|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** product, API, operation.  
  
##  <a name="XSLTransform"></a> Преобразование XML с помощью XSLT  
 Политика `Transform XML using an XSLT` применяет преобразование данных в формате XSL в формат XML в тексте запроса или ответа.  
  
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
|Параметр|Используется для определения переменных, используемых при преобразовании.|Нет|  
|xsl:stylesheet|Корневой элемент таблицы стилей. Все определенные элементы и атрибуты соответствуют стандарту [спецификации XSLT](http://www.w3.org/TR/xslt).|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound.  
  
-   **Области политики:** global, product, API, operation.  
  
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  
