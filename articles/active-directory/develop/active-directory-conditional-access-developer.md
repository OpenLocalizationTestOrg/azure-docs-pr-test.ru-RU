---
title: "aaaDeveloper руководство по Azure Active Directory условного доступа | Документы Microsoft"
description: "Руководство для разработчиков и сценарии по условному доступу в Azure AD"
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Руководство для разработчиков по условному доступу в Azure Active Directory

Azure Active Directory (AD) предлагает несколько способов toosecure приложения и службы защиты.  Одним из этих уникальных способов является условный доступ.  Условный доступ позволяет разработчикам и корпоративных клиентов служб tooprotect множеством способов, в том числе:

* Многофакторная проверка подлинности
* Разрешение только Intune зарегистрированных устройств tooaccess определенных служб
* ограничение расположения пользователей и диапазонов IP-адресов.

Дополнительные сведения о полных возможностях hello условного доступа см. в разделе [условного доступа в классический портал Azure hello](../active-directory-conditional-access.md). 

В этой статье рассматривается какие условного доступа означает toodevelopers создание приложений для Azure AD.  Предполагается знание [однотенантных](active-directory-integrating-applications.md) и [мультитенантных](active-directory-devhowto-multi-tenant-overview.md) приложений, а также [распространенных шаблонов аутентификации](active-directory-authentication-scenarios.md).

Мы будем подробно рассмотреть влияние hello доступ к ресурсам, не имеет контроль над которым может применяются политики условного доступа.  Кроме того мы исследуем последствия hello условным доступом hello от имени представляет потока веб-приложений, доступ к Microsoft Graph hello и вызова интерфейсов API.

## <a name="how-does-conditional-access-impact-an-app"></a>Как условный доступ влияет на приложения

### <a name="app-topologies-impacted"></a>Затронутые топологии приложения

В наиболее распространенных случаях условного доступа не приводит к изменению поведения приложения или требует изменения от разработчика hello.  Только в некоторых случаях при приложения без вмешательства пользователя или косвенно запрашивает маркер для службы, приложению требуются изменения кода toohandle условный доступ «проблемы».  Это может быть так же просто, как выполнение запроса на интерактивный вход. 

В частности, hello следующих сценариях требуется код toohandle условный доступ «проблемы»: 

* Приложения, обращающиеся к hello Microsoft Graph
* Выполнение hello от имени представляет поток приложения
* приложения, получающие доступ к нескольким службам или ресурсам;
* одностраничные приложения, использующие ADAL.js.

Политики условного доступа может быть применен toohello приложения, но также может быть применен tooa веб-API приложение обращается к. Дополнительные сведения о toolearn как tooconfigure политику условного доступа см. в разделе [Приступая к работе с Azure Active Directory условного доступа](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules).

В зависимости от сценария hello корпоративный клиент можно применять и удалять политики условного доступа в любое время.  Чтобы вашего приложения toocontinue работать при применении новой политики необходимо tooimplement hello» задача» обработка. Привет, следующие примеры иллюстрируют обработки запроса. 

### <a name="conditional-access-examples"></a>Примеры условного доступа

В некоторых сценариях требуется код изменения toohandle условного доступа, тогда как другие работать как есть.  Ниже приведены несколько сценариев, с помощью условного доступа toodo многофакторной проверки подлинности, предоставляет некоторые регулировать различие hello.

* Создается однотенантное приложение iOS и применяется политика условного доступа.  приложение Hello выполняет вход пользователя и не запроса доступа tooan API.  При входе в систему пользователя hello политики hello вызывается автоматически, и пользователь hello должен tooperform многофакторной проверки подлинности (MFA). 
* При создании нескольких клиентов веб-приложения, использующего Microsoft Graph hello tooaccess Exchange, среди других служб.  Корпоративный клиент, использующий это приложение, устанавливает политику для SharePoint Online.  Когда hello веб-приложение запрашивает маркер для Microsoft Graph, применения политики на любой службы Microsoft (в частности службы, которые можно получить с помощью graph).  Пользователю предлагается пройти многофакторную проверку подлинности. В случае hello hello для конечных пользователей, вошли допустимые токены, утверждения «запрос», возвращается toohello веб-приложения.  
* При создании собственного приложения, в котором используется hello tooaccess службы среднего уровня Microsoft Graph.  Корпоративный клиент компании hello, с помощью этого приложения применяется tooExchange политики в оперативный режим.  При входе в систему конечного пользователя hello собственное приложение запрашивает доступ toohello среднего уровня и отправляет токен hello.  Средний уровень Hello выполняет от имени представляет поток toorequest доступа toohello MS Graph.  На этом этапе утверждения «запрос» представлены toohello среднего уровня. Средний уровень Hello отправляет hello запрос назад toohello собственное приложение, требующий toocomply с политикой условного доступа hello.

