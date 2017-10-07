---
title: "aaaPermissions в центр безопасности Azure | Документы Microsoft"
description: "В этой статье описывается, как центр безопасности Azure использует toousers разрешения tooassign управления доступом на основе ролей и выявляет hello разрешены действия для каждой роли."
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
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="901b1-103">Разрешения в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="901b1-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="901b1-104">Центр безопасности Azure использует [управление доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md), который предоставляет [встроенных ролей](../active-directory/role-based-access-built-in-roles.md) , можно назначить toousers, групп и служб в Azure.</span><span class="sxs-lookup"><span data-stu-id="901b1-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="901b1-105">Центр обеспечения безопасности оценивает конфигурацию hello проблемы безопасности tooidentify ресурсы и уязвимости.</span><span class="sxs-lookup"><span data-stu-id="901b1-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="901b1-106">В центре безопасности отображается только сведения о связанных ресурсов tooa при назначении роли hello владельца, участника или чтения для hello подписка или группа ресурсов, к которому принадлежит ресурс.</span><span class="sxs-lookup"><span data-stu-id="901b1-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="901b1-107">В роли toothese сложения существует две конкретные роли центра обеспечения безопасности:</span><span class="sxs-lookup"><span data-stu-id="901b1-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="901b1-108">**Модуль чтения безопасности**: пользователь, принадлежащий роли toothis имеет Просмотр центра tooSecurity права.</span><span class="sxs-lookup"><span data-stu-id="901b1-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="901b1-109">Hello пользователь может просматривать рекомендации, оповещения, политики безопасности и состояния безопасности, но не могут вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="901b1-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="901b1-110">**Администратор безопасности**: пользователь, принадлежащий роли toothis имеет hello одинаковыми правами как hello чтения безопасности и можно также обновить политику безопасности hello и пропустить предупреждения и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="901b1-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="901b1-111">роли безопасности Hello, чтения безопасности и администратора безопасности имеют доступ только на центр обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="901b1-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="901b1-112">роли безопасности Hello получить доступ к областям службы tooother Azure, например Интернета вещей & мобильных устройств, хранилище или веб-нет.</span><span class="sxs-lookup"><span data-stu-id="901b1-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="901b1-113">Роли и разрешенные действия</span><span class="sxs-lookup"><span data-stu-id="901b1-113">Roles and allowed actions</span></span>

