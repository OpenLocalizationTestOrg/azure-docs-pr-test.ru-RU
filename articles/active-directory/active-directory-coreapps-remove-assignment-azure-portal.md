---
title: "Удаление назначения доступа к корпоративному приложению для пользователя или группы в Azure Active Directory | Документы Майкрософт"
description: "Узнайте, как удалить назначение доступа к корпоративному приложению для пользователя или группы в Azure Active Directory."
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
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="c8159-103">Удаление назначения доступа к корпоративному приложению для пользователя или группы в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8159-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="c8159-104">Вы можете легко удалить назначение доступа к корпоративному приложению для пользователя или группы в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c8159-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c8159-105">Необходимо иметь соответствующие разрешения для управления корпоративным приложением, а также права глобального администратора для доступа к каталогу.</span><span class="sxs-lookup"><span data-stu-id="c8159-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="c8159-106">Как удалить назначение пользователя или группы?</span><span class="sxs-lookup"><span data-stu-id="c8159-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="c8159-107">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="c8159-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c8159-108">Выберите **Другие службы**, введите **Azure Active Directory** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="c8159-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="c8159-109">В колонке **Azure Active Directory — *имя_каталога*** (то есть в колонке Azure AD для каталога, которым вы управляете) выберите **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c8159-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="c8159-111">В колонке **Корпоративные приложения** выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c8159-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="c8159-112">Отобразится список приложений, которыми можно управлять.</span><span class="sxs-lookup"><span data-stu-id="c8159-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="c8159-113">В колонке **Корпоративные приложения — Все приложения** выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="c8159-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="c8159-114">В колонке ***имя_приложения*** (то есть в колонке с именем выбранного приложения в заголовке) выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c8159-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Выбор пользователей или групп](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="c8159-116">В колонке ***имя_приложения*** **— User &amp; Group Assignment** (Назначение групп и пользователей) выберите одного из несколько пользователей или групп, а затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="c8159-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="c8159-117">При появлении запроса подтвердите свое решение.</span><span class="sxs-lookup"><span data-stu-id="c8159-117">Confirm your decision at the prompt.</span></span>

    ![Выбор команды "Удалить"](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="c8159-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8159-119">Next steps</span></span>
* [<span data-ttu-id="c8159-120">Просмотр всех моих групп</span><span class="sxs-lookup"><span data-stu-id="c8159-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c8159-121">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="c8159-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="c8159-122">Отключение входа пользователя в корпоративное приложение</span><span class="sxs-lookup"><span data-stu-id="c8159-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="c8159-123">Изменение имени или логотипа корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="c8159-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
