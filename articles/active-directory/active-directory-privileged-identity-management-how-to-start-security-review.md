---
title: "aaaHow toostart доступе | Документы Microsoft"
description: "Узнайте, как toocreate доступа просмотрите для привилегированных удостоверений с Azure Privileged Identity Management приложения hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="2d143-103">Как toostart доступа просмотрите в Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="2d143-103">How toostart an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="2d143-104">Назначения ролей становятся "устаревшими", когда у пользователей имеются права привилегированного доступа, которые им больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="2d143-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="2d143-105">В порядке tooreduce hello риски назначения этих устаревших ролей привилегированной роли администраторов следует регулярно проверять hello ролей, которым предоставлен пользователям.</span><span class="sxs-lookup"><span data-stu-id="2d143-105">In order tooreduce hello risk associated with these stale role assignments, privileged role administrators should regularly review hello roles that users have been given.</span></span> <span data-ttu-id="2d143-106">В этом документе рассматриваются hello шаги по запуску доступе в Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="2d143-106">This document covers hello steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="2d143-107">Запуск проверки доступа</span><span class="sxs-lookup"><span data-stu-id="2d143-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="2d143-108">Если панель мониторинга tooyour hello PIM приложения не был добавлен в hello портал Azure, см. шаги hello в [начало работы с управлением привилегированными пользователями Azure](active-directory-privileged-identity-management-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="2d143-108">If you haven't added hello PIM application tooyour dashboard in hello Azure portal, see hello steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="2d143-109">Hello PIM главной странице приложения существует три способа toostart доступе:</span><span class="sxs-lookup"><span data-stu-id="2d143-109">From hello PIM application main page, there are three ways toostart an access review:</span></span>

* <span data-ttu-id="2d143-110">Выберите **Проверки доступа** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2d143-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="2d143-111">Выберите **Роли** > кнопка **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="2d143-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="2d143-112">Проверены toobe выберите hello конкретной роли из списка ролей hello > **проверки** кнопку</span><span class="sxs-lookup"><span data-stu-id="2d143-112">Select hello specific role toobe reviewed from hello roles list > **Review** button</span></span>

<span data-ttu-id="2d143-113">При нажатии кнопки на hello **просмотрите** кнопки hello **запуск проверки доступа** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="2d143-113">When you click on hello **Review** button, hello **Start an access review** blade appears.</span></span> <span data-ttu-id="2d143-114">В этой колонке вы просмотрите hello tooconfigure переход с именем и ограничение времени, выберите tooreview роли и решить, кто будет выполнять проверку hello.</span><span class="sxs-lookup"><span data-stu-id="2d143-114">On this blade, you're going tooconfigure hello review with a name and time limit, choose a role tooreview, and decide who will perform hello review.</span></span>

![Запуск проверки доступа — снимок экрана][1]

### <a name="configure-hello-review"></a><span data-ttu-id="2d143-116">Настройка проверки hello</span><span class="sxs-lookup"><span data-stu-id="2d143-116">Configure hello review</span></span>
<span data-ttu-id="2d143-117">Просмотрите toocreate доступ, необходимо, чтобы tooname его и установить дату начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="2d143-117">toocreate an access review, you need tooname it and set a start and end date.</span></span>

![Настройка проверки — снимок экрана][2]

<span data-ttu-id="2d143-119">Сделайте длину hello hello просмотрите достаточно долго для toocomplete пользователей.</span><span class="sxs-lookup"><span data-stu-id="2d143-119">Make hello length of hello review long enough for users toocomplete it.</span></span> <span data-ttu-id="2d143-120">Если завершается до даты окончания hello, можно всегда остановить проверку hello раньше.</span><span class="sxs-lookup"><span data-stu-id="2d143-120">If you finish before hello end date, you can always stop hello review early.</span></span>

### <a name="choose-a-role-tooreview"></a><span data-ttu-id="2d143-121">Выберите tooreview роли</span><span class="sxs-lookup"><span data-stu-id="2d143-121">Choose a role tooreview</span></span>
<span data-ttu-id="2d143-122">Каждая проверка фокусируется только на одной роли.</span><span class="sxs-lookup"><span data-stu-id="2d143-122">Each review focuses on only one role.</span></span> <span data-ttu-id="2d143-123">Если не запустить доступе hello из колонки определенной роли, необходимо toochoose роли теперь.</span><span class="sxs-lookup"><span data-stu-id="2d143-123">Unless you started hello access review from a specific role blade, you'll need toochoose a role now.</span></span>

1. <span data-ttu-id="2d143-124">Перейдите в слишком**просмотреть членство в роли**</span><span class="sxs-lookup"><span data-stu-id="2d143-124">Navigate too**Review role membership**</span></span>
   
    ![Проверка членства в роли — снимок экрана][3]
