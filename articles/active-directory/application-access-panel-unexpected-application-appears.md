---
title: "Отображение приложений на панели доступа | Документация Майкрософт"
description: "Устранение неполадки с отображением приложения на панели доступа"
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
ms.reviewr: japere
ms.openlocfilehash: f8ccf2cf66b49940bc7f2b9f4764020efc04838e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="b43df-103">Отображение приложений на панели доступа</span><span class="sxs-lookup"><span data-stu-id="b43df-103">How applications appear on the access panel</span></span>

<span data-ttu-id="b43df-104">Панель доступа — это веб-портал, который позволяет пользователям, имеющим рабочую или учебную учетную запись Azure Active Directory (Azure AD), просматривать и запускать облачные приложения, к которым администратор Azure AD предоставил доступ.</span><span class="sxs-lookup"><span data-stu-id="b43df-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="b43df-105">Эти приложения настраиваются от имени пользователя на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b43df-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="b43df-106">Администратор может подготовить приложение непосредственно для пользователя или для группы, в которую он входит, после чего приложение появится на панели доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="b43df-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="b43df-107">Общие проблемы для первоначальной проверки</span><span class="sxs-lookup"><span data-stu-id="b43df-107">General issues to check first</span></span>

-   <span data-ttu-id="b43df-108">Если приложение было просто удалено у пользователя или в группе, в которую он входит, попробуйте выйти с панели доступа пользователя и войти на нее через несколько минут, чтобы узнать, удалено ли приложение.</span><span class="sxs-lookup"><span data-stu-id="b43df-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="b43df-109">Если лицензия была только что удалена для пользователя или группы, в которую он входит, внесение изменений может занять много времени в зависимости от размера и сложности группы.</span><span class="sxs-lookup"><span data-stu-id="b43df-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="b43df-110">Подождите некоторое время, прежде чем входить на панель доступа.</span><span class="sxs-lookup"><span data-stu-id="b43df-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="b43df-111">Проблемы, связанные с назначением приложений пользователям</span><span class="sxs-lookup"><span data-stu-id="b43df-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="b43df-112">Пользователь может видеть приложение на панели доступа, так как это приложение было назначено ему ранее.</span><span class="sxs-lookup"><span data-stu-id="b43df-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="b43df-113">Ниже приведены некоторые способы проверки.</span><span class="sxs-lookup"><span data-stu-id="b43df-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="b43df-114">Проверка того, назначено ли приложение пользователю</span><span class="sxs-lookup"><span data-stu-id="b43df-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="b43df-115">Проверка того, назначена ли пользователю лицензия, связанная с приложением</span><span class="sxs-lookup"><span data-stu-id="b43df-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="b43df-116">Проверка того, назначено ли приложение пользователю</span><span class="sxs-lookup"><span data-stu-id="b43df-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="b43df-117">Чтобы проверить, назначено ли приложение пользователю, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b43df-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="b43df-118">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="b43df-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b43df-119">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b43df-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b43df-120">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b43df-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b43df-121">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b43df-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b43df-122">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="b43df-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="b43df-123">Выполните **поиск** по имени нужного приложения.</span><span class="sxs-lookup"><span data-stu-id="b43df-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="b43df-124">Выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b43df-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="b43df-125">Проверьте, назначено ли приложение пользователю.</span><span class="sxs-lookup"><span data-stu-id="b43df-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="b43df-126">Чтобы удалить пользователя из приложения, **щелкните строку** пользователя и выберите команду **удаления**.</span><span class="sxs-lookup"><span data-stu-id="b43df-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="b43df-127">Проверка того, назначена ли пользователю лицензия, связанная с приложением</span><span class="sxs-lookup"><span data-stu-id="b43df-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="b43df-128">Чтобы проверить назначенные пользователю лицензии, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b43df-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="b43df-129">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="b43df-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b43df-130">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b43df-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b43df-131">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b43df-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b43df-132">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b43df-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b43df-133">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b43df-133">click **All users**.</span></span>

