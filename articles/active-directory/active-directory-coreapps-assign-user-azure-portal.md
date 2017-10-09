---
title: "пользователь или группа tooan приложений в Azure Active Directory aaaAssign | Документы Microsoft"
description: "Как tooselect tooassign приложения enterprise tooit пользователя или группы в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="77207-103">Назначить пользователю или группе tooan приложений в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77207-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="77207-104">Это легко tooassign пользователь или группа tooyour корпоративных приложений в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77207-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="77207-105">Необходимо иметь hello соответствующие разрешения toomanage hello приложений и должен быть глобальным администратором для каталога hello.</span><span class="sxs-lookup"><span data-stu-id="77207-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="77207-106">Как назначить приложений tooan доступ пользователя?</span><span class="sxs-lookup"><span data-stu-id="77207-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="77207-107">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="77207-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="77207-108">Выберите **дополнительные службы**, введите в текстовом поле hello Azure Active Directory и затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="77207-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="77207-109">На hello **Azure Active Directory — *directoryname***  колонке (то есть hello Azure AD колонке hello каталога, вы управляете) выберите **корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="77207-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="77207-111">На hello **корпоративных приложений** колонке выберите **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="77207-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="77207-112">Вы увидите список hello приложений, которыми можно управлять.</span><span class="sxs-lookup"><span data-stu-id="77207-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="77207-113">На hello **корпоративных приложений - все приложения** колонке выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="77207-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="77207-114">На hello ***appname*** колонке (то есть hello колонке с именем hello выбранного приложения hello в заголовок hello) выберите **пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="77207-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![При выборе команды все приложения "hello"](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="77207-116">На hello ***appname*** **-пользователей и Назначение группы** колонки, выберите hello **добавить** команды.</span><span class="sxs-lookup"><span data-stu-id="77207-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="77207-117">На hello **добавить назначение** колонке выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="77207-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Назначьте toohello приложении пользователь или группа](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="77207-119">На hello **пользователей и групп** колонки, выберите один или несколько пользователей или группы из hello и затем выберите hello **выберите** кнопку в нижней части hello колонка hello.</span><span class="sxs-lookup"><span data-stu-id="77207-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="77207-120">На hello **добавить назначение** колонке выберите **роли**.</span><span class="sxs-lookup"><span data-stu-id="77207-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="77207-121">Затем на hello **выберите роль** колонки, выберите роль tooapply toohello выбранных пользователей или групп, а затем выберите hello **ОК** кнопку в нижней части hello колонка hello.</span><span class="sxs-lookup"><span data-stu-id="77207-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="77207-122">На hello **добавить назначение** колонки, выберите hello **назначить** кнопку в нижней части hello колонка hello.</span><span class="sxs-lookup"><span data-stu-id="77207-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="77207-123">Hello назначаются пользователи или группы будут иметь hello разрешениями, определяемыми hello выбранной роли для этого приложения предприятия.</span><span class="sxs-lookup"><span data-stu-id="77207-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77207-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="77207-124">Next steps</span></span>
* [<span data-ttu-id="77207-125">Просмотр всех моих групп</span><span class="sxs-lookup"><span data-stu-id="77207-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="77207-126">Удаление назначения пользователя или группы из корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="77207-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="77207-127">Отключение входа пользователя в корпоративное приложение</span><span class="sxs-lookup"><span data-stu-id="77207-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="77207-128">Изменение имени hello или логотип корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="77207-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
