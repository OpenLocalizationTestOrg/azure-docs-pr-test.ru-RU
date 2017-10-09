---
title: "aaaAzure API управления политики взаимодействия доменов | Документы Microsoft"
description: "Дополнительные сведения о hello политики взаимодействия доменов можно использовать в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a>API Management cross domain policies (Междоменные политики службы управления API).
Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CrossDomainPolicies"></a> Политики междоменного доступа  
  
-   [Разрешить междоменные вызовы](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -становится доступным hello API из клиентов Adobe Flash и Microsoft Silverlight на основе браузера.  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -добавляет ресурсов независимо от источника (CORS) для управления доступом поддерживает операцию tooan или API tooallow междоменные вызовы из браузерных клиентов.  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) - добавляет JSON с заполнением (JSONP) поддержка tooan операции или API tooallow междоменные вызовы из браузерных клиентов JavaScript.  
  
##  <a name="AllowCrossDomainCalls"></a> Разрешение междоменных вызовов  
 Используйте hello `cross-domain` hello toomake политики API, доступную с клиентов Adobe Flash и Microsoft Silverlight на основе браузера.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|cross-domain|Корневой элемент. Дочерние элементы должны соответствовать toohello [спецификация файла междоменной политики Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).|Да|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** global.  
  
##  <a name="CORS"></a> CORS  
 Hello `cors` политики добавляет ресурсов независимо от источника (CORS) для управления доступом поддерживает операцию tooan или API tooallow междоменные вызовы из браузерных клиентов.  
  
 CORS позволяет браузеру и toointeract сервера и определения запросов независимо от наличия определенного tooallow независимо от источника (т. е. вызовы XMLHttpRequests из кода JavaScript на веб-странице tooother домены). Это обеспечивает большую гибкость, чем просто разрешение запросов из одного источника, и более высокую защищенность, чем разрешение всех запросов независимо от источника.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a>Пример  
 В этом примере показано, как запрашивает предварительных toosupport, например с пользовательскими заголовками, и методы, отличные от GET и POST. toosupport пользовательских заголовков и дополнительных команд HTTP используйте hello `allowed-methods` и `allowed-headers` разделов, как показано в следующий пример hello.  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|cors|Корневой элемент.|Да|Недоступно|  
|allowed-origins|Содержит `origin` элементы, описывающие hello допускается источники для междоменных запросах. `allowed-origins`может содержать один `origin` элемент, который задает `*` tooallow любые источники, одного или нескольких `origin` элементов, содержащих URI.|Да|Недоступно|  
|origin|Hello значение может быть либо `*` tooallow все источники, или URI, указывающий один источник. Hello URI должен включать схему, узел и порт.|Да|Если hello порт указан в URI, используется порт 80 для HTTP и порт 443 для HTTPS используется.|  
|allowed-methods|Этот элемент является обязательным, если разрешены методы, отличные от GET или POST. Содержит `method` элементы, которые задают hello поддерживается HTTP-команды.|Нет|Если этот раздел отсутствует, поддерживаются методы GET и POST.|  
|метод|Задает команду HTTP.|По крайней мере один `method` элемент является обязательным, если hello `allowed-methods` раздел присутствует.|Недоступно|  
|allowed-headers|Этот элемент содержит `header` элементы, указывающие имена заголовков hello, которые могут быть включены в запрос hello.|Нет|Недоступно|  
|expose-headers|Этот элемент содержит `header` элементы, указывающие имена hello заголовки, которые будут доступны hello клиента.|Нет|Недоступно|  
|Верхний колонтитул|Задает имя заголовка.|По крайней мере один `header` элемент является обязательным в `allowed-headers` или `expose-headers` при наличии раздела hello.|Недоступно|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|allow-credentials|Hello `Access-Control-Allow-Credentials` заголовок в hello предварительный ответ будет toohello значение этого атрибута и влияют на hello клиента возможность toosubmit и учетные данные в междоменных запросах.|Нет|нет|  
|preflight-result-max-age|Hello `Access-Control-Max-Age` заголовок в hello предварительный ответ будет toohello значение этого атрибута и влияют на агент пользователя hello возможность toocache предварительный ответ.|Нет|0|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** inbound.  
  
-   **Области политики:** API, operation.  
  
##  <a name="JSONP"></a> JSONP  
 Hello `jsonp` политики добавляет заполнение операция tooan поддержки (JSONP) или API tooallow междоменные вызовы из браузерных клиентов JavaScript. JSONP — это метод, используемый в данных toorequest программы JavaScript на сервере в другом домене. JSONP позволяет обойти ограничение hello, большинство веб-браузеров, где доступ tooweb страницы должны принадлежать hello того же домена.  
  
### <a name="policy-statement"></a>Правило политики  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>Пример  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 При вызове метода hello без hello параметр обратного вызова? cb = XXX, возвращается обычный JSON (без оболочки вызова функции).  
  
 Если добавляется параметр обратного вызова hello `?cb=XXX` он вернет результат JSONP, упаковки hello исходные результаты JSON вокруг hello функции обратного вызова, как`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>Элементы  
  
|Имя|Описание|Обязательно|  
|----------|-----------------|--------------|  
|jsonp|Корневой элемент.|Да|  
  
### <a name="attributes"></a>Атрибуты  
  
|Имя|Описание|Обязательно|значение по умолчанию|  
|----------|-----------------|--------------|-------------|  
|callback-parameter-name|Hello вызову функции JavaScript между доменами с префиксом hello полное доменное имя, где hello находится функция.|Да|Недоступно|  
  
### <a name="usage"></a>Использование  
 Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Разделы политики:** outbound.  
  
-   **Области политики:** global, product, API, operation.  
  
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  