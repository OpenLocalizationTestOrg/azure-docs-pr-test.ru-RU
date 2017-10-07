---
title: "выражения политики управления API aaaAzure | Документы Microsoft"
description: "Сведения о выражениях политики в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: ea160028-fc04-4782-aa26-4b8329df3448
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 79da0d6ca3963307ec811a33aaac3d63a7abd97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policy-expressions"></a>Выражения политики в службе управления API
В выражениях политики используется синтаксис C# 6.0. Каждое выражение имеет доступ toohello неявно предоставляется [контекста](api-management-policy-expressions.md#ContextVariables) переменной и допустимому [подмножества](api-management-policy-expressions.md#CLRTypes) типов платформы .NET Framework.  
  
> [!NOTE]
>  Дополнительные сведения о выражениях политики см. в разделе hello [выражения политики](https://azure.microsoft.com/documentation/videos/policy-expressions-in-azure-api-management/) видео.  
>   
>  Пример настройки политик с помощью выражений см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Облачное покрытие, серия 177. Дополнительные возможности службы управления API с Владом Виноградским). В этом видео содержит следующие демонстрации выражение политики hello.  
>   
>  -   10:30 — в разделе как tooapply политику на уровне hello API уровня toosupply контекста сведения toohello серверной службы с использованием hello [параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) и [значение HTTP-заголовка](api-management-transformation-policies.md#SetHTTPheader) политики. В 12:10 отсутствует Демонстрация вызова операции на портале разработчиков hello, где можно просмотреть эти политики на работе.  
> -   В разделе 13:50 - как toouse hello [проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre политики-авторизации toooperations доступа на основе маркеров утверждений. Перемотка вперед too15:00 toosee hello политики, настроенные в редакторе hello политики и затем too18:50 демонстрацию вызова операции из портала разработчиков hello как с и без hello требуется маркер авторизации.  
> -   В разделе 21:00 - как toouse [инспектора API](https://azure.microsoft.com/documentation/articles/api-management-howto-api-inspector/) трассировки toosee как политики оцениваются и hello результаты оценки hello.  
> -   25:25 - см. в разделе как hello выражения политики toouse с [получить из кэша](api-management-caching-policies.md#GetFromCache) и [toocache хранилища](api-management-caching-policies.md#StoreToCache) политики tooconfigure API управления ответа соответствует Здравствуйте, кэширование ответа hello длительность кэширования Серверная служба в соответствии с hello резервные службы `Cache-Control` директивы.  
> -   34:30 - см. в разделе как фильтрацию, удалив элементы данных из ответа hello tooperform содержимого получил от hello серверной службе hello [поток управления](api-management-advanced-policies.md#choose) и [задать текст](api-management-transformation-policies.md#SetBody) политики. Начинаются с 31:50 toosee Обзор [hello темной API прогноз Sky](https://developer.forecast.io/) для этой демонстрации.  
> -   toodownload hello политики инструкций, используемых в этом видео. в разделе hello [api--образцов и политики управления](https://github.com/Azure/api-management-samples/tree/master/policies) в репозитории github.  
  
  
##  <a name="Syntax"></a> Синтаксис  
 Выражения с одним оператором заключаются в элементы `@(expression)`, где `expression` — оператор выражения C# правильного формата.  
  
 Выражения с несколькими операторами заключаются в элементы `@{expression}`. Все ветви кода в выражениях с несколькими операторами должны заканчиваться оператором `return`.  
  
##  <a name="PolicyExpressionsExamples"></a> Примеры  
  
```  
@(true)  
  
@((1+1).ToString())  
  
@("Hi There".Length)  
  
@(Regex.Match(context.Response.Headers.GetValueOrDefault("Cache-Control",""), @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value)  
  
@(context.Variables.ContainsKey("maxAge") ? int.Parse((string)context.Variables["maxAge"]) : 3600)  
  
@{   
  string value;   
  if (context.Request.Headers.TryGetValue("Authorization", out value))   
  {   
    return Encoding.UTF8.GetString(Convert.FromBase64String(value));  
  }   
  else   
  {   
    return null;  
  }  
}  
```  
  
##  <a name="PolicyExpressionsUsage"></a> Использование  
 Выражения могут использоваться в качестве значений атрибутов или текстовыми значениями в любой hello API управления [политики](api-management-policies.md), если не указано в ссылке политики hello.  
  
> [!IMPORTANT]
>  Обратите внимание, что при использовании выражения политики только ограниченной проверки выражения политики hello при определении политики hello. Так как выражения hello выполняются во время выполнения в конвейер входящих или исходящих hello шлюзом hello, любой во время выполнения исключения, создаваемые выражения политики hello приведет к ошибку времени выполнения в вызове hello API.  
  
##  <a name="CLRTypes"></a> Типы .NET Framework, допустимые в выражениях политики  
 Hello следующей таблице перечислены типы .NET Framework hello и их члены, которые допускаются в выражениях политики.  
  
|Тип CLR|Поддерживаемые методы|  
|--------------|-----------------------|  
|Newtonsoft.Json.Linq.Extensions|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JArray|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JConstructor|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JContainer|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JObject|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JProperty|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JRaw|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JToken|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JTokenType|Поддерживаются все методы|  
|Newtonsoft.Json.Linq.JValue|Поддерживаются все методы|  
|System.Collections.Generic.IReadOnlyCollection<T\>|Все|  
|System.Collections.Generic.IReadOnlyDictionary<TKey,  TValue>|Все|  
|System.Collections.Generic.ISet<TKey, TValue>|Все|  
|System.Collections.Generic.KeyValuePair<TKey,  TValue>|Key, Value|  
|System.Collections.Generic.List<TKey, TValue>|Все|  
|System.Collections.Generic.Queue<TKey, TValue>|Все|  
|System.Collections.Generic.Stack<TKey, TValue>|Все|  
|System.Convert|Все|  
|System.DateTime|Все|  
|System.DateTimeKind|Время в формате UTC|  
|System.DateTimeOffset|Все|  
|System.Decimal|Все|  
|System.Double|Все|  
|System.Guid|Все|  
|System.IEnumerable<T\>|Все|  
|System.IEnumerator<T\>|Все|  
|System.Int16|Все|  
|System.Int32|Все|  
|System.Int64|Все|  
|System.Linq.Enumerable<T\>|Поддерживаются все методы|  
|System.Math|Все|  
|System.MidpointRounding|Все|  
|System.Nullable<T\>|Все|  
|System.Random|Все|  
|System.SByte|Все|  
|System.Security.Cryptography. HMACSHA384|Все|  
|System.Security.Cryptography. HMACSHA512|Все|  
|System.Security.Cryptography.HashAlgorithm|Все|  
|System.Security.Cryptography.HMAC|Все|  
|System.Security.Cryptography.HMACMD5|Все|  
|System.Security.Cryptography.HMACSHA1|Все|  
|System.Security.Cryptography.HMACSHA256|Все|  
|System.Security.Cryptography.KeyedHashAlgorithm|Все|  
|System.Security.Cryptography.MD5|Все|  
|System.Security.Cryptography.RNGCryptoServiceProvider|Все|  
|System.Security.Cryptography.SHA1|Все|  
|System.Security.Cryptography.SHA1Managed|Все|  
|System.Security.Cryptography.SHA256|Все|  
|System.Security.Cryptography.SHA256Managed|Все|  
|System.Security.Cryptography.SHA384|Все|  
|System.Security.Cryptography.SHA384Managed|Все|  
|System.Security.Cryptography.SHA512|Все|  
|System.Security.Cryptography.SHA512Managed|Все|  
|System.Single|Все|  
|System.String|Все|  
|System.StringSplitOptions|Все|  
|System.Text.Encoding|Все|  
|System.Text.RegularExpressions.Capture|Index, Length, Value|  
|System.Text.RegularExpressions.CaptureCollection|Count, Item|  
|System.Text.RegularExpressions.Group|Captures, Success|  
|System.Text.RegularExpressions.GroupCollection|Count, Item|  
|System.Text.RegularExpressions.Match|Empty, Groups, Result|  
|System.Text.RegularExpressions.Regex|.ctor, IsMatch, Match, Matches, Replace|  
|System.Text.RegularExpressions.RegexOptions|Compiled, IgnoreCase, IgnorePatternWhitespace, Multiline, None, RightToLeft, Singleline|  
|System.TimeSpan|Все|  
|System.Tuple|Все|  
|System.UInt16|Все|  
|System.UInt32|Все|  
|System.UInt64|Все|  
|System.Uri|Все|  
|System.Xml.Linq.Extensions|Поддерживаются все методы|  
|System.Xml.Linq.XAttribute|Поддерживаются все методы|  
|System.Xml.Linq.XCData|Поддерживаются все методы|  
|System.Xml.Linq.XComment|Поддерживаются все методы|  
|System.Xml.Linq.XContainer|Поддерживаются все методы|  
|System.Xml.Linq.XDeclaration|Поддерживаются все методы|  
|System.Xml.Linq.XDocument|Поддерживаются все методы|  
|System.Xml.Linq.XDocumentType|Поддерживаются все методы|  
|System.Xml.Linq.XElement|Поддерживаются все методы|  
|System.Xml.Linq.XName|Поддерживаются все методы|  
|System.Xml.Linq.XNamespace|Поддерживаются все методы|  
|System.Xml.Linq.XNode|Поддерживаются все методы|  
|System.Xml.Linq.XNodeDocumentOrderComparer|Поддерживаются все методы|  
|System.Xml.Linq.XNodeEqualityComparer|Поддерживаются все методы|  
|System.Xml.Linq.XObject|Поддерживаются все методы|  
|System.Xml.Linq.XProcessingInstruction|Поддерживаются все методы|  
|System.Xml.Linq.XText|Поддерживаются все методы|  
|System.Xml.XmlNodeType|Все|  
  
##  <a name="ContextVariables"></a> Переменная контекста  
 Переменная с именем `context` неявно доступна в каждом [выражении](api-management-policy-expressions.md#Syntax) политики. Ее члены содержат сведения нужные toohello `\request`. Все hello `context` члены доступны только для чтения.  
  
|Переменная контекста|Допустимые методы, свойства и значения параметров|  
|----------------------|-------------------------------------------------------|  
|context|Api: IApi<br /><br /> Развертывание<br /><br /> LastError<br /><br /> Операция<br /><br /> Продукт<br /><br /> Запрос<br /><br /> RequestId: строка<br /><br /> Ответ<br /><br /> Подписка<br /><br /> Tracing: логическое значение<br /><br /> Пользователь<br /><br /> Variables:IReadOnlyDictionary<string, object><br /><br /> void Trace(message: строка)|  
|context.Api|Id: строка<br /><br /> Name: строка<br /><br /> Path: строка<br /><br /> ServiceUrl: IUrl|  
|context.Deployment|Region: строка<br /><br /> ServiceName: строка|  
|context.LastError|Source: строка<br /><br /> Reason: строка<br /><br /> Message: строка<br /><br /> Scope: строка<br /><br /> Section: строка<br /><br /> Path: строка<br /><br /> PolicyId: строка<br /><br /> Дополнительные сведения о переменной context.LastError см. в разделе [Error handling](api-management-error-handling-policies.md) (Обработка ошибок).|  
|context.Operation|Id: строка<br /><br /> Method: строка<br /><br /> Name: строка<br /><br /> UrlTemplate: строка|  
|context.Product|Apis: IEnumerable<IApi\><br /><br /> ApprovalRequired: логическое значение<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: строка<br /><br /> Name: строка<br /><br /> State: enum ProductState {NotPublished, Published}<br /><br /> SubscriptionLimit: целое число?<br /><br /> SubscriptionRequired: логическое значение|  
|context.Request|Body: IMessageBody<br /><br /> Certificate: System.Security.Cryptography.X509Certificates.X509Certificate2<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> IpAddress: строка<br /><br /> MatchedParameters: IReadOnlyDictionary<string, string><br /><br /> Method: строка<br /><br /> OriginalUrl:IUrl<br /><br /> Url: IUrl|  
|string context.Request.Headers.GetValueOrDefault(headerName: строка, defaultValue: строка)|headerName: строка<br /><br /> defaultValue: строка<br /><br /> Возвращает разделенные запятыми значения заголовка запроса или `defaultValue` Если hello заголовок не найден.|  
|context.Response|Body: IMessageBody<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> StatusCode: целое число<br /><br /> StatusReason: строка|  
|string context.Response.Headers.GetValueOrDefault(headerName: строка, defaultValue: строка)|headerName: строка<br /><br /> defaultValue: строка<br /><br /> Возвращает значения заголовка ответа с разделителями-запятыми или `defaultValue` Если hello заголовок не найден.|  
|context.Subscription|CreatedTime: дата и время<br /><br /> EndDate: дата и время?<br /><br /> Id: строка<br /><br /> Key: строка<br /><br /> Name: строка<br /><br /> PrimaryKey: строка<br /><br /> SecondaryKey: строка<br /><br /> StartDate: дата и время?|  
|context.User|Email: строка<br /><br /> FirstName: строка<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: строка<br /><br /> Identities: IEnumerable<IUserIdentity\><br /><br /> LastName: строка<br /><br /> Note: строка<br /><br /> RegistrationDate: дата и время|  
|IApi|Id: строка<br /><br /> Name: строка<br /><br /> Path: строка<br /><br /> Protocols: IEnumerable<string\><br /><br /> ServiceUrl: IUrl<br /><br /> SubscriptionKeyParameterNames: ISubscriptionKeyParameterNames|  
|IGroup|Id: строка<br /><br /> Name: строка|  
|IMessageBody|As<T\>(preserveContent: логическое значение = false). Where T: строка, JObject, JToken, JArray, XNode, XElement, XDocument<br /><br /> Hello `context.Request.Body.As<T>` и `context.Response.Body.As<T>` методы, используемые tooread институтов запроса и ответного сообщения в указанный тип `T`. По умолчанию hello метод использует hello исходное сообщение поток текста и reneders она недоступны после его возвращает. tooavoid, назначив метод hello работать с копией поток текста hello, набор hello `preserveContent` параметр слишком`true`. Go [здесь](api-management-transformation-policies.md#SetBody) toosee пример.|  
|IUrl|Host: строка<br /><br /> Path: строка<br /><br /> Port: целое число<br /><br /> Query: IReadOnlyDictionary<string, string[]><br /><br /> QueryString: строка<br /><br /> Scheme: строка|  
|IUserIdentity|Id: строка<br /><br /> Provider: строка|  
|ISubscriptionKeyParameterNames|Header: строка<br /><br /> Query: строка|  
|string IUrl.Query.GetValueOrDefault(queryParameterName: строка, defaultValue: строка)|queryParameterName: строка<br /><br /> defaultValue: строка<br /><br /> Возвращает разделенные запятыми значения параметров запроса или `defaultValue` Если параметр hello не найден.|  
|T context.Variables.GetValueOrDefault<T\>(variableName: строка, defaultValue: T)|variableName: строка<br /><br /> defaultValue: T<br /><br /> Возвращает значение переменной приведения tootype `T` или `defaultValue` Если hello переменная не найдена.<br /><br /> Этот метод вызывает исключение, если hello указанный тип не соответствует hello фактического типа hello возвращается переменная.|  
|BasicAuthCredentials AsBasic(input: this string)|input: строка<br /><br /> Если hello входной параметр содержит допустимое значение заголовка авторизации запроса HTTP обычной проверки подлинности, hello метод возвращает объект типа `BasicAuthCredentials`; в противном случае hello метод возвращает значение null.|  
|bool TryParseBasic(input: this string, result: out BasicAuthCredentials)|input: строка<br /><br /> result: выходное значение BasicAuthCredentials<br /><br /> Если hello входной параметр содержит допустимое значение заголовка авторизации запроса HTTP обычной проверки подлинности, метод hello возвращает `true` и hello результат параметр содержит значение типа `BasicAuthCredentials`; в противном случае возвращает метод hello `false`.|  
|BasicAuthCredentials|Password: строка<br /><br /> UserId: строка|  
|Jwt AsJwt(input: this string)|input: строка<br /><br /> Если hello входной параметр содержит допустимое значение маркера JWT, метод hello возвращает объект типа `Jwt`; в противном случае возвращает метод hello `null`.|  
|bool TryParseJwt(input: this string, result: out Jwt)|input: строка<br /><br /> result: выходное значение типа Jwt<br /><br /> Если hello входной параметр содержит допустимое значение маркера JWT, метод hello возвращает `true` и hello результат параметр содержит значение типа `Jwt`; в противном случае возвращает метод hello `false`.|  
|Jwt|Algorithm: строка<br /><br /> Audience: IEnumerable<string\><br /><br /> Claims: IReadOnlyDictionary<string, string[]><br /><br /> ExpirationTime: дата и время?<br /><br /> Id: строка<br /><br /> Issuer: строка<br /><br /> NotBefore: дата и время?<br /><br /> Subject: строка<br /><br /> Type: строка|  
|string Jwt.Claims.GetValueOrDefault(claimName: string, defaultValue: string)|claimName: строка<br /><br /> defaultValue: строка<br /><br /> Возвращает разделенные запятыми значения утверждения или `defaultValue` Если hello заголовок не найден.|

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  
