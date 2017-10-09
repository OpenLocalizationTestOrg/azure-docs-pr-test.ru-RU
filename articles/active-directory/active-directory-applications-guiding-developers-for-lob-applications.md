---
title: "aaaDevelop приложений для Azure AD | Документы Microsoft"
description: "Предназначено для ИТ-специалистов hello, в этой статье рекомендации по интеграции с Active Directory приложения Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="d575f-103">Разработка бизнес-приложений для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d575f-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="d575f-104">Это руководство предоставляет сведения о разработке бизнес-приложений (LoB) для Azure Active Directory (AD) .hello нужной аудитория — Глобальные администраторы Active Directory и Office 365.</span><span class="sxs-lookup"><span data-stu-id="d575f-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="d575f-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="d575f-105">Overview</span></span>
<span data-ttu-id="d575f-106">Создание приложений, интегрированных с Azure AD, предоставляет пользователям в вашей организации возможность единого входа в Office 365.</span><span class="sxs-lookup"><span data-stu-id="d575f-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="d575f-107">Наличие приложения hello в Azure AD позволяет управлять hello политики проверки подлинности для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d575f-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="d575f-108">Дополнительные сведения о условного доступа и tooprotect приложений с помощью многофакторной проверки подлинности (MFA). в статье toolearn [Настройка правил доступа](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d575f-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="d575f-109">Зарегистрируйте toouse вашего приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d575f-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="d575f-110">Регистрации приложения hello означает, что разработчики могут использовать tooauthenticate пользователи Azure AD и запрос доступа к ресурсам toouser, например по электронной почте, календарю и документы.</span><span class="sxs-lookup"><span data-stu-id="d575f-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="d575f-111">Любой член каталога (не являющийся гостем) может зарегистрировать приложение, данный процесс также называется *созданием объекта приложения*.</span><span class="sxs-lookup"><span data-stu-id="d575f-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="d575f-112">Регистрация приложения позволяет любого пользователя toodo hello следующего:</span><span class="sxs-lookup"><span data-stu-id="d575f-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="d575f-113">получение для своего приложения удостоверения, которое распознается Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d575f-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="d575f-114">Получить лицензию или дополнительные секреты и ключи, которые hello приложения можно использовать tooauthenticate самого tooAD</span><span class="sxs-lookup"><span data-stu-id="d575f-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="d575f-115">Приложение hello фирменной символики в hello портал Azure с пользовательское имя, эмблемы, и т. д.</span><span class="sxs-lookup"><span data-stu-id="d575f-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="d575f-116">Применить приложения tootheir функции авторизации Azure AD, включая:</span><span class="sxs-lookup"><span data-stu-id="d575f-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="d575f-117">Управление доступа на основе ролей</span><span class="sxs-lookup"><span data-stu-id="d575f-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="d575f-118">Azure Active Directory в качестве сервера авторизации oAuth (безопасный интерфейс API, предоставляемые приложением hello)</span><span class="sxs-lookup"><span data-stu-id="d575f-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="d575f-119">Объявите необходимые разрешения необходимые для toofunction приложения hello, как ожидалось, включая:</span><span class="sxs-lookup"><span data-stu-id="d575f-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="d575f-120">1. Разрешения приложения (только глобальные администраторы).</span><span class="sxs-lookup"><span data-stu-id="d575f-120">App permissions (global administrators only).</span></span> <span data-ttu-id="d575f-121">Например: членство в роли в другой Azure AD приложения или роли членства относительный tooan ресурсов, группы ресурсов Azure, или подписки</span><span class="sxs-lookup"><span data-stu-id="d575f-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="d575f-122">2. Делегированные разрешения (любой пользователь).</span><span class="sxs-lookup"><span data-stu-id="d575f-122">Delegated permissions (any user).</span></span> <span data-ttu-id="d575f-123">Например: Azure AD, вход и чтение профиля.</span><span class="sxs-lookup"><span data-stu-id="d575f-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="d575f-124">По умолчанию любой член может зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="d575f-124">By default, any member can register an application.</span></span> <span data-ttu-id="d575f-125">toolearn toorestrict разрешения для регистрации приложений toospecific членов, в статье [способ добавления приложений tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="d575f-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="d575f-126">Ниже приведен теми, которые, глобальный администратор hello, требуется разработчики toohelp toodo подготовить свои приложения для производства.</span><span class="sxs-lookup"><span data-stu-id="d575f-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="d575f-127">настройка правил доступа (политика доступа и многофакторная проверка подлинности);</span><span class="sxs-lookup"><span data-stu-id="d575f-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="d575f-128">Настройте назначение пользователя toorequire приложение hello и назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="d575f-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="d575f-129">Отключение взаимодействие согласия пользователя по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="d575f-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="d575f-130">Настройка правил доступа</span><span class="sxs-lookup"><span data-stu-id="d575f-130">Configure access rules</span></span>
<span data-ttu-id="d575f-131">Настройка приложений SaaS tooyour правила доступа на уровне приложения.</span><span class="sxs-lookup"><span data-stu-id="d575f-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="d575f-132">Например можно требовать многофакторную проверку Подлинности или разрешить доступ toousers только в надежных сетях.</span><span class="sxs-lookup"><span data-stu-id="d575f-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="d575f-133">Hello сведения для этого доступны в документе hello [Настройка правил доступа](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d575f-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="d575f-134">Настройте назначение пользователя toorequire приложение hello и назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="d575f-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="d575f-135">По умолчанию пользователи могут получить доступ к приложениям без назначения.</span><span class="sxs-lookup"><span data-stu-id="d575f-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="d575f-136">Тем не менее если приложение hello предоставляет доступ к роли или если требуется tooappear приложения hello на пользовательской панели доступа, вам требуется назначение пользователей.</span><span class="sxs-lookup"><span data-stu-id="d575f-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="d575f-137">Требование назначения пользователей</span><span class="sxs-lookup"><span data-stu-id="d575f-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="d575f-138">Если вы являетесь подписчиком Azure AD Premium или Enterprise Mobility Suite (EMS), то настоятельно рекомендуется использовать группы.</span><span class="sxs-lookup"><span data-stu-id="d575f-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="d575f-139">Назначение группы toohello приложения позволяет toodelegate управления постоянный доступ toohello владельца группы hello.</span><span class="sxs-lookup"><span data-stu-id="d575f-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="d575f-140">Можно создать группы hello, или попросите Ответственный субъект hello в вашей организации toocreate hello группы с помощью механизма управления вашей группы.</span><span class="sxs-lookup"><span data-stu-id="d575f-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="d575f-141">Назначение пользователей tooan приложения</span><span class="sxs-lookup"><span data-stu-id="d575f-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="d575f-142">Назначение группы tooan приложения</span><span class="sxs-lookup"><span data-stu-id="d575f-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="d575f-143">Упрощение процедуры получения согласия пользователей</span><span class="sxs-lookup"><span data-stu-id="d575f-143">Suppress user consent</span></span>
<span data-ttu-id="d575f-144">По умолчанию каждый пользователь проходит через toosign взаимодействие согласия в.</span><span class="sxs-lookup"><span data-stu-id="d575f-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="d575f-145">взаимодействие согласия Hello, запросом toogrant пользователям разрешения на доступ приложения tooan может сбить с толку для пользователей, не знакомых с таких решений.</span><span class="sxs-lookup"><span data-stu-id="d575f-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="d575f-146">Для приложений, которым вы доверяете можно упростить взаимодействие с пользователем hello, соглашаетесь toohello приложения от имени вашей организации.</span><span class="sxs-lookup"><span data-stu-id="d575f-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="d575f-147">Дополнительные сведения о согласие пользователя и hello согласия в Azure качества программного обеспечения см. в разделе [интеграция приложений с Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d575f-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="d575f-148">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="d575f-148">Related Articles</span></span>
* [<span data-ttu-id="d575f-149">Включение безопасного удаленного доступа tooon локальные приложения с помощью прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="d575f-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="d575f-150">Предварительная версия Azure условного доступа для приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="d575f-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="d575f-151">Управление tooapps доступ с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="d575f-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="d575f-152">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d575f-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
