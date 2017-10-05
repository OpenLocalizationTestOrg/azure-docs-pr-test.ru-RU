---
title: "Проблемы при входе в приложение с помощью прямой ссылки | Документы Майкрософт"
description: "Устранение проблем с обращением к приложению по URL-адресу прямой ссылки с помощью Azure AD"
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="f5d77-103">Проблемы при входе в приложение с помощью прямой ссылки</span><span class="sxs-lookup"><span data-stu-id="f5d77-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="f5d77-104">Панель доступа — это веб-портал, позволяющий пользователям с рабочей или учебной учетной записью Azure Active Directory (Azure AD) просматривать и запускать облачные приложения, к которым администратор Azure AD предоставил доступ</span><span class="sxs-lookup"><span data-stu-id="f5d77-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="f5d77-105">Эти приложения настраиваются от имени пользователя на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5d77-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="f5d77-106">Чтобы пользователь видел приложение на панели доступа, оно должно быть правильно настроено и назначено пользователю или группе, к которой он относится.</span><span class="sxs-lookup"><span data-stu-id="f5d77-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="f5d77-107">Прямые ссылки или URL-адреса пользовательского доступа представляют собой ссылки, с помощью которых пользователи могут осуществлять доступ к приложениям с единым входом по паролю прямо из строки URL-адреса в браузере.</span><span class="sxs-lookup"><span data-stu-id="f5d77-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="f5d77-108">Перейдя по такой ссылке, пользователи автоматически входят в приложение без посещения панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f5d77-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="f5d77-109">С помощью той же самой ссылки пользователи могут получить доступ к приложениям из средства запуска приложений Office 365.</span><span class="sxs-lookup"><span data-stu-id="f5d77-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="f5d77-110">Общие проблемы, которые следует проверить в первую очередь</span><span class="sxs-lookup"><span data-stu-id="f5d77-110">General issues to check first</span></span>

-   <span data-ttu-id="f5d77-111">Убедитесь, что используемый **браузер** соответствует минимальным требованиям для панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f5d77-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="f5d77-112">Проверьте, добавил ли пользовательский браузер URL-адрес приложения в список **надежных сайтов**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="f5d77-113">Убедитесь, что приложение **настроено** правильно.</span><span class="sxs-lookup"><span data-stu-id="f5d77-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="f5d77-114">Проверьте, **включена** ли учетная запись пользователя для входа.</span><span class="sxs-lookup"><span data-stu-id="f5d77-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="f5d77-115">Убедитесь, что учетная запись пользователя **не заблокирована**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="f5d77-116">Удостоверьтесь в том, что **пароль действителен и пользователь не забыл его**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="f5d77-117">Проверьте, не блокирует ли **Многофакторная Идентификация** доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="f5d77-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="f5d77-118">Убедитесь, что **политика условного доступа** или политика **защиты идентификации** не блокирует доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="f5d77-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="f5d77-119">Убедитесь, что **контактная информация для проверки подлинности** актуальна, чтобы разрешить применение политик Многофакторной Идентификации или условного доступа.</span><span class="sxs-lookup"><span data-stu-id="f5d77-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="f5d77-120">Не забудьте также очистить файлы cookie в браузере и повторите попытку входа.</span><span class="sxs-lookup"><span data-stu-id="f5d77-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="f5d77-121">Проверка прямой ссылки</span><span class="sxs-lookup"><span data-stu-id="f5d77-121">Checking the deeplink</span></span>

