---
title: "aaaHow tooassign пользователей и групп tooan приложения | Документы Microsoft"
description: "Назначить пользователей доступ toogrant toohello приложения"
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
ms.openlocfilehash: e039a26e4b8f88ad747354859f1071b8f74b6789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-and-groups-tooan-application"></a><span data-ttu-id="35b3f-103">Как приложение tooan tooassign пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="35b3f-103">How tooassign users and groups tooan application</span></span>

<span data-ttu-id="35b3f-104">Для пользователей можно выполнять hello ниже для конкретного приложения, необходимо, чтобы toofirst **их назначение приложения toohello** toogrant им доступа:</span><span class="sxs-lookup"><span data-stu-id="35b3f-104">Before your users can do any of hello below for a specific application, you need toofirst **assign them toohello application** toogrant them access:</span></span>

-   <span data-ttu-id="35b3f-105">Получить доступ к приложению, **навигации непосредственно по URL-адрес приложения toohello** (также известный как инициируемая SP вход).</span><span class="sxs-lookup"><span data-stu-id="35b3f-105">Access an application by **navigating toohello application’s URL directly** (also known as SP-initiated sign-on).</span></span>

-   <span data-ttu-id="35b3f-106">Получить доступ к приложению с помощью hello **URL-адрес пользователя** в приложении **свойства** страницы (также известный как инициированный IDP вход).</span><span class="sxs-lookup"><span data-stu-id="35b3f-106">Access an application by using hello **User Access URL** on an application’s **Properties** page (also known as IDP-initiated sign on).</span></span>

