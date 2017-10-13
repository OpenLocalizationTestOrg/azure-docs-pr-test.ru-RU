---
title: "Приступая к работе с Azure AD версии 2 для веб-сервера ASP.NET. Проверка | Документация Майкрософт"
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
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a>Тестирование кода

Щелкните `F5`, чтобы запустить проект в Visual Studio. Откроется браузер, и вы будете перенаправлены на страницу *http://localhost:{порт}*, где вы увидите кнопку *Вход с учетной записью Майкрософт*. Щелкните ее, чтобы выполнить вход.

Когда вы будете готовы выполнить проверку, используйте рабочую или учебную учетную запись (Azure Active Directory) либо личную учетную запись (live.com, outlook.com), чтобы выполнить вход. 

![Окно браузера для входа с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Окно браузера для входа с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Ожидаемые результаты
После входа в систему пользователь перенаправляется на домашнюю страницу веб-сайта, URL-адрес для протокола HTTPS которой указан в сведениях о регистрации приложения на портале регистрации приложений Майкрософт. Теперь на этой странице отображается *приветствие*, ссылка, чтобы выйти из приложения, и ссылка, чтобы увидеть утверждения пользователя. Она является ссылкой на ранее созданный контроллер авторизации.

### <a name="see-users-claims"></a>Просмотр утверждений пользователя
Выберите гиперссылку, чтобы просмотреть утверждения пользователя. Вы перейдете к контроллеру и представлению, которое доступно только для пользователей, прошедших проверку подлинности.

#### <a name="expected-results"></a>Ожидаемые результаты
 Вы должны увидеть таблицу, содержащую основные свойства пользователя, выполнившего вход.

| Свойство | Значение | Описание|
|---|---|---|
| Имя | {Полное имя пользователя} | Имя и фамилия пользователя
|Имя пользователя | <span>user@domain.com</span>| Имя пользователя, используемое для его идентификации
| Субъект| {Тема}|Строка для уникальной идентификации входа пользователя в Интернете|
| Tenant ID| Guid| Значение *guid* используется для однозначного представления организации пользователя Azure Active Directory.|

Кроме того, вы увидите таблицу со всеми утверждениями пользователя, включенными в запрос проверки подлинности. Список всех утверждений в маркере идентификатора и их описание см. в этой [статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Список утверждений в маркере идентификатора").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Проверка доступа к методу, включающему атрибут *[Authorize]* (необязательно)
На этом шаге вы проверите доступ к аутентифицированному контроллеру как анонимный пользователь.<br/>
Выберите ссылку для выхода пользователя и завершения процесса выхода.<br/>
Теперь в окне браузера введите http://localhost:{порт}/authenticated, чтобы получить доступ к контроллеру, защищенному атрибутом `[Authorize]`.

#### <a name="expected-results"></a>Ожидаемые результаты
Вы должны получить запрос на выполнение проверки подлинности, чтобы открылось представление.

## <a name="additional-information"></a>Дополнительная информация

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Защита всего веб-сайта
Для защиты всего веб-сайта добавьте `AuthorizeAttribute` для `GlobalFilters` в метод `Global.asax` `Application_Start`:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Как разрешить вход в приложение только пользователям одной организации**

> По умолчанию в приложение можно выполнить вход с помощью личных учетных записей (включая outlook.com, live.com и другие), а также рабочих и учебных учетных записей из любой компании или организации, которая использует Azure Active Directory. 

> Если вы хотите, чтобы вход в приложение был настроен только для пользователей из одной организации Azure Active Directory, замените параметр `Tenant` в файле *web.config* с `Common` на имя клиента организации, например *contoso.onmicrosoft.com*. После этого измените аргумент `ValidateIssuer` в *классе запуска OWIN*, задав ему значение `true`.

> Чтобы разрешить вход для пользователей из списка определенных организаций, задайте параметру `ValidateIssuer` значение true и используйте параметр `ValidIssuers`, чтобы указать список организаций.

> Другой вариант — реализовать пользовательский метод для проверки издателей с помощью параметра IssuerValidator. Дополнительные сведения о `TokenValidationParameters` см. в этой [статье](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Статья о классе TokenValidationParameters на сайте MSDN") на сайте MSDN.

