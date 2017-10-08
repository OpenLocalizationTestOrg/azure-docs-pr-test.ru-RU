---
title: "параметры активации роли toomanage aaaHow | Документы Microsoft"
description: "Узнайте, как toochange hello параметры по умолчанию для привилегированных удостоверений с Azure Active Directory Privileged Identity Management расширения hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="ead53-103">Как toomanage параметры активации роли в Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="ead53-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="ead53-104">Привилегированные роли Администратор может настроить Azure AD Privileged Identity Management (PIM) в своей организации, включая изменение hello взаимодействие для пользователя, который выполняется активация назначение ролей на право.</span><span class="sxs-lookup"><span data-stu-id="ead53-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="ead53-105">Управление параметрами активации роли hello</span><span class="sxs-lookup"><span data-stu-id="ead53-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="ead53-106">Go toohello [портал Azure](https://portal.azure.com) и выберите hello **Azure AD Privileged Identity Management** приложения hello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="ead53-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="ead53-107">Выберите **Управление привилегированными ролями** > **Параметры**  > **Привилегированные роли**.</span><span class="sxs-lookup"><span data-stu-id="ead53-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="ead53-108">Выберите роль hello, параметры которого требуется toomanage.</span><span class="sxs-lookup"><span data-stu-id="ead53-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="ead53-109">На странице приветствия параметров для каждой роли существует несколько параметров, которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="ead53-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="ead53-110">Эти параметры распространяются только на пользователей, которые являются временными администраторами, а не постоянными.</span><span class="sxs-lookup"><span data-stu-id="ead53-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="ead53-111">**Активаций**: hello время в часах, которые роль остается активной до истечения срока его действия.</span><span class="sxs-lookup"><span data-stu-id="ead53-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="ead53-112">Возможное значение: от 1 до 72 часов.</span><span class="sxs-lookup"><span data-stu-id="ead53-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="ead53-113">**Уведомления о**: можно ли hello система отправляет tooadmins сообщений электронной почты, подтверждающее, что они активации роли.</span><span class="sxs-lookup"><span data-stu-id="ead53-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="ead53-114">Этот параметр полезен, если требуется обнаружить несанкционированные или недопустимые активации.</span><span class="sxs-lookup"><span data-stu-id="ead53-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="ead53-115">**Билет инцидента или запроса**: можно выбрать номер ли tooinclude соответствующих администраторов toorequire билет при активации их роли.</span><span class="sxs-lookup"><span data-stu-id="ead53-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="ead53-116">Этот параметр полезен при выполнении аудита доступа к ролям.</span><span class="sxs-lookup"><span data-stu-id="ead53-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="ead53-117">**Многофакторная проверка подлинности**: можно ли tooverify пользователей toorequire свою личность с помощью многофакторной проверки Подлинности, чтобы активировать их роли.</span><span class="sxs-lookup"><span data-stu-id="ead53-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="ead53-118">Они достаточно tooverify один раз за сеанс не каждый раз при активации роли.</span><span class="sxs-lookup"><span data-stu-id="ead53-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="ead53-119">Существует два tookeep советы помнить при включении многофакторной проверки Подлинности.</span><span class="sxs-lookup"><span data-stu-id="ead53-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="ead53-120">Пользователи, имеющие учетные записи Майкрософт для адреса электронной почты (обычно @outlook.com, но не всегда) не может зарегистрироваться для многофакторной проверки Подлинности Azure.</span><span class="sxs-lookup"><span data-stu-id="ead53-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="ead53-121">Если требуется tooassign toousers ролей с учетными записями Microsoft следует сделать их постоянных администраторов или отключить многофакторную проверку Подлинности для этой роли.</span><span class="sxs-lookup"><span data-stu-id="ead53-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="ead53-122">Нельзя отключить MFA для ролей с высоким уровнем привилегий в Azure AD и Office 365.</span><span class="sxs-lookup"><span data-stu-id="ead53-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="ead53-123">С помощью этой функции безопасности должны быть надежно защищены следующие роли:</span><span class="sxs-lookup"><span data-stu-id="ead53-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="ead53-124">администратор приложений;</span><span class="sxs-lookup"><span data-stu-id="ead53-124">Application administrator</span></span>
  * <span data-ttu-id="ead53-125">администратор прокси-сервера приложений;</span><span class="sxs-lookup"><span data-stu-id="ead53-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="ead53-126">Администратор выставления счетов</span><span class="sxs-lookup"><span data-stu-id="ead53-126">Billing administrator</span></span>  
  * <span data-ttu-id="ead53-127">администратор соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="ead53-127">Compliance administrator</span></span>  
  * <span data-ttu-id="ead53-128">администратор службы CRM;</span><span class="sxs-lookup"><span data-stu-id="ead53-128">CRM service administrator</span></span>
  * <span data-ttu-id="ead53-129">лицо, утверждающее доступ клиентов к LockBox;</span><span class="sxs-lookup"><span data-stu-id="ead53-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="ead53-130">редактор каталогов;</span><span class="sxs-lookup"><span data-stu-id="ead53-130">Directory writer</span></span>  
  * <span data-ttu-id="ead53-131">администратор Exchange;</span><span class="sxs-lookup"><span data-stu-id="ead53-131">Exchange administrator</span></span>  
  * <span data-ttu-id="ead53-132">Глобальный администратор</span><span class="sxs-lookup"><span data-stu-id="ead53-132">Global administrator</span></span>
  * <span data-ttu-id="ead53-133">администратор службы Intune;</span><span class="sxs-lookup"><span data-stu-id="ead53-133">Intune service administrator</span></span>
  * <span data-ttu-id="ead53-134">администратор почтовых ящиков;</span><span class="sxs-lookup"><span data-stu-id="ead53-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="ead53-135">партнер с поддержкой 1 уровня;</span><span class="sxs-lookup"><span data-stu-id="ead53-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="ead53-136">партнер с поддержкой 2 уровня;</span><span class="sxs-lookup"><span data-stu-id="ead53-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="ead53-137">администратор привилегированных ролей;</span><span class="sxs-lookup"><span data-stu-id="ead53-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="ead53-138">администратор безопасности;</span><span class="sxs-lookup"><span data-stu-id="ead53-138">Security administrator</span></span>  
  * <span data-ttu-id="ead53-139">администратор SharePoint;</span><span class="sxs-lookup"><span data-stu-id="ead53-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="ead53-140">администратор Skype для бизнеса;</span><span class="sxs-lookup"><span data-stu-id="ead53-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="ead53-141">администратор учетных записей;</span><span class="sxs-lookup"><span data-stu-id="ead53-141">User account administrator</span></span>  

<span data-ttu-id="ead53-142">Дополнительные сведения об использовании многофакторной проверки Подлинности с PIM. в разделе [как tooRequire многофакторной проверки Подлинности](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="ead53-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="ead53-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ead53-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

