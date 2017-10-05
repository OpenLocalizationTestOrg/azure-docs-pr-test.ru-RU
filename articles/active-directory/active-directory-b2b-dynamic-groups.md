---
title: "Динамические группы и служба совместной работы Azure Active Directory B2B | Документация Майкрософт"
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
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="270b7-103">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="270b7-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="270b7-104">Что такое динамические группы?</span><span class="sxs-lookup"><span data-stu-id="270b7-104">What are dynamic groups?</span></span>
<span data-ttu-id="270b7-105">Динамическая конфигурация членства в группе безопасности для Azure Active Directory (Azure AD) доступна на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="270b7-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="270b7-106">Администраторы могут устанавливать правила для заполнения групп, создаваемых в Azure Active Directory на основе атрибутов пользователей (например, userType, отдел или страна).</span><span class="sxs-lookup"><span data-stu-id="270b7-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="270b7-107">Участников можно автоматически добавлять в группу безопасности или удалять их из нее в зависимости от атрибутов.</span><span class="sxs-lookup"><span data-stu-id="270b7-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="270b7-108">Эти группы могут предоставлять доступ к приложениям или облачным ресурсам, таким как сайты и документы SharePoint. Их также можно использовать для назначения лицензий участникам.</span><span class="sxs-lookup"><span data-stu-id="270b7-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="270b7-109">Дополнительные сведения о динамических групп см. в статье [Выделенные группы в Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="270b7-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="270b7-110">Для создания и использования динамических групп требуется соответствующее [лицензирование Azure AD Premium P1 или P2](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="270b7-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="270b7-111">Дополнительные сведения см. в статье [Создание правил на основе атрибутов для динамического членства в группах в Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="270b7-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="270b7-112">Что такое встроенные динамические группы?</span><span class="sxs-lookup"><span data-stu-id="270b7-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="270b7-113">Динамическая группа **Все пользователи** дает администраторам клиента возможность одним щелчком создать группу, которая содержит всех пользователей в клиенте.</span><span class="sxs-lookup"><span data-stu-id="270b7-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="270b7-114">По умолчанию группа **Все пользователи** включает в себя всех пользователей в каталоге, в том числе участников и гостей.</span><span class="sxs-lookup"><span data-stu-id="270b7-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="270b7-115">На новом портале администрирования Azure Active Directory в представлении "Параметры группы" можно включить группу **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="270b7-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![встроенные группы](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="270b7-117">Усиление защиты динамической группы "Все пользователи"</span><span class="sxs-lookup"><span data-stu-id="270b7-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="270b7-118">По умолчанию группа **Все пользователи** также включает (гостевых) пользователей службы совместной работы B2B.</span><span class="sxs-lookup"><span data-stu-id="270b7-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="270b7-119">Вы можете дополнительно обеспечить безопасность группы **Все пользователи**, используя правило для удаления гостевых пользователей.</span><span class="sxs-lookup"><span data-stu-id="270b7-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="270b7-120">На следующем снимке экрана показана группа **Все пользователи**, измененная для исключения гостей.</span><span class="sxs-lookup"><span data-stu-id="270b7-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![включение группы "Все пользователи"](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="270b7-122">Вы можете также рассмотреть создание новой динамической группы, содержащей только гостевых пользователей, чтобы применить политики (например, политики условного доступа Azure AD).</span><span class="sxs-lookup"><span data-stu-id="270b7-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="270b7-123">Как такая группа может выглядеть:</span><span class="sxs-lookup"><span data-stu-id="270b7-123">What such a group might look like:</span></span>

![исключение гостевых пользователей](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="270b7-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="270b7-125">Next steps</span></span>

<span data-ttu-id="270b7-126">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="270b7-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="270b7-127">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="270b7-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="270b7-128">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="270b7-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="270b7-129">Добавление пользователя службы совместной работы Azure Active Directory B2B в роль</span><span class="sxs-lookup"><span data-stu-id="270b7-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="270b7-130">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="270b7-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="270b7-131">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="270b7-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="270b7-132">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="270b7-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="270b7-133">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="270b7-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="270b7-134">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="270b7-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="270b7-135">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="270b7-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="270b7-136">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="270b7-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
