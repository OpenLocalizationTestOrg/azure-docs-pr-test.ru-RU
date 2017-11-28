---
title: "aaaHow приложения отображаются на панели доступа hello | Документы Microsoft"
description: "Устранение неполадок, поэтому приложения, отображаются в панели доступа hello"
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
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="1790d-103">Как приложения отображаются на панели доступа hello</span><span class="sxs-lookup"><span data-stu-id="1790d-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="1790d-104">Hello панель доступа является Интернет-порталом, который позволяет пользователю с помощью рабочей или рабочую учетную запись в Azure Active Directory (Azure AD) tooview и запуск облачных приложений, hello администратор Azure AD им предоставлен доступ.</span><span class="sxs-lookup"><span data-stu-id="1790d-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="1790d-105">Эти приложения настроены от имени пользователя hello hello портала Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1790d-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="1790d-106">Здравствуйте, администратор может подготовить пользователя toohello приложения hello напрямую или пользователь является частью приведет к приложения hello, отображаемых на панели доступа пользователя hello tooa группы.</span><span class="sxs-lookup"><span data-stu-id="1790d-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="1790d-107">Общие проблемы toocheck сначала</span><span class="sxs-lookup"><span data-stu-id="1790d-107">General issues toocheck first</span></span>

-   <span data-ttu-id="1790d-108">Если приложение только что был удален из пользователь или группа hello пользователь является членом, повторите toosign и выхода из системы в hello пользовательской панели доступа после нескольких минут toosee при удалении приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1790d-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="1790d-109">Если лицензия только что был удален из пользователь или группа hello пользователь является членом это может занять много времени, в зависимости от hello размера и сложности hello группы для toobe изменения внесены.</span><span class="sxs-lookup"><span data-stu-id="1790d-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="1790d-110">Разрешить дополнительное время, прежде чем войти в панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="1790d-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="1790d-111">Проблемы tooassigning связанных приложений toousers</span><span class="sxs-lookup"><span data-stu-id="1790d-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="1790d-112">Пользователь может отображается приложения на своей панели доступа потому, что они ей ранее была назначена tooit.</span><span class="sxs-lookup"><span data-stu-id="1790d-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="1790d-113">Ниже приведены некоторые способы toocheck.</span><span class="sxs-lookup"><span data-stu-id="1790d-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="1790d-114">Проверьте, если пользователю назначено toohello приложения</span><span class="sxs-lookup"><span data-stu-id="1790d-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="1790d-115">Проверьте, является ли пользователь по лицензии связанных toohello приложения</span><span class="sxs-lookup"><span data-stu-id="1790d-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="1790d-116">Проверьте, если пользователю назначено toohello приложения</span><span class="sxs-lookup"><span data-stu-id="1790d-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="1790d-117">toocheck, если пользователю назначено toohello приложения, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="1790d-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1790d-118">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="1790d-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1790d-119">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="1790d-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1790d-120">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="1790d-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1790d-121">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="1790d-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1790d-122">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="1790d-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="1790d-123">**Поиск** для hello имя приложения hello в вопросе.</span><span class="sxs-lookup"><span data-stu-id="1790d-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="1790d-124">Выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1790d-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="1790d-125">Проверьте toosee, если пользователю назначено toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="1790d-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="1790d-126">Если требуется, чтобы пользователь hello tooremove из приложения hello **щелкните строку hello** пользователя hello и выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="1790d-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="1790d-127">Проверьте, является ли пользователь по лицензии связанных toohello приложения</span><span class="sxs-lookup"><span data-stu-id="1790d-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="1790d-128">toocheck пользователя назначить лицензии, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="1790d-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="1790d-129">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="1790d-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1790d-130">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="1790d-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1790d-131">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="1790d-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1790d-132">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="1790d-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1790d-133">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="1790d-133">click **All users**.</span></span>

