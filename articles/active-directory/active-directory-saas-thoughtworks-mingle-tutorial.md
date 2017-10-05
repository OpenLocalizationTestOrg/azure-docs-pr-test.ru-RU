---
title: "Руководство по интеграции Azure Active Directory с Thoughtworks Mingle | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="c7642-103">Учебник. Интеграция Azure Active Directory с Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="c7642-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="c7642-104">В этом руководстве описано, как интегрировать Thoughtworks Mingle с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7642-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7642-105">Интеграция Azure AD с Thoughtworks Mingle обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="c7642-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7642-106">С помощью Azure AD вы можете контролировать доступ к Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="c7642-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="c7642-107">Вы можете включить автоматический вход пользователей в Thoughtworks Mingle (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7642-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7642-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c7642-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7642-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7642-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7642-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7642-110">Prerequisites</span></span>

<span data-ttu-id="c7642-111">Чтобы настроить интеграцию Azure AD с Thoughtworks Mingle, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c7642-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="c7642-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c7642-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7642-113">подписка Thoughtworks Mingle с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c7642-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7642-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c7642-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7642-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c7642-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7642-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c7642-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7642-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7642-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7642-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c7642-118">Scenario description</span></span>
<span data-ttu-id="c7642-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c7642-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7642-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c7642-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7642-121">Добавление Thoughtworks Mingle из коллекции</span><span class="sxs-lookup"><span data-stu-id="c7642-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="c7642-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7642-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="c7642-123">Добавление Thoughtworks Mingle из коллекции</span><span class="sxs-lookup"><span data-stu-id="c7642-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="c7642-124">Чтобы настроить интеграцию Thoughtworks Mingle с Azure AD, необходимо добавить Thoughtworks Mingle из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c7642-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7642-125">**Чтобы добавить Thoughtworks Mingle из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c7642-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7642-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7642-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="c7642-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7642-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7642-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7642-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="c7642-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c7642-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="c7642-133">В поле поиска введите **Thoughtworks Mingle**, выберите **Thoughtworks Mingle** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="c7642-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![ThoughtWorks Mingle в списке результатов](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c7642-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7642-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c7642-136">В этом разделе описана настройка и проверка единого входа Azure AD в Thoughtworks Mingle с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7642-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c7642-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Thoughtworks Mingle соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7642-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="c7642-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="c7642-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="c7642-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="c7642-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c7642-140">Чтобы настроить и проверить единый вход Azure AD в Thoughtworks Mingle, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="c7642-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7642-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c7642-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7642-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7642-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7642-143">**[Создание тестового пользователя Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)** требуется для того, чтобы в Thoughtworks Mingle существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7642-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7642-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7642-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7642-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c7642-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c7642-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7642-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c7642-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="c7642-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="c7642-148">**Чтобы настроить единый вход Azure AD в Thoughtworks Mingle, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c7642-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="c7642-149">На портале Azure на странице интеграции с приложением **Thoughtworks Mingle** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c7642-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c7642-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c7642-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="c7642-153">В разделе **Домены и URL-адреса приложения Thoughtworks Mingle** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c7642-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="c7642-155">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="c7642-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7642-156">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="c7642-156">The value is not real.</span></span> <span data-ttu-id="c7642-157">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="c7642-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="c7642-158">Чтобы получить это значение, обратитесь в [службу поддержки клиентов Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support).</span><span class="sxs-lookup"><span data-stu-id="c7642-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="c7642-159">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c7642-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="c7642-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c7642-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7642-163">Войдите на корпоративный веб-сайт **Thoughtworks Mingle** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c7642-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="c7642-164">Откройте вкладку **Admin** (Администратор), а затем щелкните **SSO Config** (Конфигурация единого входа).</span><span class="sxs-lookup"><span data-stu-id="c7642-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="c7642-165">![Вкладка Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c7642-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="c7642-166">В разделе **Конфигурация единого входа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c7642-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c7642-167">![Настройка единого входа](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="c7642-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="c7642-168">а.</span><span class="sxs-lookup"><span data-stu-id="c7642-168">a.</span></span> <span data-ttu-id="c7642-169">Чтобы отправить файл метаданных, нажмите кнопку **Выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="c7642-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="c7642-170">b.</span><span class="sxs-lookup"><span data-stu-id="c7642-170">b.</span></span> <span data-ttu-id="c7642-171">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="c7642-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c7642-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c7642-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7642-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c7642-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7642-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c7642-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c7642-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7642-175">Create an Azure AD test user</span></span>
<span data-ttu-id="c7642-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7642-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="c7642-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c7642-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7642-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7642-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7642-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c7642-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7642-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7642-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7642-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c7642-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7642-187">а.</span><span class="sxs-lookup"><span data-stu-id="c7642-187">a.</span></span> <span data-ttu-id="c7642-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7642-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7642-189">b.</span><span class="sxs-lookup"><span data-stu-id="c7642-189">b.</span></span> <span data-ttu-id="c7642-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7642-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7642-191">c.</span><span class="sxs-lookup"><span data-stu-id="c7642-191">c.</span></span> <span data-ttu-id="c7642-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c7642-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7642-193">d.</span><span class="sxs-lookup"><span data-stu-id="c7642-193">d.</span></span> <span data-ttu-id="c7642-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c7642-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="c7642-195">Создание тестового пользователя Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="c7642-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="c7642-196">Чтобы пользователи AAD могли войти систему, их необходимо подготовить для приложения Thoughtworks Mingle, используя их имена пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c7642-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="c7642-197">В случае с Thoughtworks Mingle подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="c7642-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="c7642-198">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c7642-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="c7642-199">Войдите на корпоративный веб-сайт Thoughtworks Mingle в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c7642-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="c7642-200">Щелкните **Профиль**.</span><span class="sxs-lookup"><span data-stu-id="c7642-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="c7642-201">![Ваш первый проект](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Ваш первый проект")</span><span class="sxs-lookup"><span data-stu-id="c7642-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="c7642-202">Откройте вкладку **Admin** (Администратор), а затем щелкните **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="c7642-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="c7642-203">![Пользователи](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="c7642-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="c7642-204">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="c7642-204">Click **New User**.</span></span>
   
    <span data-ttu-id="c7642-205">![Новый пользователь](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="c7642-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="c7642-206">На странице диалогового окна **Новый пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c7642-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="c7642-207">![Диалоговое окно нового пользователя](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="c7642-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="c7642-208">а.</span><span class="sxs-lookup"><span data-stu-id="c7642-208">a.</span></span> <span data-ttu-id="c7642-209">Введите в текстовые поля **Sign-in name** (Учетное имя), **Display name** (Отображаемое имя), **Choose password** (Выберите пароль) и **Confirm password** (Подтвердите пароль) соответствующие данные действующей учетной записи Azure AD, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="c7642-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="c7642-210">b.</span><span class="sxs-lookup"><span data-stu-id="c7642-210">b.</span></span> <span data-ttu-id="c7642-211">В поле **User type** (Тип пользователя) выберите значение **Full user** (С полным доступом).</span><span class="sxs-lookup"><span data-stu-id="c7642-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="c7642-212">c.</span><span class="sxs-lookup"><span data-stu-id="c7642-212">c.</span></span> <span data-ttu-id="c7642-213">Щелкните **Создать этот профиль**.</span><span class="sxs-lookup"><span data-stu-id="c7642-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="c7642-214">Вы можете использовать любые другие инструменты создания учетных записей пользователя Thoughtworks Mingle или API-интерфейсы, предоставляемые Thoughtworks Mingle для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="c7642-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c7642-215">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7642-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="c7642-216">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Thoughtworks Mingle, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="c7642-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="c7642-218">**Чтобы назначить пользователя Britta Simon в Thoughtworks Mingle, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="c7642-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="c7642-219">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7642-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c7642-221">В списке приложений выберите **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="c7642-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![Ссылка на Thoughtworks Mingle в списке "Приложения"](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="c7642-223">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c7642-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="c7642-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7642-225">Click **Add** button.</span></span> <span data-ttu-id="c7642-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c7642-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="c7642-228">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c7642-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7642-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c7642-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7642-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c7642-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c7642-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c7642-231">Test single sign-on</span></span>

<span data-ttu-id="c7642-232">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c7642-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7642-233">Щелкнув элемент Thoughtworks Mingle на панели доступа, вы автоматически войдете в приложение Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="c7642-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7642-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c7642-234">Additional resources</span></span>

* [<span data-ttu-id="c7642-235">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7642-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7642-236">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7642-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

