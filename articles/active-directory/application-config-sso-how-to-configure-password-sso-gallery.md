---
title: "Как настроить единый вход по паролю для приложения из коллекции Azure AD | Документация Майкрософт"
description: "Как настроить приложение для защищенного единого входа на основе паролей, если оно указано в коллекции приложений Azure AD"
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
ms.openlocfilehash: d4dc110eb25c3e550ac4663d28e626a696b58f62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="d1069-103">Настройка единого входа по паролю для приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1069-103">How to configure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="d1069-104">При добавлении приложения из [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery) вы можете выбрать для него способ входа пользователей.</span><span class="sxs-lookup"><span data-stu-id="d1069-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span></span> <span data-ttu-id="d1069-105">Этот способ можно настроить в любое время, выбрав элемент навигации **Единый вход** в корпоративном приложении на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d1069-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="d1069-106">Один из доступных методов единого входа — это [Единый вход на основе пароля](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="d1069-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="d1069-107">Это отличный способ для быстрой интеграции приложений в Azure AD. Он предоставляет следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="d1069-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="d1069-108">Использование **единого входа для пользователей** путем безопасного хранения и воспроизведения имен пользователей и паролей для приложений, интегрированных с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1069-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="d1069-109">**Поддержка приложений, использующих несколько полей ввода учетных данных** помимо обычных имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="d1069-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="d1069-110">**Настройка меток** для полей ввода имени пользователя и пароля, которые будут отображаться при вводе учетных данных на [панели доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).</span><span class="sxs-lookup"><span data-stu-id="d1069-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="d1069-111">**Пользователи** могут использовать имена пользователей и пароли для любых существующих учетных записей при вводе вручную в [панели доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).</span><span class="sxs-lookup"><span data-stu-id="d1069-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="d1069-112">**Члены бизнес-группы** могут назначать пользователям имена для входа и пароли, используя функцию [самостоятельной настройки доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access).</span><span class="sxs-lookup"><span data-stu-id="d1069-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="d1069-113">**Администратор** может назначать пользователям имена для входа и пароли, используя функцию обновления учетных данных при [назначении пользователей приложениям](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="d1069-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="d1069-114">**Администратор** может назначать группам людей совместно используемые имена для входа и пароли, используя функцию обновления учетных данных при [назначении групп приложениям](#assign-an-application-to-a-group-directly).</span><span class="sxs-lookup"><span data-stu-id="d1069-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="d1069-115">Ниже представлены сведения о том, как включить [единый вход по паролю](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) для приложения, которое уже находится в [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="d1069-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="d1069-116">Обзор необходимых действий</span><span class="sxs-lookup"><span data-stu-id="d1069-116">Overview of steps required</span></span>
<span data-ttu-id="d1069-117">Чтобы настроить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d1069-117">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="d1069-118">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1069-118">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   <span data-ttu-id="d1069-119">[Настройте приложение для единого входа на основе пароля](#configure-the-application-for-password-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d1069-119">[Configure the application for password single sign-on](#configure-the-application-for-password-single-sign-on)</span></span>

-   <span data-ttu-id="d1069-120">[назначьте приложение пользователю или группе](#assign-the-application-to-a-user-or-a-group);</span><span class="sxs-lookup"><span data-stu-id="d1069-120">[Assign the application to a user or a group](#assign-the-application-to-a-user-or-a-group)</span></span>

    -   <span data-ttu-id="d1069-121">[назначьте приложение пользователю напрямую](#assign-a-user-to-an-application-directly);</span><span class="sxs-lookup"><span data-stu-id="d1069-121">[Assign a user to an application directly](#assign-a-user-to-an-application-directly)</span></span>

    -   <span data-ttu-id="d1069-122">[Назначьте приложение группе напрямую](#assign-an-application-to-a-group-directly).</span><span class="sxs-lookup"><span data-stu-id="d1069-122">[Assign an application to a group directly](#assign-an-application-to-a-group-directly)</span></span>

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="d1069-123">Добавление приложения из коллекции Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1069-123">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="d1069-124">Чтобы добавить приложение из коллекции Azure AD, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d1069-124">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="d1069-125">Откройте [портал Azure](https://portal.azure.com) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="d1069-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="d1069-126">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d1069-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1069-127">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1069-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1069-128">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d1069-129">В правом верхнем углу колонки **Корпоративные приложения** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d1069-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="d1069-130">В разделе **Добавить из коллекции** в текстовом поле **Введите имя** введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="d1069-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="d1069-131">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="d1069-131">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="d1069-132">Перед добавлением приложения можно изменить его имя в текстовом поле **Имя**.</span><span class="sxs-lookup"><span data-stu-id="d1069-132">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="d1069-133">Нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="d1069-133">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="d1069-134">Через некоторое время появится колонка настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d1069-134">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="d1069-135">Настройка приложения для единого входа на основе пароля</span><span class="sxs-lookup"><span data-stu-id="d1069-135">Configure the application for password single sign-on</span></span>

<span data-ttu-id="d1069-136">Чтобы настроить единый вход для приложения, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d1069-136">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="d1069-137">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="d1069-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d1069-138">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d1069-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1069-139">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1069-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1069-140">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d1069-141">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="d1069-141">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="d1069-142">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d1069-143">Выберите приложение, для которого нужно настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="d1069-143">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="d1069-144">После загрузки приложения выберите пункт **Единый вход** в левом меню навигации этого приложения.</span><span class="sxs-lookup"><span data-stu-id="d1069-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d1069-145">Выберите режим **Вход по паролю**.</span><span class="sxs-lookup"><span data-stu-id="d1069-145">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="d1069-146">[Назначьте пользователей приложению](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="d1069-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="d1069-147">Кроме того, можно также предоставить учетные данные от имени пользователя, выбрав строки пользователей, щелкнув **Обновить учетные данные** и введя имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="d1069-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="d1069-148">Если этого не сделать, пользователям будет предложено самостоятельно ввести учетные данные при первом запуске.</span><span class="sxs-lookup"><span data-stu-id="d1069-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="d1069-149">Назначение приложения пользователю напрямую</span><span class="sxs-lookup"><span data-stu-id="d1069-149">Assign a user to an application directly</span></span>

<span data-ttu-id="d1069-150">Чтобы напрямую назначить одного или нескольких пользователей для приложения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d1069-150">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="d1069-151">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d1069-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d1069-152">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d1069-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1069-153">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1069-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1069-154">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d1069-155">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="d1069-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="d1069-156">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d1069-157">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="d1069-157">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="d1069-158">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d1069-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d1069-159">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d1069-160">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d1069-160">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d1069-161">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** пользователя, которого требуется назначить.</span><span class="sxs-lookup"><span data-stu-id="d1069-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d1069-162">Наведите указатель мыши на **пользователя** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="d1069-162">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="d1069-163">Чтобы добавить пользователя в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этого пользователя.</span><span class="sxs-lookup"><span data-stu-id="d1069-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="d1069-164">**Необязательно.** Если вы хотите **добавить более одного пользователя**, в поле **Поиск по имени или адресу электронной почты** введите **полное имя** или **адрес электронной почты** другого пользователя и установите флажок, чтобы добавить этого пользователя в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="d1069-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="d1069-165">Выбрав всех пользователей, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="d1069-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="d1069-166">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="d1069-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="d1069-167">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным пользователям.</span><span class="sxs-lookup"><span data-stu-id="d1069-167">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="d1069-168">Назначение приложения группе напрямую</span><span class="sxs-lookup"><span data-stu-id="d1069-168">Assign an application to a group directly</span></span>

<span data-ttu-id="d1069-169">Чтобы напрямую назначить одну или несколько групп для приложения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d1069-169">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="d1069-170">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="d1069-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d1069-171">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="d1069-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d1069-172">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1069-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d1069-173">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d1069-174">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="d1069-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="d1069-175">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="d1069-176">Выберите из списка приложение, которое необходимо назначить пользователю.</span><span class="sxs-lookup"><span data-stu-id="d1069-176">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="d1069-177">После загрузки приложения в меню навигации слева щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d1069-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d1069-178">В верхней части списка **Пользователи и группы** щелкните **Добавить**, чтобы открыть колонку **Добавление назначения**.</span><span class="sxs-lookup"><span data-stu-id="d1069-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d1069-179">В колонке **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d1069-179">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d1069-180">В поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя группы**, которой требуется назначить приложение.</span><span class="sxs-lookup"><span data-stu-id="d1069-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d1069-181">Наведите указатель мыши на **группу** в списке, чтобы отобразить **флажок**.</span><span class="sxs-lookup"><span data-stu-id="d1069-181">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="d1069-182">Чтобы добавить группу в список **Выбрано**, установите флажок рядом с фотографией или логотипом профиля этой группы.</span><span class="sxs-lookup"><span data-stu-id="d1069-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="d1069-183">**Необязательно.** Если вы хотите **добавить более одной группы**, в поле поиска **Поиск по имени или адресу электронной почты** введите **полное имя группы** и установите флажок, чтобы добавить группу в список **Выбрано**.</span><span class="sxs-lookup"><span data-stu-id="d1069-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="d1069-184">Выбрав все группы, щелкните **Выбрать**, чтобы добавить их в список пользователей и групп, которые будут назначены для приложения.</span><span class="sxs-lookup"><span data-stu-id="d1069-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="d1069-185">**Необязательно.** В колонке **Добавление назначения** щелкните **Выбор роли**, чтобы выбрать роль, которая будет назначена выбранным группам.</span><span class="sxs-lookup"><span data-stu-id="d1069-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="d1069-186">Нажмите кнопку **Назначить**, чтобы назначить приложение выбранным группам.</span><span class="sxs-lookup"><span data-stu-id="d1069-186">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="d1069-187">Вскоре выбранные пользователи смогут запускать это приложение через панель доступа.</span><span class="sxs-lookup"><span data-stu-id="d1069-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1069-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1069-188">Next steps</span></span>
[<span data-ttu-id="d1069-189">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="d1069-189">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