### <a name="complying-with-a-conditional-access-policy"></a>Соответствие политике условного доступа

Для разных топологий другое приложение при установлении сеанса hello оценивается политика условного доступа.  Как политики условного доступа оперирует гранулярности hello приложений и служб, hello точки, с которой он вызывается сильно зависит от сценария hello вы пытаетесь tooaccomplish.

Если приложение пытается tooaccess службы с помощью политики условного доступа, могут возникнуть проблема условного доступа.  Этот запрос зашифрован в hello `claims` параметр, который поставляется в ответе от Azure AD или hello Microsoft Graph.  Ниже приведен пример этого параметра запроса: 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Разработчики могут воспользоваться этой проблемы и добавить его на новый tooAzure запрос AD.  Передача это состояние предлагает toocomply любые необходимые действия, с помощью политики условного доступа hello hello tooperform конечного пользователя. Следующие сценарии hello описываются особенности ошибки hello и как tooextract hello параметра. 

## <a name="scenarios"></a>Сценарии

### <a name="prerequisites"></a>Предварительные требования

Условный доступ Azure AD — это функция, включенная в [Azure AD Premium](../active-directory-whatis.md#choose-an-edition).  Дополнительные сведения о лицензировании требований в hello [Нелицензированное использование отчетов](../active-directory-conditional-access-unlicensed-usage-report.md).  Разработчики могут присоединить hello [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), включающее toohello бесплатная подписка Enterprise Mobility Suite, которая включает Azure AD Premium.

### <a name="considerations-for-specific-scenarios"></a>Рекомендации для конкретных сценариев

в этих сценариях условного доступа применяется Hello следующую информацию только:

* Приложения, обращающиеся к hello Microsoft Graph
* Выполнение hello от имени представляет поток приложения
* приложения, получающие доступ к нескольким службам или ресурсам;
* одностраничные приложения, использующие ADAL.js.

В следующих разделах hello мы получаем в общих сценариев, в которых являются более сложными.  Hello принцип работы лежит политики оцениваются на hello hello маркера при запросе службы hello с политикой условного доступа применяются, если осуществляется через hello Microsoft Graph условного доступа.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Сценария: Доступ к hello Microsoft Graph приложение

В этом сценарии мы будем рассматривать hello случай если веб-приложение запрашивает доступ toohello Microsoft Graph. политики условного доступа Hello в этом случае может назначаться tooSharePoint Exchange и другие службы, к которому осуществляется в качестве рабочей нагрузки по hello Microsoft Graph.  В этом примере предположим, что для Sharepoint Online имеется политика условного доступа.

![Приложения, доступ к Microsoft Graph схема hello](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

приложение Hello сначала запрашивает авторизацию toohello Microsoft Graph, которой требуется доступ к подчиненным рабочую нагрузку без условного доступа.  Hello запрос завершается успешно без вызова любая политика, и приложение hello получение маркеров для Microsoft Graph.  На этом этапе приложение hello имеете права использовать маркер доступа hello запрос носителя для конечной точки hello запрошено. Теперь приложение hello требуется tooaccess к Sharepoint Online конечной точке Microsoft Graph, например:`https://graph.microsoft.com/v1.0/me/mySite`

приложение Hello уже имеет допустимый токен для hello Microsoft Graph, поэтому он может выполнять hello новый запрос без выдается новый токен. Этот запрос завершается неудачей и запрос утверждения, выданные Microsoft Graph в форме hello HTTP 403 — запрещено с ```WWW-Authenticate``` задачей.
Ниже приведен пример hello ответа: 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

Hello утверждений запрос находится внутри hello ```WWW-Authenticate``` заголовок, который может быть параметром утверждений hello проанализированный tooextract hello следующего запроса.  После присоединенных toohello новый запрос, Azure AD знает политики условного доступа hello tooevaluate при входе пользователя hello и приложение hello теперь hello политики условного доступа в соответствии с.  Повторение hello запроса toohello Sharepoint Online конечная точка была выполнена успешно.

Примеры кода демонстрируют, как toohandle hello утверждения запроса, см. в разделе toohello [образца кода рабочего стола .NET](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) для ADAL .NET или hello [образец кода от имени представляет](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) для ADAL .NET.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Сценария: Выполнение hello от имени представляет поток приложения

В этом сценарии мы будем рассматривать hello случай, в котором собственное приложение вызывает веб-службы или API.  В свою очередь, применения службы [Здравствуйте, «от имени представляет» потока](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall нижестоящую службу.  В нашем случае мы применили условного доступа политики toohello подчиненных услуги (веб-API 2) и используете собственное приложение, а не серверное/управляющее приложение. 

![Выполнение hello от имени представляет блок-схема приложения](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

исходный запрос маркера Hello для веб-API 1 не запрашивает hello конечного пользователя для многофакторной проверки подлинности как веб-API 1 могут не всегда обращение hello подчиненных API.  Когда веб-API 1 пытается toorequest hello маркера от имени представляет пользователя для веб-API 2, hello запрос завершается с ошибкой, поскольку hello пользователь не выполнил вход с помощью многофакторной проверки подлинности.

Azure AD возвращает ответ HTTP с некоторыми полезными данными: 

> [!NOTE]
> В данном случае это описание ошибки многофакторной проверки подлинности, но существует широкий спектр `interaction_required` относится tooconditional доступ.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

В наших веб-API 1 мы перехватывать ошибки hello `error=interaction_required`и отправить назад hello `claims` запроса toohello классического приложения.  На этом этапе можно сделать новый классического приложения hello `acquireToken()` вызова и добавить hello `claims`запрос как параметр запроса лишние строки.  Этот новый запрос требует hello пользователя toodo многофакторной проверки подлинности, а затем отправьте этот новый токен задней tooWeb API 1 и завершения hello от имени представляет поток.

tootry out этого сценария см. наш [образец кода .NET](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Он демонстрирует, как toopass hello утверждения запроса из веб-API 1 toohello собственное приложение и создать новый запрос в клиентское приложение hello. 

### <a name="scenario-app-accessing-multiple-services"></a>Сценарий: приложение, получающее доступ к нескольким службам

В этом сценарии мы будем рассматривать случай hello две службы обращается к веб-приложения, один из которых имеет назначенный политику условного доступа.  В зависимости от логики приложения могут существовать пути, в которой приложение не требует доступа tooboth веб-службы.  В этом сценарии hello порядок, в котором запрос маркера играет важную роль в hello взаимодействие с пользователем.

Предположим, что у нас есть веб-службы A и B. К веб-службе B применяется политика условного доступа.  Хотя запрос начальной проверки подлинности интерактивных hello необходимы разрешения для обеих служб, hello политики условного доступа не требуется во всех случаях.  Если приложение hello запрашивает маркер для веб-службы B, вызывается политика hello, и последующие запросы для веб-службы, А также завершается успешно, как показано ниже.

![Схема приложения, получающего доступ к нескольким службам](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

Кроме того Если приложение hello изначально запрашивает маркер для web service A, hello для конечных пользователей не вызывает hello политики условного доступа.  Это позволяет разработчику приложения hello hello toocontrol взаимодействии с пользователем и не используется принудительное hello условным доступом политики toobe вызывается во всех случаях. Hello сложным случаем является, если приложение hello впоследствии запрашивает маркер для веб-службы б. На этом этапе конечный пользователь hello должен toocomply с политикой условного доступа hello.  Когда приложение hello пытается слишком`acquireToken`, он может генерировать hello следующая ошибка (как показано на следующая диаграмме hello): 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![Приложение, получающее доступ к нескольким службам, запрашивающим новый маркер](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Если приложение hello используется библиотека ADAL hello, маркер сбоя tooacquire hello интерактивно всегда перезапускается.  При возникновении этого интерактивного запроса, конечный пользователь hello должен toocomply возможности hello с hello условным доступом.  Это верно, если запрашивается hello `AcquireTokenSilentAsync` или `PromptBehavior.Never` в этом случае приложение hello должен tooperform интерактивная ```AcquireToken``` запроса toocomply toogive hello конечного использования hello возможных сделок с политикой hello. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>Сценарий: одностраничное приложение (SPA), использующее ADAL.js

В этом сценарии мы будем рассматривать hello случай, когда у нас есть приложения, написанного на одной странице (SPA), защищенные с помощью ADAL.js toocall условного доступа веб-API.  Это простой архитектуры, но имеет некоторые особенности, которые необходимо принимать во внимание при разработке решения условного доступа toobe.

В ADAL.js есть несколько функций получения маркеров: `login()`, `acquireToken(...)`, `acquireTokenPopup(…)` и `acquireTokenRedirect(…)`. 

* `login()` получает маркер идентификатора через интерактивный запрос на вход, но не получает маркер доступа для любой службы (включая защищенный условным доступом веб-API).  
* `acquireToken(…)`может быть используется toosilently получить маркер доступа, это означает, что он не отображается пользовательский Интерфейс при любых обстоятельствах.  
* `acquireTokenPopup(…)`и `acquireTokenRedirect(…)` являются обоих используется toointeractively запроса маркера для ресурса, то есть они всегда отображать пользовательский Интерфейс входа в систему.

Когда приложению нужен toocall токена доступа веб-API, он предпримет новые попытки `acquireToken(…)`.  Если истек срок действия маркера сеанса hello или нам нужно toocomply с политикой условного доступа, затем hello *acquireToken* функция завершается с ошибкой, и использует приложение hello `acquireTokenPopup()` или `acquireTokenRedirect()`.

![Схема одностраничного приложения, использующего поток ADAL](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

Давайте подробно рассмотрим пример со сценарием условного доступа.  Hello для конечных пользователей просто приобретенных на сайте hello и не имеет сеанса.  Мы выполним вызов `login()` и получим идентификатор маркера без многофакторной проверки подлинности.  Затем hello пользователь нажимает кнопку, которая требует hello приложения toorequest данные из веб-API.  приложение Hello пытается toodo `acquireToken()` вызов но попытка завершается неудачей, так как пользователь hello многофакторной проверки подлинности еще не выполнено и должен toocomply с политикой условного доступа hello.

Azure AD отправляет назад hello, выполнив HTTP-ответа: 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

Наш приложению toocatch hello `error=interaction_required`.  Hello затем приложение может использовать либо `acquireTokenPopup()` или `acquireTokenRedirect()` на hello же ресурса.  пользователь Hello является принудительное toodo многофакторной проверки подлинности. После завершения пользователем hello hello многофакторной проверки подлинности, приложение hello выдается новый токен доступа для hello запрашиваемый ресурс.

tootry out этого сценария см. наш [образец кода от имени представляет JS SPA](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Этот пример кода использует политику условного доступа hello и веб-API, которые вы ранее зарегистрированы с toodemonstrate JS SPA этот сценарий. Показано, как утверждения hello дескриптор tooproperly запрос и получить маркер доступа, который может использоваться для веб-API. Кроме того, извлечение hello Общие [образец кода Angular.js](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) рекомендации по углового SPA


## <a name="see-also"></a>См. также

* toolearn Дополнительные сведения о возможностях hello. в разделе [условного доступа в Azure AD](../active-directory-conditional-access.md).
* Дополнительные примеры кода Azure AD см. в [репозитории примеров кода GitHub](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory). 
* Дополнительные сведения о hello ADAL SDK и доступа к справочной документации hello см. в разделе [руководство по библиотеки](active-directory-authentication-libraries.md).
* toolearn Дополнительные сведения о сценариях с несколькими клиентами, в разделе [как toosign пользователей, используя шаблон несколькими клиентами hello](active-directory-devhowto-multi-tenant-overview.md).
