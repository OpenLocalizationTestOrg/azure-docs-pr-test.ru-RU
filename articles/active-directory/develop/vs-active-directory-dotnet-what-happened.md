---
title: "внесенные aaaChanges tooa MVC проекта при подключении tooAzure AD | Документы Microsoft"
description: "Описывает, что происходит проекта MVC tooyour при подключении tooAzure AD с помощью Visual Studio подключенных служб"
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>Какая ошибка toomy проекта MVC (Visual Studio Azure Active Directory подключенных служб)?
> [!div class="op_single_selector"]
> * [Приступая к работе](vs-active-directory-dotnet-getting-started.md)
> * [Что произошло?](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Добавлены ссылки
### <a name="nuget-package-references"></a>Ссылки на пакет NuGet
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>Ссылки на .NET
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>Добавлен код
### <a name="code-files-were-added-tooyour-project"></a>Файлы кода были добавлены tooyour проекта
Класс запуска проверки подлинности, **App_Start/Startup.Auth.cs** был добавлен tooyour проект, содержащий логику запуска для проверки подлинности Azure AD. Кроме того, добавлен класс контролера Controllers/AccountController.cs, который содержит методы **SignIn()** и **SignOut()**. Наконец, добавлено частичное представление **Views/Shared/_LoginPartial.cshtml**, содержащее ссылку действия для SignIn и SignOut.

### <a name="startup-code-was-added-tooyour-project"></a>Код запуска был добавлен tooyour проекта
Если класс запуска уже есть в вашем проекте, hello **конфигурации** метод было обновленные tooinclude вызов слишком**ConfigureAuth(app)**. В противном случае класс запуска была добавлена tooyour проекта.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>В файл app.config или web.config добавлены значения конфигурации
были добавлены следующие записи конфигурации Hello.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>Было создано приложение Azure Active Directory (AD)
Приложения Azure AD был создан в каталоге hello, выбранная в мастере hello.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Если после проверки *отключить проверку подлинности учетных записей отдельных пользователей*, какие дополнительные изменения были сделаны toomy проекта?
Удалены ссылки на пакет NuGet. Для файлов созданы резервные копии, а сами файлы удалены. В зависимости от состояния hello проекта вы можете иметь toomanually удалите дополнительные материалы или файлы или измените код соответствующим образом.

### <a name="nuget-package-references-removed-for-those-present"></a>Ссылки на существующие пакеты NuGet удалены
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Для существующих файлов кода созданы резервные копии, а сами файлы удалены.
Каждый из следующих файлов был заархивирован и удален из проекта hello. Файлы резервных копий расположены в папке «Backup» в корневой каталог проекта hello hello.

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>Для существующих файлов кода созданы резервные копии
Для каждого из следующих файлов создана резервная копия, после чего файлы были заменены. Файлы резервных копий расположены в папке «Backup» в корневой каталог проекта hello hello.

* **Startup.cs.**
* **App_Start\Startup.Auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Если после проверки *читать данные каталога*, какие дополнительные изменения были сделаны toomy проекта?
Добавлены дополнительные ссылки.

### <a name="additional-nuget-package-references"></a>Дополнительные ссылки на пакет NuGet
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Дополнительные ссылки на .NET
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>Дополнительные файлы кода были добавлены tooyour проекта
Два файла были добавлены toosupport кэширования токенов: **Models\ADALTokenCache.cs** и **Models\ApplicationDbContext.cs**.  Доступ к сведениям профиля пользователя с помощью Azure graph API-интерфейсы tooillustrate были добавлены дополнительного контроллера и представления.  Они содержатся в файлах **Controllers\UserProfileController.cs** и **Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-tooyour-project"></a>Дополнительный код запуска был добавлен tooyour проекта
В hello **startup.auth.cs** файл, новый **OpenIdConnectAuthenticationNotifications** объект был добавлен toohello **уведомления** членом hello  **OpenIdConnectAuthenticationOptions**.  Это tooenable получение кода OAuth hello и обмен его маркера доступа.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Были внесены дополнительные изменения tooyour app.config или web.config
Hello следующие дополнительные настройки записи были добавлены.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

Hello следующих разделов конфигурации и строка подключения были добавлены.

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a>Обновлено приложение Azure Active Directory
Приложение Azure Active Directory была hello обновленные tooinclude *читать данные каталога* разрешений и дополнительный раздел был создан, затем которой использовался как hello *ida: ClientSecret* в hello  **Web.config** файла.

## <a name="next-steps"></a>Дальнейшие действия
- [Дополнительная информация о службе Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

