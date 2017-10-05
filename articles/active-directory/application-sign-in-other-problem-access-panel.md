---
title: "Проблемы при входе в приложение из панели доступа | Документы Майкрософт"
description: "Устранение проблем с обращением к приложению из панели доступа Microsoft Azure AD на сайте myapps.microsoft.com"
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
ms.reviewer: japere
ms.openlocfilehash: 188a00db59b0aa8d26facc678fb52d96272183b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="4ef83-103">Проблемы при входе в приложение из панели доступа</span><span class="sxs-lookup"><span data-stu-id="4ef83-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="4ef83-104">Панель доступа — это веб-портал, позволяющий пользователям с рабочей или учебной учетной записью Azure Active Directory (Azure AD) просматривать и запускать облачные приложения, к которым администратор Azure AD предоставил доступ</span><span class="sxs-lookup"><span data-stu-id="4ef83-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="4ef83-105">Эти приложения настраиваются от имени пользователя на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ef83-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="4ef83-106">Чтобы пользователь видел приложение на панели доступа, оно должно быть правильно настроено и назначено пользователю или группе, к которой он относится.</span><span class="sxs-lookup"><span data-stu-id="4ef83-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="4ef83-107">Типы приложений, которые может видеть пользователь, делятся на следующие категории:</span><span class="sxs-lookup"><span data-stu-id="4ef83-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="4ef83-108">приложения Office 365;</span><span class="sxs-lookup"><span data-stu-id="4ef83-108">Office 365 Applications</span></span>

-   <span data-ttu-id="4ef83-109">приложения Майкрософт и сторонние приложения с единым входом на основе федерации;</span><span class="sxs-lookup"><span data-stu-id="4ef83-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="4ef83-110">приложения с единым входом на основе паролей;</span><span class="sxs-lookup"><span data-stu-id="4ef83-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="4ef83-111">приложения с существующими решениями единого входа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="4ef83-112">Общие проблемы, которые следует проверить в первую очередь</span><span class="sxs-lookup"><span data-stu-id="4ef83-112">General issues to check first</span></span>

