---
title: "aaaError на странице приложения после входа в систему | Документы Microsoft"
description: "Как tooresolve проблемы, связанные с Azure AD выполнять вход при само приложение hello выдает ошибку"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="61cef-103">Ошибка на странице приложения после входа</span><span class="sxs-lookup"><span data-stu-id="61cef-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="61cef-104">В этом случае вход пользователя hello в Azure AD, но приложение hello отображает ошибку, не допускающей hello пользователя toosuccessfully Готово hello знак в поток.</span><span class="sxs-lookup"><span data-stu-id="61cef-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="61cef-105">В этом сценарии приложение hello не принимает hello ответа проблему по Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61cef-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="61cef-106">Существуют некоторые возможные причины, почему приложение hello не приняли hello ответа от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61cef-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="61cef-107">Если ошибка hello в приложении hello не является достаточно tooknow что отсутствует в ответе hello затем:</span><span class="sxs-lookup"><span data-stu-id="61cef-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="61cef-108">Если приложение hello коллекции hello Azure AD, проверьте, были выполнены все шаги hello в статье hello [как toodebug на основе SAML единого входа tooapplications в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="61cef-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="61cef-109">Использование таких средств, как [Fiddler](http://www.telerik.com/fiddler) toocapture SAML запрос, ответ SAML и маркера SAML.</span><span class="sxs-lookup"><span data-stu-id="61cef-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="61cef-110">Предоставить ответ SAML hello tooknow поставщика приложения hello недостатков.</span><span class="sxs-lookup"><span data-stu-id="61cef-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="61cef-111">Недостающие атрибуты в ответе SAML hello</span><span class="sxs-lookup"><span data-stu-id="61cef-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="61cef-112">tooadd атрибута в конфигурации toobe hello Azure AD, отправляемый в ответ hello Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="61cef-113">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="61cef-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="61cef-114">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="61cef-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="61cef-115">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="61cef-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="61cef-116">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="61cef-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="61cef-117">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="61cef-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="61cef-118">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="61cef-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="61cef-119">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="61cef-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="61cef-120">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="61cef-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="61cef-121">Нажмите кнопку **Просмотр и изменение атрибутов всех других пользователей в группе** hello **атрибуты пользователя** hello tooedit разделе атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.</span><span class="sxs-lookup"><span data-stu-id="61cef-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="61cef-122">tooadd атрибута:</span><span class="sxs-lookup"><span data-stu-id="61cef-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="61cef-123">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="61cef-123">click **Add attribute**.</span></span> <span data-ttu-id="61cef-124">Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="61cef-125">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="61cef-125">Click **Save.**</span></span> <span data-ttu-id="61cef-126">Вы увидите новый атрибут hello в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="61cef-127">Сохранение конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-127">Save hello configuration.</span></span>

<span data-ttu-id="61cef-128">Очередном входе hello в приложении toohello Azure AD отправляет новый атрибут hello в hello ответ SAML.</span><span class="sxs-lookup"><span data-stu-id="61cef-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="61cef-129">приложение Hello ожидает другое значение идентификатора пользователя или в другом формате</span><span class="sxs-lookup"><span data-stu-id="61cef-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="61cef-130">Hello toohello входа в приложения происходит сбой, так как hello ответ SAML отсутствует атрибуты, такие как роли или приложение hello ожидает один из форматов для атрибута EntityID hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="61cef-131">Добавьте атрибут в конфигурации приложения hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="61cef-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="61cef-132">hello toochange значение идентификатора пользователя, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="61cef-133">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="61cef-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="61cef-134">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="61cef-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="61cef-135">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="61cef-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="61cef-136">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="61cef-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="61cef-137">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="61cef-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="61cef-138">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="61cef-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="61cef-139">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="61cef-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="61cef-140">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="61cef-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="61cef-141">В разделе hello **атрибуты пользователя**, выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="61cef-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="61cef-142">Изменение формата идентификатора EntityID (идентификатора пользователя)</span><span class="sxs-lookup"><span data-stu-id="61cef-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="61cef-143">Если приложение hello и ожидает другого формата для атрибута EntityID hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="61cef-144">Затем не будет возможности tooselect hello EntityID (идентификатор пользователя) формат, что Azure AD отправляет toohello приложения hello ответа после проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="61cef-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="61cef-145">Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="61cef-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="61cef-146">Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) под hello статьи политики идентификатора имени.</span><span class="sxs-lookup"><span data-stu-id="61cef-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="61cef-147">приложение Hello ожидает другой сигнатурой метода для hello ответ SAML</span><span class="sxs-lookup"><span data-stu-id="61cef-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="61cef-148">toochange того, какие части маркера SAML hello цифровой подписи Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="61cef-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="61cef-149">Выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="61cef-150">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="61cef-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="61cef-151">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="61cef-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="61cef-152">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="61cef-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="61cef-153">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="61cef-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="61cef-154">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="61cef-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="61cef-155">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="61cef-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="61cef-156">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="61cef-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="61cef-157">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="61cef-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="61cef-158">Нажмите кнопку **Показывать дополнительные параметры подписи сертификата** под hello **сертификат подписи SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="61cef-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="61cef-159">Выберите hello соответствующие **подписи параметр** ожидаемый приложения hello:</span><span class="sxs-lookup"><span data-stu-id="61cef-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="61cef-160">Ответ знака SAML</span><span class="sxs-lookup"><span data-stu-id="61cef-160">Sign SAML response</span></span>

  * <span data-ttu-id="61cef-161">Ответ знака SAML и утверждение</span><span class="sxs-lookup"><span data-stu-id="61cef-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="61cef-162">Утверждение знака SAML</span><span class="sxs-lookup"><span data-stu-id="61cef-162">Sign SAML assertion</span></span>

<span data-ttu-id="61cef-163">Очередном входе hello в приложении toohello входа Azure AD hello часть выбран ответ SAML hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="61cef-164">приложение Hello ожидает hello подписи toobe алгоритм SHA-1</span><span class="sxs-lookup"><span data-stu-id="61cef-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="61cef-165">По умолчанию Azure AD подписывает маркер SAML hello, с помощью hello большинство алгоритмов безопасности.</span><span class="sxs-lookup"><span data-stu-id="61cef-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="61cef-166">Изменение алгоритма входа hello tooSHA-1 не рекомендуется, если только приложение hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="61cef-167">toochange hello алгоритм подписи, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="61cef-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="61cef-168">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="61cef-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="61cef-169">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="61cef-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="61cef-170">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="61cef-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="61cef-171">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="61cef-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="61cef-172">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="61cef-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="61cef-173">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="61cef-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="61cef-174">Выберите приложение hello, требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="61cef-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="61cef-175">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="61cef-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="61cef-176">Нажмите кнопку **Показывать дополнительные параметры подписи сертификата** под hello **сертификат подписи SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="61cef-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="61cef-177">Выберите алгоритм SHA-1, в hello **алгоритм подписи**.</span><span class="sxs-lookup"><span data-stu-id="61cef-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="61cef-178">При очередном Здравствуйте, которым пользователь входит в приложении toohello, входа Azure AD hello маркер SAML с помощью алгоритма SHA-1.</span><span class="sxs-lookup"><span data-stu-id="61cef-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61cef-179">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61cef-179">Next steps</span></span>
[<span data-ttu-id="61cef-180">Как toodebug на основе SAML единого входа tooapplications в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61cef-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
