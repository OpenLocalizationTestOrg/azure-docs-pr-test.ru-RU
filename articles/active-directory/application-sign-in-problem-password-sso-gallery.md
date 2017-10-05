---
title: "Проблемы с входом в приложение из коллекции Azure AD, для которого настроен федеративный единый вход | Документы Майкрософт"
description: "Устранение неполадок с приложением из коллекции Azure AD, для которого настроен единый вход по паролю"
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
ms.openlocfilehash: f8521d1386bba8004e84fe8862a5f59a65ea19ad
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="fbdcc-103">Проблемы с входом в приложение из коллекции Azure AD, для которого настроен федеративный единый вход</span><span class="sxs-lookup"><span data-stu-id="fbdcc-103">Problems signing in to an Azure AD Gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="fbdcc-104">Панель доступа — это веб-портал, позволяющий пользователям с рабочей или учебной учетной записью Azure Active Directory (Azure AD) просматривать и запускать облачные приложения, к которым администратор Azure AD предоставил доступ.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="fbdcc-105">Пользователь, у которого есть выпуски Azure AD, также может использовать возможности самостоятельного управления группами и приложениями с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="fbdcc-106">Панель доступа отделена от портала Azure, и для нее не требуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="fbdcc-107">Чтобы использовать единый вход на основе пароля на панели доступа, в браузере нужно установить расширение панели доступа.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="fbdcc-108">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="fbdcc-109">Соответствие требованиям к браузеру для панели доступа</span><span class="sxs-lookup"><span data-stu-id="fbdcc-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="fbdcc-110">Для работы с панелью доступа требуется браузер с включенной поддержкой JavaScript и CSS.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="fbdcc-111">Чтобы использовать единый вход на основе пароля на панели доступа, в браузере нужно установить расширение панели доступа.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="fbdcc-112">Это расширение автоматически загружается при выборе пользователем приложения, настроенного на работу с единым входом с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="fbdcc-113">Единый вход с использованием пароля работает в таких браузерах:</span><span class="sxs-lookup"><span data-stu-id="fbdcc-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="fbdcc-114">Internet Explorer 8, 9, 10, 11 (в Windows 7 или более поздней версии);</span><span class="sxs-lookup"><span data-stu-id="fbdcc-114">Internet Explorer 8, 9, 10, 11 - on Windows 7 or later</span></span>

-   <span data-ttu-id="fbdcc-115">Chrome (начиная с Windows 7 и MacOS X);</span><span class="sxs-lookup"><span data-stu-id="fbdcc-115">Chrome - on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="fbdcc-116">Firefox 26.0 и более поздние версии (начиная с Windows XP с пакетом обновления 2 (SP2) и Mac OS X 10.6).</span><span class="sxs-lookup"><span data-stu-id="fbdcc-116">Firefox 26.0 or later - on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="fbdcc-117">Расширение для единого входа с использованием пароля будет доступно для браузера Edge в Windows 10 после того, как он начнет поддерживать расширения.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="fbdcc-118">Установка расширения "Панель доступа" для браузера</span><span class="sxs-lookup"><span data-stu-id="fbdcc-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="fbdcc-119">Чтобы установить расширение "Панель доступа" для браузера, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="fbdcc-120">Откройте [панель доступа](https://myapps.microsoft.com) в одном из поддерживаемых браузеров и войдите в систему как **пользователь** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="fbdcc-121">Щелкните **password-SSO application** (приложение с единым входом по паролю) на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="fbdcc-122">При появлении запроса на установку программного обеспечения выберите **Установить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="fbdcc-123">Откроется страница для скачивания расширения в зависимости от вашего браузера.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="fbdcc-124">**Добавьте** расширение в свой браузер.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="fbdcc-125">При необходимости **включите** или **разрешите** расширение.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="fbdcc-126">После установки **перезапустите** сеанс браузера.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="fbdcc-127">Войдите в панель доступа и посмотрите, можете ли вы **запустить** приложения с единым входом по паролю.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="fbdcc-128">Чтобы скачать расширение для Chrome и Firefox, воспользуйтесь следующими ссылками:</span><span class="sxs-lookup"><span data-stu-id="fbdcc-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="fbdcc-129">Расширение "Панель доступа" для Chrome</span><span class="sxs-lookup"><span data-stu-id="fbdcc-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="fbdcc-130">Расширение "Панель доступа" для Firefox</span><span class="sxs-lookup"><span data-stu-id="fbdcc-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="fbdcc-131">Настройка групповой политики для Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="fbdcc-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="fbdcc-132">Вы можете настроить групповую политику, которая позволяет удаленно устанавливать расширение панели доступа для Internet Explorer на компьютерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="fbdcc-133">Предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="fbdcc-133">The prerequisites include:</span></span>