<span data-ttu-id="f5d77-122">Чтобы проверить правильность прямой ссылки, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f5d77-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="f5d77-123">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f5d77-124">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="f5d77-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f5d77-125">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f5d77-126">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f5d77-127">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="f5d77-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f5d77-128">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f5d77-129">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="f5d77-130">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="f5d77-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="f5d77-131">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="f5d77-132">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="f5d77-133">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="f5d77-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="f5d77-134">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="f5d77-135">Выберите приложение, для которого требуется проверить прямую ссылку.</span><span class="sxs-lookup"><span data-stu-id="f5d77-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="f5d77-136">Найдите метку **URL-адрес пользовательского доступа**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="f5d77-137">Прямая ссылка должна соответствовать этому URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="f5d77-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="f5d77-138">Установка расширения "Панель доступа" для браузера</span><span class="sxs-lookup"><span data-stu-id="f5d77-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="f5d77-139">Чтобы установить расширение "Панель доступа" для браузера, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5d77-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="f5d77-140">Откройте [панель доступа](https://myapps.microsoft.com) в одном из поддерживаемых браузеров и войдите в систему как **пользователь** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5d77-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="f5d77-141">Щелкните **password-SSO application** (приложение с единым входом по паролю) на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f5d77-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="f5d77-142">При появлении запроса на установку программного обеспечения выберите **Установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="f5d77-143">Откроется страница для скачивания расширения в зависимости от вашего браузера.</span><span class="sxs-lookup"><span data-stu-id="f5d77-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="f5d77-144">**Добавьте** расширение в свой браузер.</span><span class="sxs-lookup"><span data-stu-id="f5d77-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="f5d77-145">При необходимости **включите** или **разрешите** расширение.</span><span class="sxs-lookup"><span data-stu-id="f5d77-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="f5d77-146">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="f5d77-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="f5d77-147">Войдите в панель доступа и посмотрите, можете ли вы **запустить** приложения с единым входом по паролю.</span><span class="sxs-lookup"><span data-stu-id="f5d77-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="f5d77-148">Чтобы скачать расширение для Chrome и Firefox, воспользуйтесь следующими ссылками:</span><span class="sxs-lookup"><span data-stu-id="f5d77-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="f5d77-149">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="f5d77-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="f5d77-150">Расширение "Панель доступа" для Firefox</span><span class="sxs-lookup"><span data-stu-id="f5d77-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="f5d77-151">Настройка единого входа по паролю для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5d77-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="f5d77-152">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5d77-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="f5d77-153">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5d77-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="f5d77-154">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="f5d77-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="f5d77-155">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5d77-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="f5d77-156">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5d77-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="f5d77-157">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="f5d77-158">Откройте **расширение Azure Active Directory**, щелкнув **Дополнительные службы** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="f5d77-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f5d77-159">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f5d77-160">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="f5d77-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f5d77-161">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="f5d77-162">Введите имя приложения в текстовом поле **Введите имя** в разделе **Добавить из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="f5d77-163">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="f5d77-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="f5d77-164">Перед добавлением приложения можно изменить его имя в текстовом поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="f5d77-165">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="f5d77-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="f5d77-166">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="f5d77-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="f5d77-167">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="f5d77-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="f5d77-168">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5d77-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="f5d77-169">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f5d77-170">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="f5d77-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f5d77-171">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f5d77-172">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f5d77-173">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="f5d77-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f5d77-174">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f5d77-175">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="f5d77-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="f5d77-176">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="f5d77-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f5d77-177">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="f5d77-178">[Назначьте пользователей приложению](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="f5d77-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="f5d77-179">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="f5d77-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="f5d77-180">В противном случае пользователям будет предложено ввести учетные данные при запуске.</span><span class="sxs-lookup"><span data-stu-id="f5d77-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="f5d77-181">Настройка единого входа по паролю для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="f5d77-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="f5d77-182">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5d77-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="f5d77-183">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="f5d77-183">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="f5d77-184">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="f5d77-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="f5d77-185">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="f5d77-185">Add a non-gallery application</span></span>

<span data-ttu-id="f5d77-186">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5d77-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="f5d77-187">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="f5d77-188">Откройте **расширение Azure Active Directory**, щелкнув **Дополнительные службы** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="f5d77-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f5d77-189">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f5d77-190">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="f5d77-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f5d77-191">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="f5d77-192">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="f5d77-193">Введите имя приложения в текстовое поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="f5d77-194">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-194">Select **Add.**</span></span>

<span data-ttu-id="f5d77-195">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="f5d77-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="f5d77-196">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="f5d77-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="f5d77-197">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5d77-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="f5d77-198">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f5d77-199">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="f5d77-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f5d77-200">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f5d77-201">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f5d77-202">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="f5d77-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="f5d77-203">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f5d77-204">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="f5d77-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="f5d77-205">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="f5d77-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f5d77-206">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="f5d77-207">Введите **URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="f5d77-208">Это URL-адрес страницы, на которой пользователи вводят имена и пароли для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="f5d77-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="f5d77-209">Убедитесь, что на странице по этому URL-адресу отображаются поля для ввода учетных данных.</span><span class="sxs-lookup"><span data-stu-id="f5d77-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="f5d77-210">Назначьте пользователей приложению.</span><span class="sxs-lookup"><span data-stu-id="f5d77-210">Assign users to the application.</span></span>

11. <span data-ttu-id="f5d77-211">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="f5d77-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="f5d77-212">В противном случае пользователям будет предложено ввести учетные данные при запуске.</span><span class="sxs-lookup"><span data-stu-id="f5d77-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="f5d77-213">Назначение приложения пользователю напрямую</span><span class="sxs-lookup"><span data-stu-id="f5d77-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="f5d77-214">Чтобы напрямую назначить одного или нескольких пользователей для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f5d77-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="f5d77-215">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f5d77-216">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="f5d77-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f5d77-217">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f5d77-218">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f5d77-219">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="f5d77-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f5d77-220">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f5d77-221">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="f5d77-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="f5d77-222">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="f5d77-223">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="f5d77-224">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="f5d77-225">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="f5d77-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="f5d77-226">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="f5d77-227">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="f5d77-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="f5d77-228">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="f5d77-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="f5d77-229">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="f5d77-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="f5d77-230">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="f5d77-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="f5d77-231">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="f5d77-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="f5d77-232">Вскоре выбранные пользователи смогут запускать это приложение на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f5d77-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="f5d77-233">Действия по устранению неполадок безрезультатны</span><span class="sxs-lookup"><span data-stu-id="f5d77-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="f5d77-234">В таком случае создайте запрос в службу поддержки, указав следующие сведения (при наличии):</span><span class="sxs-lookup"><span data-stu-id="f5d77-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="f5d77-235">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="f5d77-235">Correlation error ID</span></span>

-   <span data-ttu-id="f5d77-236">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="f5d77-236">UPN (user email address)</span></span>

-   <span data-ttu-id="f5d77-237">идентификатор клиента;</span><span class="sxs-lookup"><span data-stu-id="f5d77-237">TenantID</span></span>

-   <span data-ttu-id="f5d77-238">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="f5d77-238">Browser type</span></span>

-   <span data-ttu-id="f5d77-239">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="f5d77-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="f5d77-240">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="f5d77-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5d77-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5d77-241">Next steps</span></span>
[<span data-ttu-id="f5d77-242">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="f5d77-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