2. <span data-ttu-id="2d143-126">Выберите одну роль из списка hello.</span><span class="sxs-lookup"><span data-stu-id="2d143-126">Choose one role from hello list.</span></span>

### <a name="decide-who-will-perform-hello-review"></a><span data-ttu-id="2d143-127">Решите, кто будет выполнять проверку hello</span><span class="sxs-lookup"><span data-stu-id="2d143-127">Decide who will perform hello review</span></span>
<span data-ttu-id="2d143-128">Существует три способа выполнения проверки.</span><span class="sxs-lookup"><span data-stu-id="2d143-128">There are three options for performing a review.</span></span> <span data-ttu-id="2d143-129">Можно назначить toosomeone проверки hello else toocomplete вы можете сделать это самостоятельно, или у вас есть каждого пользователя, просмотрите свой собственный доступ.</span><span class="sxs-lookup"><span data-stu-id="2d143-129">You can assign hello review toosomeone else toocomplete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="2d143-130">Перейдите в слишком**выберите проверяющих**</span><span class="sxs-lookup"><span data-stu-id="2d143-130">Navigate too**Select reviewers**</span></span>
   
    ![Выбор проверяющих — снимок экрана][4]
2. <span data-ttu-id="2d143-132">Выберите один из вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="2d143-132">Choose one of hello options:</span></span>
   
   * <span data-ttu-id="2d143-133">**Выбор рецензента**: используйте этот параметр, если вы не знаете, кому нужен доступ.</span><span class="sxs-lookup"><span data-stu-id="2d143-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="2d143-134">Этот параметр можно назначить владельцем ресурса tooa проверки hello или toocomplete диспетчер группы.</span><span class="sxs-lookup"><span data-stu-id="2d143-134">With this option, you can assign hello review tooa resource owner or group manager toocomplete.</span></span>
   * <span data-ttu-id="2d143-135">**Мне**: используется при необходимости toopreview как рабочих проверок доступа, либо требуется tooreview от имени пользователей, которые невозможно.</span><span class="sxs-lookup"><span data-stu-id="2d143-135">**Me**: Useful if you want toopreview how access reviews work, or you want tooreview on behalf of people who can't.</span></span>
   * <span data-ttu-id="2d143-136">**Членам просмотреть сами**: используйте этот параметр toohave hello пользователей анализ назначениях роли.</span><span class="sxs-lookup"><span data-stu-id="2d143-136">**Members review themselves**: Use this option toohave hello users review their own role assignments.</span></span>

### <a name="start-hello-review"></a><span data-ttu-id="2d143-137">Запуск проверки hello</span><span class="sxs-lookup"><span data-stu-id="2d143-137">Start hello review</span></span>
<span data-ttu-id="2d143-138">Наконец у вас есть toorequire параметр hello, что пользователи указать причину, если они утвердить свой доступ.</span><span class="sxs-lookup"><span data-stu-id="2d143-138">Finally, you have hello option toorequire that users provide a reason if they approve their access.</span></span> <span data-ttu-id="2d143-139">При желании добавьте описание проверки hello и выберите **запустить**.</span><span class="sxs-lookup"><span data-stu-id="2d143-139">Add a description of hello review if you like, and select **Start**.</span></span>

<span data-ttu-id="2d143-140">Убедитесь, что предоставление пользователям знать, что доступе, ожидая его и выводить их [как tooperform доступа просмотрите](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="2d143-140">Make sure you let your users know that there's an access review waiting for them, and show them [How tooperform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-hello-access-review"></a><span data-ttu-id="2d143-141">Управление hello доступе</span><span class="sxs-lookup"><span data-stu-id="2d143-141">Manage hello access review</span></span>
<span data-ttu-id="2d143-142">Вы можете отслеживать ход выполнения hello рецензенты hello выполнить проверку в панель мониторинга Azure AD PIM hello, в hello доступа просматривает раздел.</span><span class="sxs-lookup"><span data-stu-id="2d143-142">You can track hello progress as hello reviewers complete their reviews in hello Azure AD PIM dashboard, in hello access reviews section.</span></span> <span data-ttu-id="2d143-143">Нет прав доступа будет изменен в каталоге hello до [завершения проверки hello](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="2d143-143">No access rights will be changed in hello directory until [hello review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="2d143-144">До окончания периода hello проверки вы можете напомнить пользователям toocomplete просмотра или просмотрите hello stop раннее из hello access просматривает раздел.</span><span class="sxs-lookup"><span data-stu-id="2d143-144">Until hello review period is over, you can remind users toocomplete their review, or stop hello review early from hello access reviews section.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="2d143-145">Материалы по управлению привилегированными пользователями</span><span class="sxs-lookup"><span data-stu-id="2d143-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
