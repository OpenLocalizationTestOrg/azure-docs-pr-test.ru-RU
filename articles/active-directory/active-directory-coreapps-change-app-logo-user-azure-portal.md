---
title: "Изменение имени или логотипа корпоративного приложения в Azure Active Directory | Документы Майкрософт"
description: "Узнайте, как изменить имя или логотип настраиваемого корпоративного приложения в Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="5be5c-103">Изменение имени или логотипа корпоративного приложения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5be5c-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="5be5c-104">Вы можете легко изменить имя или логотип настраиваемого корпоративного приложения в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5be5c-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5be5c-105">Для внесения этих изменений необходимо иметь соответствующие разрешения и быть создателем пользовательского приложения.</span><span class="sxs-lookup"><span data-stu-id="5be5c-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="5be5c-106">Как изменить имя или логотип корпоративного приложения?</span><span class="sxs-lookup"><span data-stu-id="5be5c-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="5be5c-107">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="5be5c-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="5be5c-108">Выберите **Другие службы**, введите **Azure Active Directory** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="5be5c-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="5be5c-109">В колонке **Azure Active Directory — *имя_каталога*** (то есть в колонке Azure AD для каталога, которым вы управляете) выберите **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5be5c-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="5be5c-111">В колонке **Корпоративные приложения** выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5be5c-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="5be5c-112">Отобразится список приложений, которыми можно управлять.</span><span class="sxs-lookup"><span data-stu-id="5be5c-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="5be5c-113">В колонке **Корпоративные приложения — Все приложения** выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="5be5c-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="5be5c-114">В колонке ***имя_приложения*** (то есть в колонке с именем выбранного приложения в заголовке) выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="5be5c-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Выбор команды "Свойства"](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="5be5c-116">В колонке ***имя_приложения*** **— свойства** укажите файл нового логотипа или измените имя приложения.</span><span class="sxs-lookup"><span data-stu-id="5be5c-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![Изменение свойств для логотипа или имени приложения](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="5be5c-118">Щелкните **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5be5c-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5be5c-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5be5c-119">Next steps</span></span>
* [<span data-ttu-id="5be5c-120">Просмотр всех моих групп</span><span class="sxs-lookup"><span data-stu-id="5be5c-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="5be5c-121">Назначение корпоративному приложению пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="5be5c-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="5be5c-122">Удаление назначения пользователя или группы из корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="5be5c-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="5be5c-123">Отключение входа пользователя в корпоративное приложение</span><span class="sxs-lookup"><span data-stu-id="5be5c-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
