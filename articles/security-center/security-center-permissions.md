---
title: "Разрешения в центре безопасности Azure | Документация Майкрософт"
description: "В этой статье объясняется, как центр безопасности Azure использует управление доступом на основе ролей для назначения разрешений пользователям и определяет разрешенные действия для каждой роли."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 0aaa99dda44d2020afd3e841e84020eb4ff87a85
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="1ea22-103">Разрешения в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="1ea22-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="1ea22-104">Центр безопасности Azure использует [управление доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md), в котором предусмотрены [встроенные роли](../active-directory/role-based-access-built-in-roles.md). Эти роли можно назначать пользователям, группам и службам.</span><span class="sxs-lookup"><span data-stu-id="1ea22-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.</span></span>

<span data-ttu-id="1ea22-105">Центр безопасности оценивает конфигурацию ресурсов, чтобы выявить проблемы безопасности и уязвимости.</span><span class="sxs-lookup"><span data-stu-id="1ea22-105">Security Center assesses the configuration of your resources to identify security issues and vulnerabilities.</span></span> <span data-ttu-id="1ea22-106">В центре безопасности отображается только информация, связанная с ресурсами, для которых вам назначена роль владельца, участника или читателя в рамках подписки или группы ресурсов, к которым принадлежит ресурс.</span><span class="sxs-lookup"><span data-stu-id="1ea22-106">In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="1ea22-107">Помимо этих ролей, существует две конкретные роли центра обеспечения безопасности:</span><span class="sxs-lookup"><span data-stu-id="1ea22-107">In addition to these roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="1ea22-108">**Читатель безопасности**. Пользователь с этой ролью имеет право просматривать центр безопасности.</span><span class="sxs-lookup"><span data-stu-id="1ea22-108">**Security Reader**: A user that belongs to this role has viewing rights to Security Center.</span></span> <span data-ttu-id="1ea22-109">Он может просматривать рекомендации, оповещения, политику и состояние безопасности, но не может вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="1ea22-109">The user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="1ea22-110">**Администратор безопасности**. Пользователь с этой ролью имеет те же права, что и читатель безопасности, но также может изменять политику безопасности, отклонять рекомендации и оповещения.</span><span class="sxs-lookup"><span data-stu-id="1ea22-110">**Security Administrator**: A user that belongs to this role has the same rights as the Security Reader and can also update the security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="1ea22-111">Роли безопасности (читатель безопасности и администратор безопасности) предоставляют доступ только к центру безопасности.</span><span class="sxs-lookup"><span data-stu-id="1ea22-111">The security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="1ea22-112">Они не предоставляют доступ к другим областям Azure, например к службе хранилища, Интернету и мобильным устройствам или "Интернету вещей".</span><span class="sxs-lookup"><span data-stu-id="1ea22-112">The security roles do not have access to other service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="1ea22-113">Роли и разрешенные действия</span><span class="sxs-lookup"><span data-stu-id="1ea22-113">Roles and allowed actions</span></span>

<span data-ttu-id="1ea22-114">В следующей таблице показаны роли и разрешенные им действия в центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="1ea22-114">The following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="1ea22-115">Значок "X" указывает, что данное действие разрешено для роли.</span><span class="sxs-lookup"><span data-stu-id="1ea22-115">An X indicates that the action is allowed for that role.</span></span>