<span data-ttu-id="901b1-114">Hello следующей таблице показаны роли и действий в центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="901b1-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="901b1-115">X указывает, что действие hello разрешен для этой роли.</span><span class="sxs-lookup"><span data-stu-id="901b1-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="901b1-116">Роль</span><span class="sxs-lookup"><span data-stu-id="901b1-116">Role</span></span> | <span data-ttu-id="901b1-117">Изменение политики безопасности</span><span class="sxs-lookup"><span data-stu-id="901b1-117">Edit security policy</span></span> | <span data-ttu-id="901b1-118">Применение рекомендаций по безопасности к ресурсу</span><span class="sxs-lookup"><span data-stu-id="901b1-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="901b1-119">Отклонение оповещений и рекомендаций</span><span class="sxs-lookup"><span data-stu-id="901b1-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="901b1-120">Просмотр оповещений и рекомендаций</span><span class="sxs-lookup"><span data-stu-id="901b1-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="901b1-121">Владелец подписки</span><span class="sxs-lookup"><span data-stu-id="901b1-121">Subscription Owner</span></span> | <span data-ttu-id="901b1-122">X</span><span class="sxs-lookup"><span data-stu-id="901b1-122">X</span></span> | <span data-ttu-id="901b1-123">X</span><span class="sxs-lookup"><span data-stu-id="901b1-123">X</span></span> | <span data-ttu-id="901b1-124">X</span><span class="sxs-lookup"><span data-stu-id="901b1-124">X</span></span> | <span data-ttu-id="901b1-125">X</span><span class="sxs-lookup"><span data-stu-id="901b1-125">X</span></span> |
| <span data-ttu-id="901b1-126">Участник подписки</span><span class="sxs-lookup"><span data-stu-id="901b1-126">Subscription Contributor</span></span> | <span data-ttu-id="901b1-127">X</span><span class="sxs-lookup"><span data-stu-id="901b1-127">X</span></span> | <span data-ttu-id="901b1-128">X</span><span class="sxs-lookup"><span data-stu-id="901b1-128">X</span></span> | <span data-ttu-id="901b1-129">X</span><span class="sxs-lookup"><span data-stu-id="901b1-129">X</span></span> | <span data-ttu-id="901b1-130">X</span><span class="sxs-lookup"><span data-stu-id="901b1-130">X</span></span> |
| <span data-ttu-id="901b1-131">Владелец группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="901b1-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="901b1-132">X</span><span class="sxs-lookup"><span data-stu-id="901b1-132">X</span></span> | -- | <span data-ttu-id="901b1-133">X</span><span class="sxs-lookup"><span data-stu-id="901b1-133">X</span></span> |
| <span data-ttu-id="901b1-134">Участник группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="901b1-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="901b1-135">X</span><span class="sxs-lookup"><span data-stu-id="901b1-135">X</span></span> | -- | <span data-ttu-id="901b1-136">X</span><span class="sxs-lookup"><span data-stu-id="901b1-136">X</span></span> |
| <span data-ttu-id="901b1-137">читатель.</span><span class="sxs-lookup"><span data-stu-id="901b1-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="901b1-138">X</span><span class="sxs-lookup"><span data-stu-id="901b1-138">X</span></span> |
| <span data-ttu-id="901b1-139">Администратор безопасности</span><span class="sxs-lookup"><span data-stu-id="901b1-139">Security Administrator</span></span> | <span data-ttu-id="901b1-140">X</span><span class="sxs-lookup"><span data-stu-id="901b1-140">X</span></span> | -- | <span data-ttu-id="901b1-141">X</span><span class="sxs-lookup"><span data-stu-id="901b1-141">X</span></span> | <span data-ttu-id="901b1-142">X</span><span class="sxs-lookup"><span data-stu-id="901b1-142">X</span></span> |
| <span data-ttu-id="901b1-143">Чтение данных безопасности</span><span class="sxs-lookup"><span data-stu-id="901b1-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="901b1-144">X</span><span class="sxs-lookup"><span data-stu-id="901b1-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="901b1-145">Рекомендуется назначать hello минимальным роль требуется для пользователей toocomplete своих задач.</span><span class="sxs-lookup"><span data-stu-id="901b1-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="901b1-146">Например назначьте toousers роль модуля чтения hello, достаточно tooview сведения о работоспособности hello безопасности ресурса, но не выполнять действия, такие как применение рекомендаций или изменения политики.</span><span class="sxs-lookup"><span data-stu-id="901b1-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="901b1-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="901b1-147">Next steps</span></span>
<span data-ttu-id="901b1-148">В этой статье описано, как центр обеспечения безопасности использует toousers разрешения tooassign RBAC и идентифицировать hello разрешены действия для каждой роли.</span><span class="sxs-lookup"><span data-stu-id="901b1-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="901b1-149">Теперь, когда вы знакомы с назначениями ролей hello необходимости toomonitor hello состояние безопасности вашей подписки, изменение политик безопасности и применить рекомендации, узнайте, как:</span><span class="sxs-lookup"><span data-stu-id="901b1-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="901b1-150">Настройка политик безопасности в центре безопасности</span><span class="sxs-lookup"><span data-stu-id="901b1-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="901b1-151">Управление рекомендациями по безопасности в Центре безопасности</span><span class="sxs-lookup"><span data-stu-id="901b1-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="901b1-152">Для отслеживания работоспособности безопасности hello ресурсами Azure</span><span class="sxs-lookup"><span data-stu-id="901b1-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="901b1-153">Управление и отвечать toosecurity оповещения в центр безопасности</span><span class="sxs-lookup"><span data-stu-id="901b1-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="901b1-154">Мониторинг партнерских решений безопасности</span><span class="sxs-lookup"><span data-stu-id="901b1-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
