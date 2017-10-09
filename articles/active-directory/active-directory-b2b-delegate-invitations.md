---
title: "aaaDelegate приглашения для совместной работы Azure Active Directory B2B | Документы Microsoft"
description: "Свойства пользователя службы совместной работы Azure Active Directory B2B можно настраивать."
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="c805e-103">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c805e-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="c805e-104">В сотрудничестве бизнес бизнес (B2B) Azure Active Directory (Azure AD) у вас toobe приглашения toosend глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="c805e-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="c805e-105">Вместо этого можно использовать политики и делегировать toousers приглашения, роли которой разрешить их toosend приглашения.</span><span class="sxs-lookup"><span data-stu-id="c805e-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="c805e-106">Важные новый способ toodelegate гостевой пользователь приглашения выполняется с помощью роли приглашающего гостевой hello.</span><span class="sxs-lookup"><span data-stu-id="c805e-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="c805e-107">Роль Guest Inviter</span><span class="sxs-lookup"><span data-stu-id="c805e-107">Guest Inviter role</span></span>
<span data-ttu-id="c805e-108">Можно назначить пользователя tooGuest hello приглашающего роли toosend приглашения.</span><span class="sxs-lookup"><span data-stu-id="c805e-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="c805e-109">У вас нет toobe членом приглашения toosend роли глобального администратора hello.</span><span class="sxs-lookup"><span data-stu-id="c805e-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="c805e-110">По умолчанию обычных пользователей можно также вызвать API приглашения hello глобального администратора отключить приглашения для обычных пользователей.</span><span class="sxs-lookup"><span data-stu-id="c805e-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="c805e-111">Пользователь также может вызвать API hello, с помощью портала Azure hello или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c805e-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="c805e-112">Ниже приведен пример, в котором показано, как tooadd PowerShell toouse toohello гостевой приглашающего роль пользователя:</span><span class="sxs-lookup"><span data-stu-id="c805e-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="c805e-113">Управление пользователями, имеющими разрешение на приглашение</span><span class="sxs-lookup"><span data-stu-id="c805e-113">Control who can invite</span></span>

![Элемент управления как tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="c805e-115">С совместной работы Azure AD B2B администратор клиента можно задать следующие политики приглашения hello.</span><span class="sxs-lookup"><span data-stu-id="c805e-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="c805e-116">отключение приглашений;</span><span class="sxs-lookup"><span data-stu-id="c805e-116">Turn off invitations</span></span>
- <span data-ttu-id="c805e-117">Только администраторы и пользователи с ролью гостя приглашающего hello можно пригласить</span><span class="sxs-lookup"><span data-stu-id="c805e-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="c805e-118">Администраторы, роль гостя приглашающего hello и члены можно пригласить</span><span class="sxs-lookup"><span data-stu-id="c805e-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="c805e-119">приглашать могут все пользователи, включая гостей.</span><span class="sxs-lookup"><span data-stu-id="c805e-119">All users, including guests, can invite</span></span>

<span data-ttu-id="c805e-120">По умолчанию, клиенты настроены слишком № 4.</span><span class="sxs-lookup"><span data-stu-id="c805e-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="c805e-121">(приглашать пользователей B2B могут все пользователи, включая гостей).</span><span class="sxs-lookup"><span data-stu-id="c805e-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c805e-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c805e-122">Next steps</span></span>

<span data-ttu-id="c805e-123">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="c805e-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c805e-124">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="c805e-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c805e-125">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c805e-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c805e-126">Добавление роли пользователя tooa B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="c805e-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c805e-127">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c805e-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c805e-128">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c805e-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="c805e-129">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="c805e-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="c805e-130">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c805e-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c805e-131">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c805e-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="c805e-132">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="c805e-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c805e-133">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c805e-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
