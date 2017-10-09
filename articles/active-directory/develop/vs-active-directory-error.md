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
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="f34fb-103">Диагностика ошибок посредством hello мастер подключения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f34fb-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="f34fb-104">При обнаружении предыдущий код проверки подлинности, hello мастер обнаружил тип проверки подлинности несовместимы.</span><span class="sxs-lookup"><span data-stu-id="f34fb-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="f34fb-105">Что проверяется?</span><span class="sxs-lookup"><span data-stu-id="f34fb-105">What is being checked?</span></span>
<span data-ttu-id="f34fb-106">**Примечание:** toocorrectly определить предыдущий код проверки подлинности в проекте, должны быть построены hello проекта.</span><span class="sxs-lookup"><span data-stu-id="f34fb-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="f34fb-107">Если возникла эта ошибка и в вашем проекте нет предыдущего кода аутентификации, еще раз выполните сборку проекта и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="f34fb-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="f34fb-108">Типы проектов</span><span class="sxs-lookup"><span data-stu-id="f34fb-108">Project Types</span></span>
<span data-ttu-id="f34fb-109">Hello мастер проверяет hello типа проекта, которое вы разрабатываете, поэтому его можно внедрить логику проверки подлинности правой hello в hello проекта.</span><span class="sxs-lookup"><span data-stu-id="f34fb-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="f34fb-110">При наличии любого контроллера, который является производным от `ApiController` в проекте hello hello проекта считается WebAPI проекта.</span><span class="sxs-lookup"><span data-stu-id="f34fb-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="f34fb-111">При наличии только контроллеров, которые являются производными от `MVC.Controller` в проекте hello hello проекта считается проекта MVC.</span><span class="sxs-lookup"><span data-stu-id="f34fb-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="f34fb-112">Ничего не поддерживается мастером hello.</span><span class="sxs-lookup"><span data-stu-id="f34fb-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="f34fb-113">Совместимый код проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f34fb-113">Compatible Authentication Code</span></span>
<span data-ttu-id="f34fb-114">Мастер установки Hello также проверяет наличие параметров проверки подлинности, которые были настроены ранее с помощью мастера hello и не совместим с приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="f34fb-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="f34fb-115">При наличии все параметры, он считается повторным входом обращения и откроется мастер hello hello параметры отображения.</span><span class="sxs-lookup"><span data-stu-id="f34fb-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="f34fb-116">Если только некоторые параметры hello присутствует, он считается такие ошибки.</span><span class="sxs-lookup"><span data-stu-id="f34fb-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="f34fb-117">В проект MVC hello мастер проверяет по любой из следующих параметров, полученных в результате предыдущего использования мастера hello hello:</span><span class="sxs-lookup"><span data-stu-id="f34fb-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="f34fb-118">Кроме того мастер hello проверяет все следующие параметры в проекте веб-API, полученных в результате предыдущего использования мастера hello hello:</span><span class="sxs-lookup"><span data-stu-id="f34fb-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="f34fb-119">Несовместимый код проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f34fb-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="f34fb-120">Наконец hello мастер попытается выполнить toodetect версии кода проверки подлинности, настроенные с помощью предыдущих версий Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f34fb-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="f34fb-121">Эта ошибка означает, что проект содержит несовместимый тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f34fb-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="f34fb-122">Hello мастер обнаруживает hello следующие типы проверки подлинности из предыдущих версий Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f34fb-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="f34fb-123">Проверка подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="f34fb-123">Windows Authentication</span></span> 
* <span data-ttu-id="f34fb-124">Учетные записи индивидуальных пользователей</span><span class="sxs-lookup"><span data-stu-id="f34fb-124">Individual User Accounts</span></span> 
* <span data-ttu-id="f34fb-125">Учетные записи организации</span><span class="sxs-lookup"><span data-stu-id="f34fb-125">Organizational Accounts</span></span> 

<span data-ttu-id="f34fb-126">в проект MVC toodetect проверку подлинности Windows hello Мастер ищет hello `authentication` элемент из вашего **web.config** файла.</span><span class="sxs-lookup"><span data-stu-id="f34fb-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="f34fb-127">в проекте веб-API toodetect проверку подлинности Windows hello Мастер ищет hello `IISExpressWindowsAuthentication` элемент из проекта **.csproj** файла:</span><span class="sxs-lookup"><span data-stu-id="f34fb-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="f34fb-128">toodetect индивидуальные учетные записи проверки подлинности, мастер hello ищет элемент package hello из вашего **Packages.config** файла.</span><span class="sxs-lookup"><span data-stu-id="f34fb-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="f34fb-129">toodetect старую форму проверки подлинности учетной записи организации hello Мастер ищет следующий элементом из hello **web.config**:</span><span class="sxs-lookup"><span data-stu-id="f34fb-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="f34fb-130">Тип проверки подлинности toochange hello, удалите тип проверки подлинности несовместимые hello и снова запустите мастер hello.</span><span class="sxs-lookup"><span data-stu-id="f34fb-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="f34fb-131">Дополнительные сведения см. в статье [Сценарии аутентификации в Azure Active Directory](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="f34fb-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="f34fb-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f34fb-132">Next steps</span></span>
- [<span data-ttu-id="f34fb-133">Сценарии аутентификации в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f34fb-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)