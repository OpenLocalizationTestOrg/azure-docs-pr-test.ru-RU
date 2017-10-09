---
title: "aaaChange hello логотипа корпоративного приложения в Azure Active Directory или имя | Документы Microsoft"
description: "Как toochange hello логотипа для корпоративные приложения в Azure Active Directory или имя"
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
ms.openlocfilehash: b660e1f0f6c7ffd626e17e2e3399e7169f6e8bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="9fee0-103">Изменение имени hello или логотип корпоративного приложения в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fee0-103">Change hello name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="9fee0-104">Это легко toochange hello названия или эмблемы для корпоративные приложения в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9fee0-104">It's easy toochange hello name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9fee0-105">Необходимо иметь соответствующие разрешения toomake hello эти изменения, и должен быть hello автор пользовательского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9fee0-105">You must have hello appropriate permissions toomake these changes, and you must be hello creator of hello custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="9fee0-106">Как изменить имя или логотип корпоративного приложения?</span><span class="sxs-lookup"><span data-stu-id="9fee0-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="9fee0-107">Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="9fee0-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="9fee0-108">Выберите **дополнительные службы**, введите **Azure Active Directory** в hello текстовое поле, а затем выберите **ввод**.</span><span class="sxs-lookup"><span data-stu-id="9fee0-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="9fee0-109">На hello **Azure Active Directory — *directoryname***  колонке (то есть hello Azure AD колонке hello каталога, вы управляете) выберите **корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="9fee0-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Открытие колонки "Корпоративные приложения"](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="9fee0-111">На hello **корпоративных приложений** колонке выберите **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9fee0-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="9fee0-112">Вы увидите список hello приложений, которыми можно управлять.</span><span class="sxs-lookup"><span data-stu-id="9fee0-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="9fee0-113">На hello **корпоративных приложений - все приложения** колонке выберите приложение.</span><span class="sxs-lookup"><span data-stu-id="9fee0-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="9fee0-114">На hello ***appname*** колонке (то есть hello колонке с именем hello выбранного приложения hello в заголовок hello) выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="9fee0-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![При выборе команды свойства hello](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="9fee0-116">На hello ***appname*** **-свойства** колонке поиск файла toouse как новый логотип, или изменение имени приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9fee0-116">On hello ***appname*** **- Properties** blade, browse for a file toouse as a new logo, or edit hello app name, or both.</span></span>

    ![Изменение эмблемы или nameproperties команда приложения hello](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="9fee0-118">Выберите hello **Сохранить** команды.</span><span class="sxs-lookup"><span data-stu-id="9fee0-118">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fee0-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fee0-119">Next steps</span></span>
* [<span data-ttu-id="9fee0-120">Просмотр всех моих групп</span><span class="sxs-lookup"><span data-stu-id="9fee0-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="9fee0-121">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="9fee0-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="9fee0-122">Удаление назначения пользователя или группы из корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="9fee0-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="9fee0-123">Отключение входа пользователя в корпоративное приложение</span><span class="sxs-lookup"><span data-stu-id="9fee0-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
