---
title: "Управление параметрами активации ролей | Документация Майкрософт"
description: "Узнайте, как изменять параметры по умолчанию для привилегированных пользователей с помощью расширения для управления привилегированными пользователями Azure Active Directory."
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
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="7649b-103">Управление параметрами активации ролей в компоненте управления привилегированными пользователями Azure AD</span><span class="sxs-lookup"><span data-stu-id="7649b-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="7649b-104">Администратор привилегированных ролей может настроить компонент управления привилегированными пользователями (PIM) Azure AD в своей организации, включая изменение среды работы для пользователей, активирующих назначения временных ролей.</span><span class="sxs-lookup"><span data-stu-id="7649b-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="7649b-105">Управление параметрами активации ролей</span><span class="sxs-lookup"><span data-stu-id="7649b-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="7649b-106">Перейдите на [портал Azure](https://portal.azure.com) и выберите в панели мониторинга приложение **Управление привилегированными пользователями Azure AD** .</span><span class="sxs-lookup"><span data-stu-id="7649b-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="7649b-107">Выберите **Управление привилегированными ролями** > **Параметры**  > **Привилегированные роли**.</span><span class="sxs-lookup"><span data-stu-id="7649b-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="7649b-108">Выберите роль, параметрами которой вы хотите управлять.</span><span class="sxs-lookup"><span data-stu-id="7649b-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="7649b-109">На странице параметров для каждой роли есть ряд параметров, которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="7649b-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="7649b-110">Эти параметры распространяются только на пользователей, которые являются временными администраторами, а не постоянными.</span><span class="sxs-lookup"><span data-stu-id="7649b-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="7649b-111">**Активации**: время, указанное в часах, в течение которого роль остается активной.</span><span class="sxs-lookup"><span data-stu-id="7649b-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="7649b-112">Возможное значение: от 1 до 72 часов.</span><span class="sxs-lookup"><span data-stu-id="7649b-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="7649b-113">**Уведомления**: можно выбрать, будет ли система отправлять администраторам сообщения электронной почты, подтверждающие активацию роли.</span><span class="sxs-lookup"><span data-stu-id="7649b-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="7649b-114">Этот параметр полезен, если требуется обнаружить несанкционированные или недопустимые активации.</span><span class="sxs-lookup"><span data-stu-id="7649b-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="7649b-115">**Обращение с запросом или инцидентом**: можно выбрать, требовать ли от временных администраторов включать номер обращения при активации своей роли.</span><span class="sxs-lookup"><span data-stu-id="7649b-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="7649b-116">Этот параметр полезен при выполнении аудита доступа к ролям.</span><span class="sxs-lookup"><span data-stu-id="7649b-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="7649b-117">**Многофакторная идентификация**: можно выбрать, нужгл ли требовать от пользователей перед активацией ролей проходить проверку подлинности с использованием многофакторной идентификации.</span><span class="sxs-lookup"><span data-stu-id="7649b-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="7649b-118">Такая проверка будет выполняться один раз за сеанс, а не при каждой активации роли.</span><span class="sxs-lookup"><span data-stu-id="7649b-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="7649b-119">Есть две подсказки, которые рекомендуется учитывать при включении проверки MFA:</span><span class="sxs-lookup"><span data-stu-id="7649b-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="7649b-120">Пользователи, имеющие учетные записи Майкрософт для адреса электронной почты (обычно @outlook.com, но не всегда) не может зарегистрироваться для многофакторной проверки Подлинности Azure.</span><span class="sxs-lookup"><span data-stu-id="7649b-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="7649b-121">Если вы хотите назначить роли пользователям с учетными записями Майкрософт, то следует сделать их постоянными администраторами или отключить проверку MFA для этих ролей.</span><span class="sxs-lookup"><span data-stu-id="7649b-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="7649b-122">Нельзя отключить MFA для ролей с высоким уровнем привилегий в Azure AD и Office 365.</span><span class="sxs-lookup"><span data-stu-id="7649b-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="7649b-123">С помощью этой функции безопасности должны быть надежно защищены следующие роли:</span><span class="sxs-lookup"><span data-stu-id="7649b-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="7649b-124">администратор приложений;</span><span class="sxs-lookup"><span data-stu-id="7649b-124">Application administrator</span></span>
  * <span data-ttu-id="7649b-125">администратор прокси-сервера приложений;</span><span class="sxs-lookup"><span data-stu-id="7649b-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="7649b-126">Администратор выставления счетов</span><span class="sxs-lookup"><span data-stu-id="7649b-126">Billing administrator</span></span>  
  * <span data-ttu-id="7649b-127">администратор соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="7649b-127">Compliance administrator</span></span>  
  * <span data-ttu-id="7649b-128">администратор службы CRM;</span><span class="sxs-lookup"><span data-stu-id="7649b-128">CRM service administrator</span></span>
  * <span data-ttu-id="7649b-129">лицо, утверждающее доступ клиентов к LockBox;</span><span class="sxs-lookup"><span data-stu-id="7649b-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="7649b-130">редактор каталогов;</span><span class="sxs-lookup"><span data-stu-id="7649b-130">Directory writer</span></span>  
  * <span data-ttu-id="7649b-131">администратор Exchange;</span><span class="sxs-lookup"><span data-stu-id="7649b-131">Exchange administrator</span></span>  
  * <span data-ttu-id="7649b-132">Глобальный администратор</span><span class="sxs-lookup"><span data-stu-id="7649b-132">Global administrator</span></span>
  * <span data-ttu-id="7649b-133">администратор службы Intune;</span><span class="sxs-lookup"><span data-stu-id="7649b-133">Intune service administrator</span></span>
  * <span data-ttu-id="7649b-134">администратор почтовых ящиков;</span><span class="sxs-lookup"><span data-stu-id="7649b-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="7649b-135">партнер с поддержкой 1 уровня;</span><span class="sxs-lookup"><span data-stu-id="7649b-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="7649b-136">партнер с поддержкой 2 уровня;</span><span class="sxs-lookup"><span data-stu-id="7649b-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="7649b-137">администратор привилегированных ролей;</span><span class="sxs-lookup"><span data-stu-id="7649b-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="7649b-138">администратор безопасности;</span><span class="sxs-lookup"><span data-stu-id="7649b-138">Security administrator</span></span>  
  * <span data-ttu-id="7649b-139">администратор SharePoint;</span><span class="sxs-lookup"><span data-stu-id="7649b-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="7649b-140">администратор Skype для бизнеса;</span><span class="sxs-lookup"><span data-stu-id="7649b-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="7649b-141">администратор учетных записей;</span><span class="sxs-lookup"><span data-stu-id="7649b-141">User account administrator</span></span>  

<span data-ttu-id="7649b-142">Дополнительные сведения об использовании MFA при управлении привилегированными пользователями см. в статье [Настройка требования MFA в компоненте управления привилегированными пользователями Azure AD](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="7649b-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="7649b-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7649b-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

