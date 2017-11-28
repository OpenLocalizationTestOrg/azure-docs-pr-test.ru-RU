---
title: "aaaDynamic групп и совместной работы Azure Active Directory B2B | Документы Microsoft"
description: "Службу совместной работы Azure Active Directory B2B можно использовать с динамическими группами Azure AD."
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="8019a-103">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8019a-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="8019a-104">Что такое динамические группы?</span><span class="sxs-lookup"><span data-stu-id="8019a-104">What are dynamic groups?</span></span>
<span data-ttu-id="8019a-105">Динамическая настройка членства в группах для Azure Active Directory (Azure AD) доступен в [hello портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8019a-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8019a-106">Администраторы могут задать правила, которые toopopulate группы, созданные в Azure Active Directory на основе атрибутов пользователя (например, userType, отделу или страны).</span><span class="sxs-lookup"><span data-stu-id="8019a-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="8019a-107">Элементы могут добавляться автоматически tooor удалены из группы безопасности на основе их атрибутов.</span><span class="sxs-lookup"><span data-stu-id="8019a-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="8019a-108">Эти группы можно предоставить доступ tooapplications или облачные ресурсы (сайтов SharePoint, документы) и tooassign лицензирует toomembers.</span><span class="sxs-lookup"><span data-stu-id="8019a-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="8019a-109">Дополнительные сведения о динамических групп см. в статье [Выделенные группы в Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="8019a-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="8019a-110">Hello соответствующие [лицензирования Azure AD Premium P1 и P2](https://azure.microsoft.com/pricing/details/active-directory/) необходимые toocreate и использование динамических групп.</span><span class="sxs-lookup"><span data-stu-id="8019a-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="8019a-111">Дополнительные сведения см. в статье hello [создавать правила на основе атрибутов для динамического членства в группе в Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8019a-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="8019a-112">Что такое hello встроенных динамические группы?</span><span class="sxs-lookup"><span data-stu-id="8019a-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="8019a-113">Hello **всех пользователей** динамическая группа включает toocreate администраторов клиента, выберите группы, содержащей всех пользователей в клиенте hello с одним.</span><span class="sxs-lookup"><span data-stu-id="8019a-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="8019a-114">По умолчанию hello **всех пользователей** группа включает всех пользователей в каталоге hello, включая элементы и гостевых систем.</span><span class="sxs-lookup"><span data-stu-id="8019a-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="8019a-115">Hello новый портал администрирования Azure Active Directory, можно выбрать tooenable hello **всех пользователей** в hello, просмотреть параметры группы.</span><span class="sxs-lookup"><span data-stu-id="8019a-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![встроенные группы](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="8019a-117">Усиление hello все динамические группы пользователей</span><span class="sxs-lookup"><span data-stu-id="8019a-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="8019a-118">По умолчанию hello **всех пользователей** группа содержит также пользователей совместной работы (гостевая) B2B.</span><span class="sxs-lookup"><span data-stu-id="8019a-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="8019a-119">Могут дополнительно обеспечить безопасность вашей **всех пользователей** группу с помощью правила tooremove гостевых пользователей.</span><span class="sxs-lookup"><span data-stu-id="8019a-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="8019a-120">Hello ниже показан hello **всех пользователей** tooexclude Гости изменения группы.</span><span class="sxs-lookup"><span data-stu-id="8019a-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![включение группы "Все пользователи"](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="8019a-122">Может также оказаться полезным toocreate новый динамическую группу, содержащую только гостевых пользователей, так, чтобы можно было применить toothem политики (такие как политики Azure AD условного доступа).</span><span class="sxs-lookup"><span data-stu-id="8019a-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="8019a-123">Как такая группа может выглядеть:</span><span class="sxs-lookup"><span data-stu-id="8019a-123">What such a group might look like:</span></span>

![исключение гостевых пользователей](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="8019a-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8019a-125">Next steps</span></span>

<span data-ttu-id="8019a-126">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="8019a-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="8019a-127">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="8019a-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="8019a-128">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8019a-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="8019a-129">Добавление роли пользователя tooa B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="8019a-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="8019a-130">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8019a-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="8019a-131">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8019a-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="8019a-132">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="8019a-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="8019a-133">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8019a-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="8019a-134">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8019a-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="8019a-135">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="8019a-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="8019a-136">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8019a-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