6.  <span data-ttu-id="1790d-134">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1790d-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1790d-135">Нажмите кнопку **лицензий** toosee hello какие лицензии пользователя в настоящее время назначено.</span><span class="sxs-lookup"><span data-stu-id="1790d-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="1790d-136">Здравствуйте, если hello пользователю назначается лицензия Office tooan это включить tooappear приложений первой стороной Office на панели доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="1790d-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="1790d-137">Проблемы tooassigning связанных приложений toogroups</span><span class="sxs-lookup"><span data-stu-id="1790d-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="1790d-138">Пользователь видите приложения на своей панели доступа, так как они являются частью группы, имеющей разрешение приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1790d-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="1790d-139">Ниже приведены некоторые способы toocheck.</span><span class="sxs-lookup"><span data-stu-id="1790d-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="1790d-140">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="1790d-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="1790d-141">Установите флажок, если пользователь является членом группы, назначает tooa лицензию</span><span class="sxs-lookup"><span data-stu-id="1790d-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="1790d-142">Проверка членства пользователя в группах</span><span class="sxs-lookup"><span data-stu-id="1790d-142">Check a user’s group memberships</span></span>

<span data-ttu-id="1790d-143">toocheck членство в группе, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="1790d-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="1790d-144">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="1790d-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1790d-145">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="1790d-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1790d-146">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="1790d-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1790d-147">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="1790d-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1790d-148">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="1790d-148">click **All users**.</span></span>

6.  <span data-ttu-id="1790d-149">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1790d-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1790d-150">Щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="1790d-150">click **Groups.**</span></span>

8.  <span data-ttu-id="1790d-151">Проверка toosee, если пользователь входит в состав группы назначить toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="1790d-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="1790d-152">Если требуется, чтобы tooremove hello пользователя из группы hello **щелкните строку hello** hello группы и выберите Удалить.</span><span class="sxs-lookup"><span data-stu-id="1790d-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="1790d-153">Установите флажок, если пользователь является членом группы, назначает tooa лицензию</span><span class="sxs-lookup"><span data-stu-id="1790d-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="1790d-154">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="1790d-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1790d-155">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="1790d-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1790d-156">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="1790d-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1790d-157">Нажмите кнопку **пользователей и групп** в меню навигации hello.</span><span class="sxs-lookup"><span data-stu-id="1790d-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="1790d-158">Щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="1790d-158">click **All users**.</span></span>

6.  <span data-ttu-id="1790d-159">**Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="1790d-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="1790d-160">Щелкните **Группы**.</span><span class="sxs-lookup"><span data-stu-id="1790d-160">click **Groups.**</span></span>

8.  <span data-ttu-id="1790d-161">Щелкните строку hello в определенную группу.</span><span class="sxs-lookup"><span data-stu-id="1790d-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="1790d-162">Нажмите кнопку **лицензий** toosee, какую группу лицензий hello назначила tooit.</span><span class="sxs-lookup"><span data-stu-id="1790d-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="1790d-163">Здравствуйте, если группа hello назначена лицензия Office tooan, это может включить определенные tooappear приложений первой стороной Office на панели доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="1790d-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="1790d-164">Если эти действия по устранению неполадок не hello устраните проблему hello</span><span class="sxs-lookup"><span data-stu-id="1790d-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="1790d-165">Откройте запрос в службу поддержки с hello следующую информацию, если они доступны:</span><span class="sxs-lookup"><span data-stu-id="1790d-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="1790d-166">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="1790d-166">Correlation error ID</span></span>

-   <span data-ttu-id="1790d-167">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="1790d-167">UPN (user email address)</span></span>

-   <span data-ttu-id="1790d-168">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="1790d-168">Tenant ID</span></span>

-   <span data-ttu-id="1790d-169">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="1790d-169">Browser type</span></span>

-   <span data-ttu-id="1790d-170">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="1790d-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="1790d-171">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="1790d-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="1790d-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1790d-172">Next steps</span></span>
[<span data-ttu-id="1790d-173">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1790d-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
