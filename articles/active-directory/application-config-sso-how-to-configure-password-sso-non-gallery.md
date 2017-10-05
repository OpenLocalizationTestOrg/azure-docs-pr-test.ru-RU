---
title: "Настройка единого входа по паролю для приложения не из коллекции | Документация Майкрософт"
description: "Как настроить пользовательское приложение для защищенного единого входа по паролю, если оно не отображается в коллекции приложений Azure AD"
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
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="256c8-103">Настройка единого входа по паролю для приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="256c8-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="256c8-104">В дополнение к тем вариантам, которые доступны в коллекции приложений Azure AD, вы можете добавить любое **приложение не из коллекции**, которое не входит этот список.</span><span class="sxs-lookup"><span data-stu-id="256c8-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="256c8-105">С помощью этой функции вы можете добавить любое приложение, которое уже существует в вашей организации, или любое приложение независимого поставщика, которое не входит в экосистему [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="256c8-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="256c8-106">Добавив любое приложение, не входящее в коллекцию, вы сможете настроить для него единый вход, выбрав элемент навигации **Единый вход** в разделе корпоративных приложений на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="256c8-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="256c8-107">Один из доступных способов единого входа — это [единый вход по паролю](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="256c8-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="256c8-108">Функция **добавления приложений, не входящих в коллекцию** позволяет интегрировать любое приложение, которое отображает HTML-форму для ввода имени пользователя и пароля, даже если это приложение не входит в набор предварительно интегрированных приложений.</span><span class="sxs-lookup"><span data-stu-id="256c8-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="256c8-109">Для этого применяется технология извлечения данных из страницы, которую реализует расширение панели доступа. Оно автоматически определяет поля для имени пользователя и пароля и надежно хранит информацию об определенном экземпляре приложения.</span><span class="sxs-lookup"><span data-stu-id="256c8-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="256c8-110">Затем имена пользователей и пароли безопасно передаются в эти поля, когда пользователь переходит к приложению через панель доступа.</span><span class="sxs-lookup"><span data-stu-id="256c8-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="256c8-111">Это отличный способ для быстрой интеграции любых приложений в Azure AD. Он предоставляет следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="256c8-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="256c8-112">Интеграция с клиентом Azure AD **любого существующего в мире приложения**, которое может отображать поля для ввода имени пользователя и пароля в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="256c8-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="256c8-113">Использование **единого входа для пользователей** с помощью безопасного хранения и воспроизведения имен пользователей и паролей для приложений, интегрированных с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="256c8-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="256c8-114">**Автоопределение полей ввода** для любого приложения через расширение обозревателя панели доступа, а также возможность вручную указывать эти поля, если автоматическое определение не сработает.</span><span class="sxs-lookup"><span data-stu-id="256c8-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="256c8-115">**Поддержка приложений, использующих несколько полей ввода учетных данных** помимо обычных имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="256c8-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="256c8-116">**Настройка меток** для полей ввода имени пользователя и пароля, которые будут отображаться при вводе учетных данных на [панели доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).</span><span class="sxs-lookup"><span data-stu-id="256c8-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="256c8-117">**Пользователи** могут использовать имена пользователей и пароли для любых существующих учетных записей при вводе вручную в [панели доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).</span><span class="sxs-lookup"><span data-stu-id="256c8-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="256c8-118">**Члены бизнес-группы** могут назначать пользователям имена для входа и пароли, используя функцию [самостоятельной настройки доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access).</span><span class="sxs-lookup"><span data-stu-id="256c8-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="256c8-119">**Администратор** может назначать пользователям имена для входа и пароли, используя функцию обновления учетных данных при [назначении пользователей приложениям](#_How_to_configure_1).</span><span class="sxs-lookup"><span data-stu-id="256c8-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="256c8-120">**Администратор** может назначать группам пользователей совместно используемые имена для входа и пароли, используя функцию обновления учетных данных при [назначении групп приложениям](#assign-an-application-to-a-group-directly).</span><span class="sxs-lookup"><span data-stu-id="256c8-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="256c8-121">Ниже описывается, как включить [единый вход по паролю](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) для любого приложения, которое вы ранее добавили с помощью функции **добавления приложения не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="256c8-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="256c8-122">Обзор необходимых действий</span><span class="sxs-lookup"><span data-stu-id="256c8-122">Overview of steps required</span></span>

<span data-ttu-id="256c8-123">Чтобы настроить приложение из коллекции Azure AD, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="256c8-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   <span data-ttu-id="256c8-124">[добавьте приложение не из коллекции](#add-a-non-gallery-application);</span><span class="sxs-lookup"><span data-stu-id="256c8-124">[Add a non-gallery application](#add-a-non-gallery-application)</span></span>

-   <span data-ttu-id="256c8-125">[настройте приложение для единого входа по паролю](#configure-the-application-for-password-single-sign-on);</span><span class="sxs-lookup"><span data-stu-id="256c8-125">[Configure the application for password single sign-on](#configure-the-application-for-password-single-sign-on)</span></span>

-   <span data-ttu-id="256c8-126">[назначьте приложение пользователю или группе](#assign-the-application-to-a-user-or-a-group);</span><span class="sxs-lookup"><span data-stu-id="256c8-126">[Assign the application to a user or a group](#assign-the-application-to-a-user-or-a-group)</span></span>

    -   <span data-ttu-id="256c8-127">[назначьте приложение пользователю напрямую](#assign-a-user-to-an-application-directly);</span><span class="sxs-lookup"><span data-stu-id="256c8-127">[Assign a user to an application directly](#assign-a-user-to-an-application-directly)</span></span>

    -   <span data-ttu-id="256c8-128">[назначьте приложение группе напрямую](#assign-an-application-to-a-group-directly).</span><span class="sxs-lookup"><span data-stu-id="256c8-128">[Assign an application to a group directly](#assign-an-application-to-a-group-directly)</span></span>

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="256c8-129">Добавление приложения не из коллекции</span><span class="sxs-lookup"><span data-stu-id="256c8-129">Add a non-gallery application</span></span>

<span data-ttu-id="256c8-130">Чтобы добавить приложение, не входящее в коллекцию Azure AD, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="256c8-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="256c8-131">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="256c8-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="256c8-132">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="256c8-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="256c8-133">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="256c8-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="256c8-134">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="256c8-135">Нажмите кнопку **Добавить** в правом верхнем углу колонки **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="256c8-136">Щелкните **Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="256c8-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="256c8-137">Введите имя приложения в текстовое поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="256c8-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="256c8-138">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="256c8-138">Select **Add.**</span></span>

<span data-ttu-id="256c8-139">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="256c8-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="256c8-140">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="256c8-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="256c8-141">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="256c8-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="256c8-142">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="256c8-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="256c8-143">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="256c8-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="256c8-144">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="256c8-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="256c8-145">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="256c8-146">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="256c8-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="256c8-147">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="256c8-148">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="256c8-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="256c8-149">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="256c8-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="256c8-150">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="256c8-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="256c8-151">Введите **URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="256c8-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="256c8-152">Это URL-адрес страницы, на которой пользователи вводят имена и пароли для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="256c8-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="256c8-153">Убедитесь, что на странице по этому URL-адресу отображаются поля для ввода учетных данных.</span><span class="sxs-lookup"><span data-stu-id="256c8-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="256c8-154">Назначьте пользователей приложению.</span><span class="sxs-lookup"><span data-stu-id="256c8-154">Assign users to the application.</span></span>

11. <span data-ttu-id="256c8-155">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="256c8-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="256c8-156">Если этого не сделать, пользователям будет предложено самостоятельно ввести учетные данные при первом запуске.</span><span class="sxs-lookup"><span data-stu-id="256c8-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="256c8-157">Назначение приложения пользователю напрямую</span><span class="sxs-lookup"><span data-stu-id="256c8-157">Assign a user to an application directly</span></span>

<span data-ttu-id="256c8-158">Чтобы напрямую назначить одного или нескольких пользователей для приложения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="256c8-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="256c8-159">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="256c8-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="256c8-160">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="256c8-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="256c8-161">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="256c8-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="256c8-162">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="256c8-163">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="256c8-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="256c8-164">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="256c8-165">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="256c8-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="256c8-166">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="256c8-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="256c8-167">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="256c8-168">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="256c8-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="256c8-169">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="256c8-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="256c8-170">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="256c8-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="256c8-171">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="256c8-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="256c8-172">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="256c8-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="256c8-173">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="256c8-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="256c8-174">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="256c8-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="256c8-175">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="256c8-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="256c8-176">Назначение приложения группе напрямую</span><span class="sxs-lookup"><span data-stu-id="256c8-176">Assign an application to a group directly</span></span>

<span data-ttu-id="256c8-177">Чтобы напрямую назначить одну или несколько групп для приложения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="256c8-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="256c8-178">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="256c8-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="256c8-179">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="256c8-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="256c8-180">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="256c8-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="256c8-181">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="256c8-182">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="256c8-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="256c8-183">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="256c8-184">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="256c8-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="256c8-185">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="256c8-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="256c8-186">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="256c8-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="256c8-187">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="256c8-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="256c8-188">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя группы**, которой требуется назначить приложение.</span><span class="sxs-lookup"><span data-stu-id="256c8-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="256c8-189">Наведите указатель мыши на **группу** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="256c8-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="256c8-190">Чтобы добавить группу в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этой группы.</span><span class="sxs-lookup"><span data-stu-id="256c8-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="256c8-191">**Необязательно.** Если вы хотите **добавить более одной группы**, в поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя группы** и установите флажок, чтобы добавить группу в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="256c8-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="256c8-192">Выбрав все группы, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="256c8-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="256c8-193">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным группам.</span><span class="sxs-lookup"><span data-stu-id="256c8-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="256c8-194">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным группам.</span><span class="sxs-lookup"><span data-stu-id="256c8-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="256c8-195">Вскоре выбранные пользователи смогут запускать это приложение через панель доступа.</span><span class="sxs-lookup"><span data-stu-id="256c8-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="256c8-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="256c8-196">Next steps</span></span>
[<span data-ttu-id="256c8-197">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="256c8-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