-   <span data-ttu-id="4ef83-113">Убедитесь, что используемый **браузер** соответствует минимальным требованиям для панели доступа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="4ef83-114">Проверьте, добавил ли пользовательский браузер URL-адрес приложения в список **надежных сайтов**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="4ef83-115">Убедитесь, что приложение **настроено** правильно.</span><span class="sxs-lookup"><span data-stu-id="4ef83-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="4ef83-116">Проверьте, **включена** ли учетная запись пользователя для входа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-116">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="4ef83-117">Убедитесь, что учетная запись пользователя **не заблокирована**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="4ef83-118">Удостоверьтесь в том, что **пароль действителен и пользователь не забыл его**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="4ef83-119">Проверьте, не блокирует ли **Многофакторная Идентификация** доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="4ef83-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="4ef83-120">Убедитесь, что **политика условного доступа** или политика **защиты идентификации** не блокирует доступ пользователей.</span><span class="sxs-lookup"><span data-stu-id="4ef83-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="4ef83-121">Убедитесь, что **контактная информация для проверки подлинности** актуальна, чтобы разрешить применение политик Многофакторной Идентификации или условного доступа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="4ef83-122">Не забудьте также очистить файлы cookie в браузере и повторите попытку входа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="4ef83-123">Соответствие требованиям к браузеру для панели доступа</span><span class="sxs-lookup"><span data-stu-id="4ef83-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="4ef83-124">Для работы с панелью доступа требуется браузер с включенной поддержкой JavaScript и CSS.</span><span class="sxs-lookup"><span data-stu-id="4ef83-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="4ef83-125">Чтобы использовать единый вход на основе пароля на панели доступа, в браузере нужно установить расширение панели доступа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="4ef83-126">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="4ef83-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="4ef83-127">Единый вход с использованием пароля работает в таких браузерах:</span><span class="sxs-lookup"><span data-stu-id="4ef83-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="4ef83-128">Internet Explorer 8, 9, 10, 11 (в Windows 7 или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="4ef83-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="4ef83-129">Edge в Windows 10 Anniversary Edition или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="4ef83-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="4ef83-130">Chrome (начиная с Windows 7 и Mac OS X);</span><span class="sxs-lookup"><span data-stu-id="4ef83-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="4ef83-131">Firefox 26.0 и более поздние версии (начиная с Windows XP с пакетом обновления 2 (SP2) и Mac OS X 10.6).</span><span class="sxs-lookup"><span data-stu-id="4ef83-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="4ef83-132">Установка расширения "Панель доступа" для браузера</span><span class="sxs-lookup"><span data-stu-id="4ef83-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="4ef83-133">Чтобы установить расширение "Панель доступа" для браузера, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-134">Откройте [панель доступа](https://myapps.microsoft.com) в одном из поддерживаемых браузеров и войдите в систему как **пользователь** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ef83-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="4ef83-135">Щелкните **password-SSO application** (приложение с единым входом по паролю) на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="4ef83-136">При появлении запроса на установку программного обеспечения выберите **Установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="4ef83-137">Откроется страница для скачивания расширения в зависимости от вашего браузера.</span><span class="sxs-lookup"><span data-stu-id="4ef83-137">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="4ef83-138">**Добавьте** расширение в свой браузер.</span><span class="sxs-lookup"><span data-stu-id="4ef83-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="4ef83-139">При необходимости **включите** или **разрешите** расширение.</span><span class="sxs-lookup"><span data-stu-id="4ef83-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="4ef83-140">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="4ef83-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="4ef83-141">Войдите в панель доступа и посмотрите, можете ли вы **запустить** приложения с единым входом по паролю.</span><span class="sxs-lookup"><span data-stu-id="4ef83-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="4ef83-142">Чтобы скачать расширение для Chrome и Edge, воспользуйтесь следующими ссылками:</span><span class="sxs-lookup"><span data-stu-id="4ef83-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="4ef83-143">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="4ef83-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="4ef83-144">Расширение "Панель доступа" для Edge</span><span class="sxs-lookup"><span data-stu-id="4ef83-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="4ef83-145">Настройка федеративного единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef83-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="4ef83-146">Для всех приложений в коллекции Azure AD, для которых включен корпоративный единый вход, доступны пошаговые руководства.</span><span class="sxs-lookup"><span data-stu-id="4ef83-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="4ef83-147">Подробное пошаговое руководство можно найти в [списке учебников по интеграции приложений SaaS с Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="4ef83-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="4ef83-148">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4ef83-149">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef83-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="4ef83-150">Указание значений метаданных приложения в Azure AD (URL-адрес для входа, идентификатор, URL-адрес ответа)</span><span class="sxs-lookup"><span data-stu-id="4ef83-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="4ef83-151">Выбор идентификатора пользователя и добавление атрибутов пользователей, которые будут отправлены в приложение</span><span class="sxs-lookup"><span data-stu-id="4ef83-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="4ef83-152">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="4ef83-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="4ef83-153">Указание значений метаданных Azure AD в приложении (URL-адрес для входа, издатель, URL-адрес для выхода и сертификат)</span><span class="sxs-lookup"><span data-stu-id="4ef83-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="4ef83-154">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="4ef83-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="4ef83-155">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef83-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="4ef83-156">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-157">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="4ef83-158">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-159">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-160">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-161">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="4ef83-162">Введите имя приложения в текстовом поле **Введите имя** в разделе **Добавить из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="4ef83-163">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="4ef83-164">Перед добавлением приложения можно изменить его имя в текстовом поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="4ef83-165">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="4ef83-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="4ef83-166">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="4ef83-167">Настройка единого входа для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef83-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="4ef83-168">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4ef83-170">Откройте **расширение Azure Active Directory**, щелкнув **Дополнительные службы** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-171">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-172">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-173">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef83-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4ef83-174">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4ef83-175">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4ef83-176">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4ef83-177">В раскрывающемся списке **Режим** выберите пункт **Вход на основе SAML**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="4ef83-178">Введите необходимые значения в поле **Домены и URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="4ef83-179">Их можно получить у поставщика приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="4ef83-180">Чтобы настроить единый вход, инициированный поставщиком услуг, обязательно укажите URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-180">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="4ef83-181">Для некоторых приложений также нужно указать идентификатор.</span><span class="sxs-lookup"><span data-stu-id="4ef83-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="4ef83-182">Чтобы настроить единый вход, инициированный поставщиком удостоверений, введите URL-адрес для ответа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-182">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="4ef83-183">Для некоторых приложений также нужно указать идентификатор.</span><span class="sxs-lookup"><span data-stu-id="4ef83-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="4ef83-184">**Необязательно:** щелкните **Показать дополнительные параметры URL-адресов**, чтобы увидеть необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="4ef83-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="4ef83-185">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="4ef83-186">**Необязательно:** щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="4ef83-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4ef83-187">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-187">To add an attribute:</span></span>

   1. <span data-ttu-id="4ef83-188">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-188">click **Add attribute**.</span></span> <span data-ttu-id="4ef83-189">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="4ef83-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="4ef83-190">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-190">Click **Save.**</span></span> <span data-ttu-id="4ef83-191">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="4ef83-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="4ef83-192">Щелкните **Настроить &lt;имя приложения&gt;**, чтобы открыть документацию по настройке единого входа для приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="4ef83-193">Кроме того, для настройки единого входа для приложения также потребуются URL-адреса метаданных и сертификат.</span><span class="sxs-lookup"><span data-stu-id="4ef83-193">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="4ef83-194">Чтобы сохранить конфигурацию, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="4ef83-195">Назначьте пользователей приложению.</span><span class="sxs-lookup"><span data-stu-id="4ef83-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="4ef83-196">Выберите идентификатор пользователя и добавьте атрибуты пользователя, которые будут отправлены в приложение.</span><span class="sxs-lookup"><span data-stu-id="4ef83-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="4ef83-197">Чтобы выбрать идентификатор пользователя или добавить атрибуты пользователя, выполните указанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="4ef83-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-198">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4ef83-199">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-200">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-201">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-202">Щелкните **Все приложения** для просмотра списка всех приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef83-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4ef83-203">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4ef83-204">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4ef83-205">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4ef83-206">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="4ef83-207">Выбранный параметр должен соответствовать ожидаемому значению для проверки подлинности пользователя в приложении.</span><span class="sxs-lookup"><span data-stu-id="4ef83-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="4ef83-208">Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="4ef83-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="4ef83-209">Дополнительные сведения см. в разделе NameIDPolicy статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="4ef83-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="4ef83-210">Чтобы добавить атрибуты пользователя, щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="4ef83-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4ef83-211">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-211">To add an attribute:</span></span>

   1. <span data-ttu-id="4ef83-212">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-212">click **Add attribute**.</span></span> <span data-ttu-id="4ef83-213">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="4ef83-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="4ef83-214">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-214">Click **Save.**</span></span> <span data-ttu-id="4ef83-215">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="4ef83-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="4ef83-216">Скачивание метаданных Azure AD или сертификата</span><span class="sxs-lookup"><span data-stu-id="4ef83-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="4ef83-217">Чтобы скачать метаданные приложения или сертификат в Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4ef83-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-218">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-218">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4ef83-219">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-219">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-220">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-221">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-221">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-222">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef83-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4ef83-223">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4ef83-224">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4ef83-225">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-225">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4ef83-226">Перейдите в раздел **Сертификат подписи SAML** и выберите значение в столбце **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="4ef83-227">В зависимости от того, что именно требуется для настройки единого входа, вы сможете скачать XML-файл метаданных или сертификат.</span><span class="sxs-lookup"><span data-stu-id="4ef83-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="4ef83-228">Azure AD не предоставляет URL-адреса для получения метаданных.</span><span class="sxs-lookup"><span data-stu-id="4ef83-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="4ef83-229">Метаданные можно скачать только в виде XML-файла.</span><span class="sxs-lookup"><span data-stu-id="4ef83-229">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4ef83-230">Настройка федеративного единого входа для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="4ef83-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4ef83-231">Чтобы настроить приложение не из коллекции, вам потребуется Azure AD Premium, а приложение должно поддерживать SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="4ef83-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="4ef83-232">Дополнительные сведения о версиях Azure AD см. в разделе [Цены на Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="4ef83-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="4ef83-233">Указание значений метаданных приложения в Azure AD (URL-адрес для входа, идентификатор, URL-адрес ответа)</span><span class="sxs-lookup"><span data-stu-id="4ef83-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="4ef83-234">Выбор идентификатора пользователя и добавление атрибутов пользователей, которые будут отправлены в приложение</span><span class="sxs-lookup"><span data-stu-id="4ef83-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="4ef83-235">Получение метаданных Azure AD и сертификата</span><span class="sxs-lookup"><span data-stu-id="4ef83-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="4ef83-236">Указание значений метаданных Azure AD в приложении (URL-адрес для входа, издатель, URL-адрес для выхода и сертификат)</span><span class="sxs-lookup"><span data-stu-id="4ef83-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="4ef83-237">Указание значений метаданных приложения в Azure AD (URL-адрес для входа, идентификатор, URL-адрес ответа)</span><span class="sxs-lookup"><span data-stu-id="4ef83-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="4ef83-238">Чтобы настроить единый вход для приложения, которое не находится в коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-239">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-239">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4ef83-240">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-240">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-241">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-242">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-242">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-243">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-243">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="4ef83-244">Щелкните **Приложение не из коллекции** в разделе **Добавление собственного приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-244">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="4ef83-245">Введите имя приложения в поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="4ef83-246">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="4ef83-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="4ef83-247">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-247">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="4ef83-248">В раскрывающемся списке **Режим** выберите пункт **Вход на основе SAML**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="4ef83-249">Введите необходимые значения в поле **Домены и URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="4ef83-250">Их можно получить у поставщика приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="4ef83-251">Чтобы настроить единый вход, инициированный поставщиком удостоверений, введите URL-адрес ответа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="4ef83-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="4ef83-252">**Необязательно:** чтобы настроить единый вход, инициированный поставщиком услуг, обязательно укажите URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-252">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="4ef83-253">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="4ef83-254">**Необязательно:** щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="4ef83-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4ef83-255">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-255">To add an attribute:</span></span>

   1. <span data-ttu-id="4ef83-256">Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-256">click **Add attribute**.</span></span> <span data-ttu-id="4ef83-257">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="4ef83-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="4ef83-258">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-258">Click **Save.**</span></span> <span data-ttu-id="4ef83-259">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="4ef83-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="4ef83-260">Щелкните **Настроить &lt;имя приложения&gt;**, чтобы открыть документацию по настройке единого входа для приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="4ef83-261">Кроме того, у вас есть URL-адреса Azure AD и сертификат, необходимые для приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-261">Also, you has Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="4ef83-262">Выберите идентификатор пользователя и добавьте атрибуты пользователя, которые будут отправлены в приложение.</span><span class="sxs-lookup"><span data-stu-id="4ef83-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="4ef83-263">Чтобы выбрать идентификатор пользователя или добавить атрибуты пользователя, выполните указанные ниже действия:</span><span class="sxs-lookup"><span data-stu-id="4ef83-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-264">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-264">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4ef83-265">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-265">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-266">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-267">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-267">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-268">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef83-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4ef83-269">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4ef83-270">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4ef83-271">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-271">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4ef83-272">В разделе **Атрибуты пользователя** выберите уникальный идентификатор пользователя в раскрывающемся списке **Идентификатор пользователя**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="4ef83-273">Выбранный параметр должен соответствовать ожидаемому значению для проверки подлинности пользователя в приложении.</span><span class="sxs-lookup"><span data-stu-id="4ef83-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="4ef83-274">Azure AD выбирает формат атрибута NameID (идентификатор пользователя) на основе выбранного значения или формата, который был запрошен приложением в запросе проверки подлинности SAML.</span><span class="sxs-lookup"><span data-stu-id="4ef83-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="4ef83-275">Дополнительные сведения см. в разделе NameIDPolicy статьи [Протокол единого входа SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="4ef83-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="4ef83-276">Чтобы добавить атрибуты пользователя, щелкните **Просмотреть и изменить все другие атрибуты пользователей**, чтобы изменить атрибуты, которые будут отправлены приложению в токене SAML при входе пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="4ef83-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="4ef83-277">Чтобы добавить атрибут, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-277">To add an attribute:</span></span>

   <span data-ttu-id="4ef83-278">1. Нажмите кнопку **Добавить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-278">1.click **Add attribute**.</span></span> <span data-ttu-id="4ef83-279">Введите **Имя** и выберите **Значение** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="4ef83-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="4ef83-280">2. Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-280">2 Click **Save.**</span></span> <span data-ttu-id="4ef83-281">Новый атрибут появится в таблице.</span><span class="sxs-lookup"><span data-stu-id="4ef83-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="4ef83-282">Скачивание метаданных Azure AD или сертификата</span><span class="sxs-lookup"><span data-stu-id="4ef83-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="4ef83-283">Чтобы скачать метаданные приложения или сертификат в Azure AD, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4ef83-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-284">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-284">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4ef83-285">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-285">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-286">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-287">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-287">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-288">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef83-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4ef83-289">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4ef83-290">Выберите приложение, для которого был настроен единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="4ef83-291">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-291">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4ef83-292">Перейдите в раздел **Сертификат подписи SAML** и выберите значение в столбце **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="4ef83-293">В зависимости от того, что именно требуется для настройки единого входа, вы сможете скачать XML-файл метаданных или сертификат.</span><span class="sxs-lookup"><span data-stu-id="4ef83-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="4ef83-294">Azure AD не предоставляет URL-адреса для получения метаданных.</span><span class="sxs-lookup"><span data-stu-id="4ef83-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="4ef83-295">Метаданные можно скачать только в виде XML-файла.</span><span class="sxs-lookup"><span data-stu-id="4ef83-295">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="4ef83-296">Настройка единого входа по паролю для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef83-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="4ef83-297">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="4ef83-298">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef83-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="4ef83-299">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="4ef83-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="4ef83-300">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ef83-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="4ef83-301">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-302">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-302">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="4ef83-303">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-303">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-304">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-305">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-305">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-306">В правом верхнем углу колонки **Корпоративные приложения** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-306">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="4ef83-307">В разделе **Добавить из коллекции** в текстовом поле **Введите имя** введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="4ef83-308">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="4ef83-309">Перед добавлением приложения можно изменить его имя в текстовом поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="4ef83-310">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="4ef83-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="4ef83-311">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-311">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="4ef83-312">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="4ef83-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="4ef83-313">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-314">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-314">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4ef83-315">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-315">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-316">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-317">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-317">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-318">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef83-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="4ef83-319">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4ef83-320">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="4ef83-321">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-321">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4ef83-322">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4ef83-323">Назначьте пользователей приложению.</span><span class="sxs-lookup"><span data-stu-id="4ef83-323">Assign users to the application.</span></span>

10. <span data-ttu-id="4ef83-324">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="4ef83-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="4ef83-325">В противном случае пользователям будет предложено ввести учетные данные при запуске.</span><span class="sxs-lookup"><span data-stu-id="4ef83-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4ef83-326">Настройка единого входа по паролю для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="4ef83-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4ef83-327">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="4ef83-328">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="4ef83-328">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="4ef83-329">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="4ef83-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="4ef83-330">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="4ef83-330">Add a non-gallery application</span></span>

<span data-ttu-id="4ef83-331">Чтобы добавить приложение, не входящее в коллекцию Azure AD, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4ef83-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-332">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-332">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="4ef83-333">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-333">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-334">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-335">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-335">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-336">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-336">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="4ef83-337">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="4ef83-338">Введите имя приложения в текстовое поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="4ef83-339">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-339">Select **Add.**</span></span>

<span data-ttu-id="4ef83-340">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-340">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="4ef83-341">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="4ef83-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="4ef83-342">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-343">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-343">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4ef83-344">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-344">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-345">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-346">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-346">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-347">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef83-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="4ef83-348">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4ef83-349">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="4ef83-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4ef83-350">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-350">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4ef83-351">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4ef83-352">Введите **URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="4ef83-353">Это URL-адрес страницы, на которой пользователи вводят имена и пароли для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="4ef83-353">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="4ef83-354">Убедитесь, что на странице по этому URL-адресу отображаются поля для ввода учетных данных.</span><span class="sxs-lookup"><span data-stu-id="4ef83-354">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="4ef83-355">Назначьте пользователей приложению.</span><span class="sxs-lookup"><span data-stu-id="4ef83-355">Assign users to the application.</span></span>

11. <span data-ttu-id="4ef83-356">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="4ef83-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="4ef83-357">В противном случае пользователям будет предложено ввести учетные данные при запуске.</span><span class="sxs-lookup"><span data-stu-id="4ef83-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="4ef83-358">Назначение приложения пользователю напрямую</span><span class="sxs-lookup"><span data-stu-id="4ef83-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="4ef83-359">Чтобы напрямую назначить одного или нескольких пользователей для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4ef83-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="4ef83-360">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-360">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4ef83-361">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="4ef83-361">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4ef83-362">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4ef83-363">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-363">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4ef83-364">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="4ef83-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4ef83-365">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4ef83-366">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="4ef83-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="4ef83-367">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-367">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4ef83-368">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="4ef83-369">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-369">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="4ef83-370">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="4ef83-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="4ef83-371">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="4ef83-372">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="4ef83-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="4ef83-373">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="4ef83-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="4ef83-374">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="4ef83-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="4ef83-375">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="4ef83-375">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="4ef83-376">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="4ef83-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="4ef83-377">Вскоре выбранные пользователи смогут запускать это приложение на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="4ef83-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="4ef83-378">Действия по устранению неполадок безрезультатны</span><span class="sxs-lookup"><span data-stu-id="4ef83-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="4ef83-379">В таком случае создайте запрос в службу поддержки, указав следующие сведения (при наличии):</span><span class="sxs-lookup"><span data-stu-id="4ef83-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="4ef83-380">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="4ef83-380">Correlation error ID</span></span>

-   <span data-ttu-id="4ef83-381">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="4ef83-381">UPN (user email address)</span></span>

-   <span data-ttu-id="4ef83-382">идентификатор клиента;</span><span class="sxs-lookup"><span data-stu-id="4ef83-382">TenantID</span></span>

-   <span data-ttu-id="4ef83-383">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="4ef83-383">Browser type</span></span>

-   <span data-ttu-id="4ef83-384">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="4ef83-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="4ef83-385">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="4ef83-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ef83-386">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4ef83-386">Next steps</span></span>
[<span data-ttu-id="4ef83-387">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="4ef83-387">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

