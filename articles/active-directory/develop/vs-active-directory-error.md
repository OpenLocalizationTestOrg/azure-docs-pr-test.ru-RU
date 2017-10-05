---
title: "Как диагностировать ошибки с помощью мастера подключения к Azure Active Directory"
description: "Мастер подключения к Active Directory обнаружил несовместимый тип проверки подлинности"
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
ms.openlocfilehash: 4f29f62b2996cae98b02c1ed5fcb59eca09301ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a><span data-ttu-id="90d49-103">Диагностика ошибок с помощью мастера подключения к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90d49-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="90d49-104">Во время обнаружения предыдущего кода проверки подлинности мастер обнаружил несовместимый тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="90d49-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="90d49-105">Что проверяется?</span><span class="sxs-lookup"><span data-stu-id="90d49-105">What is being checked?</span></span>
<span data-ttu-id="90d49-106">**Примечание.** Чтобы правильно определить предыдущий код аутентификации в проекте, необходимо создать проект.</span><span class="sxs-lookup"><span data-stu-id="90d49-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="90d49-107">Если возникла эта ошибка и в вашем проекте нет предыдущего кода аутентификации, еще раз выполните сборку проекта и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="90d49-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="90d49-108">Типы проектов</span><span class="sxs-lookup"><span data-stu-id="90d49-108">Project Types</span></span>
<span data-ttu-id="90d49-109">Мастер проверяет, какого типа проект вы разрабатываете, поэтому он может внедрить в проект правильную логику аутентификации.</span><span class="sxs-lookup"><span data-stu-id="90d49-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span>  <span data-ttu-id="90d49-110">Если в проекте есть какой-либо контроллер, являющийся производным от `ApiController`, то этот проект рассматривается как проект веб-API.</span><span class="sxs-lookup"><span data-stu-id="90d49-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span>  <span data-ttu-id="90d49-111">Если в проекте есть какие-либо контроллеры, являющиеся производными от `MVC.Controller`, то этот проект рассматривается как проект MVC.</span><span class="sxs-lookup"><span data-stu-id="90d49-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span>  <span data-ttu-id="90d49-112">Все остальные варианты мастером не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="90d49-112">Anything else is not supported by the wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="90d49-113">Совместимый код проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="90d49-113">Compatible Authentication Code</span></span>
<span data-ttu-id="90d49-114">Мастер также проверяет параметры проверки подлинности, ранее настроенные с помощью мастера или совместимые с ним.</span><span class="sxs-lookup"><span data-stu-id="90d49-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span></span>  <span data-ttu-id="90d49-115">Если все параметры присутствуют, то это рассматривается как реентерабельный случай, и мастер может открыть и отобразить эти параметры.</span><span class="sxs-lookup"><span data-stu-id="90d49-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span></span>  <span data-ttu-id="90d49-116">Если присутствуют только некоторые параметры, это рассматривается как случай ошибки.</span><span class="sxs-lookup"><span data-stu-id="90d49-116">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="90d49-117">В проекте MVC мастер проверяет все перечисленные ниже параметры, которые были получены в результате предыдущего использования мастера.</span><span class="sxs-lookup"><span data-stu-id="90d49-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="90d49-118">Кроме того, мастер проверяет в проекте веб-API все перечисленные ниже параметры, которые были получены в результате предыдущего использования мастера.</span><span class="sxs-lookup"><span data-stu-id="90d49-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="90d49-119">Несовместимый код проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="90d49-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="90d49-120">Наконец, мастер пытается обнаружить версии кода проверки подлинности, настроенные в предыдущих версиях Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90d49-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="90d49-121">Эта ошибка означает, что проект содержит несовместимый тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="90d49-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="90d49-122">Мастер определяет следующие типы проверок подлинности предыдущих версий Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="90d49-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="90d49-123">Проверка подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="90d49-123">Windows Authentication</span></span> 
* <span data-ttu-id="90d49-124">Учетные записи индивидуальных пользователей</span><span class="sxs-lookup"><span data-stu-id="90d49-124">Individual User Accounts</span></span> 
* <span data-ttu-id="90d49-125">Учетные записи организации</span><span class="sxs-lookup"><span data-stu-id="90d49-125">Organizational Accounts</span></span> 

<span data-ttu-id="90d49-126">Чтобы обнаружить аутентификацию Windows в проекте MVC, мастер ищет элемент `authentication` в файле **web.config** .</span><span class="sxs-lookup"><span data-stu-id="90d49-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="90d49-127">Чтобы обнаружить аутентификацию Windows в проекте веб-API, мастер ищет элемент `IISExpressWindowsAuthentication` в **CSPROJ-файле** вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="90d49-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="90d49-128">Чтобы обнаружить проверку подлинности индивидуальных учетных записей, мастер ищет элемент пакета в файле **Packages.config** .</span><span class="sxs-lookup"><span data-stu-id="90d49-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="90d49-129">Чтобы определить старый тип проверки подлинности учетной записи организации, мастер ищет в файле **web.config**следующий элемент:</span><span class="sxs-lookup"><span data-stu-id="90d49-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="90d49-130">Чтобы изменить тип проверки подлинности, удалите несовместимый тип и повторно запустите мастер.</span><span class="sxs-lookup"><span data-stu-id="90d49-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span></span>

<span data-ttu-id="90d49-131">Дополнительные сведения см. в статье [Сценарии аутентификации в Azure Active Directory](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="90d49-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="90d49-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="90d49-132">Next steps</span></span>
- [<span data-ttu-id="90d49-133">Сценарии аутентификации в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90d49-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)