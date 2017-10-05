---
title: "Запуск проверки доступа | Документация Майкрософт"
description: "Узнайте, как создать проверку доступа для привилегированных пользователей с помощью приложения управления привилегированными пользователями Azure."
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
ms.openlocfilehash: 2b516e2f05aa883c5e37f5864e5ee8a2b37d3a46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="47dcc-103">Как запустить проверку доступа в управлении привилегированными пользователями Azure AD</span><span class="sxs-lookup"><span data-stu-id="47dcc-103">How to start an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="47dcc-104">Назначения ролей становятся "устаревшими", когда у пользователей имеются права привилегированного доступа, которые им больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="47dcc-104">Role assignments become "stale" when users have privileged access that they don't need anymore.</span></span> <span data-ttu-id="47dcc-105">Чтобы снизить риск, связанный с "устаревшими" назначениями ролей, администраторы привилегированных ролей должны периодически проверять назначенные пользователям роли.</span><span class="sxs-lookup"><span data-stu-id="47dcc-105">In order to reduce the risk associated with these stale role assignments, privileged role administrators should regularly review the roles that users have been given.</span></span> <span data-ttu-id="47dcc-106">В этом документе рассматривается процедура запуска проверки доступа в компоненте Azure AD Privileged Identity Management (PIM).</span><span class="sxs-lookup"><span data-stu-id="47dcc-106">This document covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).</span></span>