| <span data-ttu-id="1ea22-116">Роль</span><span class="sxs-lookup"><span data-stu-id="1ea22-116">Role</span></span> | <span data-ttu-id="1ea22-117">Изменение политики безопасности</span><span class="sxs-lookup"><span data-stu-id="1ea22-117">Edit security policy</span></span> | <span data-ttu-id="1ea22-118">Применение рекомендаций по безопасности к ресурсу</span><span class="sxs-lookup"><span data-stu-id="1ea22-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="1ea22-119">Отклонение оповещений и рекомендаций</span><span class="sxs-lookup"><span data-stu-id="1ea22-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="1ea22-120">Просмотр оповещений и рекомендаций</span><span class="sxs-lookup"><span data-stu-id="1ea22-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="1ea22-121">Владелец подписки</span><span class="sxs-lookup"><span data-stu-id="1ea22-121">Subscription Owner</span></span> | <span data-ttu-id="1ea22-122">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-122">X</span></span> | <span data-ttu-id="1ea22-123">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-123">X</span></span> | <span data-ttu-id="1ea22-124">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-124">X</span></span> | <span data-ttu-id="1ea22-125">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-125">X</span></span> |
| <span data-ttu-id="1ea22-126">Участник подписки</span><span class="sxs-lookup"><span data-stu-id="1ea22-126">Subscription Contributor</span></span> | <span data-ttu-id="1ea22-127">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-127">X</span></span> | <span data-ttu-id="1ea22-128">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-128">X</span></span> | <span data-ttu-id="1ea22-129">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-129">X</span></span> | <span data-ttu-id="1ea22-130">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-130">X</span></span> |
| <span data-ttu-id="1ea22-131">Владелец группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="1ea22-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="1ea22-132">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-132">X</span></span> | -- | <span data-ttu-id="1ea22-133">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-133">X</span></span> |
| <span data-ttu-id="1ea22-134">Участник группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="1ea22-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="1ea22-135">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-135">X</span></span> | -- | <span data-ttu-id="1ea22-136">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-136">X</span></span> |
| <span data-ttu-id="1ea22-137">читатель.</span><span class="sxs-lookup"><span data-stu-id="1ea22-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="1ea22-138">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-138">X</span></span> |
| <span data-ttu-id="1ea22-139">Администратор безопасности</span><span class="sxs-lookup"><span data-stu-id="1ea22-139">Security Administrator</span></span> | <span data-ttu-id="1ea22-140">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-140">X</span></span> | -- | <span data-ttu-id="1ea22-141">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-141">X</span></span> | <span data-ttu-id="1ea22-142">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-142">X</span></span> |
| <span data-ttu-id="1ea22-143">Чтение данных безопасности</span><span class="sxs-lookup"><span data-stu-id="1ea22-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="1ea22-144">X</span><span class="sxs-lookup"><span data-stu-id="1ea22-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="1ea22-145">Рекомендуется назначить пользователям роли с минимальными разрешениями, необходимыми для выполнения их задач.</span><span class="sxs-lookup"><span data-stu-id="1ea22-145">We recommend that you assign the least permissive role needed for users to complete their tasks.</span></span> <span data-ttu-id="1ea22-146">Например, назначьте роль читателя пользователям, которым нужно только просматривать сведения о работоспособности защиты ресурсов и не нужно выполнять какие-либо действия (к примеру, применять рекомендации или изменять политики).</span><span class="sxs-lookup"><span data-stu-id="1ea22-146">For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="1ea22-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ea22-147">Next steps</span></span>
<span data-ttu-id="1ea22-148">В этой статье объясняется, как центр безопасности использует управление доступом на основе ролей для назначения разрешений пользователям и определяет разрешенные действия для каждой роли.</span><span class="sxs-lookup"><span data-stu-id="1ea22-148">This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role.</span></span> <span data-ttu-id="1ea22-149">Теперь, когда вы ознакомились с назначениями ролей, необходимых для наблюдения за состоянием безопасности подписки, изменения политик безопасности и применения рекомендаций, вы можете изучить следующие темы.</span><span class="sxs-lookup"><span data-stu-id="1ea22-149">Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="1ea22-150">Настройка политик безопасности в центре безопасности</span><span class="sxs-lookup"><span data-stu-id="1ea22-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="1ea22-151">Управление рекомендациями по безопасности в Центре безопасности</span><span class="sxs-lookup"><span data-stu-id="1ea22-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="1ea22-152">Отслеживание работоспособности защиты ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="1ea22-152">Monitor the security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="1ea22-153">Управление оповещениями системы безопасности и управление ими в центре безопасности</span><span class="sxs-lookup"><span data-stu-id="1ea22-153">Manage and respond to security alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="1ea22-154">Мониторинг партнерских решений безопасности</span><span class="sxs-lookup"><span data-stu-id="1ea22-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
