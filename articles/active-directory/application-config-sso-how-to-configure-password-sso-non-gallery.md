---
title: "aaaHow tooconfigure пароля единого входа для applicationn не коллекции | Документы Microsoft"
description: "Как tooconfigure пользовательские приложения не коллекции для обеспечивать безопасность на основе пароля единого входа при отсутствует в коллекции приложений Azure AD hello"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="d80f2-103">Как tooconfigure пароля единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="d80f2-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="d80f2-104">Кроме вариантов toohello найти коллекции приложений hello Azure AD также имеется параметр tooadd hello **приложения не коллекции** при hello приложение, отсутствует в списке.</span><span class="sxs-lookup"><span data-stu-id="d80f2-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="d80f2-105">Благодаря этой возможности можно добавить любое приложение, которое уже существует в вашей организации или любого приложения сторонних разработчиков, которые могут использоваться с поставщиком, который еще не частью hello [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="d80f2-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="d80f2-106">После добавления приложения без коллекции можно настроить hello единого входа метода в данном приложении используется, выбрав hello **Single Sign-on** элемент навигации в приложении предприятия в hello [портала Azure ](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d80f2-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="d80f2-107">Одно из hello единым входом методы доступны tooyou — hello [паролю Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) параметр.</span><span class="sxs-lookup"><span data-stu-id="d80f2-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="d80f2-108">С hello **Добавление приложения, не являющихся коллекции** качества, вы можете интегрировать любое приложение, которое отображает имя пользователя на основе HTML и пароль введите поля, даже если ее нет в наш набор предварительно интегрированных приложений.</span><span class="sxs-lookup"><span data-stu-id="d80f2-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="d80f2-109">Привет, как это работает является страницей, импорт данных технология, которая является частью hello расширение панели доступа, мы сможем tooauto-определить поля ввода имени пользователя и пароля, сохраните их в безопасном месте для конкретного экземпляра определенного приложения.</span><span class="sxs-lookup"><span data-stu-id="d80f2-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="d80f2-110">Безопасно воспроизведения имена пользователей и пароли toothose полей, когда пользователь переходит по ним toothat приложения на панели доступа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="d80f2-111">Это отличный способ tooget запущен быстро интеграция приложения любого типа в Azure AD и позволяет:</span><span class="sxs-lookup"><span data-stu-id="d80f2-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="d80f2-112">Интеграция **любого приложения в Здравствуй, мир!** с вашим клиентом Azure AD, если в отображении HTML имя пользователя и пароль поле ввода</span><span class="sxs-lookup"><span data-stu-id="d80f2-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="d80f2-113">Включить **единого входа для пользователей** с помощью безопасного хранения и воспроизведения, имена пользователей и пароли для приложения hello интегрированы с Azure AD</span><span class="sxs-lookup"><span data-stu-id="d80f2-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="d80f2-114">**Автоматическое обнаружение ввода** полей для любого приложения, и позволяют toomanually обнаруживать эти поля с помощью hello расширение обозревателя панели доступа, в случае, если автоматическое обнаружение не удастся найти их</span><span class="sxs-lookup"><span data-stu-id="d80f2-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="d80f2-115">**Поддерживает приложения, которые требуют нескольких полей** для приложений, требующих больше, чем просто имя пользователя и пароль поля toosign в</span><span class="sxs-lookup"><span data-stu-id="d80f2-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="d80f2-116">**Настройка меток hello** hello имя пользователя и пароль полей ввода видят пользователи на hello [панели доступа приложений](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) при вводе учетных данных</span><span class="sxs-lookup"><span data-stu-id="d80f2-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="d80f2-117">Разрешить вашей **пользователей** tooprovide свои имена пользователей и пароли для любых существующих учетных записей приложения вводе в вручную на hello [приложения панели доступа](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="d80f2-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="d80f2-118">Разрешить **членом hello бизнес-группы** toospecify hello пользователя и пароль назначенный пользователь tooa с помощью hello [самообслуживания доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) функции</span><span class="sxs-lookup"><span data-stu-id="d80f2-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="d80f2-119">Разрешить **администратора** toospecify hello пользователя и пароль, назначенный пользователь tooa, используя учетные данные обновления hello компонент при [назначения пользовательского приложения tooan](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="d80f2-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="d80f2-120">Разрешить **администратора** toospecify hello общего пользователя или пароль, используемый группой пользователей, используя учетные данные обновления hello компонент при [назначение приложении tooan группы](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="d80f2-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="d80f2-121">Ниже описывается, как включить [паролю Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany приложения, добавить с помощью hello **Добавление приложения, не являющихся коллекции** столкнуться.</span><span class="sxs-lookup"><span data-stu-id="d80f2-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="d80f2-122">Обзор необходимых действий</span><span class="sxs-lookup"><span data-stu-id="d80f2-122">Overview of steps required</span></span>

<span data-ttu-id="d80f2-123">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="d80f2-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="d80f2-124">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="d80f2-124">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="d80f2-125">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="d80f2-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="d80f2-126">Назначить hello приложения tooa пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="d80f2-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="d80f2-127">Назначение приложения tooan пользователя напрямую</span><span class="sxs-lookup"><span data-stu-id="d80f2-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="d80f2-128">Назначение группе tooa приложения напрямую</span><span class="sxs-lookup"><span data-stu-id="d80f2-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="d80f2-129">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="d80f2-129">Add a non-gallery application</span></span>

<span data-ttu-id="d80f2-130">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="d80f2-131">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="d80f2-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="d80f2-132">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d80f2-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d80f2-133">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d80f2-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d80f2-134">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d80f2-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d80f2-135">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку</span><span class="sxs-lookup"><span data-stu-id="d80f2-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="d80f2-136">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="d80f2-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="d80f2-137">Введите имя приложения hello в hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="d80f2-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="d80f2-138">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d80f2-138">Select **Add.**</span></span>

<span data-ttu-id="d80f2-139">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="d80f2-140">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="d80f2-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="d80f2-141">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d80f2-142">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="d80f2-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d80f2-143">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d80f2-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d80f2-144">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d80f2-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d80f2-145">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d80f2-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d80f2-146">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d80f2-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d80f2-147">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="d80f2-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d80f2-148">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="d80f2-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d80f2-149">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d80f2-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d80f2-150">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="d80f2-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="d80f2-151">Введите hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="d80f2-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="d80f2-152">Это hello URL-адрес, где пользователи введите свои имя пользователя и пароль toosign в для.</span><span class="sxs-lookup"><span data-stu-id="d80f2-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="d80f2-153">Убедитесь, что вход hello поля отображаются по URL-АДРЕСУ hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="d80f2-154">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="d80f2-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="d80f2-155">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="d80f2-156">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="d80f2-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="d80f2-157">Назначение приложения tooan пользователя напрямую</span><span class="sxs-lookup"><span data-stu-id="d80f2-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="d80f2-158">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="d80f2-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="d80f2-159">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="d80f2-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d80f2-160">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d80f2-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d80f2-161">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d80f2-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d80f2-162">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d80f2-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d80f2-163">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d80f2-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d80f2-164">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="d80f2-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d80f2-165">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="d80f2-166">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d80f2-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d80f2-167">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="d80f2-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d80f2-168">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="d80f2-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d80f2-169">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="d80f2-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d80f2-170">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="d80f2-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="d80f2-171">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="d80f2-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="d80f2-172">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="d80f2-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="d80f2-173">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="d80f2-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="d80f2-174">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="d80f2-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="d80f2-175">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="d80f2-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="d80f2-176">Назначение группе tooa приложения напрямую</span><span class="sxs-lookup"><span data-stu-id="d80f2-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="d80f2-177">tooassign один или несколько групп tooan приложению напрямую, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="d80f2-178">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="d80f2-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d80f2-179">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="d80f2-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d80f2-180">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="d80f2-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d80f2-181">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d80f2-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d80f2-182">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="d80f2-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d80f2-183">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="d80f2-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d80f2-184">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="d80f2-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="d80f2-185">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d80f2-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d80f2-186">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="d80f2-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d80f2-187">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="d80f2-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d80f2-188">Тип в hello **имя полного группы** вы заинтересованы в назначение в hello группы hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="d80f2-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d80f2-189">Наведите указатель мыши на hello **группы** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="d80f2-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="d80f2-190">Нажмите кнопку tooadd hello флажок Далее toohello группы профиля фотографию или логотип вашей toohello пользователя **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="d80f2-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="d80f2-191">**Необязательно:** при желании слишком**добавить несколько групп**, тип в другой **имя полного группы** в hello **поиск по имени или адресу электронной почты** поле поиска и нажмите кнопку флажок tooadd hello этой группы toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="d80f2-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="d80f2-192">После завершения выбора групп, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="d80f2-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="d80f2-193">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** вами группах колонке tooselect toohello tooassign роли выбранных.</span><span class="sxs-lookup"><span data-stu-id="d80f2-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="d80f2-194">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранные группы.</span><span class="sxs-lookup"><span data-stu-id="d80f2-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="d80f2-195">После краткого периода hello пользователей, которые вы выбрали может toolaunch эти приложения в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d80f2-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d80f2-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d80f2-196">Next steps</span></span>
[<span data-ttu-id="d80f2-197">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="d80f2-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
