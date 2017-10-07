---
title: "aaaAzure библиотеки проверки подлинности Active Directory | Документы Microsoft"
description: "Hello библиотеки проверки подлинности Azure AD (ADAL) позволяет клиентским разработчикам приложений tooeasily проверки подлинности пользователей toocloud или локальной Active Directory (AD) и затем получать токены доступа для безопасных вызовов API."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: mbaldwin
ms.assetid: 2e4fc79a-0285-40be-8c77-65edee408a22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 20fae18807ef03463ab1bc218e5f3548b5bd5717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-authentication-libraries"></a>Библиотеки проверки подлинности Azure Active Directory
Разработчики Hello Azure Active Directory Authentication библиотеки (ADAL) включает клиентского приложения tooeasily проверки подлинности пользователей toocloud локальной Active Directory (AD) и получать токены доступа для безопасных вызовов API. ADAL упрощает для разработчиков работу с проверкой подлинности, предоставляя такие возможности, как:
 - поддержка асинхронных вызовов методов;
 - настраиваемый кэш маркеров, в котором хранятся маркеры доступа и маркеры обновления;
 - автоматическое обновление маркеров после истечения срока их действия, если доступен маркер обновления;
 - и многое другое.
 
Обрабатывая самые hello сложности, ADAL помогает разработчикам сосредоточиться на бизнес-логики и легко защитить ресурсы, не имея экспертом по безопасности.

ADAL доступна на различных платформах.

### <a name="client-libraries"></a>Клиентские библиотеки

