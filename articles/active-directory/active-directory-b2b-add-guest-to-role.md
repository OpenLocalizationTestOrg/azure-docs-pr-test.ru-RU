---
title: "роль tooa aaaAdd Azure Active Directory B2B совместную работу пользователя | Документы Microsoft"
description: "Добавление роли tooa гостевой пользователя в Azure Active Directory"
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
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="fa99c-103">Предоставьте разрешения toousers из партнерские организации в клиенте Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa99c-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="fa99c-104">Совместная работа пользователей Azure Active Directory (Azure AD) B2B добавляются в качестве гостевых пользователей toohello каталога и разрешения гостя в каталоге hello ограничены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fa99c-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="fa99c-105">Вашей организации может потребоваться некоторые гостевые пользователи toofill более высокие права доступа роли в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="fa99c-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="fa99c-106">Определение ролей более высокие права доступа, toosupport гостевых пользователей могут быть добавлены tooany роли при работе, исходя из потребностей вашей организации.</span><span class="sxs-lookup"><span data-stu-id="fa99c-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="fa99c-107">Роль по умолчанию</span><span class="sxs-lookup"><span data-stu-id="fa99c-107">Default role</span></span>

![роль по умолчанию](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="fa99c-109">Роль "Глобальный администратор"</span><span class="sxs-lookup"><span data-stu-id="fa99c-109">Global Administrator Role</span></span>

![роль "Глобальный администратор"](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="fa99c-111">Роль "Администратор с ограниченными правами"</span><span class="sxs-lookup"><span data-stu-id="fa99c-111">Limited Administrator Role</span></span>

![роль "Администратор с ограниченными правами"](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="fa99c-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa99c-113">Next steps</span></span>

<span data-ttu-id="fa99c-114">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="fa99c-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="fa99c-115">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="fa99c-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="fa99c-116">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="fa99c-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="fa99c-117">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="fa99c-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="fa99c-118">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="fa99c-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="fa99c-119">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="fa99c-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="fa99c-120">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="fa99c-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="fa99c-121">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="fa99c-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="fa99c-122">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa99c-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="fa99c-123">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="fa99c-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="fa99c-124">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="fa99c-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