-   <span data-ttu-id="35b3f-107">Выбор приложения на [панели доступа к приложениям](https://myapps.microsoft.com/) или в мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="35b3f-107">See an application appear on their [Application Access Panel](https://myapps.microsoft.com/) or mobile application.</span></span>

-   <span data-ttu-id="35b3f-108">Выбор приложения в [средстве запуска приложений Office 365](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span><span class="sxs-lookup"><span data-stu-id="35b3f-108">See an application appear on their [Office 365 Application Launcher](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a).</span></span>

## <a name="methods-tooassign-applications-with-azure-active-directory"></a><span data-ttu-id="35b3f-109">Методы tooassign приложений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35b3f-109">Methods tooassign applications with Azure Active Directory</span></span> 

<span data-ttu-id="35b3f-110">Существует 3 способа назначения приложений с помощью Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="35b3f-110">There are 3 ways you can assign applications with Azure Active Directory:</span></span>

-   [<span data-ttu-id="35b3f-111">Назначение пользователей непосредственно tooan приложения от имени администратора</span><span class="sxs-lookup"><span data-stu-id="35b3f-111">Assign a user directly tooan application as an administrator</span></span>](#assign-a-user-directly-as-an-administrator)

-   [<span data-ttu-id="35b3f-112">Назначить группу непосредственно tooan приложения от имени администратора</span><span class="sxs-lookup"><span data-stu-id="35b3f-112">Assign a group directly tooan application as an administrator</span></span>](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [<span data-ttu-id="35b3f-113">Включить toofind пользователей tooallow доступа к приложению самообслуживания своих приложений</span><span class="sxs-lookup"><span data-stu-id="35b3f-113">Enable self-service application access tooallow users toofind their own applications</span></span>](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a><span data-ttu-id="35b3f-114">Назначение пользователей напрямую от имени администратора</span><span class="sxs-lookup"><span data-stu-id="35b3f-114">Assign a user directly as an administrator</span></span>

<span data-ttu-id="35b3f-115">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="35b3f-115">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="35b3f-116">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="35b3f-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="35b3f-117">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="35b3f-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="35b3f-118">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="35b3f-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="35b3f-119">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="35b3f-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="35b3f-120">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="35b3f-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="35b3f-121">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="35b3f-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="35b3f-122">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="35b3f-122">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="35b3f-123">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="35b3f-123">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="35b3f-124">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="35b3f-124">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="35b3f-125">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="35b3f-125">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="35b3f-126">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="35b3f-126">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="35b3f-127">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="35b3f-127">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="35b3f-128">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="35b3f-128">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="35b3f-129">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="35b3f-129">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="35b3f-130">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="35b3f-130">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="35b3f-131">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="35b3f-131">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="35b3f-132">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="35b3f-132">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="35b3f-133">После краткого периода времени hello пользователей, которые вы выбрали быть может toolaunch эти приложения используют hello методов, описанных в разделе описания решений hello.</span><span class="sxs-lookup"><span data-stu-id="35b3f-133">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a><span data-ttu-id="35b3f-134">Назначить группу непосредственно tooan приложения от имени администратора</span><span class="sxs-lookup"><span data-stu-id="35b3f-134">Assign a group directly tooan application as an administrator</span></span>

<span data-ttu-id="35b3f-135">tooassign один или несколько групп tooan приложению напрямую, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="35b3f-135">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="35b3f-136">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="35b3f-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="35b3f-137">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="35b3f-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="35b3f-138">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="35b3f-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="35b3f-139">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="35b3f-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="35b3f-140">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="35b3f-140">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="35b3f-141">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="35b3f-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="35b3f-142">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="35b3f-142">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="35b3f-143">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="35b3f-143">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="35b3f-144">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="35b3f-144">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="35b3f-145">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="35b3f-145">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="35b3f-146">Тип в hello **имя полного группы** вы заинтересованы в назначение в hello группы hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="35b3f-146">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="35b3f-147">Наведите указатель мыши на hello **группы** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="35b3f-147">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="35b3f-148">Нажмите кнопку tooadd hello флажок Далее toohello группы профиля фотографию или логотип вашей toohello пользователя **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="35b3f-148">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="35b3f-149">**Необязательно:** при желании слишком**добавить несколько групп**, тип в другой **имя полного группы** в hello **поиск по имени или адресу электронной почты** поле поиска и нажмите кнопку флажок tooadd hello этой группы toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="35b3f-149">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="35b3f-150">После завершения выбора групп, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="35b3f-150">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="35b3f-151">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** вами группах колонке tooselect toohello tooassign роли выбранных.</span><span class="sxs-lookup"><span data-stu-id="35b3f-151">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="35b3f-152">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранные группы.</span><span class="sxs-lookup"><span data-stu-id="35b3f-152">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="35b3f-153">После краткого периода времени hello пользователей в группах hello выбранных быть может toolaunch эти приложения используют hello методов, описанных в разделе описания решений hello.</span><span class="sxs-lookup"><span data-stu-id="35b3f-153">After a short period of time, hello users within hello groups you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span> <span data-ttu-id="35b3f-154">Если используются динамические группы, назначения для пользователей в назначенных группах могут отображаться с некоторой задержкой.</span><span class="sxs-lookup"><span data-stu-id="35b3f-154">If these are dynamic groups, there may be some additional processing delay in these assignments appearing for users within these assigned groups.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="35b3f-155">Включить toofind пользователей tooallow доступа к приложению самообслуживания своих приложений</span><span class="sxs-lookup"><span data-stu-id="35b3f-155">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="35b3f-156">Доступ к приложению самообслуживания является хорошим способом tooallow пользователей tooself-обнаружение приложений, при необходимости разрешить hello бизнес группы tooapprove доступ toothose приложений.</span><span class="sxs-lookup"><span data-stu-id="35b3f-156">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="35b3f-157">Вы можете разрешить hello бизнес группы toomanage hello учетные данные назначены пользователи toothose для пароля единого входа в приложения непосредственно из своей панели доступа.</span><span class="sxs-lookup"><span data-stu-id="35b3f-157">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="35b3f-158">приложение tooan доступа к приложению самообслуживания tooenable, выполните следующие действия hello</span><span class="sxs-lookup"><span data-stu-id="35b3f-158">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="35b3f-159">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="35b3f-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="35b3f-160">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="35b3f-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="35b3f-161">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="35b3f-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="35b3f-162">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="35b3f-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="35b3f-163">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="35b3f-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="35b3f-164">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="35b3f-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="35b3f-165">Выберите приложение hello hello toofrom список будет tooenable самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="35b3f-165">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="35b3f-166">После загрузки приложения hello щелкните **самообслуживания** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="35b3f-166">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="35b3f-167">tooenable доступа к приложению самообслуживания для этого приложения, включите hello **пользователи приложения toothis toorequest доступ?** переключения слишком**Да.**</span><span class="sxs-lookup"><span data-stu-id="35b3f-167">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="35b3f-168">Затем toowhich tooselect hello группы пользователей, запрашивающих доступ toothis приложения должны быть добавлены, нажмите кнопку Далее метка toohello hello селектор **toowhich группы должны быть назначены пользователи будут добавлены?** и выберите группу.</span><span class="sxs-lookup"><span data-stu-id="35b3f-168">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="35b3f-169">**Необязательно:** желанию toorequire утверждения business до разрешения доступа пользователей, задайте hello **перед предоставлением доступа toothis приложения требуется утверждение?** переключения слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="35b3f-169">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="35b3f-170">**Необязательно: для приложений, только с помощью пароля единого входа на** желанию tooallow тех бизнес утверждающих toospecify hello паролей, которые отправляются toothis приложения для утвержденных пользователей, задайте hello **разрешить утверждающим tooset пароль пользователя для этого приложения?**  переключения слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="35b3f-170">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="35b3f-171">**Необязательно:** toospecify hello бизнеса утверждающие разрешены приложение toothis tooapprove access, щелкните надпись Далее toohello hello селектор **разрешениями приложения toothis tooapprove доступ?** tooselect вверх утверждающие too10 отдельных бизнеса.</span><span class="sxs-lookup"><span data-stu-id="35b3f-171">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

  >[!NOTE]
  ><span data-ttu-id="35b3f-172">Группы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="35b3f-172">Groups are not supported.</span></span>
  >
  >

13. <span data-ttu-id="35b3f-173">**Необязательно:** **для приложений, которые предоставляют роли**, при желании tooassign утвержденные пользователи tooa роли, нажмите кнопку Далее toohello селектор hello **toowhich роль следует назначить пользователей в этом приложения?**  tooselect hello роли toowhich этих пользователей следует назначить.</span><span class="sxs-lookup"><span data-stu-id="35b3f-173">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="35b3f-174">Нажмите кнопку hello **Сохранить** кнопку hello верхней части колонки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="35b3f-174">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="35b3f-175">После завершения конфигурации самостоятельного приложения пользователи могут перейти tootheir [панели доступа приложения](https://myapps.microsoft.com/) и нажмите кнопку hello **+ добавить** кнопку toofind hello приложений toowhich включен Самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="35b3f-175">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="35b3f-176">Чтобы просмотреть уведомления для бизнес-утверждений, [используйте панель доступа к приложениям](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="35b3f-176">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="35b3f-177">Вы можете включить электронное сообщение о том, когда пользователь запрашивает доступ tooan приложения, которое требует утверждения.</span><span class="sxs-lookup"><span data-stu-id="35b3f-177">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="35b3f-178">Это утверждение поддерживает один бизнес-правила утверждения, то есть, если указать несколько утверждающих лиц любой один утверждающий может утверждающий доступа toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="35b3f-178">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35b3f-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35b3f-179">Next steps</span></span>
[<span data-ttu-id="35b3f-180">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="35b3f-180">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
