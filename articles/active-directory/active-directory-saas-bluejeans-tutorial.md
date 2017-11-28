---
title: "Руководство по интеграции Azure Active Directory с BlueJeans | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 03bf65852b8d3cf14aebf155891a028db86e78d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="87da4-103">Руководство по интеграции Azure Active Directory с BlueJeans</span><span class="sxs-lookup"><span data-stu-id="87da4-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="87da4-104">В этом руководстве описано, как интегрировать BlueJeans с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87da4-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87da4-105">Интеграция Azure AD с приложением BlueJeans обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="87da4-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="87da4-106">С помощью Azure AD вы можете контролировать доступ к BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="87da4-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="87da4-107">Вы можете включить автоматический вход пользователей в BlueJeans (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87da4-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87da4-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="87da4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="87da4-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87da4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87da4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="87da4-110">Prerequisites</span></span>

<span data-ttu-id="87da4-111">Чтобы настроить интеграцию Azure AD с BlueJeans, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="87da4-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="87da4-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="87da4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87da4-113">подписка BlueJeans с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="87da4-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87da4-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="87da4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87da4-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="87da4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87da4-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="87da4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87da4-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87da4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87da4-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="87da4-118">Scenario description</span></span>
<span data-ttu-id="87da4-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="87da4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87da4-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="87da4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87da4-121">Добавление BlueJeans из коллекции</span><span class="sxs-lookup"><span data-stu-id="87da4-121">Adding BlueJeans from the gallery</span></span>
2. <span data-ttu-id="87da4-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="87da4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="87da4-123">Добавление BlueJeans из коллекции</span><span class="sxs-lookup"><span data-stu-id="87da4-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="87da4-124">Чтобы настроить интеграцию BlueJeans с Azure AD, необходимо добавить BlueJeans из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="87da4-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87da4-125">**Чтобы добавить BlueJeans из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="87da4-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87da4-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87da4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="87da4-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="87da4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="87da4-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="87da4-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="87da4-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="87da4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="87da4-133">В поле поиска введите **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="87da4-133">In the search box, type **BlueJeans**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="87da4-135">На панели результатов выберите **BlueJeans** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="87da4-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87da4-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="87da4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87da4-138">В этом разделе описана настройка и проверка единого входа Azure AD в BlueJeans с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87da4-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="87da4-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в BlueJeans соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87da4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="87da4-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="87da4-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="87da4-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="87da4-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="87da4-142">Чтобы настроить и проверить единый вход Azure AD в BlueJeans, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="87da4-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87da4-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="87da4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="87da4-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87da4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87da4-145">**[Создание тестового пользователя BlueJeans](#creating-a-bluejeans-test-user)** нужно для того, чтобы в BlueJeans также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87da4-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="87da4-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87da4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87da4-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="87da4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87da4-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="87da4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="87da4-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="87da4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="87da4-150">**Чтобы настроить единый вход Azure AD в BlueJeans, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="87da4-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="87da4-151">На портале Azure на странице интеграции с приложением **BlueJeans** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="87da4-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="87da4-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="87da4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="87da4-155">В разделе **Домены и URL-адреса приложения BlueJeans** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="87da4-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="87da4-157">а.</span><span class="sxs-lookup"><span data-stu-id="87da4-157">a.</span></span> <span data-ttu-id="87da4-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="87da4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="87da4-159">b.</span><span class="sxs-lookup"><span data-stu-id="87da4-159">b.</span></span> <span data-ttu-id="87da4-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="87da4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="87da4-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="87da4-161">These values are not real.</span></span> <span data-ttu-id="87da4-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="87da4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="87da4-163">Чтобы получить эти значения, обратитесь к [группе поддержки BlueJeans](https://support.bluejeans.com/contact).</span><span class="sxs-lookup"><span data-stu-id="87da4-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="87da4-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="87da4-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="87da4-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="87da4-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="87da4-168">В разделе **Настройка BlueJeans** щелкните **Настроить BlueJeans**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="87da4-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="87da4-169">Скопируйте **URL-адрес выхода, URL-адрес изменения пароля и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="87da4-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="87da4-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт **BlueJeans** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="87da4-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="87da4-172">Последовательно щелкните **Admin \> Group Settings \> Security** (Администратор > Параметры группы > Безопасность).</span><span class="sxs-lookup"><span data-stu-id="87da4-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="87da4-173">![Администратор](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="87da4-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="87da4-174">В разделе **Security** (Безопасность) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="87da4-174">In the **Security** section, perform the following steps:</span></span>
   
   <span data-ttu-id="87da4-175">![Единый вход SAML](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "Единый вход SAML")</span><span class="sxs-lookup"><span data-stu-id="87da4-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="87da4-176">а.</span><span class="sxs-lookup"><span data-stu-id="87da4-176">a.</span></span> <span data-ttu-id="87da4-177">Выберите параметр **SAML Single Sign On**(Единый вход SAML).</span><span class="sxs-lookup"><span data-stu-id="87da4-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="87da4-178">b.</span><span class="sxs-lookup"><span data-stu-id="87da4-178">b.</span></span> <span data-ttu-id="87da4-179">Установите флажок **Enable automatic provisioning**(Включить автоматическую подготовку).</span><span class="sxs-lookup"><span data-stu-id="87da4-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="87da4-180">После этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="87da4-180">Move on with the following steps:</span></span>

    <span data-ttu-id="87da4-181">![Путь к сертификату](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Путь к сертификату")</span><span class="sxs-lookup"><span data-stu-id="87da4-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="87da4-182">а.</span><span class="sxs-lookup"><span data-stu-id="87da4-182">a.</span></span> <span data-ttu-id="87da4-183">Нажмите кнопку **Choose File**(Выбрать файл) и отправьте скачанный сертификат.</span><span class="sxs-lookup"><span data-stu-id="87da4-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>
   
    <span data-ttu-id="87da4-184">b.</span><span class="sxs-lookup"><span data-stu-id="87da4-184">b.</span></span> <span data-ttu-id="87da4-185">Вставьте **URL-адрес службы единого входа SAML** в текстовое поле **Login URL** (URL-адрес входа).</span><span class="sxs-lookup"><span data-stu-id="87da4-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="87da4-186">c.</span><span class="sxs-lookup"><span data-stu-id="87da4-186">c.</span></span> <span data-ttu-id="87da4-187">Вставьте **URL-адрес изменения пароля** в текстовое поле **Password Change URL** (URL-адрес изменения пароля).</span><span class="sxs-lookup"><span data-stu-id="87da4-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="87da4-188">г)</span><span class="sxs-lookup"><span data-stu-id="87da4-188">d.</span></span> <span data-ttu-id="87da4-189">Вставьте **URL-адрес выхода** в текстовое поле **Logout URL** (URL-адрес выхода).</span><span class="sxs-lookup"><span data-stu-id="87da4-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

11. <span data-ttu-id="87da4-190">После этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="87da4-190">Move on with the following steps:</span></span>
    
    <span data-ttu-id="87da4-191">![Сохранение изменений](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Сохранение изменений")</span><span class="sxs-lookup"><span data-stu-id="87da4-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="87da4-192">а.</span><span class="sxs-lookup"><span data-stu-id="87da4-192">a.</span></span> <span data-ttu-id="87da4-193">В текстовое поле **User id** (Идентификатор пользователя) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="87da4-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="87da4-194">b.</span><span class="sxs-lookup"><span data-stu-id="87da4-194">b.</span></span> <span data-ttu-id="87da4-195">В текстовое поле **Email** (Электронная почта) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="87da4-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="87da4-196">c.</span><span class="sxs-lookup"><span data-stu-id="87da4-196">c.</span></span> <span data-ttu-id="87da4-197">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="87da4-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="87da4-198">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="87da4-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="87da4-199">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="87da4-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="87da4-200">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="87da4-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87da4-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="87da4-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="87da4-202">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87da4-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="87da4-204">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="87da4-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87da4-205">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87da4-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87da4-207">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="87da4-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87da4-209">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="87da4-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87da4-211">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="87da4-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87da4-213">а.</span><span class="sxs-lookup"><span data-stu-id="87da4-213">a.</span></span> <span data-ttu-id="87da4-214">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87da4-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87da4-215">b.</span><span class="sxs-lookup"><span data-stu-id="87da4-215">b.</span></span> <span data-ttu-id="87da4-216">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87da4-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87da4-217">c.</span><span class="sxs-lookup"><span data-stu-id="87da4-217">c.</span></span> <span data-ttu-id="87da4-218">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="87da4-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="87da4-219">d.</span><span class="sxs-lookup"><span data-stu-id="87da4-219">d.</span></span> <span data-ttu-id="87da4-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="87da4-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="87da4-221">Создание тестового пользователя BlueJeans</span><span class="sxs-lookup"><span data-stu-id="87da4-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="87da4-222">Чтобы пользователи Azure AD могли выполнять вход в BlueJeans, они должны быть подготовлены в BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="87da4-222">To enable Azure AD users to log in to BlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="87da4-223">В случае BlueJeans подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="87da4-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="87da4-224">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="87da4-224">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="87da4-225">Выполните вход на веб-сайт компании **BlueJeans** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="87da4-225">Log in to your **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="87da4-226">Последовательно выберите пункты **Admin \> Manage Users \> Add User** (Администратор > Управление пользователями > Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="87da4-226">Go to **ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="87da4-227">![Администратор](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="87da4-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="87da4-228">Вкладка **Add User** (Добавить пользователя) доступна, только если на вкладке **Security** (Безопасность) снят флажок **Enable automatic provisioning** (Включить автоматическую подготовку).</span><span class="sxs-lookup"><span data-stu-id="87da4-228">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="87da4-229">В разделе **Add User** (Добавление пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="87da4-229">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="87da4-230">![Добавление пользователя](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="87da4-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="87da4-231">а.</span><span class="sxs-lookup"><span data-stu-id="87da4-231">a.</span></span> <span data-ttu-id="87da4-232">Введите в текстовых полях **BlueJeans Username** (Имя пользователя BlueJeans), **Email address** (Адрес электронной почты), **BlueJeans Meeting ID** (Идентификатор собрания BlueJeans), **Moderator Passcode** (Секретный код модератора), **Full Name** (Полное имя) и **Company** (Компания) соответствующие данные действующей учетной записи AAD, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="87da4-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>
    
    <span data-ttu-id="87da4-233">b.</span><span class="sxs-lookup"><span data-stu-id="87da4-233">b.</span></span> <span data-ttu-id="87da4-234">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="87da4-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="87da4-235">Вы можете использовать любые другие средства создания учетной записи пользователя BlueJeans или API, предоставляемые BlueJeans для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="87da4-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="87da4-236">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="87da4-236">Assigning the Azure AD test user</span></span>

<span data-ttu-id="87da4-237">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="87da4-237">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="87da4-239">**Чтобы назначить пользователя Britta Simon в BlueJeans, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="87da4-239">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="87da4-240">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="87da4-240">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="87da4-242">Из списка приложений выберите **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="87da4-242">In the applications list, select **BlueJeans**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="87da4-244">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="87da4-244">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="87da4-246">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="87da4-246">Click **Add** button.</span></span> <span data-ttu-id="87da4-247">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="87da4-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="87da4-249">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="87da4-249">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="87da4-250">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="87da4-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87da4-251">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="87da4-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="87da4-252">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="87da4-252">Testing single sign-on</span></span>

<span data-ttu-id="87da4-253">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="87da4-253">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="87da4-254">Когда вы щелкните элемент "BlueJeans" на панели доступа, должна появиться страница входа в приложение BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="87da4-254">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="87da4-255">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87da4-255">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="87da4-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="87da4-256">Additional resources</span></span>

* [<span data-ttu-id="87da4-257">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87da4-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87da4-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87da4-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

