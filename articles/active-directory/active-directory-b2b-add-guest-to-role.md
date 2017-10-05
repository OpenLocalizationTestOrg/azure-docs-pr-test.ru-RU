---
title: "Добавление пользователя службы совместной работы Azure Active Directory B2B в роль | Документация Майкрософт"
description: "Добавление роли гостевого пользователя в Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e816349ea971c997f655b4d51672dba666bc3e89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permissions-to-users-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="d63da-103">Предоставление пользователям разрешений от партнерских организаций в клиенте Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d63da-103">Grant permissions to users from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="d63da-104">Пользователи службы совместной работы Azure Active Directory (Azure AD) B2B добавляются в каталог как гостевые пользователи, а разрешения гостей в каталоге по умолчанию ограничены.</span><span class="sxs-lookup"><span data-stu-id="d63da-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users to the directory, and guest permissions in the directory are restricted by default.</span></span> <span data-ttu-id="d63da-105">Ваша организация может быть заинтересована в назначении некоторым гостевым пользователям более привилегированных ролей.</span><span class="sxs-lookup"><span data-stu-id="d63da-105">Your business may need some guest users to fill higher-privilege roles in your organization.</span></span> <span data-ttu-id="d63da-106">Чтобы это сделать, вы можете добавлять гостевых пользователей в любые роли, исходя из потребностей своей организации.</span><span class="sxs-lookup"><span data-stu-id="d63da-106">To support defining higher-privilege roles, guest users can be added to any roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="d63da-107">Роль по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d63da-107">Default role</span></span>

![роль по умолчанию](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="d63da-109">Роль "Глобальный администратор"</span><span class="sxs-lookup"><span data-stu-id="d63da-109">Global Administrator Role</span></span>

![роль "Глобальный администратор"](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="d63da-111">Роль "Администратор с ограниченными правами"</span><span class="sxs-lookup"><span data-stu-id="d63da-111">Limited Administrator Role</span></span>

![роль "Администратор с ограниченными правами"](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="d63da-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d63da-113">Next steps</span></span>

<span data-ttu-id="d63da-114">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="d63da-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="d63da-115">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="d63da-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="d63da-116">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d63da-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="d63da-117">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d63da-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="d63da-118">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d63da-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="d63da-119">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d63da-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="d63da-120">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="d63da-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="d63da-121">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d63da-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="d63da-122">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d63da-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="d63da-123">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="d63da-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="d63da-124">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="d63da-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