| Платформа | Библиотека | Загрузить | Исходный код | Образец | Справочные материалы
| --- | --- | --- | --- | --- | --- |
| Клиент .NET, Магазин Windows, UWP, Xamarin iOS и Android |MSAL для .NET (предварительная версия) |[NuGet](https://www.nuget.org/packages/Microsoft.Identity.Client/1.1.0-preview) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Классическое приложение](~/articles/active-directory/develop/guidedsetups/active-directory-windesktop.md) |[Справочные материалы](https://docs.microsoft.com/dotnet/api/?view=identityclient-1.1.0-preview) | 
| JavaScript |MSAL для JavaScript (предварительная версия) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-js) | [Одностраничное приложение](~/articles/active-directory/develop/GuidedSetups/active-directory-javascriptspa.md) | [Справочные материалы](https://htmlpreview.github.io/?https://raw.githubusercontent.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/docs/classes/_useragentapplication_.msal.useragentapplication.html) | 
| iOS |MSAL для iOS (предварительная версия) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-objc) | [Приложение iOS](~/articles/active-directory/develop/GuidedSetups/active-directory-ios.md) | [Справочные материалы](https://azuread.github.io/docs/objc/) |
| Android |MSAL для Android (предварительная версия) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) |[GitHub](https://github.com/AzureAD/microsoft-authentication-library-for-android) | [Приложение Android](~/articles/active-directory/develop/GuidedSetups/active-directory-android.md) | [Справочные материалы](http://javadoc.io/doc/com.microsoft.identity.client/msal/0.1.1) |
| Клиент .NET, Магазин Windows, UWP, Xamarin iOS и Android |ADAL .NET версии 3 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) | [Классическое приложение](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-dotnet) |[Справочные материалы](https://docs.microsoft.com/dotnet/api/?view=identitymodelclientsad-3.13.9) | 
| Клиент .NET, Магазин Windows, Windows Phone 8.1 |ADAL .NET версии 2 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/2.28.4) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/releases/tag/v2.28.4) | [Классическое приложение](https://github.com/AzureADQuickStarts/NativeClient-DotNet/releases/tag/v2.X) | | 
| JavaScript |ADAL.js |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-js) |[Одностраничное приложение](https://github.com/Azure-Samples/active-directory-javascript-singlepageapp-dotnet-webapi) | |
| iOS, macOS |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc/releases) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-objc) |[Приложение iOS](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-ios) | [Справочные материалы](https://cocoapods.org/pods/ADAL)|
| Android |ADAL |[Hello центральный репозиторий](http://search.maven.org/remotecontent?filepath=com/microsoft/aad/adal/) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android) |[Приложение Android](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-android) | [Javadocs](http://javadoc.io/doc/com.microsoft.aad/adal/)|
| Node.js |ADAL |[npm](https://www.npmjs.com/package/adal-node) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs) | | |
| Java |ADAL4J |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) |[Устранение неполадок, а также вопросы и ответы по Application Insights для Java](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-java) | |
| Python |ADAL |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) |[GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-python) | | |
### <a name="server-libraries"></a>Серверные библиотеки 

| Платформа | Библиотека | Загрузить | Исходный код | Образец | Справочные материалы
| --- | --- | --- | --- | --- | --- |
| .NET |OWIN для AzureAD|[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.ActiveDirectory/) |[CodePlex](http://katanaproject.codeplex.com) |[Приложение MVC](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapp-dotnet) | |
| .NET |OWIN для OpenIDConnect |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect) |[CodePlex](http://katanaproject.codeplex.com) |[Веб-приложение](https://github.com/AzureADSamples/WebApp-OpenIDConnect-DotNet) | |
| Node.js |Azure AD Passport |[npm](https://www.npmjs.com/package/passport-azure-ad) |[GitHub](https://github.com/AzureAD/passport-azure-ad) | [Веб-интерфейс API](https://docs.microsoft.com/azure/active-directory/active-directory-devquickstarts-webapi-nodejs)| |
| .NET |OWIN для WS-Federation |[NuGet](https://www.nuget.org/packages/Microsoft.Owin.Security.WsFederation) |[CodePlex](http://katanaproject.codeplex.com) |[Веб-приложение MVC](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) | |
| .NET |Расширения протокола удостоверения для .NET 4.5 |[NuGet](https://www.nuget.org/packages/Microsoft.IdentityModel.Protocol.Extensions) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |
| .NET |Обработчик JWT для .NET 4.5 |[NuGet](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt) |[GitHub](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet) | | |



## <a name="scenarios"></a>Сценарии

Ниже приведены три типичных сценария, в которых ADAL может использоваться для проверки подлинности клиента, обращающегося к удаленному ресурсу.  

### <a name="authenticating-users-of-a-native-client-application-running-on-a-device"></a>Проверка подлинности пользователей собственного клиентского приложения, выполняющегося на устройстве 

В этом сценарии у разработчика есть клиентское приложение WPF, которому требуется tooaccess удаленному ресурсу, защищенному Azure AD, например веб-API. Он имеет подписку Azure, знает, как tooinvoke hello нижестоящий веб-API и знает hello Azure клиента AD, который использует веб-API hello. В результате он использовать проверку подлинности ADAL toofacilitate с Azure AD, полностью делегируя tooADAL возможности проверки подлинности hello или явно обрабатывая учетные данные пользователя. ADAL упрощает легко tooauthenticate hello пользователя, получить маркер доступа и токен обновления от Azure AD и воспользуйтесь hello access token toomake запросов toohello веб-API.

Образец кода, демонстрирующий этот сценарий с использованием проверки подлинности tooAzure AD, в разделе [tooWeb собственное клиентское приложение WPF API](https://github.com/azureadsamples/nativeclient-dotnet).

### <a name="authenticating-a-confidential-client-application-running-on-a-web-server"></a>Проверка подлинности конфиденциального клиентского приложения, выполняющегося на веб-сервере

В этом сценарии у разработчика есть приложение, запущенное на сервере, которому требуется tooaccess удаленному ресурсу, защищенному Azure AD, например веб-API. Он имеет подписку Azure, знает, как tooinvoke hello нижестоящие службы и известно, что hello веб-клиента hello Azure AD API. В результате он ADAL toofacilitate проверки подлинности можно использовать с Azure AD, явно обрабатывая учетные данные приложения hello. ADAL делает его легко tooretrieve токена от Azure AD, используя учетные данные клиента приложения hello, а затем использовать этот токен toomake запросов toohello веб-API. ADAL также обрабатывает управление временем существования hello hello токен доступа, кэшируя его и возобновляя действие при необходимости. Образец кода, демонстрирующий этот сценарий, в разделе [tooWeb приложения консоли управляющей программы API](https://github.com/AzureADSamples/Daemon-DotNet).

### <a name="authenticating-a-confidential-client-application-running-on-a-server-on-behalf-of-a-user"></a>Проверка подлинности конфиденциального клиентского приложения, выполняющегося на веб-сервере, от имени пользователя 

В этом сценарии у разработчика есть приложение, запущенное на сервере, которому требуется tooaccess удаленному ресурсу, защищенному Azure AD, например веб-API. Hello запрос также должен toobe выполняются от имени пользователя Azure AD. Он имеет подписку Azure, знает, как tooinvoke hello нижестоящий веб-API и известно, что использует hello службе hello клиента Azure AD. После hello пользователя toohello прошедшего проверку подлинности веб-приложения, приложение hello может получить код авторизации для пользователя hello из Azure AD. веб-приложение Hello затем можно использовать ADAL tooobtain маркер доступа и токен обновления от имени пользователя с помощью hello авторизации кода и клиентских учетных данных, связанных с приложением hello из Azure AD. После токена доступа hello присутствует hello веб-приложения, его можно вызывать hello веб-API до истечения срока действия маркера hello. По истечении срока действия маркера hello hello веб-приложения можно использовать ADAL tooget новый маркер доступа с помощью полученного ранее токена обновления hello. Образец кода, демонстрирующий этот сценарий, в разделе [tooWeb tooWeb API собственного клиента API](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof).

## <a name="see-also"></a>См. также

- [Здравствуйте, руководство разработчика Azure Active Directory](active-directory-developers-guide.md)
- [Сценарии проверки подлинности в Azure Active Directory](active-directory-authentication-scenarios.md)
- [Примеры кода Azure Active Directory](active-directory-code-samples.md)
