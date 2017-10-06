---
title: "aaaAzure AD v2 ASP.NET Web Server Приступая к работе - тестирования | Документы Microsoft"
description: "Реализация входа Майкрософт в решении ASP.NET с традиционным браузерным приложением с использованием стандарта OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Тестирование кода

Нажмите клавишу `F5` toorun свой проект в Visual Studio. Hello обозреватель и дать вам слишком*http://localhost: {port}* чего вы увидите hello *вход с Microsoft* кнопки. Продолжим и щелкните его toosign в.

Когда вы будете готовы tootest, используйте рабочую или учебную (Azure Active Directory) или личного (live.com, outlook.com) учетной записи toosign в. 

![Окно браузера для входа с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Окно браузера для входа с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Ожидаемые результаты
После входа в систему пользователя hello является домашней страницей перенаправленный toohello вашего веб-сайта, являющегося hello HTTPS-адрес, указанный в данных приложения в hello портала регистрации приложения Microsoft. Эта страница будет выглядеть *Hello {User}* и ссылка toosign исходящий и утверждения пользователей toosee ссылку hello — которых является контроллером авторизовать toohello ссылку, созданного ранее.

### <a name="see-users-claims"></a>Просмотр утверждений пользователя
Выберите hello гиперссылки toosee hello утверждения пользователя. Заставляет toohello контроллер и представление, которое можно только доступные toousers, проходят проверку подлинности.

#### <a name="expected-results"></a>Ожидаемые результаты
 Появится таблица, содержащая основные свойства hello hello вход пользователя:

| Свойство | Значение | Описание|
|---|---|---|
| Имя | {Полное имя пользователя} | пользователь Hello и фамилию имя
|Имя пользователя | <span>user@domain.com</span>| Hello имя пользователя, используемое tooidentify hello вход пользователя
| Субъект| {Тема}|Toouniquely строка идентификации hello входа пользователя в систему по hello web|
| Tenant ID| Guid| Объект *guid* toouniquely представляют Привет пользователя Azure Active Directory организации.|

Кроме того, вы увидите таблицу со всеми утверждениями пользователя, включенными в запрос проверки подлинности. Список всех утверждений в маркере идентификатора и их описание см. в этой [статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Список утверждений в маркере идентификатора").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Проверка доступа к методу, включающему атрибут *[Authorize]* (необязательно)
На этом шаге вы будет доступ к hello проверкой подлинности контроллер тестирования как анонимный пользователь:<br/>
Выберите пользователя toosign out hello ссылку hello и выхода процесса завершения hello.<br/>
Теперь в окне браузера введите http://localhost: {port} / tooaccess проверку подлинности, контроллер, защищенного hello `[Authorize]` атрибута

#### <a name="expected-results"></a>Ожидаемые результаты
Должно быть отображено сообщение hello, требуя tooauthenticate toosee hello представления.

## <a name="additional-information"></a>Дополнительная информация

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Защита всего веб-сайта
tooprotect все веб-сайте, добавить hello `AuthorizeAttribute` слишком`GlobalFilters` в `Global.asax` `Application_Start` метод:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Как пользователям toorestrict toosign только в одной организации в приложении tooyour**

> По умолчанию личные учетные записи (включая outlook.com, live.com и другие), а также работу и учебную учетные записи из любого компании или организации, интегрированное с Azure Active Directory можно входить в приложение tooyour. 

> Вашего приложения tooaccept входа в систему из только одной организации Azure Active Directory следует заменить hello `Tenant` параметр в *web.config* из `Common` имя клиента toohello hello организации — примере *contoso.onmicrosoft.com*. После этого изменить hello `ValidateIssuer` аргумента в вашей *класс запуска OWIN* слишком`true`.

> задать tooallow пользователей из списка конкретных организаций `ValidateIssuer` tootrue и использование hello `ValidIssuers` toospecify параметр список организаций.

> Другой вариант — toovalidate hello издателей, с помощью параметра IssuerValidator tooimplement пользовательский метод. Дополнительные сведения о `TokenValidationParameters` см. в этой [статье](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Статья о классе TokenValidationParameters на сайте MSDN") на сайте MSDN.

