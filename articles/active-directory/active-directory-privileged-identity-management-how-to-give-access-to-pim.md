---
title: "Предоставление доступа к управлению привилегированными пользователями в Azure | Документация Майкрософт"
description: "Узнайте, как назначать пользователям роли для управления PIM с помощью расширения для управления привилегированными пользователями Azure Active Directory."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="3b3ad-103">Предоставление доступа к Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="3b3ad-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="3b3ad-104">Глобальный администратор, который активирует в организации управление привилегированными пользователями (PIM) Azure AD, автоматически получает доступ к службе PIM и право назначать роли.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="3b3ad-105">Никто больше не получает доступ на запись по умолчанию, даже другие глобальные администраторы.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="3b3ad-106">Другие глобальные администраторы, администраторы безопасности и читатели безопасности имеют доступ только для чтения к PIM Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="3b3ad-107">Чтобы предоставить доступ к PIM, первый пользователь может назначить другим пользователям роль **администратора привилегированных ролей** .</span><span class="sxs-lookup"><span data-stu-id="3b3ad-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="3b3ad-108">Это назначение нужно выполнить в PIM, и его нельзя изменить с помощью PowerShell или на других порталах.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="3b3ad-109">Для управления PIM в Azure AD требуется MFA Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="3b3ad-110">Поскольку учетные записи Майкрософт нельзя зарегистрировать для MFA Azure, у пользователя, который входит в систему с учетной записью Майкрософт, не будет доступа к PIM в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="3b3ad-111">Убедитесь, что в роли администратора привилегированных ролей всегда есть по крайней мере два пользователя, на случай, если один пользователь будет заблокирован или его учетная запись будет удалена.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="3b3ad-112">Предоставление другому пользователю доступа для управления PIM</span><span class="sxs-lookup"><span data-stu-id="3b3ad-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="3b3ad-113">Войдите на [портал Azure](https://portal.azure.com/) и на панели мониторинга выберите приложение **Управление привилегированными пользователями Azure AD** .</span><span class="sxs-lookup"><span data-stu-id="3b3ad-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="3b3ad-114">Выберите **Управление привилегированными ролями** > **Администратор привилегированных ролей** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Добавление администраторов привилегированных ролей — снимок экрана][1]
3. <span data-ttu-id="3b3ad-116">В колонке "Добавление управляемых пользователей" шаг 1 уже выполнен.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="3b3ad-117">Перейдите к шагу 2, **Выбор пользователей** , и выполните поиск пользователя, которого необходимо добавить.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Выбор пользователей — снимок экрана][2]
4. <span data-ttu-id="3b3ad-119">Выберите пользователя из результатов поиска и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="3b3ad-120">Нажмите кнопку **ОК** , чтобы сохранить изменение.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="3b3ad-121">Выбранный пользователь отобразится в списке администраторов привилегированных ролей.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="3b3ad-122">Каждый раз, когда вы назначаете пользователю новую роль, он автоматически получает возможность активировать эту роль временно.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="3b3ad-123">Чтобы сделать назначенную роль постоянной, выберите пользователя в списке.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="3b3ad-124">Выберите в меню пользователя команду **сделать постоянной** .</span><span class="sxs-lookup"><span data-stu-id="3b3ad-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="3b3ad-125">Отправьте пользователю ссылку на статью [Приступая к работе с управлением привилегированными пользователями Azure AD](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3b3ad-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="3b3ad-126">Удаление прав доступа для управления PIM у другого пользователя</span><span class="sxs-lookup"><span data-stu-id="3b3ad-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="3b3ad-127">Прежде чем удалить кого-либо из роли администратора привилегированных ролей, всегда проверяйте, остается ли хотя бы два пользователя, которым назначена эта роль.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="3b3ad-128">На панели мониторинга PIM щелкните роль **Администратор привилегированных ролей**.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="3b3ad-129">Появится список пользователей, которые в настоящее время находятся в этой роли.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="3b3ad-130">Щелкните имя пользователя в списке пользователей.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="3b3ad-131">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-131">Click on **Remove**.</span></span>  <span data-ttu-id="3b3ad-132">Появится запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="3b3ad-133">Нажмите **Да** , чтобы удалить пользователя из роли.</span><span class="sxs-lookup"><span data-stu-id="3b3ad-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="3b3ad-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b3ad-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
