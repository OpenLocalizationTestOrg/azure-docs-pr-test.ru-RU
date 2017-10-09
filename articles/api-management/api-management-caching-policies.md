---
title: "политики кэширования API Management aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello, доступные для использования в службе управления API Azure политики кэширования."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>Политики кэширования в службе управления API
Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a> Политики кэширования  
  
-   Политики кэширования ответов  
  
    -   [Получение из кэша](api-management-caching-policies.md#GetFromCache) — выполнение поиска в кэше и возврат допустимых кэшированных ответов при их наличии.  
  
    -   [Хранить toocache](api-management-caching-policies.md#StoreToCache) - кэши ответы в соответствии с toohello указанной конфигурации управления кэшем.  
  
-   Политики кэширования значений  
  
    -   [Получение значения из кэша](#GetFromCacheByKey) — получение кэшированного элемента по ключу.  
  
    -   [Сохраните значение в кэше](#StoreToCacheByKey) -хранения элемента в кэше hello по ключу.  
  
    -   [Удалить значение из кэша](#RemoveCacheByKey) -удалить элемент из кэша hello по ключу.  
  
##  <a name="GetFromCache"></a> Получение из кэша  
 Используйте hello `cache-lookup` кэша политики tooperform поиска и возвращения допустимого кэшированного ответа, если оно доступно. Эту политику можно применять в тех случаях, когда содержимое ответа остается неизменным в течение определенного интервала времени. Кэширование ответов снижает пропускную способность и требования к обработке, применяемая hello серверной части web server и уменьшает задержку пользователей API.  
  
> [!NOTE]
>  Эта политика должна соответствовать [toocache хранилища](api-management-caching-policies.md#StoreToCache) политики.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Пример с использованием выражений политики  
 В этом примере показано, как ответ API управления tootooconfigure совпадений Здравствуйте, кэширование ответов hello серверной службы в соответствии с hello длительность кэширования резервное службы `Cache-Control` директивы. Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too25:25 Перемотка вперед.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|cache-lookup|Корневой элемент.|Да|  
|vary-by-header|Начало кэширования ответов по значению определенного заголовка, например Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.|Нет|  
|vary-by-query-parameter|Запускается процесс кэширования ответов для значения заданных параметров запроса. Введите один или несколько параметров. В качестве разделителя используйте точку с запятой. Если значение не задано, используются все параметры запроса.|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|allow-private-response-caching|Если задано слишком`true`, разрешает кэширование запросов, содержащих заголовок авторизации.|Нет|нет|  
|downstream-caching-type|Этот атрибут должен быть задан tooone из hello следующие значения.<br /><br /> - none — нисходящее кэширование не разрешено;<br />- private — разрешено нисходящее частное кэширование;<br />- public — разрешено частное и совместно используемое нисходящее кэширование.|Нет|Нет|  
|must-revalidate|При включенном кэшировании нижестоящим этот атрибут включает или выключает hello `must-revalidate` директиву управления кэшем в ответах шлюза.|Нет|Да|  
|vary-by-developer|Значение слишком`true` toocache ответов на основе ключа разработчика.|Нет|нет|  
|vary-by-developer-groups|Значение слишком`true` toocache ответов на основе роли пользователя.|Нет|нет|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** API, operation, product.  
  
##  <a name="StoreToCache"></a>Toocache хранилища  
 Hello `cache-store` политики кэши ответы в соответствии с toohello указаны параметры кэша. Эту политику можно применять в тех случаях, когда содержимое ответа остается неизменным в течение определенного интервала времени. Кэширование ответов снижает пропускную способность и требования к обработке, применяемая hello серверной части web server и уменьшает задержку пользователей API.  
  
> [!NOTE]
>  Одновременно с этой политикой должна быть определена соответствующая политика [получения из кэша](api-management-caching-policies.md#GetFromCache).  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Пример с использованием выражений политики  
 В этом примере показано, как ответ API управления tootooconfigure совпадений Здравствуйте, кэширование ответов hello серверной службы в соответствии с hello длительность кэширования резервное службы `Cache-Control` директивы. Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too25:25 Перемотка вперед.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|cache-store|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|длительность|Время жизни объекта hello кэшированных записей, указанное в секундах.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** outbound.  
  
-   **Области политики:** API, operation, product.  
  
##  <a name="GetFromCacheByKey"></a> Получение значения из кэша  
 Используйте hello `cache-lookup-value` tooperform политики кэширования Уточняющий запрос по ключу и возвращает кэшированное значение. ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики.  
  
> [!NOTE]
>  Одновременно с этой политикой должна быть определена соответствующая политика [сохранения значения в кэш](#StoreToCacheByKey).  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Пример  
 Дополнительные сведения и примеры этой политики см. в статье [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Пользовательское кэширование в службе управления API Azure).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|cache-lookup-value|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|default-value|Значение, которое будет присвоено переменной toohello, если поиск ключа кэша hello привело к созданию промах. Если этот атрибут не указан, присваивается значение `null`.|Нет|`null`|  
|key|Кэшировать toouse значение ключа в уточняющем запросе hello.|Да|Недоступно|  
|variable-name|Имя hello [переменной контекста](api-management-policy-expressions.md#ContextVariables) hello, поиск значения будет назначаться, при успешном выполнении уточняющего запроса. При поиске промах, hello переменной назначается значение hello hello `default-value` атрибута или `null`, если hello `default-value` атрибут опущен.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** global, API, operation, product.  
  
##  <a name="StoreToCacheByKey"></a> Сохранение значения в кэш  
 Hello `cache-store-value` выполняет хранилища кэша по ключу. ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики.  
  
> [!NOTE]
>  Одновременно с этой политикой должна быть определена соответствующая политика [получения значения из кэша](#GetFromCacheByKey).  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>Пример  
 Дополнительные сведения и примеры этой политики см. в статье [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Пользовательское кэширование в службе управления API Azure).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|cache-store-value|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|длительность|Значение будет кэшироваться hello указанное значение длительности, указанное в секундах.|Да|Недоступно|  
|key|Значение ключа hello кэша будет храниться в группе.|Да|Недоступно|  
|value|toobe значение Hello в кэше.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** global, API, operation, product.  
  
###  <a name="RemoveCacheByKey"></a> Удаление значения из кэша  
 Hello `cache-remove-value` удаляет кэшированный элемент, определенный по его ключу. ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики.  
  
#### <a name="policy-statement"></a>Правило политики  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Пример  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|cache-remove-value|Корневой элемент.|Да|  
  
#### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|key|ключ Hello hello кэшированные значения toobe, удаленных из кэша hello.|Да|Недоступно|  
  
#### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Разделы политики:** inbound, outbound, backend, on-error.  
  
-   **Области политики:** global, API, operation, product.  
  

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  