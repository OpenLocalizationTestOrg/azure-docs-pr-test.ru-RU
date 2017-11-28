---
title: "Удаление доступа пользователя к приложению | Документация Майкрософт"
description: "Общие сведения об удалении доступа пользователя к приложению"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="2810b-103">Удаление доступа пользователя к приложению</span><span class="sxs-lookup"><span data-stu-id="2810b-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="2810b-104">В этой статье представлены сведения об удалении доступа пользователя к приложению.</span><span class="sxs-lookup"><span data-stu-id="2810b-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="2810b-105">Я хочу удалить назначение определенного пользователя или группы приложению</span><span class="sxs-lookup"><span data-stu-id="2810b-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="2810b-106">Чтобы удалить назначение пользователя или группы приложению, выполните действия, описанные в статье [Удаление назначения доступа к корпоративному приложению для пользователя или группы в предварительной версии Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="2810b-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="2810b-107">Я хочу отключить доступ к приложению для всех пользователей</span><span class="sxs-lookup"><span data-stu-id="2810b-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="2810b-108">Чтобы отключить вход в приложение для всех пользователей, выполните действия, описанные в статье [Отключение входа пользователя в корпоративное приложение в предварительной версии Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="2810b-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="2810b-109">Я хочу полностью удалить приложение</span><span class="sxs-lookup"><span data-stu-id="2810b-109">I want to delete an application entirely</span></span>

<span data-ttu-id="2810b-110">Чтобы **удалить приложение**, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="2810b-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="2810b-111">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="2810b-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="2810b-112">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2810b-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2810b-113">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2810b-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2810b-114">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="2810b-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="2810b-115">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="2810b-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="2810b-116">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2810b-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="2810b-117">Выберите приложение, которое требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="2810b-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="2810b-118">После загрузки приложения щелкните значок **Удалить** в колонке **Обзор** для часто используемых приложений.</span><span class="sxs-lookup"><span data-stu-id="2810b-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="2810b-119">Я хочу отключить все будущие операции пользователя по предоставлению согласия для всех приложений</span><span class="sxs-lookup"><span data-stu-id="2810b-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="2810b-120">Если вы отключите для всего каталога возможность предоставлять согласие, пользователь не сможет согласиться с условиями использования приложения.</span><span class="sxs-lookup"><span data-stu-id="2810b-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="2810b-121">Администратор сохранит возможность предоставлять согласие от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="2810b-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="2810b-122">Дополнительные сведения о согласии в приложениях и возможных мотивах для его отключения или предоставления см. в разделе [Получение согласия пользователя и администратора](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="2810b-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="2810b-123">Чтобы **отключить все будущие операции по предоставлению согласия пользователя во всем каталоге**, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2810b-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="2810b-124">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="2810b-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="2810b-125">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="2810b-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="2810b-126">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2810b-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="2810b-127">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2810b-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="2810b-128">Щелкните **Параметры пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2810b-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="2810b-129">Отключите все будущие операции пользователя по предоставлению согласия, установив переключатель **Пользователи могут разрешать приложениям доступ к своим данным** в положение **Нет** и нажав кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2810b-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="2810b-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2810b-130">Next steps</span></span>
[<span data-ttu-id="2810b-131">Управление доступом к приложениям</span><span class="sxs-lookup"><span data-stu-id="2810b-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
