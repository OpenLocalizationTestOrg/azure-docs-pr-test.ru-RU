---
title: "Делегирование приглашений для службы совместной работы Azure Active Directory B2B | Документация Майкрософт"
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="763ce-103">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="763ce-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="763ce-104">Благодаря службе совместной работы Azure Active Directory (Azure AD) B2B больше не нужно быть глобальным администратором, чтобы приглашать пользователей.</span><span class="sxs-lookup"><span data-stu-id="763ce-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="763ce-105">Вместо этого можно использовать политики и делегировать приглашения пользователям, роли которых дают возможность отправлять приглашения.</span><span class="sxs-lookup"><span data-stu-id="763ce-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="763ce-106">Вам доступен важный новый способ делегирования приглашений гостевым пользователям — с помощью роли Guest Inviter.</span><span class="sxs-lookup"><span data-stu-id="763ce-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="763ce-107">Роль Guest Inviter</span><span class="sxs-lookup"><span data-stu-id="763ce-107">Guest Inviter role</span></span>
<span data-ttu-id="763ce-108">Можно назначить пользователю роль Guest Inviter для отправки приглашений.</span><span class="sxs-lookup"><span data-stu-id="763ce-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="763ce-109">Для отправки приглашений не нужно быть участником роли глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="763ce-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="763ce-110">По умолчанию обычные пользователи могут также вызывать API приглашения, если только глобальный администратор не отключил для них приглашения.</span><span class="sxs-lookup"><span data-stu-id="763ce-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="763ce-111">Кроме того, пользователь может вызвать API с помощью портала Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="763ce-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="763ce-112">Ниже приведен пример, показывающий, как использовать PowerShell, чтобы добавить пользователя в роль Guest Inviter:</span><span class="sxs-lookup"><span data-stu-id="763ce-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="763ce-113">Управление пользователями, имеющими разрешение на приглашение</span><span class="sxs-lookup"><span data-stu-id="763ce-113">Control who can invite</span></span>

![Настройка пользователей с разрешением на приглашение](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="763ce-115">Используя службу совместной работы Azure AD B2B, администратор клиентов может устанавливать следующие политики приглашения:</span><span class="sxs-lookup"><span data-stu-id="763ce-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="763ce-116">отключение приглашений;</span><span class="sxs-lookup"><span data-stu-id="763ce-116">Turn off invitations</span></span>
- <span data-ttu-id="763ce-117">приглашать могут только администраторы и пользователи с ролью Guest Inviter;</span><span class="sxs-lookup"><span data-stu-id="763ce-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="763ce-118">приглашать могут администраторы и участники роли Guest Inviter;</span><span class="sxs-lookup"><span data-stu-id="763ce-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="763ce-119">приглашать могут все пользователи, включая гостей.</span><span class="sxs-lookup"><span data-stu-id="763ce-119">All users, including guests, can invite</span></span>

<span data-ttu-id="763ce-120">По умолчанию для клиентов настраивается вариант 4</span><span class="sxs-lookup"><span data-stu-id="763ce-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="763ce-121">(приглашать пользователей B2B могут все пользователи, включая гостей).</span><span class="sxs-lookup"><span data-stu-id="763ce-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="763ce-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="763ce-122">Next steps</span></span>

<span data-ttu-id="763ce-123">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="763ce-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="763ce-124">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="763ce-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="763ce-125">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="763ce-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="763ce-126">Добавление пользователя службы совместной работы Azure Active Directory B2B в роль</span><span class="sxs-lookup"><span data-stu-id="763ce-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="763ce-127">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="763ce-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="763ce-128">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="763ce-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="763ce-129">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="763ce-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="763ce-130">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="763ce-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="763ce-131">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="763ce-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="763ce-132">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="763ce-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="763ce-133">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="763ce-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
