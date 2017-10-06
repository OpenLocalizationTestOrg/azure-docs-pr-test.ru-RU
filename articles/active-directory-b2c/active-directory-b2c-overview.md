---
title: "Обзор Azure AD B2C | Документация Майкрософт"
description: "Разработка потребительских приложений с помощью Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c465dbde-f800-4f2e-8814-0ff5f5dae610
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: saeedakhter-msft
ms.openlocfilehash: abfd742e710458de3193dc5051de7818a112376c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-focus-on-your-app-let-us-worry-about-sign-up-and-sign-in"></a>Настройка входа и регистрация приложения в Azure AD B2C

Azure AD B2C — это облачное решение, позволяющее управлять удостоверениями в веб-приложениях и мобильных приложениях. Это высокой доступности глобальной службы, которая масштабируется toohundreds миллионов идентификаторов. Так как служба Azure AD B2C разработана на основе безопасной платформы корпоративного уровня, она защищает приложения, бизнес-процессы и пользовательские данные.

С минимальной конфигурацией Azure AD B2C обеспечивает tooauthenticate вашего приложения:

* **учетных записей социальных сетей** (например, Facebook, Google, LinkedIn и другое);
* **корпоративных учетных записей** (с помощью открытых стандартных протоколов, OpenID Connect или SAML);
* **локальных учетных записей** (адрес электронной почты и пароль или имя пользователя и пароль).

## <a name="get-started"></a>Начало работы

Сначала необходимо получить своим собственным клиентом с помощью hello действия, описанные в [создание клиента Azure AD B2C](active-directory-b2c-get-started.md).

Затем выберите сценарий разработки приложения:

|  |  |  |  |
| --- | --- | --- | --- |
| <center>![Классические и мобильные приложения](../active-directory/develop/media/active-directory-developers-guide/NativeApp_Icon.png)<br />Классические и мобильные приложения</center> | [Azure Active Directory B2C: поток кода авторизации OAuth 2.0](active-directory-b2c-reference-oauth-code.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br /><br />[iOS](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal)<br /><br />[Android](https://github.com/Azure-Samples/active-directory-b2c-android-native-msal) | [.NET](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop)<br /><br />[Xamarin](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) |  |
| <center>![Веб-приложения](../active-directory/develop/media/active-directory-developers-guide/Web_app.png)<br />Веб-приложения</center> | [Обзор](active-directory-b2c-reference-oidc.md)<br /><br />[ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)<br /><br />[ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | [Node.js](active-directory-b2c-devquickstarts-web-node.md) |  |
| <center>![Одностраничные приложения](../active-directory/develop/media/active-directory-developers-guide/SPA.png)<br />Одностраничные приложения</center> | [Обзор](active-directory-b2c-reference-spa.md)<br /><br />[JavaScript](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)<br /><br /> |  |  |
| <center>![Веб-интерфейсы API](../active-directory/develop/media/active-directory-developers-guide/Web_API.png)<br />Веб-интерфейсы API</center> | [ASP.NET](active-directory-b2c-devquickstarts-api-dotnet.md)<br /><br /> [ASP.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)<br /><br /> [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | [Вызов веб-API .NET](active-directory-b2c-devquickstarts-web-api-dotnet.md) |

## <a name="whats-new"></a>Новые возможности

Обратитесь к этому списку часто toolearn о будущих изменений toohello Azure Active Directory B2C. Кроме того, мы будем сообщать о нововведениях в Twitter под именем @AzureAD.

* Кроме слишком «Встроенных политик» (общедоступная) hello [«Пользовательских политик»](active-directory-b2c-overview-custom.md) функция теперь доступна в общедоступной предварительной версии.  Настраиваемые политики предназначены для специалистов удостоверений, требующие контроля за композиции hello работы удостоверения.
* Hello [токена доступа](https://azure.microsoft.com/en-us/blog/azure-ad-b2c-access-tokens-now-in-public-preview) функция теперь доступна в общедоступной предварительной версии.
* Объявлено о выпуске каталогов [общедоступной версии Azure AD B2C в Европе](https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-eu/).
* Ознакомьтесь с постоянно растущей коллекцией [примеров кода на Github](https://github.com/Azure-Samples?q=b2c).

## <a name="how-tooarticles"></a>Как tooarticles

Узнайте, как отдельные функции Azure Active Directory B2C toouse:

* Настройка учетных записей [Facebook](active-directory-b2c-setup-fb-app.md), [Google+](active-directory-b2c-setup-goog-app.md), [Microsoft account](active-directory-b2c-setup-msa-app.md), [Amazon](active-directory-b2c-setup-amzn-app.md) и [LinkedIn](active-directory-b2c-setup-li-app.md) для использования в приложениях, ориентированных на потребителей.
* [Используйте настраиваемые атрибуты toocollect сведения о потребителей](active-directory-b2c-reference-custom-attr.md).
* [Предварительная версия Azure Active Directory B2C: включение многофакторной проверки подлинности в пользовательских приложениях](active-directory-b2c-reference-mfa.md).
* [Предварительная версия Azure Active Directory B2C: настройка самостоятельного сброса пароля для потребителей](active-directory-b2c-reference-sspr.md).
* [Настройка hello внешний вид и поведение регистрации, вход в систему и других страниц потребительском](active-directory-b2c-reference-ui-customization.md) обслуживаются Azure Active Directory B2C.
* [Используйте hello Azure Active Directory Graph API tooprogrammatically создание, чтение, обновление и удаление потребители](active-directory-b2c-devquickstarts-graph-dotnet.md) в клиенте Azure Active Directory B2C.

## <a name="next-steps"></a>Дальнейшие действия

Эти ссылки используются для изучения hello service в глубину.

* В разделе hello [сведения о ценах Azure Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).
* Ознакомьтесь с [примерами кода](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory&term=b2c) для Azure Active Directory B2C. 
* Получение справки о переполнении стека в с помощью hello [azure ad b2c](http://stackoverflow.com/questions/tagged/azure-ad-b2c) тег.
* Пришлите нам ваше мнение с помощью [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c), мы хотим toohear их!
* Просмотрите hello [ссылку Azure AD B2C протокол](active-directory-b2c-reference-protocols.md).
* Просмотрите hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md).
* Чтение hello [Azure Active Directory B2C часто задаваемые вопросы о](active-directory-b2c-faqs.md).
* [Предварительная версия Azure Active Directory B2C: регистрация запросов в службу поддержки](active-directory-b2c-support.md).

## <a name="get-security-updates-for-our-products"></a>Получение обновлений системы безопасности для наших продуктов

Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.

