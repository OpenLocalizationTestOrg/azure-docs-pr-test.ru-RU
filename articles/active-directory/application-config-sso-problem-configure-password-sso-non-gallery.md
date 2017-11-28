---
title: "Настройка пароля единого входа для приложения не коллекции aaaProblem | Документы Microsoft"
description: "Понимать лицевой стороны людей hello распространенных проблем при настройке пароля единого входа для пользовательских приложений не коллекции, которые не перечислены в hello коллекции приложений Azure AD."
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e54b3-103">Проблема при настройке единого входа по паролю для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="e54b3-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e54b3-104">В этой статье помогут людей лицевой toounderstand hello распространенных проблем при настройке **пароля единого входа** с приложением не коллекции.</span><span class="sxs-lookup"><span data-stu-id="e54b3-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="e54b3-105">Как войти toocapture поля для приложения</span><span class="sxs-lookup"><span data-stu-id="e54b3-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="e54b3-106">Определение полей входа в систему поддерживается только для страниц входа на основе HTML и **не поддерживается для нестандартных страниц входа**, например для тех, которые используют Flash и другие технологии не на основе HTML.</span><span class="sxs-lookup"><span data-stu-id="e54b3-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="e54b3-107">Существует два способа определения полей входа в систему для приложения:</span><span class="sxs-lookup"><span data-stu-id="e54b3-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="e54b3-108">Автоматическое определение полей входа в систему</span><span class="sxs-lookup"><span data-stu-id="e54b3-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="e54b3-109">Определение полей входа в систему вручную</span><span class="sxs-lookup"><span data-stu-id="e54b3-109">Manual sign-in field capture</span></span>

