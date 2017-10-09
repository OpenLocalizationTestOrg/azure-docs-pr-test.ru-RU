---
title: "Назначение пользователя или группу из корпоративного приложения в Azure Active Directory aaaRemove | Документы Microsoft"
description: "Как tooremove hello доступ к назначение пользователя или группы из корпоративного приложения в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="a8753-103">Удаление назначения доступа к корпоративному приложению для пользователя или группы в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8753-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="a8753-104">Это легко tooremove пользователя или группу из присвоенного tooone доступ корпоративных приложений в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8753-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a8753-105">Необходимо иметь hello соответствующие разрешения toomanage hello приложений и должен быть глобальным администратором для каталога hello.</span><span class="sxs-lookup"><span data-stu-id="a8753-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="a8753-106">Как удалить назначение пользователя или группы?</span><span class="sxs-lookup"><span data-stu-id="a8753-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="a8753-107">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="a8753-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="a8753-108">Выберите **дополнительные службы**, введите **Azure Active Directory** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="a8753-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="a8753-109">На hello **Azure Active Directory — *directoryname***  колонке (то есть hello Azure AD колонке hello каталога, вы управляете) выберите **корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a8753-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="a8753-111">На hello **корпоративных приложений** колонке выберите **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8753-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="a8753-112">Вы увидите список hello приложений, которыми можно управлять.</span><span class="sxs-lookup"><span data-stu-id="a8753-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="a8753-113">На hello **корпоративных приложений - все приложения** колонке выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="a8753-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="a8753-114">На hello ***appname*** колонке (то есть hello колонке с именем hello выбранного приложения hello в заголовок hello) выберите **пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a8753-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Выбор пользователей или групп](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="a8753-116">На hello ***appname*** **-пользователей и Назначение группы** колонки, выберите один из нескольких пользователей или групп, а затем выберите hello **удалить** команды.</span><span class="sxs-lookup"><span data-stu-id="a8753-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="a8753-117">Подтвердите решение в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="a8753-117">Confirm your decision at hello prompt.</span></span>

    ![Команда Remove hello](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="a8753-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8753-119">Next steps</span></span>
* [<span data-ttu-id="a8753-120">Просмотр всех моих групп</span><span class="sxs-lookup"><span data-stu-id="a8753-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="a8753-121">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="a8753-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="a8753-122">Отключение входа пользователя в корпоративное приложение</span><span class="sxs-lookup"><span data-stu-id="a8753-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="a8753-123">Изменение имени hello или логотип корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="a8753-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
