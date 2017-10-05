---
title: "Добавление или удаление роли пользователя | Документация Майкрософт"
description: "Сведения о добавлении ролей для привилегированных пользователей с помощью приложения для управления привилегированными пользователями Azure Active Directory."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: 3ac07bb7b070f44595c099a454b3d0dbc66126c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-privileged-identity-management-how-to-add-or-remove-a-user-role"></a><span data-ttu-id="63ae4-103">Управление привилегированными пользователями Azure AD: добавление и удаление роли пользователя</span><span class="sxs-lookup"><span data-stu-id="63ae4-103">Azure AD Privileged Identity Management: How to add or remove a user role</span></span>
<span data-ttu-id="63ae4-104">С помощью Azure Active Directory (AD) глобальный администратор (или администратор организации) может изменить назначения **постоянных** ролей для пользователей в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63ae4-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned to roles in Azure AD.</span></span> <span data-ttu-id="63ae4-105">Это делается с помощью таких командлетов PowerShell, как `Add-MsolRoleMember` и `Remove-MsolRoleMember`.</span><span class="sxs-lookup"><span data-stu-id="63ae4-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span></span> <span data-ttu-id="63ae4-106">Кроме того, можно использовать классический портал Azure, как описано в разделе [Назначение ролей администраторов в Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="63ae4-106">Or they can use the Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="63ae4-107">Приложение "Управление привилегированными пользователями" (PIM) Azure AD также позволяет администраторам привилегированных ролей назначать постоянные роли.</span><span class="sxs-lookup"><span data-stu-id="63ae4-107">The Azure AD Privileged Identity Management application allows privileged role administrators to make permanent role assignments, as well.</span></span> <span data-ttu-id="63ae4-108">Кроме того, администраторы привилегированных ролей могут предоставлять пользователям **право** на получение ролей администратора.</span><span class="sxs-lookup"><span data-stu-id="63ae4-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span></span> <span data-ttu-id="63ae4-109">Временные администраторы могут активировать роль при необходимости; срок действия их разрешений истекает, когда роль больше не требуется им для работы.</span><span class="sxs-lookup"><span data-stu-id="63ae4-109">An eligible admin can activate the role when they need it, and then their permissions expire once they're done.</span></span>

