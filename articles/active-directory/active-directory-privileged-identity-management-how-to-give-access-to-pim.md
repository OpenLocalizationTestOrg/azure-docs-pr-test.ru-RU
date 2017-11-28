---
title: "aaaHow toogive tooPrivileged доступа удостоверений - Azure | Документы Microsoft"
description: "Узнайте, как tooadd toousers ролей с hello Azure Active Directory Privileged Identity Management расширение так ими PIM."
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
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="b5324-103">Предоставление доступа toomanage Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="b5324-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="b5324-104">глобальный администратор Hello, позволяет Azure AD Privileged Identity Management (PIM) для организации автоматически получить назначения ролей и доступ к tooPIM.</span><span class="sxs-lookup"><span data-stu-id="b5324-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="b5324-105">Никто больше не получает доступ на запись по умолчанию, даже другие глобальные администраторы.</span><span class="sxs-lookup"><span data-stu-id="b5324-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="b5324-106">Другие глобальные Администраторы, Администраторы безопасности и безопасности модулей чтения имеют доступ только для чтения tooAzure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="b5324-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="b5324-107">tooPIM toogive доступ, hello первого пользователя можно предоставить другим пользователям toohello **привилегированной роли администратора** роли.</span><span class="sxs-lookup"><span data-stu-id="b5324-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="b5324-108">Это назначение нужно выполнить в PIM, и его нельзя изменить с помощью PowerShell или на других порталах.</span><span class="sxs-lookup"><span data-stu-id="b5324-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="b5324-109">Для управления PIM в Azure AD требуется MFA Azure.</span><span class="sxs-lookup"><span data-stu-id="b5324-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="b5324-110">Поскольку учетные записи Майкрософт нельзя зарегистрировать для MFA Azure, у пользователя, который входит в систему с учетной записью Майкрософт, не будет доступа к PIM в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5324-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="b5324-111">Убедитесь, что в роли администратора привилегированных ролей всегда есть по крайней мере два пользователя, на случай, если один пользователь будет заблокирован или его учетная запись будет удалена.</span><span class="sxs-lookup"><span data-stu-id="b5324-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="b5324-112">Предоставьте доступ toomanage другой пользователь PIM</span><span class="sxs-lookup"><span data-stu-id="b5324-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="b5324-113">Войдите в toohello [портал Azure](https://portal.azure.com/) и выберите hello **Azure AD Privileged Identity Management** приложения на панель мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="b5324-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="b5324-114">Выберите **Управление привилегированными ролями** > **Администратор привилегированных ролей** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b5324-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Добавление администраторов привилегированных ролей — снимок экрана][1]
3. <span data-ttu-id="b5324-116">На панели управляемые пользователи hello добавить шаг 1 уже завершена.</span><span class="sxs-lookup"><span data-stu-id="b5324-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="b5324-117">Выберите шаг 2, **выберите пользователей** и поиска для hello пользователя требуется tooadd.</span><span class="sxs-lookup"><span data-stu-id="b5324-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![Выбор пользователей — снимок экрана][2]
4. <span data-ttu-id="b5324-119">Выберите пользователя hello hello результатов поиска и нажмите кнопку **сделать**.</span><span class="sxs-lookup"><span data-stu-id="b5324-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="b5324-120">Нажмите кнопку **ОК** toosave ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="b5324-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="b5324-121">Hello пользователя, которые вы выбрали будет отображаться в списке hello привилегированной роли администраторов.</span><span class="sxs-lookup"><span data-stu-id="b5324-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="b5324-122">При назначении нового toosomeone роли, они автоматически настраиваются как роль hello подходящих tooactivate.</span><span class="sxs-lookup"><span data-stu-id="b5324-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="b5324-123">Если требуется, чтобы toomake их в роль hello выберите hello пользователя в списке hello.</span><span class="sxs-lookup"><span data-stu-id="b5324-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="b5324-124">Выберите **сделать разрешений** в меню сведения пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b5324-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="b5324-125">Отправить пользователю hello ссылку слишком[Приступая к работе с Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b5324-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="b5324-126">Удаление прав доступа для управления PIM у другого пользователя</span><span class="sxs-lookup"><span data-stu-id="b5324-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="b5324-127">Прежде чем удалить пользователя из роли администратора привилегированной роли hello, всегда проверяйте, по-прежнему будет существовать двух пользователей, назначенных tooit.</span><span class="sxs-lookup"><span data-stu-id="b5324-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="b5324-128">В панели мониторинга PIM hello, щелкните роль hello **привилегированной роли администратора**.</span><span class="sxs-lookup"><span data-stu-id="b5324-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="b5324-129">отображается список пользователей в настоящее время в этой роли Hello.</span><span class="sxs-lookup"><span data-stu-id="b5324-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="b5324-130">Щелкните hello пользователя в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b5324-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="b5324-131">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="b5324-131">Click on **Remove**.</span></span>  <span data-ttu-id="b5324-132">Появится запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="b5324-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="b5324-133">Нажмите кнопку **Да** tooremove hello пользователя из роли hello.</span><span class="sxs-lookup"><span data-stu-id="b5324-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="b5324-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5324-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
