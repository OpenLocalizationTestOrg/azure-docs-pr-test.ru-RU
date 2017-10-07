---
title: "библиотеки проверки подлинности aaaAzure Active Directory версии 2.0 | Документы Microsoft"
description: "Совместимые клиентские библиотеки и библиотеки по промежуточного слоя сервера и связанные библиотеки, источник и ссылки на образцы, для конечной v2.0 hello Azure Active Directory."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 19cec615-e51f-4141-9f8c-aaf38ff9f746
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: d7affdaac3a087b951d54d96fa68edde2a065172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-authentication-libraries"></a>Библиотеки проверки подлинности Azure Active Directory версии 2.0
Конечная точка, v2.0 Hello Azure Active Directory (Azure AD) поддерживает hello стандартных OAuth 2.0 и OpenID Connect 1.0 протоколов. Можно использовать различные библиотеки от корпорации Майкрософт и других организаций с конечной точкой v2.0 hello.

При создании приложения, которое использует конечную точку v2.0 hello, мы рекомендуем использовать библиотеки, написанные с протокола специалистами в предметной области, использующих методологию Security Development Lifecycle (SDL), таких как [hello один следуют Microsoft] [Microsoft-SDL]. В случае кода toohand поддержка протоколов hello, рекомендуется следовать методологии SDL и уделять особое внимание toohello вопросы безопасности в спецификации hello стандартов для каждого протокола.

## <a name="types-of-libraries"></a>Типы библиотек
Azure AD версии 2.0 поддерживает два типа библиотек.

* **Клиентские библиотеки.** Собственный клиенты и серверы используют токены доступа tooget библиотеки клиента для вызова ресурса, например Microsoft Graph.
* **Серверные библиотеки ПО промежуточного слоя.** Веб-приложения используют серверные библиотеки ПО промежуточного слоя для входа пользователей. Веб-API использовать сервер библиотеки по промежуточного слоя toovalidate маркеров, отправляемых по собственных клиентов или по другим серверам.

## <a name="library-support"></a>Поддержка библиотек
Поскольку вы можете выбрать любой совместимый со стандартами библиотеку, при использовании конечной точки v2.0 hello, это важно tooknow где toogo для поддержки. Проблемы и запрашивать новые функции в коде библиотеки обратитесь в службу hello библиотеки владельца. Проблемы и запрашивать новые функции в реализации протокола на стороне службы hello обратитесь в Майкрософт.

Для библиотек предусмотрено две категории поддержки:

* **Библиотеки, поддерживаемые корпорацией Майкрософт.** Корпорация Майкрософт предоставляет исправления для этих библиотек, к тому же она провела для них комплексную экспертизу жизненного цикла разработки защищенных приложений.
* **Совместимые библиотеки.** Корпорация Майкрософт протестировала эти библиотеки в основных сценариях и подтверждает, что они работают с конечной точкой v2.0 hello. Корпорация Майкрософт не предоставляет исправления для этих библиотек и не выполняла их проверку. Проблемы и запрашивать новые функции должно быть проект с открытым исходным направленной toohello библиотеки.

Список библиотек, которые работают с конечной точкой v2.0 hello разделах hello далее в этой статье.


## <a name="microsoft-supported-client-libraries"></a>Клиентские библиотеки, поддерживаемые корпорацией Майкрософт

> [!IMPORTANT]
> Hello MSAL предварительной версии библиотеки пригодные для использования в рабочей среде. Мы предоставляем hello же соответствующий уровень поддержки для этих библиотек, как это было сделано наши текущие библиотеки в рабочей среде (ADAL). Во время предварительного просмотра hello мы можем сделать изменения toohello MSAL API формат внутреннего кэша и другие механизмы этих библиотек, без предварительного уведомления, которое будет иметь необходимых tootake вместе с исправления или улучшения функций. Это может повлиять на приложение. Для экземпляра кэша формате toohello изменение может повлиять на пользователей, например, требуя их toosign в снова. API-Интерфейс может требовать вы tooupdate кода. Когда мы предоставляем hello общедоступный выпуск, вам будет нужно tooupdate toohello общедоступной версии в течение шести месяцев, как приложения, написанные с использованием Предварительный просмотр версия библиотеки может перестать работать.

