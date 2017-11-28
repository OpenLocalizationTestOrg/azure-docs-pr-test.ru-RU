---
title: "Проблемы с входом в приложение из коллекции Azure AD, для которого настроен единый вход по паролю | Документы Майкрософт"
description: "Описание проблемных областей и рекомендаций по устранению неполадок, связанных с входом в приложения из коллекции Azure AD, для которых настроен единый вход по паролю."
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
ms.openlocfilehash: c90b61812affb7e7af05cf3e302d045958da59be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="b328d-103">Проблемы с входом в приложение из коллекции Azure AD, для которого настроен единый вход по паролю</span><span class="sxs-lookup"><span data-stu-id="b328d-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="b328d-104">Панель доступа — это веб-портал, позволяющий пользователям с рабочей или учебной учетной записью Azure Active Directory (Azure AD) просматривать и запускать облачные приложения, к которым администратор Azure AD предоставил доступ.</span><span class="sxs-lookup"><span data-stu-id="b328d-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="b328d-105">Пользователь, у которого есть выпуски Azure AD, также может использовать возможности самостоятельного управления группами и приложениями с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b328d-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="b328d-106">Панель доступа отделена от портала Azure, и для нее не требуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="b328d-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="b328d-107">Чтобы использовать единый вход на основе пароля на панели доступа, в браузере нужно установить расширение панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b328d-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="b328d-108">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="b328d-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="b328d-109">Соответствие требованиям к браузеру для панели доступа</span><span class="sxs-lookup"><span data-stu-id="b328d-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="b328d-110">Для работы с панелью доступа требуется браузер с включенной поддержкой JavaScript и CSS.</span><span class="sxs-lookup"><span data-stu-id="b328d-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="b328d-111">Чтобы использовать единый вход на основе пароля на панели доступа, в браузере нужно установить расширение панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b328d-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="b328d-112">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="b328d-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="b328d-113">Единый вход с использованием пароля работает в таких браузерах:</span><span class="sxs-lookup"><span data-stu-id="b328d-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="b328d-114">Internet Explorer 8, 9, 10, 11 (в Windows 7 или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="b328d-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="b328d-115">Chrome (начиная с Windows 7 и Mac OS X);</span><span class="sxs-lookup"><span data-stu-id="b328d-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="b328d-116">Firefox 26.0 и более поздние версии (начиная с Windows XP с пакетом обновления 2 (SP2) и Mac OS X 10.6).</span><span class="sxs-lookup"><span data-stu-id="b328d-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="b328d-117">Расширение для единого входа с использованием пароля будет доступно для браузера Edge в Windows 10 после того, как он начнет поддерживать расширения.</span><span class="sxs-lookup"><span data-stu-id="b328d-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="b328d-118">Установка расширения "Панель доступа" для браузера</span><span class="sxs-lookup"><span data-stu-id="b328d-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="b328d-119">Чтобы установить расширение "Панель доступа" для браузера, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b328d-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="b328d-120">Откройте [панель доступа](https://myapps.microsoft.com) в одном из поддерживаемых браузеров и войдите в систему как **пользователь** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b328d-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="b328d-121">Щелкните **password-SSO application** (приложение с единым входом по паролю) на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b328d-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="b328d-122">При появлении запроса на установку программного обеспечения выберите **Установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="b328d-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="b328d-123">Откроется страница для скачивания расширения в зависимости от вашего браузера.</span><span class="sxs-lookup"><span data-stu-id="b328d-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="b328d-124">**Добавьте** расширение в свой браузер.</span><span class="sxs-lookup"><span data-stu-id="b328d-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="b328d-125">При необходимости **включите** или **разрешите** расширение.</span><span class="sxs-lookup"><span data-stu-id="b328d-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="b328d-126">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="b328d-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="b328d-127">Войдите в панель доступа и посмотрите, можете ли вы **запустить** приложения с единым входом по паролю.</span><span class="sxs-lookup"><span data-stu-id="b328d-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="b328d-128">Чтобы скачать расширение для Chrome и Firefox, воспользуйтесь следующими ссылками:</span><span class="sxs-lookup"><span data-stu-id="b328d-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="b328d-129">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="b328d-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="b328d-130">Расширение "Панель доступа" для Firefox</span><span class="sxs-lookup"><span data-stu-id="b328d-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="b328d-131">Настройка групповой политики для Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b328d-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="b328d-132">Вы можете настроить групповую политику, которая позволяет удаленно устанавливать расширение панели доступа для Internet Explorer на компьютерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="b328d-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="b328d-133">Предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="b328d-133">The prerequisites include:</span></span>

-   <span data-ttu-id="b328d-134">Вы уже настроили [доменные службы Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)и подключили компьютеры пользователей к домену.</span><span class="sxs-lookup"><span data-stu-id="b328d-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="b328d-135">У вас есть разрешение на изменение параметров для редактирования объекта групповой политики.</span><span class="sxs-lookup"><span data-stu-id="b328d-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="b328d-136">По умолчанию такое разрешение имеют члены следующих групп безопасности: «Администраторы домена», «Администраторы предприятия» и «Владельцы-создатели групповой политики».</span><span class="sxs-lookup"><span data-stu-id="b328d-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="b328d-137">[Подробнее](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b328d-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="b328d-138">Пошаговые инструкции по настройке групповой политики и ее развертыванию для пользователей см. в учебнике [Развертывание расширения панели доступа для Internet Explorer с помощью групповой политики](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy).</span><span class="sxs-lookup"><span data-stu-id="b328d-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="b328d-139">Устранение неполадок панели доступа в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b328d-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="b328d-140">Сведения о доступе к средству диагностики и пошаговые инструкции по настройке расширения для Internet Explorer см. в руководстве [Устранение неполадок расширения "Панель доступа" для Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="b328d-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b328d-141">Настройка единого входа по паролю для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="b328d-141">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b328d-142">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b328d-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="b328d-143">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="b328d-143">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   [<span data-ttu-id="b328d-144">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="b328d-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="b328d-145">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="b328d-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="b328d-146">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="b328d-146">Add a non-gallery application</span></span>

<span data-ttu-id="b328d-147">Чтобы добавить приложение, не входящее в коллекцию Azure AD, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b328d-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="b328d-148">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="b328d-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="b328d-149">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b328d-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b328d-150">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b328d-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b328d-151">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b328d-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b328d-152">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b328d-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="b328d-153">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="b328d-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="b328d-154">Введите имя приложения в текстовое поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="b328d-154">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="b328d-155">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b328d-155">Select **Add.**</span></span>

<span data-ttu-id="b328d-156">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b328d-156">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="b328d-157">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="b328d-157">Configure the application for password single sign-on</span></span>

<span data-ttu-id="b328d-158">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b328d-158">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="b328d-159">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="b328d-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b328d-160">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b328d-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b328d-161">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b328d-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b328d-162">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b328d-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b328d-163">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="b328d-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="b328d-164">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b328d-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b328d-165">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="b328d-165">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="b328d-166">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="b328d-166">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b328d-167">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="b328d-167">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="b328d-168">Введите **URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="b328d-168">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="b328d-169">Это URL-адрес страницы, на которой пользователи вводят имена и пароли для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="b328d-169">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="b328d-170">Убедитесь, что на странице по этому URL-адресу отображаются поля для ввода учетных данных.</span><span class="sxs-lookup"><span data-stu-id="b328d-170">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="b328d-171">Назначьте пользователей приложению.</span><span class="sxs-lookup"><span data-stu-id="b328d-171">Assign users to the application.</span></span>

11. <span data-ttu-id="b328d-172">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="b328d-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="b328d-173">В противном случае пользователям будет предложено ввести учетные данные при запуске.</span><span class="sxs-lookup"><span data-stu-id="b328d-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="b328d-174">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="b328d-174">Assign users to the application</span></span>

<span data-ttu-id="b328d-175">Чтобы напрямую назначить одного или нескольких пользователей для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b328d-175">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="b328d-176">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="b328d-176">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="b328d-177">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="b328d-177">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b328d-178">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b328d-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b328d-179">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b328d-179">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b328d-180">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="b328d-180">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="b328d-181">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b328d-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b328d-182">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="b328d-182">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="b328d-183">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b328d-183">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b328d-184">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="b328d-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="b328d-185">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b328d-185">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="b328d-186">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="b328d-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="b328d-187">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="b328d-187">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="b328d-188">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="b328d-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="b328d-189">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="b328d-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="b328d-190">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="b328d-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="b328d-191">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="b328d-191">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="b328d-192">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="b328d-192">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="b328d-193">Вскоре выбранные пользователи смогут запускать это приложение на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b328d-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="b328d-194">Действия по устранению неполадок безрезультатны</span><span class="sxs-lookup"><span data-stu-id="b328d-194">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="b328d-195">В таком случае создайте запрос в службу поддержки, указав следующие сведения (при наличии):</span><span class="sxs-lookup"><span data-stu-id="b328d-195">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="b328d-196">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="b328d-196">Correlation error ID</span></span>

-   <span data-ttu-id="b328d-197">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="b328d-197">UPN (user email address)</span></span>

-   <span data-ttu-id="b328d-198">идентификатор клиента;</span><span class="sxs-lookup"><span data-stu-id="b328d-198">TenantID</span></span>

-   <span data-ttu-id="b328d-199">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="b328d-199">Browser type</span></span>

-   <span data-ttu-id="b328d-200">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="b328d-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="b328d-201">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b328d-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="b328d-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b328d-202">Next steps</span></span>
[<span data-ttu-id="b328d-203">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="b328d-203">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

