---
title: "Обработка в политики управления API Azure aaaError | Документы Microsoft"
description: "Узнайте, как toorespond tooerror условия, которые могут возникнуть в процессе hello обработки запросов в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>Обработка ошибок в политиках управления API
Управления API Azure позволяет издателей toorespond tooerror условия, которые могут возникнуть во время обработки hello прокси-сервера toohello запросы, предоставляя `ProxyError` объекта. Hello `ProxyError` объекту осуществляется через hello [контекста. LastError](api-management-policy-expressions.md#ContextVariables) свойства и может использоваться с политиками hello `on-error` раздел политики. Здесь вы найдете ссылку для ошибки hello возможности обработки в Azure API Management.  
  
## <a name="error-handling-in-api-management"></a>Обработка ошибок в службе управления API  
 Политики в службе управления API Azure делятся `inbound`, `backend`, `outbound`, и `on-error` разделов, как показано в следующий пример hello.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Во время обработки запроса hello, встроенные действия выполняются вместе с любой политики, которые находятся в области действия для запроса hello. Если возникает ошибка, обработка немедленно переходит toohello `on-error` раздел политики. Hello `on-error` раздел политики можно использовать в любой области и издателей API можно настроить пользовательское поведение ведения журнала концентраторов tooevent hello ошибки или создание нового вызывающий toohello tooreturn ответа.  
  
> [!NOTE]
>  Hello `on-error` раздел отсутствует в политике по умолчанию. tooadd hello `on-error` статьи tooa политики, Обзор toohello требуемого политики в редакторе политики hello и добавьте его. Дополнительные сведения о настройке политик см. в статье [Политики в Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  Если в политике нет раздела `on-error`, вызывающий объект при возникновении ошибки получит сообщение с HTTP-кодом 400 или 500.  
  
### <a name="policies-allowed-in-on-error"></a>Политики, которые можно использовать в разделе on-error  
 Hello следующие политики могут быть использованы в hello `on-error` раздел политики.  
  
-   [choose](api-management-advanced-policies.md#choose)  
  
-   [set-variable](api-management-advanced-policies.md#set-variable)  
  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [return-response](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set-method](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [set-status](api-management-advanced-policies.md#SetStatus)  
  
-   [send-request](api-management-advanced-policies.md#SendRequest)  
  
-   [send-one-way-request](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [log-to-eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 При возникновении ошибки и управление переходит toohello `on-error` раздел политики ошибки hello хранится в [контекста. LastError](api-management-policy-expressions.md#ContextVariables) свойство, к которому можно получить политиками в hello `on-error` статьи и имеет следующие свойства hello.  
  
|Имя|Тип|Описание|Обязательно|  
|----------|----------|-----------------|--------------|  
|Источник|string|Элемент hello имена, где произошла ошибка hello. Это может быть имя политики или встроенного шага конвейера.|Да|  
|Причина|строка|Код ошибки в машинном формате, который удобно использовать для обработки ошибок.|Нет|  
|Сообщение|строка|Описание ошибки в понятном для человека формате.|Да|  
|Область|string|Имя области hello, где произошла ошибка hello и может быть «глобальные», «продукт», «api» или «операция»|Нет|  
|Раздел|строка|Имя раздела, в котором произошла ошибка. Здесь возможны следующие значения: inbound, backend, outbound или on-error.|Нет|  
|Путь|строка|Задает вложенные политики, например: choose[3]/when[2].|Нет|  
|PolicyId|string|Значение hello `id` атрибута, если заданные hello клиента, на которой произошла ошибка политики hello|Нет|  
  
> [!NOTE]
>  Все политики иметь дополнительный `id` атрибут, который можно добавить корневой элемент toohello hello политики. Если этот атрибут присутствует в политике, когда происходит ошибка, значение hello hello атрибута может быть получен посредством hello `context.LastError.PolicyId` свойство.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Стандартные ошибки для встроенных шагов  
 Hello следующие ошибки являются стандартными для ошибок, которые могут возникнуть во время вычисления hello встроенные возможности обработки действия.  
  
|Источник|Условие|Причина|Сообщение|  
|------------|---------------|------------|-------------|  
|Конфигурация|URI не соответствует tooany Api или операция|OperationNotFound|Не удается toomatch входящих tooan операции запроса.|  
|authorization|Не предоставлен ключ подписки|SubscriptionKeyNotFound|Доступ запрещен из-за toomissing ключ подписки. Сделать убедиться, что ключ tooinclude подписки, при выполнении запросов toothis API.|  
|authorization|Недопустимое значение ключа подписки|SubscriptionKeyInvalid|Доступ запрещен из-за tooinvalid ключ подписки. Убедитесь, что tooprovide допустимый ключ для активной подписки.|  
  
## <a name="predefined-errors-for-policies"></a>Стандартные ошибки для политик  
 Hello следующие ошибки являются стандартными для ошибок, которые могут возникнуть во время оценки политики.  
  
|Источник|Условие|Причина|Сообщение|  
|------------|---------------|------------|-------------|  
|rate-limit|Превышено ограничение скорости|RateLimitExceeded|Rate limit is exceeded (Превышено ограничение скорости)|  
|quota|Превышена квота|QuotaExceeded|превышена квота на количество вызовов. Quota will be replenished in xx:xx:xx. (Квота будет пополнена в xx:xx:xx.) -или- Out of bandwidth quota. (Превышена квота пропускной способности.) Quota will be replenished in xx:xx:xx. (Квота будет пополнена в xx:xx:xx.)|  
|jsonp|Недопустимое значение параметра обратного вызова (содержит неправильные символы)|CallbackParameterInvalid|Value of callback parameter {callback-parameter-name} is not a valid JavaScript identifier. (Значение параметра обратного вызова {имя параметра обратного вызова} не является допустимым идентификатором JavaScript.)|  
|ip-filter|Не удалось tooparse IP вызывающего объекта из запроса|FailedToParseCallerIP|Не удалось выполнить tooestablish IP-адрес для hello вызывающего объекта. Access denied. (Недопустимое значение {значение_утверждения} для утверждения {имя_утверждения}. Доступ запрещен.)|  
|ip-filter|IP-адрес вызывающего объекта не входит в список разрешенных|CallerIpNotAllowed|Caller IP address {ip-address} is not allowed. Access denied. (Недопустимый IP-адрес вызывающего объекта: {IP-адрес}. Доступ запрещен.)|  
|ip-filter|IP-адрес вызывающего объекта включен в список заблокированных|CallerIpBlocked|Caller IP address is blocked. Access denied. (IP-адрес вызывающего объекта заблокирован. Доступ запрещен.)|  
|check-header|Отсутствует обязательный заголовок или его значение|HeaderNotFound|В запросе hello не удалось найти заголовок {имя заголовка}. Access denied. (Недопустимое значение {значение_утверждения} для утверждения {имя_утверждения}. Доступ запрещен.)|  
|check-header|Отсутствует обязательный заголовок или его значение|HeaderValueNotAllowed|Header {header-name} value of {header-value} is not allowed. Access denied. (Недопустимое значение {значение_заголовка} для заголовка {имя_заголовка}. Доступ запрещен.)|  
|validate-jwt|В запросе отсутствует маркер JWT|TokenNotFound|JWT не найден в запросе hello. Access denied. (Недопустимое значение {значение_утверждения} для утверждения {имя_утверждения}. Доступ запрещен.)|  
|validate-jwt|Ошибка при проверке подписи|TokenSignatureInvalid|<сообщение из библиотеки jwt\>. Access denied. (Доступ запрещен.)|  
|validate-jwt|Недопустимая аудитория|TokenAudienceNotAllowed|<сообщение из библиотеки jwt\>. Access denied. (Доступ запрещен.)|  
|validate-jwt|Недопустимый издатель|TokenIssuerNotAllowed|<сообщение из библиотеки jwt\>. Access denied. (Доступ запрещен.)|  
|validate-jwt|Истек срок действия маркера|TokenExpired|<сообщение из библиотеки jwt\>. Access denied. (Доступ запрещен.)|  
|validate-jwt|Ключ подписи не удалось разрешить по идентификатору|TokenSignatureKeyNotFound|<сообщение из библиотеки jwt\>. Access denied. (Доступ запрещен.)|  
|validate-jwt|В маркере отсутствуют необходимые утверждения|TokenClaimNotFound|Токен JWT отсутствует hello следующих утверждений: < c1\>, < c2\>,... Access denied. (Недопустимое значение {значение_утверждения} для утверждения {имя_утверждения}. Доступ запрещен.)|  
|validate-jwt|Несоответствие значений утверждения|TokenClaimValueNotAllowed|Claim {claim-name} value of {claim-value} is not allowed. Access denied. (Недопустимое значение {значение_утверждения} для утверждения {имя_утверждения}. Доступ запрещен.)|  
|validate-jwt|Прочие сбои при проверке данных|JwtInvalid|<сообщение из библиотеки jwt\>|

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  