<span data-ttu-id="e54b3-110">**Автоматическое поля отслеживания** хорошо работает с большинством поддержкой HTML страницы входа, если они используют **известные идентификаторы DIV hello имя пользователя и пароль, которые ввода** поля.</span><span class="sxs-lookup"><span data-stu-id="e54b3-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="e54b3-111">Привет, как это работает-Импорт данных hello HTML на страницу приветствия toofind DIV идентификаторы, соответствующие определенным условиям и затем мы позже воспроизвести пароли tooit сохранения этих метаданных для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e54b3-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="e54b3-112">**Вручную поле записи** можно использовать в случае hello, приложение hello **поставщика имеются метки не** hello ввода поля, используемые для входа.</span><span class="sxs-lookup"><span data-stu-id="e54b3-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="e54b3-113">Вручную поле записи может использоваться также в случае hello, если hello **поставщика отображает несколько полей** которого не может быть автоматически.</span><span class="sxs-lookup"><span data-stu-id="e54b3-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="e54b3-114">Azure AD данные могут храниться как количество полей в hello вход страницы, при условии, что вы Расскажите, где эти поля находятся на странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="e54b3-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="e54b3-115">В общем случае **Если автоматический поле записи не работает, рекомендуется всегда идет hello-ручной режим.**</span><span class="sxs-lookup"><span data-stu-id="e54b3-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="e54b3-116">Как tooautomatically запись полей входа для приложения</span><span class="sxs-lookup"><span data-stu-id="e54b3-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="e54b3-117">tooconfigure **паролю Single Sign-on** для приложения с помощью **автоматического поля отслеживания**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e54b3-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="e54b3-118">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="e54b3-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e54b3-119">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="e54b3-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e54b3-120">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="e54b3-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e54b3-121">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e54b3-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e54b3-122">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="e54b3-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e54b3-123">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="e54b3-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e54b3-124">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="e54b3-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e54b3-125">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e54b3-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e54b3-126">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="e54b3-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e54b3-127">Введите hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="e54b3-128">Это hello URL-адрес, где пользователи введите свои имя пользователя и пароль toosign в для.</span><span class="sxs-lookup"><span data-stu-id="e54b3-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="e54b3-129">**Обеспечение отображения по URL-АДРЕСУ hello, указываемые полей входа hello**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="e54b3-130">Нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e54b3-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="e54b3-131">После этого, мы будем автоматически очистки этот URL-адрес для имени пользователя и пароля, поле ввода и позволяют toosecurely Azure AD toouse передавать пароли toothat приложения с помощью панели обозревателя hello доступа модуля.</span><span class="sxs-lookup"><span data-stu-id="e54b3-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="e54b3-132">Как toomanually запись полей входа для приложения</span><span class="sxs-lookup"><span data-stu-id="e54b3-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="e54b3-133">toomanually полей входа захвата, сначала необходимо выполнить после установки расширения доступа к панели обозревателя hello и **не запущен в режиме inPrivate, incognito или закрытый.**</span><span class="sxs-lookup"><span data-stu-id="e54b3-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="e54b3-134">расширение обозревателя hello tooinstall, повторите шаги hello в hello [как tooinstall hello расширение доступа к панели обозревателя](#i-cannot-manually-detect-sign-in-fields-for-my-application) раздела.</span><span class="sxs-lookup"><span data-stu-id="e54b3-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="e54b3-135">tooconfigure **паролю Single Sign-on** для приложения с помощью **вручную поля отслеживания**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e54b3-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="e54b3-136">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="e54b3-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e54b3-137">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="e54b3-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e54b3-138">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="e54b3-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e54b3-139">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e54b3-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e54b3-140">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="e54b3-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="e54b3-141">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="e54b3-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e54b3-142">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="e54b3-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e54b3-143">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="e54b3-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e54b3-144">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="e54b3-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e54b3-145">Введите hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="e54b3-146">Это hello URL-адрес, где пользователи введите свои имя пользователя и пароль toosign в для.</span><span class="sxs-lookup"><span data-stu-id="e54b3-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="e54b3-147">**Обеспечение отображения по URL-АДРЕСУ hello, указываемые полей входа hello**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="e54b3-148">Нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e54b3-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="e54b3-149">После этого, мы будем автоматически очистки этот URL-адрес для имени пользователя и пароля, поле ввода и позволяют toosecurely Azure AD toouse передавать пароли toothat приложения с помощью панели обозревателя hello доступа модуля.</span><span class="sxs-lookup"><span data-stu-id="e54b3-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="e54b3-150">В случае hello, это не удается, вы можете **измененных вручную поле toouse входа в режим hello** продолжая toostep 12.</span><span class="sxs-lookup"><span data-stu-id="e54b3-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="e54b3-151">Щелкните **Настроить параметры единого входа по паролю для &lt;имя_приложения&gt;**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="e54b3-152">Выберите hello **вручную определить поля вход** параметра конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e54b3-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="e54b3-153">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-153">Click **Ok**.</span></span>

15. <span data-ttu-id="e54b3-154">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-154">Click **Save**.</span></span>

16. <span data-ttu-id="e54b3-155">Следуйте hello на экране инструкции toouse hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e54b3-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="e54b3-156">Появляется сообщение об ошибке "Не удалось найти ни одного поля входа в систему на этой странице"</span><span class="sxs-lookup"><span data-stu-id="e54b3-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="e54b3-157">Эта ошибка возникает, если не удается определить поля входа в систему автоматически.</span><span class="sxs-lookup"><span data-stu-id="e54b3-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="e54b3-158">эту проблему, попробуйте вручную поле определение по hello следующие шаги в hello tooresolve [как toomanually запись полей входа для приложения](#how-to-manually-capture-sign-in-fields-for-an-application) раздела.</span><span class="sxs-lookup"><span data-stu-id="e54b3-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="e54b3-159">Отображается ошибка «не удается toosave Single Sign-on конфигурация»</span><span class="sxs-lookup"><span data-stu-id="e54b3-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="e54b3-160">В настройках hello единого входа может произойти сбой в некоторых редких случаях.</span><span class="sxs-lookup"><span data-stu-id="e54b3-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="e54b3-161">tooresolve это попробуйте сохранить hello единого входа конфигурации еще раз.</span><span class="sxs-lookup"><span data-stu-id="e54b3-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="e54b3-162">Если проблема toofail постоянно обращение в службу поддержки и предоставить hello сведения, собранные в hello [как toosee hello сведения портала уведомления](#i-cannot-manually-detect-sign-in-fields-for-my-application) и [помощь tooget путем отправки уведомления tooa подробные сведения Инженер поддержки](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) разделы.</span><span class="sxs-lookup"><span data-stu-id="e54b3-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="e54b3-163">Не удается определить поля входа в систему вручную для моего приложения</span><span class="sxs-lookup"><span data-stu-id="e54b3-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="e54b3-164">Ниже перечислены некоторые hello поведений, которые можно увидеть при ручном не работает.</span><span class="sxs-lookup"><span data-stu-id="e54b3-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="e54b3-165">процесс вручную отслеживания Hello появлялись toowork, но hello поля записи не были правильно</span><span class="sxs-lookup"><span data-stu-id="e54b3-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="e54b3-166">При выполнении процесса отслеживания hello, не будут выявлены полей справа Hello</span><span class="sxs-lookup"><span data-stu-id="e54b3-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="e54b3-167">процесс отслеживания Hello занимает мне страницы входа toohello приложения должным образом, но ничего не происходит</span><span class="sxs-lookup"><span data-stu-id="e54b3-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="e54b3-168">Ручной захват отображается toowork, но единого входа не происходит, когда пользователи переходят toohello приложения hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e54b3-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="e54b3-169">Проверьте ниже hello, если обнаруживаются любые из этих проблем.</span><span class="sxs-lookup"><span data-stu-id="e54b3-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="e54b3-170">Убедитесь, что последняя версия hello расширение обозревателя панели доступа hello **установлен** и **включен** , следуя указаниям hello hello [как tooinstall hello доступа панель обозревателя расширение](#how-to-install-the-access-panel-browser-extension) раздела.</span><span class="sxs-lookup"><span data-stu-id="e54b3-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="e54b3-171">Убедитесь, что не процесс отслеживания hello при браузер, **incognito, inPrivate или Private режим**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="e54b3-172">расширение панели доступа Hello не поддерживается в этих режимах.</span><span class="sxs-lookup"><span data-stu-id="e54b3-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="e54b3-173">Убедитесь, что пользователи не toosign в приложении toohello из панели доступа hello при в **incognito, inPrivate или Private режим**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="e54b3-174">расширение панели доступа Hello не поддерживается в этих режимах.</span><span class="sxs-lookup"><span data-stu-id="e54b3-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="e54b3-175">Повторите процесс вручную отслеживания hello, обеспечение маркеры hello красным, а не hello нужные поля.</span><span class="sxs-lookup"><span data-stu-id="e54b3-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="e54b3-176">Если hello ручной захват процесс кажется toohang или страница входа hello не делает ничего (вариант 3 выше), повторите процесс вручную отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="e54b3-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="e54b3-177">Но на этот раз после завершения процесса hello, нажмите клавишу hello **F12** кнопку tooopen обозревателя в консоли разработчика.</span><span class="sxs-lookup"><span data-stu-id="e54b3-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="e54b3-178">Один раз, откройте hello **консоли** и тип **window.location=»&lt;введите знак hello в URL-адрес, указанный при настройке приложения hello&gt;»** и нажмите клавишу  **Введите**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="e54b3-179">Этой страницей Принудительное перенаправление которой завершить процесс отслеживания hello и хранения hello полей, которые были записаны.</span><span class="sxs-lookup"><span data-stu-id="e54b3-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="e54b3-180">Если ни один из этих подходов не помогает, обратитесь к нам.</span><span class="sxs-lookup"><span data-stu-id="e54b3-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="e54b3-181">Обращение в службу поддержки с подробными сведениями hello была предпринята, а также hello сведения, собранные в hello [как toosee hello сведения портала уведомления](#i-cannot-manually-detect-sign-in-fields-for-my-application) и [помощь tooget путем отправки сведений об уведомлениях tooa поддержки Инженер](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) разделов (если применимо).</span><span class="sxs-lookup"><span data-stu-id="e54b3-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="e54b3-182">Как tooinstall hello расширение обозревателя панели доступа</span><span class="sxs-lookup"><span data-stu-id="e54b3-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="e54b3-183">hello tooinstall расширение обозревателя панели доступа, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="e54b3-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="e54b3-184">Откройте hello [панели доступа](https://myapps.microsoft.com) в одном hello поддерживаемых браузеров и входа в качестве **пользователя** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e54b3-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="e54b3-185">Нажмите кнопку **SSO на ОСНОВЕ пароля приложения** в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e54b3-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="e54b3-186">В hello запрос запросом tooinstall hello программного обеспечения, выберите **установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="e54b3-187">На основе браузера можно направленной toohello ссылку для скачивания.</span><span class="sxs-lookup"><span data-stu-id="e54b3-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="e54b3-188">**Добавить** браузер tooyour расширений hello.</span><span class="sxs-lookup"><span data-stu-id="e54b3-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="e54b3-189">Если браузер запрашивает, выберите tooeither **включить** или **Разрешить** hello расширения.</span><span class="sxs-lookup"><span data-stu-id="e54b3-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="e54b3-190">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="e54b3-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="e54b3-191">Войдите в панель доступа hello и разделе, если вы можете **запуска** приложения SSO на ОСНОВЕ пароля.</span><span class="sxs-lookup"><span data-stu-id="e54b3-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="e54b3-192">Можно также загрузить расширения hello Chrome и Firefox из hello прямые ссылки ниже:</span><span class="sxs-lookup"><span data-stu-id="e54b3-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="e54b3-193">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="e54b3-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="e54b3-194">Расширение "Панель доступа" для Firefox</span><span class="sxs-lookup"><span data-stu-id="e54b3-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="e54b3-195">Как toosee hello сведения портала уведомления</span><span class="sxs-lookup"><span data-stu-id="e54b3-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="e54b3-196">Чтобы просмотреть сведения hello любого портала уведомления с hello описанных ниже действий:</span><span class="sxs-lookup"><span data-stu-id="e54b3-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="e54b3-197">Нажмите кнопку hello **уведомления** значок (hello звонка) в правом верхнем углу hello объекта hello портала Azure</span><span class="sxs-lookup"><span data-stu-id="e54b3-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="e54b3-198">Выберите все уведомления в **ошибка** состояние (имеющими toothem Далее красный (!)).</span><span class="sxs-lookup"><span data-stu-id="e54b3-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="e54b3-199">!Примечание] Не следует выбирать уведомления, которые находятся в состоянии **Успешно** или **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="e54b3-200">Это Привет открыть **сведений об уведомлениях** колонку.</span><span class="sxs-lookup"><span data-stu-id="e54b3-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="e54b3-201">Эти сведения можно используйте самостоятельно toounderstand больше сведений о проблеме hello.</span><span class="sxs-lookup"><span data-stu-id="e54b3-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="e54b3-202">Если вы по-прежнему нужна помощь, вы можете использовать эти сведения с поддержки инженер или hello группы tooget Справка по продукту с конкретной задачи.</span><span class="sxs-lookup"><span data-stu-id="e54b3-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="e54b3-203">Нажмите кнопку hello **копирования** **значок** toohello справа от приветствия **скопируйте ошибку** textbox toocopy все hello tooshare сведения уведомлений с инженером группы поддержки или продукта.</span><span class="sxs-lookup"><span data-stu-id="e54b3-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="e54b3-204">Как помочь tooget путем отправки уведомления инженером по tooa подробные сведения</span><span class="sxs-lookup"><span data-stu-id="e54b3-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="e54b3-205">Очень важно использовать общее **все hello перечисленные ниже сведения** с сотрудник службы поддержки, если вам нужна помощь, так что они помогут вам быстро.</span><span class="sxs-lookup"><span data-stu-id="e54b3-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="e54b3-206">Вы это легко сделать, **создания снимка экрана,** или щелкнув hello **значок ошибки копирования**, найти toohello правой части hello **скопируйте ошибку** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="e54b3-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="e54b3-207">Объяснение сведений об уведомлении</span><span class="sxs-lookup"><span data-stu-id="e54b3-207">Notification Details Explained</span></span>

<span data-ttu-id="e54b3-208">Hello ниже объясняется означает более содержимого каждого из элементов уведомления hello и предоставляет примеры каждого из них.</span><span class="sxs-lookup"><span data-stu-id="e54b3-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="e54b3-209">Основные элементы уведомления</span><span class="sxs-lookup"><span data-stu-id="e54b3-209">Essential Notification Items</span></span>

-   <span data-ttu-id="e54b3-210">**Заголовок** — hello описательное название hello уведомления</span><span class="sxs-lookup"><span data-stu-id="e54b3-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="e54b3-211">Пример: **Настройки прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="e54b3-212">**Описание** — hello о том, что произошло в результате операции hello</span><span class="sxs-lookup"><span data-stu-id="e54b3-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="e54b3-213">Пример: **Введенный внутренний URL-адрес уже используется другим приложением**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="e54b3-214">**Идентификатор уведомления** — уникальный идентификатор hello hello уведомления</span><span class="sxs-lookup"><span data-stu-id="e54b3-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="e54b3-215">Пример: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="e54b3-216">**Идентификатор запроса клиента** — идентификатор hello конкретного запроса, внесенных в браузере</span><span class="sxs-lookup"><span data-stu-id="e54b3-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="e54b3-217">Пример: **302fd775-3329-4670-a9f3-bea37004f0bc**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="e54b3-218">**Время UTC штамп** — hello отметки времени, во время которого произошло hello уведомлений в формате UTC</span><span class="sxs-lookup"><span data-stu-id="e54b3-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="e54b3-219">Пример: **2017-03-23T19:50:43.7583681Z**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="e54b3-220">**Внутренний идентификатор транзакции** — внутренний идентификатор, мы используем ошибки hello toolook в наших системах hello</span><span class="sxs-lookup"><span data-stu-id="e54b3-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="e54b3-221">Пример: **71a2f329-ca29-402f-aa72-bc00a7aca603**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="e54b3-222">**Имя участника-пользователя** — hello пользователя, выполнившего операцию hello</span><span class="sxs-lookup"><span data-stu-id="e54b3-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="e54b3-223">Пример: **tperkins@f128.info**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="e54b3-224">**Идентификатор клиента** — уникальный идентификатор клиента hello, hello пользователя, выполнившего операцию hello hello был членом</span><span class="sxs-lookup"><span data-stu-id="e54b3-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="e54b3-225">Пример: **7918d4b5-0442-4a97-be2d-36f9f9962ece**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="e54b3-226">**Объект User Id** — уникальный идентификатор hello пользователя, выполнившего операцию hello hello</span><span class="sxs-lookup"><span data-stu-id="e54b3-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="e54b3-227">Пример: **17f84be4-51f8-483a-b533-383791227a99**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="e54b3-228">Дополнительные элементы уведомления с подробными сведениями</span><span class="sxs-lookup"><span data-stu-id="e54b3-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="e54b3-229">**Отображаемое имя** — **(может быть пустым)** подробных отображаемое имя для ошибки hello</span><span class="sxs-lookup"><span data-stu-id="e54b3-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="e54b3-230">Пример*: **Параметры прокси приложения**</span><span class="sxs-lookup"><span data-stu-id="e54b3-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="e54b3-231">**Состояние** — hello определенным состоянием hello уведомления</span><span class="sxs-lookup"><span data-stu-id="e54b3-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="e54b3-232">Пример*: **Сбой**</span><span class="sxs-lookup"><span data-stu-id="e54b3-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="e54b3-233">**Идентификатор объекта** — **(может быть пустым)** hello идентификатор объекта, к какой hello операции</span><span class="sxs-lookup"><span data-stu-id="e54b3-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="e54b3-234">Пример: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="e54b3-235">**Сведения о** — hello подробное описание том, что произошло в результате операции hello</span><span class="sxs-lookup"><span data-stu-id="e54b3-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="e54b3-236">Пример: **Внутренний URL-адрес http://bing.com/ является недопустимым, так как он уже используется**.</span><span class="sxs-lookup"><span data-stu-id="e54b3-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="e54b3-237">**Скопируйте ошибку** — щелкните hello **значок копирования** toohello справа от приветствия **скопируйте ошибку** все toocopy textbox hello tooshare сведения уведомлений с инженером группы поддержки или продукта</span><span class="sxs-lookup"><span data-stu-id="e54b3-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="e54b3-238">Пример: ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="e54b3-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="e54b3-239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e54b3-239">Next steps</span></span>
[<span data-ttu-id="e54b3-240">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="e54b3-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