6.  <span data-ttu-id="b43df-134">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="b43df-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b43df-135">Чтобы просмотреть лицензии, которые в настоящее время назначены пользователю, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="b43df-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="b43df-136">Если пользователю назначена лицензия Office, на его панели доступа будут отображаться основные приложения Office.</span><span class="sxs-lookup"><span data-stu-id="b43df-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="b43df-137">Проблемы, связанные с назначением приложений группам</span><span class="sxs-lookup"><span data-stu-id="b43df-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="b43df-138">Пользователь может видеть приложение на панели доступа, если он входит в группу, которой назначено это приложение.</span><span class="sxs-lookup"><span data-stu-id="b43df-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="b43df-139">Ниже приведены некоторые способы проверки.</span><span class="sxs-lookup"><span data-stu-id="b43df-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="b43df-140">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="b43df-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="b43df-141">Проверка членства пользователя в группе, назначенной лицензии</span><span class="sxs-lookup"><span data-stu-id="b43df-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="b43df-142">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="b43df-142">Check a user’s group memberships</span></span>

<span data-ttu-id="b43df-143">Чтобы проверить членство в группе, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b43df-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="b43df-144">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="b43df-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b43df-145">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b43df-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b43df-146">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b43df-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b43df-147">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b43df-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b43df-148">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b43df-148">click **All users**.</span></span>

6.  <span data-ttu-id="b43df-149">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="b43df-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b43df-150">Щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="b43df-150">click **Groups.**</span></span>

8.  <span data-ttu-id="b43df-151">Проверьте, входит ли пользователь в группу, которой назначено приложение.</span><span class="sxs-lookup"><span data-stu-id="b43df-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="b43df-152">Чтобы удалить пользователя из группы, **щелкните строку** группы и выберите команду удаления.</span><span class="sxs-lookup"><span data-stu-id="b43df-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="b43df-153">Проверка членства пользователя в группе, назначенной лицензии</span><span class="sxs-lookup"><span data-stu-id="b43df-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="b43df-154">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="b43df-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b43df-155">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b43df-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b43df-156">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b43df-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b43df-157">В меню навигации выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b43df-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="b43df-158">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b43df-158">click **All users**.</span></span>

6.  <span data-ttu-id="b43df-159">**Найдите** нужного пользователя и выберите его, **щелкнув соответствующую строку**.</span><span class="sxs-lookup"><span data-stu-id="b43df-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="b43df-160">Щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="b43df-160">click **Groups.**</span></span>

8.  <span data-ttu-id="b43df-161">Щелкните строку определенной группы.</span><span class="sxs-lookup"><span data-stu-id="b43df-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="b43df-162">Чтобы просмотреть лицензии, которые назначены группе, щелкните **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="b43df-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="b43df-163">Если группе назначена лицензия Office, на панели доступа пользователя могут отображаться некоторые основные приложения Office.</span><span class="sxs-lookup"><span data-stu-id="b43df-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="b43df-164">Если действия по устранению неполадок безрезультатны,</span><span class="sxs-lookup"><span data-stu-id="b43df-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="b43df-165">В таком случае создайте запрос в службу поддержки, указав следующие сведения (при наличии):</span><span class="sxs-lookup"><span data-stu-id="b43df-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="b43df-166">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="b43df-166">Correlation error ID</span></span>

-   <span data-ttu-id="b43df-167">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="b43df-167">UPN (user email address)</span></span>

-   <span data-ttu-id="b43df-168">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="b43df-168">Tenant ID</span></span>

-   <span data-ttu-id="b43df-169">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="b43df-169">Browser type</span></span>

-   <span data-ttu-id="b43df-170">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="b43df-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="b43df-171">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b43df-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="b43df-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b43df-172">Next steps</span></span>
[<span data-ttu-id="b43df-173">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b43df-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
