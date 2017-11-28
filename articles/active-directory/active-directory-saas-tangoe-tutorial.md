---
title: "Руководство по интеграции Azure Active Directory с Tangoe Command Premium Mobile | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Tangoe Command Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 595541e7248a7486e58123927389c552af0e50f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="df234-103">Учебник. Интеграция Azure Active Directory с Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="df234-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="df234-104">В этом учебнике описано, как интегрировать Tangoe Command Premium Mobile с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df234-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df234-105">Интеграция Tangoe Command Premium Mobile с Azure AD дает приведенные далее преимущества:</span><span class="sxs-lookup"><span data-stu-id="df234-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="df234-106">С помощью Azure AD вы можете контролировать доступ к Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="df234-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
- <span data-ttu-id="df234-107">Вы можете включить автоматический вход пользователей в Tangoe Command Premium Mobile (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df234-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df234-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="df234-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="df234-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df234-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df234-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="df234-110">Prerequisites</span></span>

<span data-ttu-id="df234-111">Чтобы настроить интеграцию Azure AD с Tangoe Command Premium Mobile, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="df234-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

- <span data-ttu-id="df234-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="df234-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df234-113">подписка Tangoe Command Premium Mobile с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="df234-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df234-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="df234-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df234-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="df234-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df234-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="df234-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df234-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df234-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df234-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="df234-118">Scenario description</span></span>
<span data-ttu-id="df234-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="df234-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df234-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="df234-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df234-121">Добавление Tangoe Command Premium Mobile из коллекции.</span><span class="sxs-lookup"><span data-stu-id="df234-121">Add Tangoe Command Premium Mobile from the gallery</span></span>
2. <span data-ttu-id="df234-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df234-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="df234-123">Добавление Tangoe Command Premium Mobile из коллекции</span><span class="sxs-lookup"><span data-stu-id="df234-123">Add Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="df234-124">Чтобы настроить интеграцию Tangoe Command Premium Mobile с Azure AD, необходимо добавить Tangoe Command Premium Mobile из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="df234-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df234-125">**Чтобы добавить Tangoe Command Premium Mobile из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="df234-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df234-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df234-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df234-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="df234-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="df234-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="df234-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="df234-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="df234-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="df234-133">В поле поиска введите **Tangoe Command Premium Mobile**, на панели результатов выберите **Tangoe Command Premium Mobile** и нажмите кнопку **Добавить**, чтобы добавить выбранное приложение.</span><span class="sxs-lookup"><span data-stu-id="df234-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span></span>

    ![<span data-ttu-id="df234-134">Добавление Tangoe Command Premium Mobile из коллекции</span><span class="sxs-lookup"><span data-stu-id="df234-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="df234-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="df234-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="df234-136">В этом разделе описана настройка и проверка единого входа Azure AD в Tangoe Command Premium Mobile с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df234-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df234-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Tangoe Command Premium Mobile соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df234-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="df234-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="df234-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="df234-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="df234-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="df234-140">Чтобы настроить и проверить единый вход Azure AD в Tangoe Command Premium Mobile, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="df234-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df234-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="df234-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df234-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df234-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df234-143">**[Создание тестового пользователя Tangoe Command Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)** требуется для того, чтобы в Tangoe Command Premium Mobile существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df234-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="df234-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df234-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df234-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="df234-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="df234-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="df234-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="df234-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="df234-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="df234-148">**Чтобы настроить единый вход Azure AD в Tangoe Command Premium Mobile, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="df234-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="df234-149">На портале Azure на странице интеграции с приложением **Tangoe Command Premium Mobile** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="df234-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="df234-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="df234-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="df234-153">В разделе **Домены и URL-адреса приложения Tangoe Command Premium Mobile** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="df234-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span></span>

    ![Домены и URL-адреса приложения Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="df234-155">а.</span><span class="sxs-lookup"><span data-stu-id="df234-155">a.</span></span> <span data-ttu-id="df234-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="df234-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="df234-157">b.</span><span class="sxs-lookup"><span data-stu-id="df234-157">b.</span></span> <span data-ttu-id="df234-158">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://sso.tangoe.com/sp/ACS.saml2`.</span><span class="sxs-lookup"><span data-stu-id="df234-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df234-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="df234-159">These values are not real.</span></span> <span data-ttu-id="df234-160">Замените их фактическими значениями URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="df234-160">Update these values with the actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="df234-161">Для получения этих значений обратитесь в [службу поддержки клиентов Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/).</span><span class="sxs-lookup"><span data-stu-id="df234-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to get these values.</span></span> 

4. <span data-ttu-id="df234-162">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="df234-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="df234-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="df234-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="df234-166">В разделе **Настройка Tangoe Command Premium Mobile** щелкните **Настроить Tangoe Command Premium Mobile**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="df234-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="df234-167">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="df234-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Раздел настройки Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="df234-169">Чтобы настроить единый вход для своего приложения, обратитесь в [службу поддержки клиентов Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/) и предоставьте следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="df234-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide the following:</span></span>

   - <span data-ttu-id="df234-170">скачанный файл метаданных;</span><span class="sxs-lookup"><span data-stu-id="df234-170">The downloaded metadata file</span></span>
   - <span data-ttu-id="df234-171">**идентификатор сущности SAML**;</span><span class="sxs-lookup"><span data-stu-id="df234-171">The **SAML Entity ID**</span></span>
   - <span data-ttu-id="df234-172">**URL-адрес службы единого входа SAML**;</span><span class="sxs-lookup"><span data-stu-id="df234-172">The **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="df234-173">**URL-адрес выхода**.</span><span class="sxs-lookup"><span data-stu-id="df234-173">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="df234-174">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="df234-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="df234-175">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="df234-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="df234-176">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="df234-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="df234-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="df234-177">Create an Azure AD test user</span></span>
<span data-ttu-id="df234-178">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df234-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="df234-180">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="df234-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df234-181">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df234-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df234-183">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="df234-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Выберите "Пользователи и группы" > "Все пользователи".](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df234-185">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="df234-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Добавить пользователя](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df234-187">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="df234-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df234-189">а.</span><span class="sxs-lookup"><span data-stu-id="df234-189">a.</span></span> <span data-ttu-id="df234-190">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df234-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df234-191">b.</span><span class="sxs-lookup"><span data-stu-id="df234-191">b.</span></span> <span data-ttu-id="df234-192">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df234-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df234-193">c.</span><span class="sxs-lookup"><span data-stu-id="df234-193">c.</span></span> <span data-ttu-id="df234-194">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="df234-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="df234-195">d.</span><span class="sxs-lookup"><span data-stu-id="df234-195">d.</span></span> <span data-ttu-id="df234-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="df234-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="df234-197">Создание тестового пользователя Tangoe Command Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="df234-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="df234-198">В этом разделе мы создадим пользователя Britta Simon в приложении Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="df234-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="df234-199">Перед выполнением единого входа все пользователи должны быть подготовлены в приложении Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="df234-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="df234-200">Для этого обратитесь в [службу поддержки клиентов Tangoe Command Premium Mobile](https://www.tangoe.com/contact-2/).</span><span class="sxs-lookup"><span data-stu-id="df234-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to provision all these users into the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="df234-201">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="df234-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="df234-202">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="df234-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="df234-204">**Чтобы назначить пользователя Britta Simon приложению Tangoe Command Premium Mobile, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="df234-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="df234-205">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="df234-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="df234-207">В списке приложений выберите **Tangoe Command Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="df234-207">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe Command Premium Mobile в списке приложений](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="df234-209">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="df234-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="df234-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="df234-211">Click **Add** button.</span></span> <span data-ttu-id="df234-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="df234-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="df234-214">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="df234-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="df234-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="df234-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df234-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="df234-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="df234-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="df234-217">Test single sign-on</span></span>

<span data-ttu-id="df234-218">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="df234-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="df234-219">Щелкнув элемент Tangoe Command Premium Mobile, вы автоматически войдете в приложение Tangoe Command Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="df234-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="df234-220">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="df234-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="df234-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="df234-221">Additional resources</span></span>

* [<span data-ttu-id="df234-222">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df234-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df234-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df234-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

