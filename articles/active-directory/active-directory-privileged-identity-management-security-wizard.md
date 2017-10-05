---
title: "Мастер защиты в расширении для управления привилегированными пользователями Azure AD"
description: "Когда вы в первый раз запускаете управление привилегированными пользователями Azure Active Directory, открывается мастер защиты. В этой статье описаны этапы работы мастера."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 260d178f3d8158411b3ad266e3b0d15edbebc722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-security-wizard-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="82b10-104">Использование мастера защиты в Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="82b10-104">Using the security wizard in Azure AD Privileged Identity Management</span></span> 
<span data-ttu-id="82b10-105">Если вы впервые запускаете компонент управления привилегированными пользователями (PIM) Azure, открывается мастер.</span><span class="sxs-lookup"><span data-stu-id="82b10-105">If you're the first person to run Azure Privileged Identity Management (PIM) for your organization, you will be presented with a wizard.</span></span> <span data-ttu-id="82b10-106">Этот мастер поможет вам оценить риски безопасности, связанные с привилегированными пользователями, и понять, как их снизить с помощью компонента PIM.</span><span class="sxs-lookup"><span data-stu-id="82b10-106">The wizard helps you understand the security risks of privileged identities and how to use PIM to reduce those risks.</span></span> <span data-ttu-id="82b10-107">Нет необходимости вносить изменения в существующие назначения ролей в мастере, это можно сделать позже.</span><span class="sxs-lookup"><span data-stu-id="82b10-107">You don't need to make any changes to existing role assignments in the wizard, if you prefer to do it later.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="82b10-108">Основные принципы</span><span class="sxs-lookup"><span data-stu-id="82b10-108">What to expect</span></span>
<span data-ttu-id="82b10-109">Перед использованием компонента PIM в организации все назначения ролей являются постоянными: пользователи всегда находятся в заданных ролях, даже если на данный момент эти права им не требуются.</span><span class="sxs-lookup"><span data-stu-id="82b10-109">Before your organization starts using PIM, all role assignments are permanent: the users are always in these roles even if they do not presently need their privileges.</span></span>  <span data-ttu-id="82b10-110">На первом шаге мастера выводится список ролей с высоким уровнем привилегий и текущее количество пользователей с этими ролями.</span><span class="sxs-lookup"><span data-stu-id="82b10-110">The first step of the wizard shows you a list of high-privileged roles and how many users are currently in those roles.</span></span> <span data-ttu-id="82b10-111">Можно просмотреть сведения об определенной роли для получения дополнительных сведений о пользователях, если один или несколько из них вам неизвестны.</span><span class="sxs-lookup"><span data-stu-id="82b10-111">You can drill in to a particular role to learn more about users if one or more of them are unfamiliar.</span></span>

<span data-ttu-id="82b10-112">Второй шаг мастера предоставляет возможность изменить назначения ролей администраторов.</span><span class="sxs-lookup"><span data-stu-id="82b10-112">The second step of the wizard gives you an opportunity to change administrator's role assignments.</span></span>  

> [!WARNING]
> <span data-ttu-id="82b10-113">Очень важно иметь как минимум одного глобального администратора и несколько администраторов привилегированных ролей с учетной записью организации (не учетной записью Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="82b10-113">It is important that you have at least one global administrator, and more than one privileged role administrator with an organizational account (not a Microsoft account).</span></span> <span data-ttu-id="82b10-114">При наличии только одного администратора привилегированных ролей в организации нельзя будет работать с компонентом PIM, если эта учетная запись будет удалена.</span><span class="sxs-lookup"><span data-stu-id="82b10-114">If there is only one privileged role administrator, the organization will not be able to manage PIM if that account is deleted.</span></span>
> <span data-ttu-id="82b10-115">Кроме того, рекомендуется назначать постоянные роли, если пользователь имеет учетную запись Майкрософт (учетную запись, используемую для входа в службы Майкрософт, такие как Skype и Outlook.com).</span><span class="sxs-lookup"><span data-stu-id="82b10-115">Also, keep role assignments permanent if a user has a Microsoft account (An account they use to sign in to Microsoft services like Skype and Outlook.com).</span></span> <span data-ttu-id="82b10-116">Если планируется использовать обязательную проверку MFA при активации этой роли, доступ пользователя будет заблокирован.</span><span class="sxs-lookup"><span data-stu-id="82b10-116">If you plan to require MFA for activation for that role, that user will be locked out.</span></span>
> 
> 

<span data-ttu-id="82b10-117">Впоследствии мастер отображаться не будет.</span><span class="sxs-lookup"><span data-stu-id="82b10-117">After you have made changes, the wizard will no longer show up.</span></span> <span data-ttu-id="82b10-118">При следующем использовании PIM вы или администратор привилегированных ролей увидите панель мониторинга PIM.</span><span class="sxs-lookup"><span data-stu-id="82b10-118">The next time you or another privileged role administrator use PIM, you will see the PIM dashboard.</span></span>  

* <span data-ttu-id="82b10-119">Чтобы научиться добавлять пользователей в роли и удалять их, а также изменять назначения с постоянных на временные, ознакомьтесь с разделом, посвященным [добавлению и удалению ролей пользователей](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span><span class="sxs-lookup"><span data-stu-id="82b10-119">If you would like to add or remove users from roles or change assignments from permanent to eligible, read more at [how to add or remove a user's role](active-directory-privileged-identity-management-how-to-add-role-to-user.md).</span></span>
* <span data-ttu-id="82b10-120">Если вы хотите предоставить доступ к управлению PIM большему количеству пользователей, ознакомьтесь с разделом, посвященным [предоставлению доступа к управлению в PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="82b10-120">If you would like to give more users access to manage PIM, read more at [how to give access to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82b10-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82b10-121">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