-   <span data-ttu-id="fbdcc-134">Вы уже настроили [доменные службы Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)и подключили компьютеры пользователей к домену.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="fbdcc-135">У вас есть разрешение на изменение параметров для редактирования объекта групповой политики.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="fbdcc-136">По умолчанию такое разрешение имеют члены следующих групп безопасности: «Администраторы домена», «Администраторы предприятия» и «Владельцы-создатели групповой политики».</span><span class="sxs-lookup"><span data-stu-id="fbdcc-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="fbdcc-137">[Подробнее](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbdcc-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="fbdcc-138">Пошаговые инструкции по настройке групповой политики и ее развертыванию для пользователей см. в учебнике [Развертывание расширения панели доступа для Internet Explorer с помощью групповой политики](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy).</span><span class="sxs-lookup"><span data-stu-id="fbdcc-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="fbdcc-139">Устранение неполадок панели доступа в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="fbdcc-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="fbdcc-140">Сведения о доступе к средству диагностики и пошаговые инструкции по настройке расширения для Internet Explorer см. в руководстве [Устранение неполадок расширения "Панель доступа" для Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="fbdcc-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="fbdcc-141">Настройка единого входа по паролю для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbdcc-141">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="fbdcc-142">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="fbdcc-143">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbdcc-143">Add an application from the Azure AD gallery</span></span>](#_Add_an_application)

-   [<span data-ttu-id="fbdcc-144">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="fbdcc-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="fbdcc-145">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="fbdcc-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="fbdcc-146">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbdcc-146">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="fbdcc-147">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="fbdcc-148">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="fbdcc-149">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fbdcc-150">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fbdcc-151">Щелкните **Корпоративные приложения** в меню навигации Azure Active Directory слева.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fbdcc-152">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="fbdcc-153">Введите имя приложения в текстовом поле **Введите имя** в разделе **Добавить из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-153">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="fbdcc-154">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-154">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="fbdcc-155">Перед добавлением приложения можно изменить его имя в текстовом поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-155">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="fbdcc-156">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-156">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="fbdcc-157">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-157">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="fbdcc-158">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="fbdcc-158">Configure the application for password single sign-on</span></span>

<span data-ttu-id="fbdcc-159">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-159">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="fbdcc-160">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-160">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fbdcc-161">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-161">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fbdcc-162">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-162">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fbdcc-163">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-163">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fbdcc-164">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-164">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="fbdcc-165">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-165">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fbdcc-166">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-166">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="fbdcc-167">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-167">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fbdcc-168">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-168">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="fbdcc-169">[Назначьте пользователей приложению](#_How_to_assign).</span><span class="sxs-lookup"><span data-stu-id="fbdcc-169">[Assign users to the application](#_How_to_assign).</span></span>

10. <span data-ttu-id="fbdcc-170">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-170">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="fbdcc-171">В противном случае пользователям будет предложено ввести учетные данные при запуске.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-171">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="fbdcc-172">Назначение пользователей для приложения</span><span class="sxs-lookup"><span data-stu-id="fbdcc-172">Assign users to the application</span></span>

<span data-ttu-id="fbdcc-173">Чтобы напрямую назначить одного или нескольких пользователей для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-173">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="fbdcc-174">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-174">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="fbdcc-175">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-175">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fbdcc-176">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-176">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fbdcc-177">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-177">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fbdcc-178">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-178">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="fbdcc-179">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-179">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="fbdcc-180">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-180">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="fbdcc-181">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-181">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="fbdcc-182">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-182">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="fbdcc-183">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-183">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="fbdcc-184">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-184">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="fbdcc-185">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-185">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="fbdcc-186">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-186">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="fbdcc-187">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-187">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="fbdcc-188">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-188">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="fbdcc-189">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-189">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="fbdcc-190">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-190">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="fbdcc-191">Вскоре выбранные пользователи смогут запускать это приложение на панели доступа.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-191">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshoot-steps-dont-resolve-the-issue"></a><span data-ttu-id="fbdcc-192">Действия по устранению неполадок безрезультатны</span><span class="sxs-lookup"><span data-stu-id="fbdcc-192">If these troubleshoot steps don't resolve the issue</span></span> 
<span data-ttu-id="fbdcc-193">В таком случае создайте запрос в службу поддержки, указав следующие сведения (при наличии):</span><span class="sxs-lookup"><span data-stu-id="fbdcc-193">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="fbdcc-194">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="fbdcc-194">Correlation error ID</span></span>

-   <span data-ttu-id="fbdcc-195">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="fbdcc-195">UPN (user email address)</span></span>

-   <span data-ttu-id="fbdcc-196">идентификатор клиента;</span><span class="sxs-lookup"><span data-stu-id="fbdcc-196">TenantID</span></span>

-   <span data-ttu-id="fbdcc-197">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="fbdcc-197">Browser type</span></span>

-   <span data-ttu-id="fbdcc-198">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="fbdcc-198">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="fbdcc-199">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="fbdcc-199">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbdcc-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbdcc-200">Next steps</span></span>
[<span data-ttu-id="fbdcc-201">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="fbdcc-201">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
