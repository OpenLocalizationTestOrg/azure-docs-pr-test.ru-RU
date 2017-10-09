---
title: "aaaDisable пользователя войти в приложение в Azure Active Directory предприятия | Документы Microsoft"
description: "Как toodisable приложения предприятия, чтобы пользователи не могут войти в tooit в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="23dcc-103">Отключение входа пользователя в корпоративное приложение в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23dcc-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="23dcc-104">Это легко toodisable приложения предприятия, чтобы пользователи не могут войти в tooit в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="23dcc-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="23dcc-105">Необходимо иметь hello соответствующие разрешения toomanage hello приложений и должен быть глобальным администратором для каталога hello.</span><span class="sxs-lookup"><span data-stu-id="23dcc-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="23dcc-106">Как отключить вход пользователей?</span><span class="sxs-lookup"><span data-stu-id="23dcc-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="23dcc-107">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="23dcc-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="23dcc-108">Выберите **дополнительные службы**, введите **Azure Active Directory** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="23dcc-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="23dcc-109">На hello **Azure Active Directory** -  ***directoryname*** колонке (то есть hello Azure AD колонке hello каталога, вы управляете) выберите **корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="23dcc-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="23dcc-111">На hello **корпоративных приложений** колонке выберите **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="23dcc-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="23dcc-112">Появится список hello приложений, которыми можно управлять.</span><span class="sxs-lookup"><span data-stu-id="23dcc-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="23dcc-113">На hello **корпоративных приложений - все приложения** колонке выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="23dcc-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="23dcc-114">На hello ***appname*** колонке (то есть hello колонке с именем hello выбранного приложения hello в заголовок hello) выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="23dcc-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![При выборе команды все приложения "hello"](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="23dcc-116">На hello ***appname*** - **свойства** колонке выберите **нет** для **доступна для пользователей в toosign?**.</span><span class="sxs-lookup"><span data-stu-id="23dcc-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="23dcc-117">Выберите hello **Сохранить** команды.</span><span class="sxs-lookup"><span data-stu-id="23dcc-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23dcc-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23dcc-118">Next steps</span></span>
* [<span data-ttu-id="23dcc-119">Просмотр всех моих групп</span><span class="sxs-lookup"><span data-stu-id="23dcc-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="23dcc-120">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="23dcc-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="23dcc-121">Удаление назначения пользователя или группы из корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="23dcc-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="23dcc-122">Изменение имени hello или логотип корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="23dcc-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
