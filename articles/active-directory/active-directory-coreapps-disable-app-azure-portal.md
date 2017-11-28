---
title: "Отключение входа пользователя в корпоративное приложение в Azure Active Directory | Документы Майкрософт"
description: "Узнайте, как в Azure Active Directory можно отключить корпоративное приложение, чтобы пользователи не могли войти в него."
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
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="c667e-103">Отключение входа пользователя в корпоративное приложение в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c667e-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="c667e-104">В Azure Active Directory (Azure AD) вы можете легко отключить корпоративное приложение, чтобы пользователи не могли войти в него.</span><span class="sxs-lookup"><span data-stu-id="c667e-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c667e-105">Необходимо иметь соответствующие разрешения для управления корпоративным приложением, а также права глобального администратора для доступа к каталогу.</span><span class="sxs-lookup"><span data-stu-id="c667e-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="c667e-106">Как отключить вход пользователей?</span><span class="sxs-lookup"><span data-stu-id="c667e-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="c667e-107">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="c667e-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c667e-108">Выберите **Другие службы**, введите **Azure Active Directory** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="c667e-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="c667e-109">В колонке **Azure Active Directory** -  ***имя_каталога*** (то есть в колонке Azure AD для каталога, которым вы управляете) выберите **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c667e-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="c667e-111">В колонке **Корпоративные приложения** выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c667e-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="c667e-112">Отобразится список приложений, которыми можно управлять.</span><span class="sxs-lookup"><span data-stu-id="c667e-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="c667e-113">В колонке **Корпоративные приложения — Все приложения** выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="c667e-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="c667e-114">В колонке ***имя_приложения*** (то есть в колонке с именем выбранного приложения в заголовке) выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="c667e-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Выбор команды "Все приложения"](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="c667e-116">В колонке ***имя_приложения*** - **Свойства** для параметра **Включен ли вход для пользователей?** выберите значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="c667e-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="c667e-117">Щелкните **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c667e-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c667e-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c667e-118">Next steps</span></span>
* [<span data-ttu-id="c667e-119">Просмотр всех моих групп</span><span class="sxs-lookup"><span data-stu-id="c667e-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c667e-120">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="c667e-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="c667e-121">Удаление назначения пользователя или группы из корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="c667e-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="c667e-122">Изменение имени или логотипа корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="c667e-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