## <a name="manage-roles-with-pim-in-the-azure-portal"></a><span data-ttu-id="63ae4-110">Управление ролями с помощью PIM на портале Azure</span><span class="sxs-lookup"><span data-stu-id="63ae4-110">Manage roles with PIM in the Azure portal</span></span>
<span data-ttu-id="63ae4-111">В Azure AD, Office 365 и других службах и приложениях Майкрософт можно назначать пользователям организации различные административные роли.</span><span class="sxs-lookup"><span data-stu-id="63ae4-111">In your organization, you can assign users to different administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span></span>  <span data-ttu-id="63ae4-112">Дополнительные сведения о доступных ролях можно найти в разделе, посвященном [ролям в Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span><span class="sxs-lookup"><span data-stu-id="63ae4-112">More details on the available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span></span>

<span data-ttu-id="63ae4-113">Чтобы добавить или удалить пользователя в роли с помощью управления привилегированными пользователями, откройте панель мониторинга PIM.</span><span class="sxs-lookup"><span data-stu-id="63ae4-113">To add or remove a user in a role using Privileged Identity Management, bring up the PIM dashboard.</span></span> <span data-ttu-id="63ae4-114">Нажмите кнопку **Пользователи в роли администратора** или выберите определенную роль (например, глобальный администратор) в таблице ролей.</span><span class="sxs-lookup"><span data-stu-id="63ae4-114">Then either click the **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from the roles table.</span></span>

> [!NOTE]
> <span data-ttu-id="63ae4-115">Если компонент PIM еще не включен на портале Azure, см. статью [Приступая к работе с управлением привилегированными пользователями Azure AD](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="63ae4-115">If you haven't enabled PIM in the Azure portal yet, go to [Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span></span>

<span data-ttu-id="63ae4-116">Если требуется предоставить другому пользователю доступ к приложению PIM, требуемые роли пользователя описаны далее в статье о том, [как предоставить доступ к компоненту PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="63ae4-116">If you want to give another user access to PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="add-a-user-to-a-role"></a><span data-ttu-id="63ae4-117">Добавление пользователя к роли</span><span class="sxs-lookup"><span data-stu-id="63ae4-117">Add a user to a role</span></span>
1. <span data-ttu-id="63ae4-118">На [портале Azure](https://portal.azure.com/)выберите на панели мониторинга элемент **Управление привилегированными пользователями Azure AD** .</span><span class="sxs-lookup"><span data-stu-id="63ae4-118">In the [Azure portal](https://portal.azure.com/), select the **Azure AD Privileged Identity Management** tile on the dashboard.</span></span>
2. <span data-ttu-id="63ae4-119">Выберите **Управление привилегированными ролями**.</span><span class="sxs-lookup"><span data-stu-id="63ae4-119">Select **Manage privileged roles**.</span></span>
3. <span data-ttu-id="63ae4-120">В таблице **Сводка ролей** выберите нужную роль.</span><span class="sxs-lookup"><span data-stu-id="63ae4-120">In the **Role summary** table, select the role you want to manage.</span></span>
4. <span data-ttu-id="63ae4-121">В колонке роли выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="63ae4-121">In the role blade, select **Add**.</span></span>
5. <span data-ttu-id="63ae4-122">Щелкните **Выбор пользователей** и найдите пользователя в колонке **Выбор пользователей**.</span><span class="sxs-lookup"><span data-stu-id="63ae4-122">Click **Select users** and search for the user on the **Select users** blade.</span></span>  
6. <span data-ttu-id="63ae4-123">Выберите пользователя из результатов поиска и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="63ae4-123">Select the user from the search results list, and click **Done**.</span></span>
7. <span data-ttu-id="63ae4-124">Нажмите кнопку **ОК** , чтобы сохранить изменение.</span><span class="sxs-lookup"><span data-stu-id="63ae4-124">Click **OK** to save your selection.</span></span> <span data-ttu-id="63ae4-125">Выбранный пользователь отобразится в списке как временный владелец этой роли.</span><span class="sxs-lookup"><span data-stu-id="63ae4-125">The user you have selected will appear in the list as eligible for the role.</span></span>

> [!NOTE]
> <span data-ttu-id="63ae4-126">Новым пользователям роль по умолчанию назначается временно.</span><span class="sxs-lookup"><span data-stu-id="63ae4-126">New users in a role are only eligible for the role by default.</span></span> <span data-ttu-id="63ae4-127">Если вы хотите сделать роль постоянной, выберите пользователя в списке.</span><span class="sxs-lookup"><span data-stu-id="63ae4-127">If you want to make the role permanent, click the user in the list.</span></span> <span data-ttu-id="63ae4-128">Откроется отдельная колонка со сведениями о пользователе.</span><span class="sxs-lookup"><span data-stu-id="63ae4-128">The user's information will appear in a new blade.</span></span> <span data-ttu-id="63ae4-129">Выберите в меню пользователя команду **Сделать постоянным** .</span><span class="sxs-lookup"><span data-stu-id="63ae4-129">Select **Make perm** in the user information menu.</span></span>  
> <span data-ttu-id="63ae4-130">Если пользователь не может зарегистрировать Azure многофакторной проверки подлинности (MFA), или использует учетную запись Майкрософт (обычно @outlook.com), необходимо внести их в их роли.</span><span class="sxs-lookup"><span data-stu-id="63ae4-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span></span> <span data-ttu-id="63ae4-131">Временным администраторам будет предложено зарегистрироваться для использования MFA во время активации.</span><span class="sxs-lookup"><span data-stu-id="63ae4-131">Eligible admins are asked to register for MFA during activation.</span></span>

<span data-ttu-id="63ae4-132">Предоставив пользователям право на получение ролей, сообщите им, что они могут активировать их согласно инструкциям в статье [Как активировать и деактивировать роли в компоненте управления привилегированными пользователями Azure AD](active-directory-privileged-identity-management-how-to-activate-role.md).</span><span class="sxs-lookup"><span data-stu-id="63ae4-132">Now that the user is eligible for a role, let them know that they can activate it according to the instructions in [How to activate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="63ae4-133">Удаление пользователя из роли</span><span class="sxs-lookup"><span data-stu-id="63ae4-133">Remove a user from a role</span></span>
<span data-ttu-id="63ae4-134">Пользователей из временных ролей можно удалять, однако в системе всегда должен оставаться по крайней мере один пользователь с постоянной ролью глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="63ae4-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span></span>

<span data-ttu-id="63ae4-135">Выполните следующие действия, чтобы удалить конкретного пользователя из роли.</span><span class="sxs-lookup"><span data-stu-id="63ae4-135">Follow these steps to remove a specific user from a role:</span></span>

1. <span data-ttu-id="63ae4-136">Перейдите к роли в списке ролей, выбрав ее на панели мониторинга Azure AD PIM или нажав кнопку **Пользователи с ролями администраторов** .</span><span class="sxs-lookup"><span data-stu-id="63ae4-136">Navigate to the role in the role list either by selecting a role in the Azure AD PIM dashboard or by clicking on the **Users in Admin Roles** button.</span></span>
2. <span data-ttu-id="63ae4-137">Щелкните имя пользователя в списке пользователей.</span><span class="sxs-lookup"><span data-stu-id="63ae4-137">Click on the user in the user list.</span></span>
3. <span data-ttu-id="63ae4-138">Нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="63ae4-138">Click **Remove**.</span></span> <span data-ttu-id="63ae4-139">Появится сообщение с запросом подтверждения.</span><span class="sxs-lookup"><span data-stu-id="63ae4-139">A message will ask you to confirm.</span></span>
4. <span data-ttu-id="63ae4-140">Нажмите **Да** , чтобы удалить роль у пользователя.</span><span class="sxs-lookup"><span data-stu-id="63ae4-140">Click **Yes** to remove the role from the user.</span></span>

<span data-ttu-id="63ae4-141">Если вам неизвестно, каким пользователям по-прежнему требуются назначенные им роли, можно [запустить проверку доступа для ролей](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="63ae4-141">If you're not sure which users still need their role assignments, then you can [start an access review for the role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63ae4-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63ae4-142">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