## <a name="start-an-access-review"></a><span data-ttu-id="47dcc-107">Запуск проверки доступа</span><span class="sxs-lookup"><span data-stu-id="47dcc-107">Start an access review</span></span>
> [!NOTE]
> <span data-ttu-id="47dcc-108">Если вы еще не добавили приложение PIM на панель мониторинга портала Azure, ознакомьтесь с инструкциями в статье [Приступая к работе с управлением привилегированными пользователями Azure AD](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="47dcc-108">If you haven't added the PIM application to your dashboard in the Azure portal, see the steps in  [Getting Started with Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)</span></span>
> 
> 

<span data-ttu-id="47dcc-109">Есть три способа запуска проверки доступа с главной страницы приложения PIM:</span><span class="sxs-lookup"><span data-stu-id="47dcc-109">From the PIM application main page, there are three ways to start an access review:</span></span>

* <span data-ttu-id="47dcc-110">Выберите **Проверки доступа** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="47dcc-110">**Access reviews** > **Add**</span></span>
* <span data-ttu-id="47dcc-111">Выберите **Роли** > кнопка **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="47dcc-111">**Roles** > **Review** button</span></span>
* <span data-ttu-id="47dcc-112">Из списка ролей выберите одну роль, которую необходимо проверить, и нажмите кнопку **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="47dcc-112">Select the specific role to be reviewed from the roles list > **Review** button</span></span>

<span data-ttu-id="47dcc-113">После нажатия кнопки **Проверить** появится колонка **Начало проверки доступа**.</span><span class="sxs-lookup"><span data-stu-id="47dcc-113">When you click on the **Review** button, the **Start an access review** blade appears.</span></span> <span data-ttu-id="47dcc-114">В этой колонке можно ввести имя проверки, настроить ее временной интервал, выбрать проверяемую роль, а также решить, кто будет выполнять проверку.</span><span class="sxs-lookup"><span data-stu-id="47dcc-114">On this blade, you're going to configure the review with a name and time limit, choose a role to review, and decide who will perform the review.</span></span>

![Запуск проверки доступа — снимок экрана][1]

### <a name="configure-the-review"></a><span data-ttu-id="47dcc-116">Настройка проверки</span><span class="sxs-lookup"><span data-stu-id="47dcc-116">Configure the review</span></span>
<span data-ttu-id="47dcc-117">Чтобы создать проверку доступа, необходимо присвоить ей имя и указать даты начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="47dcc-117">To create an access review, you need to name it and set a start and end date.</span></span>

![Настройка проверки — снимок экрана][2]

<span data-ttu-id="47dcc-119">Укажите продолжительность проверки, достаточную для ее выполнения пользователями.</span><span class="sxs-lookup"><span data-stu-id="47dcc-119">Make the length of the review long enough for users to complete it.</span></span> <span data-ttu-id="47dcc-120">Если проверка завершена до выбранной даты окончания, то ее всегда можно остановить досрочно.</span><span class="sxs-lookup"><span data-stu-id="47dcc-120">If you finish before the end date, you can always stop the review early.</span></span>

### <a name="choose-a-role-to-review"></a><span data-ttu-id="47dcc-121">Выбор проверяемой роли</span><span class="sxs-lookup"><span data-stu-id="47dcc-121">Choose a role to review</span></span>
<span data-ttu-id="47dcc-122">Каждая проверка фокусируется только на одной роли.</span><span class="sxs-lookup"><span data-stu-id="47dcc-122">Each review focuses on only one role.</span></span> <span data-ttu-id="47dcc-123">Если проверка доступа не запущена из колонки определенной роли, то на данном этапе необходимо выбрать роль.</span><span class="sxs-lookup"><span data-stu-id="47dcc-123">Unless you started the access review from a specific role blade, you'll need to choose a role now.</span></span>

1. <span data-ttu-id="47dcc-124">Перейдите к разделу **Проверка членства в роли**</span><span class="sxs-lookup"><span data-stu-id="47dcc-124">Navigate to **Review role membership**</span></span>
   
    ![Проверка членства в роли — снимок экрана][3]
2. <span data-ttu-id="47dcc-126">Выберите роль из списка.</span><span class="sxs-lookup"><span data-stu-id="47dcc-126">Choose one role from the list.</span></span>

### <a name="decide-who-will-perform-the-review"></a><span data-ttu-id="47dcc-127">Выбор пользователя, который будет выполнять проверку</span><span class="sxs-lookup"><span data-stu-id="47dcc-127">Decide who will perform the review</span></span>
<span data-ttu-id="47dcc-128">Существует три способа выполнения проверки.</span><span class="sxs-lookup"><span data-stu-id="47dcc-128">There are three options for performing a review.</span></span> <span data-ttu-id="47dcc-129">Можно назначить выполнение проверки другому пользователю, можно сделать это самостоятельно, или же каждый пользователь может проверить свой доступ.</span><span class="sxs-lookup"><span data-stu-id="47dcc-129">You can assign the review to someone else to complete, you can do it yourself, or you can have each user review their own access.</span></span>

1. <span data-ttu-id="47dcc-130">Перейдите к разделу **Выбор проверяющих**</span><span class="sxs-lookup"><span data-stu-id="47dcc-130">Navigate to **Select reviewers**</span></span>
   
    ![Выбор проверяющих — снимок экрана][4]
2. <span data-ttu-id="47dcc-132">Выберите один из способов:</span><span class="sxs-lookup"><span data-stu-id="47dcc-132">Choose one of the options:</span></span>
   
   * <span data-ttu-id="47dcc-133">**Выбор рецензента**: используйте этот параметр, если вы не знаете, кому нужен доступ.</span><span class="sxs-lookup"><span data-stu-id="47dcc-133">**Select reviewer**: Use this option when you don't know who needs access.</span></span> <span data-ttu-id="47dcc-134">С помощью этого параметра можно назначить выполнение проверки владельцу ресурса или руководителю группы.</span><span class="sxs-lookup"><span data-stu-id="47dcc-134">With this option, you can assign the review to a resource owner or group manager to complete.</span></span>
   * <span data-ttu-id="47dcc-135">**Я**: этот способ полезен, если требуется просмотреть, как действует проверка доступа, или если вы хотите выполнить проверку от имени пользователей, которые не могут это сделать сами.</span><span class="sxs-lookup"><span data-stu-id="47dcc-135">**Me**: Useful if you want to preview how access reviews work, or you want to review on behalf of people who can't.</span></span>
   * <span data-ttu-id="47dcc-136">**Members review themselves**(Участники проверяют себя сами): выберите этот способ, чтобы пользователи сами проверили назначенные им роли.</span><span class="sxs-lookup"><span data-stu-id="47dcc-136">**Members review themselves**: Use this option to have the users review their own role assignments.</span></span>

### <a name="start-the-review"></a><span data-ttu-id="47dcc-137">Запуск проверки</span><span class="sxs-lookup"><span data-stu-id="47dcc-137">Start the review</span></span>
<span data-ttu-id="47dcc-138">В завершение стоит добавить, что имеется возможность запросить у пользователей указать причину, если они подтверждают свой доступ.</span><span class="sxs-lookup"><span data-stu-id="47dcc-138">Finally, you have the option to require that users provide a reason if they approve their access.</span></span> <span data-ttu-id="47dcc-139">При необходимости добавьте описание проверки и нажмите кнопку **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="47dcc-139">Add a description of the review if you like, and select **Start**.</span></span>

<span data-ttu-id="47dcc-140">Убедитесь, что пользователи знают об ожидающей их проверке доступа, и покажите им, [как выполнить эту проверку](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="47dcc-140">Make sure you let your users know that there's an access review waiting for them, and show them [How to perform an access review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

## <a name="manage-the-access-review"></a><span data-ttu-id="47dcc-141">Управление проверкой доступа</span><span class="sxs-lookup"><span data-stu-id="47dcc-141">Manage the access review</span></span>
<span data-ttu-id="47dcc-142">Отслеживать ход выполнения проверяющими их проверок можно на панели мониторинга Azure AD PIM в разделе "Проверки доступа".</span><span class="sxs-lookup"><span data-stu-id="47dcc-142">You can track the progress as the reviewers complete their reviews in the Azure AD PIM dashboard, in the access reviews section.</span></span> <span data-ttu-id="47dcc-143">Права доступа в каталоге не изменяются до [завершения проверки](active-directory-privileged-identity-management-how-to-complete-review.md).</span><span class="sxs-lookup"><span data-stu-id="47dcc-143">No access rights will be changed in the directory until [the review completes](active-directory-privileged-identity-management-how-to-complete-review.md).</span></span>

<span data-ttu-id="47dcc-144">Пока не истек заданный временной интервал, можно напомнить пользователям о необходимости завершить проверку. Также в разделе "Проверки доступа" можно остановить выполнение проверки досрочно.</span><span class="sxs-lookup"><span data-stu-id="47dcc-144">Until the review period is over, you can remind users to complete their review, or stop the review early from the access reviews section.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a><span data-ttu-id="47dcc-145">Материалы по управлению привилегированными пользователями</span><span class="sxs-lookup"><span data-stu-id="47dcc-145">PIM Table of Contents</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