| Платформа | Библиотека | Загрузить | Исходный код | Образец | Справочные материалы
| --- | --- | --- | --- | --- | --- |
| Клиент .NET, Магазин Windows, UWP, Xamarin iOS и Android | MSAL для .NET (предварительная версия) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Классическое приложение](guidedsetups/active-directory-mobileanddesktopapp-windowsdesktop-intro.md) |  |
| JavaScript | MSAL.js (предварительная версия) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Одностраничное приложение](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi-v2) |  |
| iOS, macOS | MSAL (предварительная версия) | [GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Приложение iOS](https://github.com/Azure-Samples/active-directory-msal-ios-swift) |  |
| Android | MSAL (предварительная версия) | [Hello центральный репозиторий](https://repo1.maven.org/maven2/com/microsoft/identity/client/msal/) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Приложение Android](guidedsetups/active-directory-mobileanddesktopapp-android-intro.md) | [Javadocs](http://javadoc.io/doc/com.microsoft.identity.client/msal) |

## <a name="microsoft-supported-server-middleware-libraries"></a>Серверные библиотеки ПО промежуточного слоя, поддерживаемые корпорацией Майкрософт

| Платформа | Библиотека | Загрузить | Исходный код | Образец | Справочные материалы
| --- | --- | --- | --- | --- | --- |
| .NET 4.x | ПО промежуточного слоя OWIN OpenID Connect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Приложение MVC](guidedsetups/active-directory-serversidewebapp-aspnetwebappowin-intro.md) | |
| .NET 4.x | ПО промежуточного слоя носителя OWIN OAuth для AzureAD |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |  | |
| .NET 4.x | Обработчик JWT для .NET 4.5 | [NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/4.0.4.403061554) | [GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET Core | ПО промежуточного слоя ASP.NET OpenID Connect |[Microsoft.AspNetCore.Authentication.OpenIdConnect (NuGet)][ServerLib-NetCore-Owin-Oidc-Lib] |[Безопасность ASP.NET (GitHub)][ServerLib-NetCore-Owin-Oidc-Repo] |[Приложение MVC](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2) |
| .NET Core | ПО промежуточного слоя носителя ASP.NET OAuth |[Microsoft.AspNetCore.Authentication.OAuth (NuGet)][ServerLib-NetCore-Owin-Oauth-Lib] |[Безопасность ASP.NET (GitHub)][ServerLib-NetCore-Owin-Oauth-Repo] |  |
| .NET Core | Обработчик JWT для .NET Core  |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Веб-приложение](active-directory-v2-devquickstarts-node-web.md)| |

## <a name="compatible-client-libraries"></a>Совместимые клиентские библиотеки
| Платформа | Имя библиотеки | Проверенные версии | Исходный код | Образец |
|:---:|:---:|:---:|:---:|:---:|
| Android |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib/wiki) |0.2.1 |[OIDCAndroidLib](https://github.com/kalemontes/OIDCAndroidLib) |[Пример встроенного приложения](active-directory-v2-devquickstarts-android.md) |
| iOS |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |1.2.8 |[NXOAuth2Client](https://github.com/nxtbgthng/OAuth2Client) |[Пример встроенного приложения](active-directory-v2-devquickstarts-ios.md) |
| JavaScript |[Hello.js](https://adodson.com/hello.js/) |1.13.5 |[Hello.js](https://github.com/MrSwitch/hello.js) |[Безопасная проверка пароля](https://github.com/Azure-Samples/active-directory-javascript-graphapi-web-v2) |

## <a name="compatible-server-middleware-libraries"></a>Совместимые серверные библиотеки ПО промежуточного слоя
| Платформа | Имя библиотеки | Проверенные версии | Исходный код | Образец |
|:---:|:---:|:---:|:---:|:---:|
| Java | [Scribe Java (scribejava)](https://github.com/scribejava/scribejava) | [Версия 3.2.0](https://github.com/scribejava/scribejava/releases/tag/scribejava-3.2.0) | [ScribeJava](https://github.com/scribejava/scribejava/archive/scribejava-3.2.0.zip) | |
| PHP | [Hello лиги PHP oauth2-клиента](https://github.com/thephpleague/oauth2-client) | [Версия 1.4.2](https://github.com/thephpleague/oauth2-client/releases/tag/1.4.2) | [oauth2-client](https://github.com/thephpleague/oauth2-client/archive/1.4.2.zip) | |
| Python-Flask |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |0.9.3 |[Flask-OAuthlib](https://github.com/lepture/flask-oauthlib) |[Веб-приложение](https://github.com/Azure-Samples/active-directory-python-flask-graphapi-web-v2) |
| Ruby |[OmniAuth](https://github.com/omniauth/omniauth/wiki) |omniauth:1.3.1</br>omniauth-oauth2:1.4.0 |[OmniAuth](https://github.com/omniauth/omniauth)</br>[OmniAuth OAuth2](https://github.com/intridea/omniauth-oauth2) |  |

## <a name="related-content"></a>Связанная информация
Дополнительные сведения о конечной точке v2.0 hello Azure AD см. в разделе hello [Обзор v2.0 модели приложений Azure AD][AAD-App-Model-V2-Overview].

<!--Image references-->

<!--Reference style links -->
[AAD-App-Model-V2-Overview]: ../active-directory-appmodel-v2-overview.md
[ClientLib-NET-Lib]: http://www.nuget.org/packages/Microsoft.Identity.Client
[ClientLib-NET-Repo]: https://github.com/AzureAD/microsoft-authentication-library-for-dotnet
[ClientLib-NET-Sample]: active-directory-v2-devquickstarts-wpf.md
[ClientLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ClientLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad
[ClientLib-Node-Sample]:/
[ClientLib-Iosmac-Lib]:/
[ClientLib-Iosmac-Repo]:/
[ClientLib-Iosmac-Sample]:/
[ClientLib-Android-Lib]:/
[ClientLib-Android-Repo]:/
[ClientLib-Android-Sample]:/
[ClientLib-Js-Lib]:/
[ClientLib-Js-Repo]:/
[ClientLib-Js-Sample]:/

[Microsoft-SDL]: http://www.microsoft.com/sdl/default.aspx
[ServerLib-Net4-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/
[ServerLib-Net4-Owin-Oidc-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oidc-Sample]: active-directory-v2-devquickstarts-dotnet-web.md
[ServerLib-Net4-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.Owin.Security.OAuth/
[ServerLib-Net4-Owin-Oauth-Repo]: http://katanaproject.codeplex.com/
[ServerLib-Net4-Owin-Oauth-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-dotnet-api/
[ServerLib-Net-Jwt-Lib]: https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt
[ServerLib-Net-Jwt-Repo]: https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet
[ServerLib-Net-Jwt-Sample]:/
[ServerLib-NetCore-Owin-Oidc-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect/
[ServerLib-NetCore-Owin-Oidc-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oidc-Sample]: https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect-aspnetcore-v2
[ServerLib-NetCore-Owin-Oauth-Lib]: https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OAuth/
[ServerLib-NetCore-Owin-Oauth-Repo]: https://github.com/aspnet/Security
[ServerLib-NetCore-Owin-Oauth-Sample]:/
[ServerLib-Node-Lib]: https://www.npmjs.com/package/passport-azure-ad
[ServerLib-Node-Repo]: https://github.com/AzureAD/passport-azure-ad/
[ServerLib-Node-Sample]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-v2-devquickstarts-node-web/
