---
title: "политики ограниченного использования программ для доступа к API управления aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о политиках ограниченного использования программ hello доступа доступны для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>Политики ограничения доступа в службе управления API
Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a> Политики ограничения доступа  
  
-   [Проверка заголовка HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) – обеспечивает принудительный ввод заголовка HTTP и/или его значения.  
  
-   [Ограничение частоты вызовов по подписке](api-management-access-restriction-policies.md#LimitCallRate) — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.  
  
-   [Ограничение частоты вызовов по ключу](#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.  
  
-   [Ограничение IP-адресов вызывающих объектов](api-management-access-restriction-policies.md#RestrictCallerIPs) – фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и/или диапазонов адресов.  
  
-   [Задание квоты использования по подписке](api-management-access-restriction-policies.md#SetUsageQuota) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, для каждой подписки.  
  
-   [Задание квоты использования ключом](#SetUsageQuotaByKey) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, на основе каждого ключа.  
  
-   [Проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) – обеспечивает принудительное задание и проверку JWT, извлеченного из заданного заголовка HTTP или параметра запроса.  
  
##  <a name="CheckHTTPHeader"></a> Проверка заголовка HTTP  
 Используйте hello `check-header` tooenforce политики, что запрос содержит указанный заголовок HTTP. При необходимости можно было проверить toosee Если заголовок hello имеет определенное значение или диапазону допустимых значений. При невозможности проверки hello hello политики обработка запроса прекращается и возвращает hello HTTP состояние код и сообщение об ошибке указано политикой hello.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|check-header|Корневой элемент.|Да|  
|значение|Допустимое значение заголовка HTTP. Если указаны элементы с несколькими значениями, hello проверка считается успешно, если один из значения hello соответствие.|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|failed-check-error-message|Ошибка tooreturn сообщений в текст ответа hello HTTP, если hello заголовок не существует или имеет недопустимое значение. Это сообщение должно содержать правильно экранированные специальные символы.|Да|Недоступно|  
|failed-check-httpcode|Tooreturn код состояния HTTP, если hello заголовок не существует или имеет недопустимое значение.|Да|Недоступно|  
|header-name|Имя Hello hello toocheck заголовка HTTP.|Да|Недоступно|  
|ignore-case|Можно задать tooTrue или False. Если набор tooTrue регистр учитывается, если значение заголовка hello сравнивается hello набором допустимых значений.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound, outbound.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="LimitCallRate"></a> Ограничение частоты вызовов по подписке  
 Hello `rate-limit` политики предотвращает использование API пики на основе каждой подписки, ограничивая hello вызвать указанный tooa скорость номеров за указанный период времени. При запуске этой политики вызывающий объект hello получает `429 Too Many Requests` код состояния ответа.  
  
> [!IMPORTANT]
>  Эту политику можно использовать для каждого документа политики только один раз.  
>   
>  [Выражения политики](api-management-policy-expressions.md) не может использоваться в атрибутах hello политики для этой политики.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|set-limit|Корневой элемент.|Да|  
|api|Добавьте один или несколько из этих элементов tooimpose ограничение частоты вызовов по интерфейсам API в пределах продукта hello. Ограничения частоты вызовов продукта и API применяются раздельно.|Нет|  
|операция|Добавьте один или несколько из этих элементов tooimpose ограничение частоты вызовов операций в пределах интерфейса API. Ограничения частоты вызовов продукта, API и операции применяются раздельно.|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|name|Hello имя hello API какие ограничение частоты tooapply hello.|Да|Недоступно|  
|calls|Здравствуйте, максимальное общее число вызовов, допускается hello временной интервал, указанный в hello `renewal-period`.|Да|Недоступно|  
|renewal-period|Здравствуйте, период времени в секундах, после которого hello сброса квоты.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** product.  
  
##  <a name="LimitCallRateByKey"></a> Ограничение частоты вызовов по ключу  
 Hello `rate-limit-by-key` политики предотвращает использование API пики на основе каждого ключа, ограничивая hello вызвать указанный tooa скорость номеров за указанный период времени. ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики. Необязательный шаг условия могут быть добавлены toospecify, какие запросы должны быть подсчитаны расчете предельного числа hello. При запуске этой политики вызывающий объект hello получает `429 Too Many Requests` код состояния ответа.  
  
 Дополнительные сведения и примеры этой политики см. в статье [Расширенное регулирование запросов с помощью управления API](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Эту политику можно использовать для каждого документа политики только один раз.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>Пример  
 В следующем примере hello ограничение частоты hello шифруется по IP-адресу hello вызывающего объекта.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|set-limit|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|calls|Здравствуйте, максимальное общее число вызовов, допускается hello временной интервал, указанный в hello `renewal-period`.|Да|Недоступно|  
|counter-key|Hello ключа toouse для политики ограничения скорости hello.|Да|Недоступно|  
|increment-condition|Hello логическое выражение, указывающее, если запрос hello следует засчитывается квоты hello (`true`).|Нет|Недоступно|  
|renewal-period|Здравствуйте, период времени в секундах, после которого hello сброса квоты.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="RestrictCallerIPs"></a> Ограничение IP-адресов вызывающих объектов  
 Hello `ip-filter` политики Фильтрация (разрешение или запрет) вызовов с конкретных IP-адресов и/или диапазоны адресов.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|ip-filter|Корневой элемент.|Да|  
|address|Указывает один IP-адрес, на какие toofilter.|По крайней мере один элемент `address` или `address-range` является обязательным.|  
|address-range from="address" to="address"|Указывает диапазон IP-адресов, на какие toofilter.|По крайней мере один элемент `address` или `address-range` является обязательным.|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|address-range from="address" to="address"|Диапазон IP-адресов tooallow или запретить доступ.|Требуется, если hello `address-range` используется элемент.|Недоступно|  
|ip-filter action="allow &#124; forbid"|Определяет, следует разрешить вызовы или не для hello указан IP-адреса и диапазоны.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="SetUsageQuota"></a> Задание квоты использования по подписке  
 Hello `quota` политика принудительно применяет задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, для каждой подписки.  
  
> [!IMPORTANT]
>  Эту политику можно использовать для каждого документа политики только один раз.  
>   
>  [Выражения политики](api-management-policy-expressions.md) не может использоваться в атрибутах hello политики для этой политики.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|quota|Корневой элемент.|Да|  
|api|Добавьте один или несколько из этих элементов tooimpose квоты на интерфейсы API в пределах продукта hello. Квоты продукта и API применяются раздельно.|Нет|  
|операция|Добавьте один или несколько из этих элементов tooimpose квоты на операции в пределах интерфейса API. Квоты продукта, API и операции применяются раздельно.|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|name|Имя Hello hello API или операция, для которых hello применяется Квота.|Да|Недоступно|  
|bandwidth|Здравствуйте, максимальное общее число килобайт допускается hello временной интервал, указанный в hello `renewal-period`.|Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.|Недоступно|  
|calls|Здравствуйте, максимальное общее число вызовов, допускается hello временной интервал, указанный в hello `renewal-period`.|Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.|Недоступно|  
|renewal-period|Здравствуйте, период времени в секундах, после которого hello сброса квоты.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** product.  
  
##  <a name="SetUsageQuotaByKey"></a> Задание квоты использования по ключу  
 Hello `quota-by-key` политика принудительно применяет задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, на основе каждого ключа. ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики. Необязательный шаг условия могут быть добавлены toospecify, какие запросы должны быть засчитывается hello квоты.  
  
 Дополнительные сведения и примеры этой политики см. в статье [Расширенное регулирование запросов с помощью управления API](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Эту политику можно использовать для каждого документа политики только один раз.  
>   
>  [Выражения политики](api-management-policy-expressions.md) не может использоваться в атрибутах hello политики для этой политики.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Пример  
 В следующем примере hello Квота hello шифруется по IP-адресу hello вызывающего объекта.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|quota|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|bandwidth|Здравствуйте, максимальное общее число килобайт допускается hello временной интервал, указанный в hello `renewal-period`.|Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.|Недоступно|  
|calls|Здравствуйте, максимальное общее число вызовов, допускается hello временной интервал, указанный в hello `renewal-period`.|Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.|Недоступно|  
|counter-key|Hello ключа toouse политики квоты hello.|Да|Недоступно|  
|increment-condition|Hello логическое выражение, указывающее, если запрос hello следует засчитывается квоты hello (`true`)|Нет|Недоступно|  
|renewal-period|Здравствуйте, период времени в секундах, после которого hello сброса квоты.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** global, product, API, operation.  
  
##  <a name="ValidateJWT"></a> Проверка JWT  
 Hello `validate-jwt` политика обеспечивает существование и подтверждение JWT, извлеченных из любого указанного заголовка HTTP или параметра запроса.  
  
> [!IMPORTANT]
>  Hello `validate-jwt` политика требует этого hello `exp` зарегистрированных утверждений является включено в токене JWT hello, за исключением случаев `require-expiration-time` атрибут задан и имеет слишком`false`.  
> Hello `validate-jwt` политики поддерживает HS256 и RS256 алгоритма подписи. HS256 hello ключа необходимо указать встроенный в политике hello в форме hello в кодировке base64. Для RS256 hello ключ имеет toobe предоставляете посредством конечной точки конфигурации Open ID.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>Примеры  
  
#### <a name="azure-mobile-services-token-validation"></a>Проверка маркеров мобильных служб Azure  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Проверка маркеров Azure Active Directory  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Проверка токена Azure Active Directory B2C  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>Авторизовать toooperations доступа на основе маркеров утверждений  
 В этом примере показано, как toouse hello [проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre политики-авторизовать toooperations доступа на основе маркеров утверждений. Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too13:50 Перемотка вперед. Перемотка вперед too15:00 toosee hello политики, настроенные в редакторе hello политики и затем too18:50 демонстрацию вызова операции из портала разработчиков hello как с и без hello требуется маркер авторизации.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>Элементы  
  
|Элемент|Описание|Обязательно|  
|-------------|-----------------|--------------|  
|validate-jwt|Корневой элемент.|Да|  
|audiences|Содержит список допустимых заявок audience, могут быть представлены на маркер hello. При наличии нескольких значений audience каждое значение проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего значения. Необходимо указать по крайней мере один элемент audience.|Нет|  
|issuer-signing-keys|Список ключей, используемых toovalidate безопасности в кодировке Base64 подписи токенов. При наличии нескольких ключей безопасности каждый ключ проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего ключа (удобно для смены маркеров). Ключевые элементы имеют дополнительный `id` toomatch атрибут, используемый для `kid` утверждения.|Нет|  
|issuers|Список допустимых субъектов, выпустивших токен hello. При наличии нескольких значений элемента issuer каждое значение проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего значения.|Нет|  
|openid-config|элемент Hello, используемая для указания совместимые конечной точки конфигурации Open ID из которого можно получить ключи подписывания и издателя.|Нет|  
|required-claims|Содержит список утверждений, которые toobe присутствует для hello маркер для его toobe считается действительным. Здравствуйте, когда `match` атрибута задано слишком`all` все значения утверждений в политике hello должны присутствовать в маркере hello для проверки toosucceed. Здравствуйте, когда `match` атрибута задано слишком`any` по крайней мере одно утверждение должны присутствовать в маркере hello для проверки toosucceed.|Нет|  
|zumo-master-key|Главный ключ для маркеров, выданных мобильными службами Azure.|Нет|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|clock-skew|Интервал времени. Предоставляет кратковременную отсрочку в том случае, если утверждение истечения срока действия маркера hello присутствует в маркере hello и выходит за пределы текущего hello даты / времени.|Нет|0 секунд|  
|failed-validation-error-message|Ошибка tooreturn сообщений в текст ответа hello HTTP, если hello JWT не проходит проверку. Это сообщение должно содержать правильно экранированные специальные символы.|Нет|Сообщение об ошибке по умолчанию зависит от проблемы проверки, например "JWT отсутствует".|  
|failed-validation-httpcode|Tooreturn код состояния HTTP, если hello JWT не проходит проверку.|Нет|401|  
|header-name|Hello имя заголовка hello HTTP, удерживая токен hello.|Необходимо указать один из двух атрибутов (`header-name` или `query-paremeter-name`), но не оба.|Недоступно|  
|id|Hello `id` атрибут hello `key` элемент позволяет toospecify hello строку, которая будет сопоставлена с `kid` утверждений в токен (при его наличии) toofind hello out hello toouse соответствующего ключа для проверки подписи.|Нет|Недоступно|  
|match|Hello `match` атрибут hello `claim` элемент указывает, должен ли все значения утверждений в политике hello присутствует hello маркер для проверки toosucceed. Возможные значения:<br /><br /> -                          `all`-все значения утверждений в политике hello должны присутствовать в маркере hello для проверки toosucceed.<br /><br /> -                          `any`-значение хотя бы одно утверждение должны присутствовать в маркере hello для проверки toosucceed.|Нет|все|  
|query-paremeter-name|Hello имя параметра запроса hello hello, содержащий токен hello.|Необходимо указать один из двух атрибутов (`header-name` или `query-paremeter-name`), но не оба.|Недоступно|  
|require-expiration-time|Логическое значение. Указывает, требуется ли утверждение истечения срока действия маркера hello.|Нет|Да|
|require-scheme|Здравствуйте, имя схемы токенов hello, например "Bearer". Если этот атрибут задан, политики hello обеспечит, указано, что схема присутствует в hello значение заголовка авторизации.|Нет|Недоступно|
|require-signed-tokens|Логическое значение. Указывает, является ли токен обязательный toobe подписи.|Нет|Да|  
|url|URL-адрес конечной точки конфигурации Open ID, по которому можно получить метаданные конфигурации Open ID. Для Azure Active Directory используйте hello URL-адреса: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` подставив имя клиента каталога, например `contoso.onmicrosoft.com`.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** global, product, API, operation.  
  
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  
