---
title: "Разработка приложений для Azure AD | Документация Майкрософт"
description: "Эта статья, предназначенная для ИТ-специалистов, содержит рекомендации по интеграции приложений Azure с Active Directory."
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
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="29939-103">Разработка бизнес-приложений для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29939-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="29939-104">Это руководство содержит сведения о разработке бизнес-приложений для Azure Active Directory (AD). Оно предназначено специально для глобальных администраторов Active Directory и Office 365.</span><span class="sxs-lookup"><span data-stu-id="29939-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="29939-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="29939-105">Overview</span></span>
<span data-ttu-id="29939-106">Создание приложений, интегрированных с Azure AD, предоставляет пользователям в вашей организации возможность единого входа в Office 365.</span><span class="sxs-lookup"><span data-stu-id="29939-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="29939-107">Помещение приложения в Azure AD позволяет управлять политикой аутентификации для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="29939-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="29939-108">Дополнительные сведения об условном доступе и защите приложений с помощью Многофакторной идентификации (MFA) см. в статье [Приступая к работе с условным доступом Azure Active Directory](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="29939-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="29939-109">Зарегистрируйте свое приложение для использования Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29939-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="29939-110">Регистрация приложения означает, что разработчики смогут использовать Azure AD для аутентификации пользователей и для запроса доступа к ресурсам пользователей, таким как электронная почта, календарь и документы.</span><span class="sxs-lookup"><span data-stu-id="29939-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="29939-111">Любой член каталога (не являющийся гостем) может зарегистрировать приложение, данный процесс также называется *созданием объекта приложения*.</span><span class="sxs-lookup"><span data-stu-id="29939-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="29939-112">Регистрация приложения позволяет любому пользователю выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="29939-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="29939-113">получение для своего приложения удостоверения, которое распознается Azure AD;</span><span class="sxs-lookup"><span data-stu-id="29939-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="29939-114">получение одного или нескольких секретов/ключей, которые приложение может использовать для проверки подлинности в AD;</span><span class="sxs-lookup"><span data-stu-id="29939-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="29939-115">добавление в приложение фирменной символики (имени, логотипа и т. д.) на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="29939-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="29939-116">применение функций авторизации Azure AD для приложения, включая:</span><span class="sxs-lookup"><span data-stu-id="29939-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="29939-117">Управление доступа на основе ролей</span><span class="sxs-lookup"><span data-stu-id="29939-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="29939-118">использование Azure Active Directory в качестве сервера авторизации oAuth (защита API, предоставляемого приложением).</span><span class="sxs-lookup"><span data-stu-id="29939-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="29939-119">объявление требуемых разрешений для правильной работы приложения, включая:</span><span class="sxs-lookup"><span data-stu-id="29939-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="29939-120">1. Разрешения приложения (только глобальные администраторы).</span><span class="sxs-lookup"><span data-stu-id="29939-120">App permissions (global administrators only).</span></span> <span data-ttu-id="29939-121">Например: членство в роли в другом приложении Azure AD или членство в роли, связанное с ресурсом, группой ресурсов или подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="29939-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="29939-122">2. Делегированные разрешения (любой пользователь).</span><span class="sxs-lookup"><span data-stu-id="29939-122">Delegated permissions (any user).</span></span> <span data-ttu-id="29939-123">Например: Azure AD, вход и чтение профиля.</span><span class="sxs-lookup"><span data-stu-id="29939-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="29939-124">По умолчанию любой член может зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="29939-124">By default, any member can register an application.</span></span> <span data-ttu-id="29939-125">Чтобы узнать, как ограничить разрешения по регистрации приложений для определенных членов, см. раздел [Кто имеет право добавлять приложения в мой экземпляр Azure AD?](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance)</span><span class="sxs-lookup"><span data-stu-id="29939-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="29939-126">Вот что понадобится сделать вам как глобальному администратору, чтобы помочь разработчикам подготовить их приложения для рабочей среды:</span><span class="sxs-lookup"><span data-stu-id="29939-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="29939-127">настройка правил доступа (политика доступа и многофакторная проверка подлинности);</span><span class="sxs-lookup"><span data-stu-id="29939-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="29939-128">настройка приложения для запроса назначений пользователей и назначение пользователей;</span><span class="sxs-lookup"><span data-stu-id="29939-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="29939-129">подавление процедуры использования согласия пользователей.</span><span class="sxs-lookup"><span data-stu-id="29939-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="29939-130">Настройка правил доступа</span><span class="sxs-lookup"><span data-stu-id="29939-130">Configure access rules</span></span>
<span data-ttu-id="29939-131">Настройте правила доступа для каждого приложения SaaS.</span><span class="sxs-lookup"><span data-stu-id="29939-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="29939-132">Например, это может быть запрос на многофакторную проверку подлинности или предоставление доступа только для пользователей в доверенных сетях.</span><span class="sxs-lookup"><span data-stu-id="29939-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="29939-133">Подробные сведения см. в документе [Приступая к работе с условным доступом Azure Active Directory](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="29939-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="29939-134">настройка приложения для запроса назначений пользователей и назначение пользователей;</span><span class="sxs-lookup"><span data-stu-id="29939-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="29939-135">По умолчанию пользователи могут получить доступ к приложениям без назначения.</span><span class="sxs-lookup"><span data-stu-id="29939-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="29939-136">Однако если приложение предоставляет роли или вы хотите, чтобы приложение отображалось на панели доступа пользователя, то следует запросить назначение пользователей.</span><span class="sxs-lookup"><span data-stu-id="29939-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="29939-137">Требование назначения пользователей</span><span class="sxs-lookup"><span data-stu-id="29939-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="29939-138">Если вы являетесь подписчиком Azure AD Premium или Enterprise Mobility Suite (EMS), то настоятельно рекомендуется использовать группы.</span><span class="sxs-lookup"><span data-stu-id="29939-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="29939-139">Назначение групп приложению позволяет делегировать процесс управления доступом владельцу группы.</span><span class="sxs-lookup"><span data-stu-id="29939-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="29939-140">Вы можете создать группу самостоятельно или попросить ответственное лицо в своей организации создать такую группу с помощью средства управления группами.</span><span class="sxs-lookup"><span data-stu-id="29939-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="29939-141">Назначение пользователей приложения</span><span class="sxs-lookup"><span data-stu-id="29939-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="29939-142">Назначение групп для приложения</span><span class="sxs-lookup"><span data-stu-id="29939-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="29939-143">Упрощение процедуры получения согласия пользователей</span><span class="sxs-lookup"><span data-stu-id="29939-143">Suppress user consent</span></span>
<span data-ttu-id="29939-144">По умолчанию, чтобы войти в систему, каждый пользователь должен дать согласие на предоставление приложению определенных разрешений.</span><span class="sxs-lookup"><span data-stu-id="29939-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="29939-145">Процедура получения согласия, запрашиваемая с целью предоставления разрешений для приложения, может удивить пользователя, неосведомленного о том, что ему придется принять такое решение.</span><span class="sxs-lookup"><span data-stu-id="29939-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="29939-146">При использовании приложений, которым вы доверяете, можно упростить процедуру, предоставляя приложению согласие от имени организации.</span><span class="sxs-lookup"><span data-stu-id="29939-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="29939-147">Дополнительные сведения о согласии пользователей и процедуре использования согласия в Azure см. в статье [Интеграция приложений с Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="29939-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="29939-148">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="29939-148">Related Articles</span></span>
* [<span data-ttu-id="29939-149">Как обеспечить безопасный удаленный доступ к локальным приложениям</span><span class="sxs-lookup"><span data-stu-id="29939-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="29939-150">Предварительная версия Azure условного доступа для приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="29939-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="29939-151">Управление доступом к приложениям с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="29939-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="29939-152">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29939-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
