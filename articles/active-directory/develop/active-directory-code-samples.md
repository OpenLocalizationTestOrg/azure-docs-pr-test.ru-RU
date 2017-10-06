---
title: "Примеры кода для Active Directory aaaAzure | Документы Microsoft"
description: "Список примеров кода Azure Active Directory, сгруппированных по сценарию."
services: active-directory
documentationcenter: dev-center-name
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: a242a5ff-7300-40c2-ba83-fb6035707433
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: mbaldwin
ms.custom: aaddev
ms.openlocfilehash: 921ce08766cc6e29a6db2c4f38d216e6de11730f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-code-samples"></a>Примеры кода Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Можно использовать Microsoft Azure Active Directory (Azure AD) tooadd проверки подлинности и авторизации tooyour веб-приложений и веб-API. Этот раздел перенаправит вас toosamples, показывающие, как это можно сделать и фрагменты кода, которые можно использовать в приложениях. На странице примеров кода hello, вы найдете подробные чтения — мне статьи, которые помогут с требованиями, установке и настройке. А hello код комментариями toohelp понять критические секции hello.

toounderstand hello базовый сценарий для каждого типа примера в разделе сценарии проверки подлинности Azure AD.

Передавать образцы tooour на GitHub: [примеров Microsoft Azure Active Directory и документация](https://github.com/Azure-Samples?page=3&query=active-directory).

## <a name="web-browser-tooweb-application"></a>Веб-браузер tooWeb приложения
В этих примерах показано, как toowrite веб-приложение, направляющее hello toosign браузера пользователя в tooAzure AD.

| Язык или платформа | Образец | Описание |
| --- | --- | --- |
| C#/.NET |[WebApp-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Используйте OpenID Connect (по промежуточного слоя ASP.Net OpenID Connect OWIN) tooauthenticate пользователей из клиента Azure AD. |
| C#/.NET |[WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Несколькими клиентами .NET MVC веб-приложения, использующего OpenID Connect (по промежуточного слоя ASP.Net OpenID Connect OWIN) tooauthenticate пользователей из нескольких клиентов Azure AD. |
| C#/.NET |[WebApp-WSFederation-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-wsfederation) |Используйте WS-Federation (по промежуточного слоя ASP.Net WS-Federation OWIN) tooauthenticate пользователей из клиента Azure AD. |

## <a name="single-page-application-spa"></a>Одностраничное приложение (SPA)
В этом примере показано, как toowrite приложение на одной странице защищен с помощью Azure AD.  

| Язык или платформа | Образец | Описание |
| --- | --- | --- |
| JavaScript, C#/.NET |[SinglePageApp-DotNet](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) |Используйте ADAL для JavaScript и Azure AD toosecure основе AngularJS приложения на одной странице реализуется с помощью серверной части веб-API ASP.NET. |

## <a name="native-application-tooweb-api"></a>TooWeb собственного приложения API
В этих примерах кода показано, как toobuild собственные клиентские приложения, которые вызывают веб-API, защищенные Azure AD. Они используют [библиотеку проверки подлинности Azure AD (ADAL)](active-directory-authentication-libraries.md) и [OAuth 2.0 в Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Язык или платформа | Образец | Описание |
| --- | --- | --- |
| JavaScript |[NativeClient-MultiTarget-Cordova](https://github.com/Azure-Samples/active-directory-cordova-multitarget) |Используйте ADAL hello подключаемого модуля для Apache Cordova toobuild приложении Apache Cordova, который вызывает веб-API и использует Azure AD для проверки подлинности. |
| C#/.NET |[NativeClient-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) |Приложение .NET WPF, которое вызывает веб-интерфейс API, защищенный с помощью Azure AD. |
| C#/.NET |[NativeClient-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Приложение Магазина Windows, которое вызывает веб-интерфейс API, защищенный с помощью Azure AD. |
| C#/.NET |[NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/Azure-Samples/active-directory-dotnet-webapi-multitenant-windows-store) |Приложение Магазина Windows, которое вызывает мультитенантный веб-интерфейс API, защищенный с помощью Azure AD. |
| C#/.NET |[WebAPI-OnBehalfOf-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof) |Собственного клиентского приложения, вызывающий веб-API, который получает маркер tooact от имени исходного пользователя hello, а затем использует hello маркера toocall другой веб-API. |
| C#/.NET |[NativeClient-WindowsPhone8.1](https://github.com/Azure-Samples/active-directory-dotnet-windowsphone-8.1) |Приложение Магазина Windows для Windows Phone 8.1, которое вызывает веб-интерфейс API, защищенный с помощью Azure AD. |
| ObjC |[NativeClient-iOS](https://github.com/Azure-Samples/active-directory-ios) |Приложение iOS, которое вызывает веб-интерфейс API, необходимый для проверки подлинности Azure AD. |
| C#/.NET |[WebAPI-ManuallyValidateJwt-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation) |Собственное клиентское приложение, включающее tooprocess логику токена JWT в веб-API, вместо использования по промежуточного слоя OWIN. |
| C#/Xamarin |[NativeClient-Xamarin-Android](https://github.com/Azure-Samples/active-directory-xamarin-android) |Привязка toohello собственного Azure AD Xamarin библиотеки проверки подлинности (ADAL) для hello библиотеку Android. |
| C#/Xamarin |[NativeClient-Xamarin-iOS](https://github.com/Azure-Samples/active-directory-xamarin-ios) |Toohello привязки Xamarin native Azure AD библиотеки проверки подлинности (ADAL) для операций ввода-вывода. |
| C#/Xamarin |[NativeClient-MultiTarget-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-multitarget) |Проект Xamarin, имеющий пять целевых платформ и выполняющий вызовы веб-интерфейса API, защищенного с помощью Azure AD. |
| C#/.NET |[NativeClient-Headless-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-native-headless) |Собственное приложение, имеющее пять целевых платформ и выполняющее вызовы веб-интерфейса API, защищенного с помощью Azure AD. |

## <a name="web-application-tooweb-api"></a>Веб-приложения tooWeb API
В этих примерах кода показано, как использовать [OAuth 2.0 в Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) toobuild веб-приложений, которые вызывают веб-API, защищенные Azure AD.

| Язык или платформа | Образец | Описание |
| --- | --- | --- |
| C#/.NET |[WebApp-WebAPI-OpenIDConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-openidconnect) |Вызов веб-API с разрешениями hello выполнившего вход пользователя. |
| C#/.NET |[WebApp-WebAPI-OAuth2-AppIdentity-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity) |Вызов веб-API с разрешениями приложения hello. |
| C#/.NET |[WebApp-WebAPI-OAuth2-UserIdentity-Dotnet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-useridentity) |Добавьте авторизацию с [OAuth 2.0 в Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooan существующего веб-приложения, оно может вызвать веб-API. |
| JavaScript |[WebAPI-Nodejs](https://github.com/Azure-Samples/active-directory-node-webapi) |Настройка службы API REST, интегрированной с Azure AD, для защиты API. Включает сервер Node.js с веб-интерфейсом API. |
| C#/.NET |[WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-multitenant-openidconnect) |Многопользовательское MVC веб-приложение, использующее OpenID Connect (по промежуточного слоя ASP.Net OpenID Connect OWIN) tooauthenticate пользователей из клиента Azure AD. Использует hello tooinvoke код авторизации Graph API. |

## <a name="server-or-daemon-application-tooweb-api"></a>Сервер или приложение управляющей программы tooWeb API
В этих примерах кода показано, как toobuild управляющая программа или серверное приложение, получает ресурсы из веб-API с помощью [библиотеки проверки подлинности Azure AD (ADAL)](active-directory-authentication-libraries.md) и [OAuth 2.0 в Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx).

| Язык или платформа | Образец | Описание |
| --- | --- | --- |
| C#/.NET |[Daemon-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon) |Консольное приложение, выполняющее вызовы веб-интерфейса API. Hello учетных данных клиента являются паролем. |
| C#/.NET |[Daemon-CertificateCredential-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential) |Консольное приложение, выполняющее вызовы веб-интерфейса API. Hello учетных данных клиента является сертификатом. |

## <a name="calling-azure-ad-graph-api"></a>Вызов Graph API Azure AD
В этих примерах кода показано, как toobuild приложения, вызывающие hello Azure AD Graph API tooread и запись данных каталога.

| Язык или платформа | Образец | Описание |
| --- | --- | --- |
| Java |[WebApp-GraphAPI-Java](https://github.com/Azure-Samples/active-directory-java-graphapi-web) |Веб-приложения, использующего Graph API hello tooaccess данным каталога Azure AD. |
| PHP |[WebApp-GraphAPI-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-web) |Веб-приложения, использующего Graph API hello tooaccess данным каталога Azure AD. |
| C#/.NET |[WebApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Веб-приложения, использующего Graph API hello tooaccess данным каталога Azure AD. |
| C#/.NET |[ConsoleApp-GraphAPI-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-console) |Это консольное приложение демонстрирует общие чтение и запись вызовы toohello Graph API и показано, как пользователь tooexecute назначения лицензии и обновить эскиз фотографии и ссылки для пользователя. |
| C#/.NET |[ConsoleApp-GraphAPI-DiffQuery-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-diffquery) |Консольное приложение, которое использует разностный запрос hello в периодических tooget Graph API hello изменяет toouser объектов в клиенте Azure AD. |
| C#/.NET |[WebApp-GraphAPI-DirectoryExtensions-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-directoryextensions-web) |Приложение MVC использует toogenerate запросы Graph API простой диаграммы организации. |
| PHP |[WebApp-GraphAPI-DirectoryExtensions-PHP](https://github.com/Azure-Samples/active-directory-php-graphapi-directoryextensions-web) |Приложение PHP, которое вызывает Graph API tooregister hello расширением и затем читать, обновление и удаление значений в атрибуте расширения hello. |

## <a name="authorization"></a>Авторизация
Эти образцы Показать кода как toouse Azure AD для авторизации.

| Язык или платформа | Образец | Описание |
| --- | --- | --- |
| C#/.NET |[WebApp-GroupClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-groupclaims) |Выполнение управления доступом на основе ролей (RBAC) с помощью утверждений о группах Azure Active Directory в приложении, которое интегрировано с Azure AD. |
| C#/.NET |[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) |Выполнение управления доступом на основе ролей (RBAC) с помощью ролей приложения Azure Active Directory в приложении, которое интегрировано с Azure AD. |

## <a name="legacy-walkthroughs"></a>Предыдущие пошаговые руководства
В этих пошаговых руководствах используется более старая технология, но она также может представлять интерес.

| Язык или платформа | Образец | Описание |
| --- | --- | --- |
| C#/.NET |[Авторизация на основе ролей и на основе ACL в приложении Microsoft Azure AD](http://go.microsoft.com/fwlink/?LinkId=331694) |Выполнение авторизации на основе роли (RBAC) и авторизации на основе ACL в приложении, интегрированным Azure AD. |
| C#/.NET |[AAL — служба tooREST приложения магазина Windows — проверка подлинности](http://go.microsoft.com/fwlink/?LinkId=330605) |Используйте [библиотеки проверки подлинности Azure AD (ADAL)](active-directory-authentication-libraries.md) (ранее AAL) для бета-версии магазина Windows tooadd пользователя проверки подлинности возможности tooa приложения для магазина Windows. |
| C#/.NET |[ADAL — собственное приложение службы tooREST - проверка подлинности с помощью диалогового окна браузера AAD](http://go.microsoft.com/fwlink/?LinkId=259814) |Используйте [библиотеки проверки подлинности Azure AD (ADAL)](active-directory-authentication-libraries.md) клиент WPF tooa возможности проверки подлинности tooadd пользователя. |
| C#/.NET |[ADAL — собственное приложение службы tooREST - проверка подлинности с помощью диалогового окна браузера ACS](http://code.msdn.microsoft.com/AAL-Native-App-to-REST-de57f2cc) |Используйте [библиотеки проверки подлинности Azure AD (ADAL)](active-directory-authentication-libraries.md) и [2.0 службы контроля доступа (ACS)](http://msdn.microsoft.com/library/azure/hh147631.aspx) клиент WPF tooa возможности проверки подлинности tooadd пользователя. |
| C#/.NET |[ADAL - tooServer сервера проверки подлинности](http://go.microsoft.com/fwlink/?LinkId=259816) |Используйте [библиотеки проверки подлинности Azure AD (ADAL)](active-directory-authentication-libraries.md) toosecure вызовов службы от tooan процесса стороны сервера службы MVC4 Web API REST. |
| C#/.NET |[Добавление tooYour входа Web приложения с помощью Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) |Настройте .NET приложение tooperform web единого входа для вашего каталога Azure AD предприятия. |
| C#/.NET |[Разработка мультитенантных веб-приложений с помощью Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-multitenant-openidconnect) |Использование Azure AD tooadd toohello единого входа и возможности доступа к каталогу одного toowork приложения .NET в нескольких организациях. |
| Java |[Образец приложения Java для API Graph Azure AD](http://go.microsoft.com/fwlink/?LinkId=263969) |Используйте данные каталога tooaccess hello Graph API из Azure AD. |
| PHP |[Образец приложения PHP для API Graph Azure AD](http://code.msdn.microsoft.com/PHP-Sample-App-For-Windows-228c6ddb) |Используйте данные каталога tooaccess hello Graph API из Azure AD. |
| C#/.NET |[Образец приложения для API Graph Azure AD](http://go.microsoft.com/fwlink/?LinkID=262648) |Используйте данные каталога tooaccess hello Graph API из Azure AD. |
| C#/.NET |[Образец приложения для дифференциального запроса Azure AD Graph](http://go.microsoft.com/fwlink/?LinkId=275398) |Используйте разностный запрос hello в hello Graph API tooget периодических изменений toouser объектов в клиенте Azure AD. |
| C#/.NET |[Образец приложения для интеграции мультитенантного облачного приложения с Azure AD](http://go.microsoft.com/fwlink/?LinkId=275397) |Интеграция мультитенантного приложения в Azure AD. |
| C#/.NET |[Защита приложения Магазина Windows и веб-службы REST с помощью Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-windows-store) |Создание простого веб-API ресурса и клиентского приложения для магазина Windows с помощью Azure AD и hello [библиотеки проверки подлинности Azure AD (ADAL)](active-directory-authentication-libraries.md). |
| C#/.NET |[С помощью tooQuery hello Graph API Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-graphapi-web) |Настройте hello toouse приложения Microsoft .NET API Azure AD Graph tooaccess данных из каталога клиента Azure AD. |

## <a name="see-also"></a>См. также
##### <a name="other-resources"></a>Другие ресурсы
[Руководство разработчика по Azure Active Directory](active-directory-developers-guide.md)

[Основные понятия и справочные материалы по Azure AD API Graph](https://msdn.microsoft.com/library/azure/hh974476.aspx)

[Библиотека вспомогательных методов для Azure AD Graph API](https://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)
