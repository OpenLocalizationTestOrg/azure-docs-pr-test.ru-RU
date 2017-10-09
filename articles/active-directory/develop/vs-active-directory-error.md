---
title: "ошибки toodiagnose aaaHow hello мастер подключения Azure Active Directory"
description: "Мастер подключения active directory Hello обнаружил тип несовместимые проверки подлинности"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Диагностика ошибок посредством hello мастер подключения Azure Active Directory
При обнаружении предыдущий код проверки подлинности, hello мастер обнаружил тип проверки подлинности несовместимы.   

## <a name="what-is-being-checked"></a>Что проверяется?
**Примечание:** toocorrectly определить предыдущий код проверки подлинности в проекте, должны быть построены hello проекта.  Если возникла эта ошибка и в вашем проекте нет предыдущего кода аутентификации, еще раз выполните сборку проекта и повторите попытку.

### <a name="project-types"></a>Типы проектов
Hello мастер проверяет hello типа проекта, которое вы разрабатываете, поэтому его можно внедрить логику проверки подлинности правой hello в hello проекта.  При наличии любого контроллера, который является производным от `ApiController` в проекте hello hello проекта считается WebAPI проекта.  При наличии только контроллеров, которые являются производными от `MVC.Controller` в проекте hello hello проекта считается проекта MVC.  Ничего не поддерживается мастером hello.

### <a name="compatible-authentication-code"></a>Совместимый код проверки подлинности
Мастер установки Hello также проверяет наличие параметров проверки подлинности, которые были настроены ранее с помощью мастера hello и не совместим с приветствия мастера.  При наличии все параметры, он считается повторным входом обращения и откроется мастер hello hello параметры отображения.  Если только некоторые параметры hello присутствует, он считается такие ошибки.

В проект MVC hello мастер проверяет по любой из следующих параметров, полученных в результате предыдущего использования мастера hello hello:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Кроме того мастер hello проверяет все следующие параметры в проекте веб-API, полученных в результате предыдущего использования мастера hello hello:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Несовместимый код проверки подлинности
Наконец hello мастер попытается выполнить toodetect версии кода проверки подлинности, настроенные с помощью предыдущих версий Visual Studio. Эта ошибка означает, что проект содержит несовместимый тип проверки подлинности. Hello мастер обнаруживает hello следующие типы проверки подлинности из предыдущих версий Visual Studio:

* Проверка подлинности Windows 
* Учетные записи индивидуальных пользователей 
* Учетные записи организации 

в проект MVC toodetect проверку подлинности Windows hello Мастер ищет hello `authentication` элемент из вашего **web.config** файла.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

в проекте веб-API toodetect проверку подлинности Windows hello Мастер ищет hello `IISExpressWindowsAuthentication` элемент из проекта **.csproj** файла:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

toodetect индивидуальные учетные записи проверки подлинности, мастер hello ищет элемент package hello из вашего **Packages.config** файла.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect старую форму проверки подлинности учетной записи организации hello Мастер ищет следующий элементом из hello **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

Тип проверки подлинности toochange hello, удалите тип проверки подлинности несовместимые hello и снова запустите мастер hello.

Дополнительные сведения см. в статье [Сценарии аутентификации в Azure Active Directory](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Дальнейшие действия
- [Сценарии аутентификации в Azure Active Directory](active-directory-authentication-scenarios.md)