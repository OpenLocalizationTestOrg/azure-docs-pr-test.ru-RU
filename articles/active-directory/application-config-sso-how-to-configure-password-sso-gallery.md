---
title: "aaaHow tooconfigure пароля единого входа для приложения Azure AD коллекции | Документы Microsoft"
description: "Как tooconfigure приложения для защиты на основе пароля единого входа при уже присутствует в коллекции приложений Azure AD hello"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="3fa97-103">Как tooconfigure пароля единого входа для приложения Azure AD коллекции</span><span class="sxs-lookup"><span data-stu-id="3fa97-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="3fa97-104">При добавлении приложения из hello [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), у вас есть выбор способа вашей toosign пользователей в приложении toothat hello.</span><span class="sxs-lookup"><span data-stu-id="3fa97-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="3fa97-105">Этот выбор можно настроить в любое время, выбрав hello **Single Sign-on** элемент навигации в приложении предприятия в hello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3fa97-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="3fa97-106">Один из доступных tooyou методы-hello — hello [паролю Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) параметр.</span><span class="sxs-lookup"><span data-stu-id="3fa97-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="3fa97-107">Это отличный способ tooget запущен быстро интеграция приложений в Azure AD и позволяет:</span><span class="sxs-lookup"><span data-stu-id="3fa97-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="3fa97-108">Включить **единого входа для пользователей** с помощью безопасного хранения и воспроизведения, имена пользователей и пароли для приложения hello интегрированы с Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fa97-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="3fa97-109">**Поддерживает приложения, которые требуют нескольких полей** для приложений, требующих больше, чем просто имя пользователя и пароль поля toosign в</span><span class="sxs-lookup"><span data-stu-id="3fa97-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="3fa97-110">**Настройка меток hello** hello имя пользователя и пароль полей ввода видят пользователи на hello [панели доступа приложений](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) при вводе учетных данных</span><span class="sxs-lookup"><span data-stu-id="3fa97-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="3fa97-111">Разрешить вашей **пользователей** tooprovide свои имена пользователей и пароли для любых существующих учетных записей приложения вводе в вручную на hello [приложения панели доступа](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="3fa97-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="3fa97-112">Разрешить **членом hello бизнес-группы** toospecify hello пользователя и пароль назначенный пользователь tooa с помощью hello [самообслуживания доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) функции</span><span class="sxs-lookup"><span data-stu-id="3fa97-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="3fa97-113">Разрешить **администратора** toospecify hello пользователя и пароль, назначенный пользователь tooa, используя учетные данные обновления hello компонент при [назначения пользовательского приложения tooan](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="3fa97-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="3fa97-114">Разрешить **администратора** toospecify hello общего пользователя или пароль, используемый группой пользователей, используя учетные данные обновления hello компонент при [назначение приложении tooan группы](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="3fa97-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="3fa97-115">Ниже описывается, как включить [паролю Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan приложение, которое уже находится в hello [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="3fa97-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="3fa97-116">Обзор необходимых действий</span><span class="sxs-lookup"><span data-stu-id="3fa97-116">Overview of steps required</span></span>
<span data-ttu-id="3fa97-117">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="3fa97-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="3fa97-118">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fa97-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="3fa97-119">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="3fa97-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="3fa97-120">Назначить hello приложения tooa пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="3fa97-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="3fa97-121">Назначение приложения tooan пользователя напрямую</span><span class="sxs-lookup"><span data-stu-id="3fa97-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="3fa97-122">Назначение группе tooa приложения напрямую</span><span class="sxs-lookup"><span data-stu-id="3fa97-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="3fa97-123">Добавить приложение из коллекции hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fa97-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="3fa97-124">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="3fa97-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="3fa97-125">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="3fa97-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="3fa97-126">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="3fa97-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3fa97-127">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="3fa97-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3fa97-128">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3fa97-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3fa97-129">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку</span><span class="sxs-lookup"><span data-stu-id="3fa97-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="3fa97-130">В hello **введите имя** текстового поля из hello **добавить из галереи hello** раздел, имя типа hello приложения hello</span><span class="sxs-lookup"><span data-stu-id="3fa97-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="3fa97-131">Выберите hello приложение tooconfigure для единого входа</span><span class="sxs-lookup"><span data-stu-id="3fa97-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="3fa97-132">Перед добавлением приложения hello, можно изменить его имя из hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="3fa97-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="3fa97-133">Нажмите кнопку **добавить** кнопки, приложение hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3fa97-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="3fa97-134">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="3fa97-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="3fa97-135">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="3fa97-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="3fa97-136">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="3fa97-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="3fa97-137">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="3fa97-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3fa97-138">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="3fa97-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3fa97-139">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="3fa97-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3fa97-140">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3fa97-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3fa97-141">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="3fa97-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3fa97-142">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="3fa97-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3fa97-143">Выберите hello приложение tooconfigure единого входа</span><span class="sxs-lookup"><span data-stu-id="3fa97-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="3fa97-144">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3fa97-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3fa97-145">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="3fa97-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="3fa97-146">[Назначить пользователей приложения toohello](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="3fa97-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="3fa97-147">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="3fa97-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="3fa97-148">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="3fa97-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="3fa97-149">Назначение приложения tooan пользователя напрямую</span><span class="sxs-lookup"><span data-stu-id="3fa97-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="3fa97-150">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="3fa97-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3fa97-151">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="3fa97-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3fa97-152">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="3fa97-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3fa97-153">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="3fa97-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3fa97-154">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3fa97-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3fa97-155">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="3fa97-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3fa97-156">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="3fa97-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3fa97-157">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="3fa97-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3fa97-158">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3fa97-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3fa97-159">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="3fa97-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3fa97-160">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="3fa97-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3fa97-161">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="3fa97-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3fa97-162">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="3fa97-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3fa97-163">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="3fa97-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3fa97-164">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="3fa97-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="3fa97-165">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="3fa97-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3fa97-166">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="3fa97-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="3fa97-167">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="3fa97-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="3fa97-168">Назначение группе tooa приложения напрямую</span><span class="sxs-lookup"><span data-stu-id="3fa97-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="3fa97-169">tooassign один или несколько групп tooan приложению напрямую, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="3fa97-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="3fa97-170">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="3fa97-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3fa97-171">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="3fa97-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3fa97-172">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="3fa97-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3fa97-173">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3fa97-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3fa97-174">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="3fa97-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3fa97-175">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="3fa97-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3fa97-176">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="3fa97-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="3fa97-177">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3fa97-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3fa97-178">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="3fa97-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3fa97-179">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="3fa97-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3fa97-180">Тип в hello **имя полного группы** вы заинтересованы в назначение в hello группы hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="3fa97-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3fa97-181">Наведите указатель мыши на hello **группы** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="3fa97-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="3fa97-182">Нажмите кнопку tooadd hello флажок Далее toohello группы профиля фотографию или логотип вашей toohello пользователя **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="3fa97-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="3fa97-183">**Необязательно:** при желании слишком**добавить несколько групп**, тип в другой **имя полного группы** в hello **поиск по имени или адресу электронной почты** поле поиска и нажмите кнопку флажок tooadd hello этой группы toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="3fa97-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="3fa97-184">После завершения выбора групп, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="3fa97-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="3fa97-185">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** вами группах колонке tooselect toohello tooassign роли выбранных.</span><span class="sxs-lookup"><span data-stu-id="3fa97-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="3fa97-186">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранные группы.</span><span class="sxs-lookup"><span data-stu-id="3fa97-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="3fa97-187">После краткого периода hello пользователей, которые вы выбрали может toolaunch эти приложения в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3fa97-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fa97-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fa97-188">Next steps</span></span>
[<span data-ttu-id="3fa97-189">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="3fa97-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
