---
title: "внесенные aaaChanges tooa WebApi проекта при подключении tooAzure AD | Документы Microsoft"
description: "Описывает, что происходит tooyour WebApi проекта при подключении tooAzure AD с помощью Visual Studio"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a>В каком проекте WebApi ошибка toomy (Visual Studio Azure Active Directory подключенных служб)
> [!div class="op_single_selector"]
> * [Приступая к работе](vs-active-directory-webapi-getting-started.md)
> * [Что произошло?](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>Добавлены ссылки
### <a name="nuget-package-references"></a>Ссылки на пакет NuGet
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>Ссылки на .NET
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Изменения в коде
### <a name="code-files-were-added-tooyour-project"></a>Файлы кода были добавлены tooyour проекта
Класс запуска проверки подлинности, **App_Start/Startup.Auth.cs** был добавлен tooyour проект, содержащий логику запуска для проверки подлинности Azure AD.

### <a name="startup-code-was-added-tooyour-project"></a>Код запуска был добавлен tooyour проекта
Если класс запуска уже есть в вашем проекте, hello **конфигурации** метод было обновленные tooinclude вызов слишком`ConfigureAuth(app)`. В противном случае класс запуска была добавлена tooyour проекта.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>Один из файлов app.config или web.config имеет новое значение конфигурации.
были добавлены следующие записи конфигурации Hello.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>Создано приложение Azure AD
Приложения Azure AD был создан в каталоге hello, выбранная в мастере hello.

[Дополнительная информация о службе Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>Если после проверки *отключить проверку подлинности учетных записей отдельных пользователей*, какие дополнительные изменения были сделаны toomy проекта?
Удалены ссылки на пакет NuGet. Для файлов созданы резервные копии, а сами файлы удалены. В зависимости от состояния hello проекта вы можете иметь toomanually удалите дополнительные материалы или файлы или измените код соответствующим образом.

### <a name="nuget-package-references-removed-for-those-present"></a>Ссылки на существующие пакеты NuGet удалены
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Для существующих файлов кода созданы резервные копии, а сами файлы удалены.
Каждый из следующих файлов был заархивирован и удален из проекта hello. Файлы резервных копий расположены в папке «Backup» в корневой каталог проекта hello hello.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Для существующих файлов кода созданы резервные копии
Для каждого из следующих файлов создана резервная копия, после чего файлы были заменены. Файлы резервных копий расположены в папке «Backup» в корневой каталог проекта hello hello.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>Если после проверки *читать данные каталога*, какие дополнительные изменения были сделаны toomy проекта?
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Были внесены дополнительные изменения tooyour app.config или web.config
Hello следующие дополнительные настройки записи были добавлены.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Обновлено приложение Azure Active Directory
Приложение Azure Active Directory была hello обновленные tooinclude *читать данные каталога* разрешение и дополнительный раздел был создан, затем которой использовался как hello *ida: пароль* в hello `web.config` файла.

## <a name="next-steps"></a>Дальнейшие действия
- [Дополнительная информация о службе Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

