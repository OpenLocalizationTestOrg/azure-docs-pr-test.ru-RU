---
title: "вход tooan коллекции Azure AD приложение, настроенное для пароля aaaProblems единый вход | Документы Microsoft"
description: "Описание проблем, предоставляющие руководство tootroubleshoot выдает связанных toosigning в tooAzure коллекции AD приложений, настроенных для пароля единого входа"
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="c30de-103">Проблемы со входом в tooan коллекции Azure AD приложение, настроенное для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="c30de-103">Problems signing in tooan Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="c30de-104">Hello панель доступа является Интернет-порталом, который дает возможность пользователя, имеющего рабочей или учебной учетной записи в Azure Active Directory (Azure AD) tooview и запуск облачных приложений, администратор hello Azure AD предоставил им доступ к.</span><span class="sxs-lookup"><span data-stu-id="c30de-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="c30de-105">Пользователь, имеющий выпуски Azure AD можно также использовать группы самообслуживания и возможности управления приложениями через панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="c30de-106">Панель доступа Hello отделен от hello портал Azure и не требует toohave пользователей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c30de-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="c30de-107">toouse паролю единого входа (SSO) в панели доступа, hello расширение панели доступа hello должны устанавливаться в браузере пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="c30de-108">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="c30de-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="c30de-109">Соответствующие требования к браузеру для hello панели доступа</span><span class="sxs-lookup"><span data-stu-id="c30de-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="c30de-110">Hello панели доступа требуется браузер, поддерживающий JavaScript и CSS включена.</span><span class="sxs-lookup"><span data-stu-id="c30de-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="c30de-111">toouse паролю единого входа (SSO) в панели доступа, hello расширение панели доступа hello должны устанавливаться в браузере пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="c30de-112">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="c30de-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="c30de-113">Для единого входа по паролю может быть браузеров hello конечных пользователей:</span><span class="sxs-lookup"><span data-stu-id="c30de-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="c30de-114">Internet Explorer 8, 9, 10, 11 (в Windows 7 или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="c30de-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="c30de-115">Chrome (начиная с Windows 7 и Mac OS X);</span><span class="sxs-lookup"><span data-stu-id="c30de-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="c30de-116">Firefox 26.0 и более поздние версии (начиная с Windows XP с пакетом обновления 2 (SP2) и Mac OS X 10.6).</span><span class="sxs-lookup"><span data-stu-id="c30de-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="c30de-117">Hello паролю SSO расширения становятся доступными для Edge в Windows 10, если для края становятся поддерживается расширения обозревателя.</span><span class="sxs-lookup"><span data-stu-id="c30de-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="c30de-118">Как tooinstall hello расширение обозревателя панели доступа</span><span class="sxs-lookup"><span data-stu-id="c30de-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="c30de-119">hello tooinstall расширение обозревателя панели доступа, следуйте инструкциям hello:</span><span class="sxs-lookup"><span data-stu-id="c30de-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="c30de-120">Откройте hello [панели доступа](https://myapps.microsoft.com) в одном hello поддерживаемых браузеров и входа в качестве **пользователя** в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c30de-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="c30de-121">Нажмите кнопку **SSO на ОСНОВЕ пароля приложения** в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c30de-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="c30de-122">В hello запрос запросом tooinstall hello программного обеспечения, выберите **установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="c30de-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="c30de-123">На основе браузера можно направленной toohello ссылку для скачивания.</span><span class="sxs-lookup"><span data-stu-id="c30de-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="c30de-124">**Добавить** браузер tooyour расширений hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="c30de-125">Если браузер запрашивает, выберите tooeither **включить** или **Разрешить** hello расширения.</span><span class="sxs-lookup"><span data-stu-id="c30de-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="c30de-126">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="c30de-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="c30de-127">Войдите в панель доступа hello и разделе, если вы можете **запуска** приложения SSO на ОСНОВЕ пароля</span><span class="sxs-lookup"><span data-stu-id="c30de-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="c30de-128">Можно также загрузить расширения hello Chrome и Firefox из hello прямые ссылки ниже:</span><span class="sxs-lookup"><span data-stu-id="c30de-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="c30de-129">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="c30de-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="c30de-130">Расширение "Панель доступа" для Firefox</span><span class="sxs-lookup"><span data-stu-id="c30de-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="c30de-131">Настройка групповой политики для Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c30de-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="c30de-132">Вы можете настроить групповой политики, которые позволяют вам tooremotely установки hello расширение для Internet Explorer на компьютерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="c30de-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="c30de-133">Предварительные требования Hello включают следующие:</span><span class="sxs-lookup"><span data-stu-id="c30de-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="c30de-134">Вы настроили [доменных служб Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), и вы присоединились к домену tooyour машин пользователей.</span><span class="sxs-lookup"><span data-stu-id="c30de-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="c30de-135">Необходимо иметь hello «Изменить параметры» разрешение tooedit hello объекта групповой политики (GPO).</span><span class="sxs-lookup"><span data-stu-id="c30de-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="c30de-136">По умолчанию это разрешение имеют члены элемента hello следующие группы безопасности: Администраторы домена "," Администраторы предприятия "и" Владельцы-создатели групповой политики.</span><span class="sxs-lookup"><span data-stu-id="c30de-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="c30de-137">[Подробнее](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c30de-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="c30de-138">Выполните действия из учебника hello [как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) пошаговые инструкции по как tooconfigure hello групповую политику и развернуть ее toousers.</span><span class="sxs-lookup"><span data-stu-id="c30de-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="c30de-139">Устранение неполадок hello панели доступа в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c30de-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="c30de-140">Выполните hello [Устранение hello расширение панели доступа для Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) руководстве доступ средства диагностики и пошаговые инструкции по настройке расширения hello для IE.</span><span class="sxs-lookup"><span data-stu-id="c30de-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="c30de-141">Как tooconfigure пароля единого входа для приложения не коллекции</span><span class="sxs-lookup"><span data-stu-id="c30de-141">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="c30de-142">tooconfigure приложение из коллекции hello Azure AD необходимо:</span><span class="sxs-lookup"><span data-stu-id="c30de-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="c30de-143">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="c30de-143">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="c30de-144">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="c30de-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="c30de-145">Назначить пользователей toohello приложения</span><span class="sxs-lookup"><span data-stu-id="c30de-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="c30de-146">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="c30de-146">Add a non-gallery application</span></span>

<span data-ttu-id="c30de-147">tooadd приложения hello коллекции Azure AD, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="c30de-148">Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**</span><span class="sxs-lookup"><span data-stu-id="c30de-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="c30de-149">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="c30de-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c30de-150">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="c30de-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c30de-151">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c30de-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c30de-152">Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку</span><span class="sxs-lookup"><span data-stu-id="c30de-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="c30de-153">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="c30de-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="c30de-154">Введите имя приложения hello в hello **имя** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="c30de-154">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="c30de-155">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c30de-155">Select **Add.**</span></span>

<span data-ttu-id="c30de-156">После краткого периода быть колонке конфигурации приложения может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-156">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="c30de-157">Настройка приложения hello для пароля единого входа</span><span class="sxs-lookup"><span data-stu-id="c30de-157">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="c30de-158">tooconfigure единого входа для приложения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-158">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="c30de-159">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="c30de-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c30de-160">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="c30de-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c30de-161">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="c30de-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c30de-162">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c30de-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c30de-163">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="c30de-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c30de-164">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="c30de-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c30de-165">Выберите hello приложение tooconfigure единого входа</span><span class="sxs-lookup"><span data-stu-id="c30de-165">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="c30de-166">После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c30de-166">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c30de-167">Режим выбора hello **входа на базе пароля.**</span><span class="sxs-lookup"><span data-stu-id="c30de-167">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="c30de-168">Введите hello **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="c30de-168">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="c30de-169">Это hello URL-адрес, где пользователи введите свои имя пользователя и пароль toosign в для.</span><span class="sxs-lookup"><span data-stu-id="c30de-169">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="c30de-170">Убедитесь, что вход hello поля отображаются по URL-АДРЕСУ hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-170">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="c30de-171">Назначьте пользователей toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="c30de-171">Assign users toohello application.</span></span>

11. <span data-ttu-id="c30de-172">Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-172">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="c30de-173">В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.</span><span class="sxs-lookup"><span data-stu-id="c30de-173">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="c30de-174">Назначить пользователей toohello приложения</span><span class="sxs-lookup"><span data-stu-id="c30de-174">Assign users toohello application</span></span>

<span data-ttu-id="c30de-175">tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c30de-175">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="c30de-176">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="c30de-176">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c30de-177">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="c30de-177">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c30de-178">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="c30de-178">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c30de-179">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c30de-179">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c30de-180">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="c30de-180">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c30de-181">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="c30de-181">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c30de-182">Выберите hello приложение tooassign список пользователей toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="c30de-182">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="c30de-183">После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c30de-183">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c30de-184">Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="c30de-184">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="c30de-185">Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.</span><span class="sxs-lookup"><span data-stu-id="c30de-185">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="c30de-186">Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="c30de-186">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="c30de-187">Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**.</span><span class="sxs-lookup"><span data-stu-id="c30de-187">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="c30de-188">Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="c30de-188">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="c30de-189">**Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.</span><span class="sxs-lookup"><span data-stu-id="c30de-189">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="c30de-190">После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.</span><span class="sxs-lookup"><span data-stu-id="c30de-190">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="c30de-191">**Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.</span><span class="sxs-lookup"><span data-stu-id="c30de-191">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="c30de-192">Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="c30de-192">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="c30de-193">После краткого периода hello пользователей, которые вы выбрали может toolaunch эти приложения в hello панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c30de-193">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="c30de-194">Если эти действия по устранению неполадок не hello устраните проблему hello</span><span class="sxs-lookup"><span data-stu-id="c30de-194">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="c30de-195">Откройте запрос в службу поддержки с hello следующую информацию, если они доступны:</span><span class="sxs-lookup"><span data-stu-id="c30de-195">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="c30de-196">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="c30de-196">Correlation error ID</span></span>

-   <span data-ttu-id="c30de-197">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="c30de-197">UPN (user email address)</span></span>

-   <span data-ttu-id="c30de-198">идентификатор клиента;</span><span class="sxs-lookup"><span data-stu-id="c30de-198">TenantID</span></span>

-   <span data-ttu-id="c30de-199">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="c30de-199">Browser type</span></span>

-   <span data-ttu-id="c30de-200">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="c30de-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="c30de-201">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="c30de-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="c30de-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c30de-202">Next steps</span></span>
[<span data-ttu-id="c30de-203">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="c30de-203">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

