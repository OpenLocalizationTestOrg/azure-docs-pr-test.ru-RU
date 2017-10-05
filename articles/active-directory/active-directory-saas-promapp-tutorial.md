---
title: "Руководство по интеграции Azure Active Directory с Promapp | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 27013ca9724cf2f57fc85f5f4ccb71921ca57a3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="c1436-103">Руководство по интеграции Azure Active Directory с Promapp</span><span class="sxs-lookup"><span data-stu-id="c1436-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="c1436-104">В этом руководстве описано, как интегрировать Promapp с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c1436-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1436-105">Интеграция Azure AD с приложением Promapp обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="c1436-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c1436-106">С помощью Azure AD вы можете контролировать доступ к Promapp.</span><span class="sxs-lookup"><span data-stu-id="c1436-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="c1436-107">Вы можете включить автоматический вход пользователей в Promapp (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1436-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1436-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c1436-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c1436-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1436-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1436-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c1436-110">Prerequisites</span></span>

<span data-ttu-id="c1436-111">Чтобы настроить интеграцию Azure AD с Promapp, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c1436-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="c1436-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c1436-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1436-113">подписка Promapp с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c1436-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1436-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c1436-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1436-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c1436-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1436-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c1436-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1436-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1436-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1436-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c1436-118">Scenario description</span></span>
<span data-ttu-id="c1436-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c1436-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1436-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c1436-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1436-121">Добавление Promapp из коллекции</span><span class="sxs-lookup"><span data-stu-id="c1436-121">Adding Promapp from the gallery</span></span>
2. <span data-ttu-id="c1436-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1436-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="c1436-123">Добавление Promapp из коллекции</span><span class="sxs-lookup"><span data-stu-id="c1436-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="c1436-124">Чтобы настроить интеграцию Promapp с Azure AD, необходимо добавить Promapp из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c1436-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c1436-125">**Чтобы добавить Promapp из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c1436-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c1436-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1436-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1436-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c1436-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c1436-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c1436-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c1436-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c1436-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c1436-133">В поле поиска введите **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="c1436-133">In the search box, type **Promapp**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="c1436-135">На панели результатов выберите **Promapp** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="c1436-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1436-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1436-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1436-138">В этом разделе описана настройка и проверка единого входа Azure AD в Promapp с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1436-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1436-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Promapp соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1436-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="c1436-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Promapp.</span><span class="sxs-lookup"><span data-stu-id="c1436-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="c1436-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Promapp.</span><span class="sxs-lookup"><span data-stu-id="c1436-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c1436-142">Чтобы настроить и проверить единый вход Azure AD в Promapp, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="c1436-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c1436-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c1436-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c1436-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1436-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1436-145">**[Создание тестового пользователя Promapp](#creating-a-promapp-test-user)** требуется для того, чтобы в Promapp существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1436-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1436-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c1436-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1436-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c1436-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1436-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1436-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1436-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Promapp.</span><span class="sxs-lookup"><span data-stu-id="c1436-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="c1436-150">**Чтобы настроить единый вход Azure AD в Promapp, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c1436-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="c1436-151">На портале Azure на странице интеграции с приложением **Promapp** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c1436-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c1436-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c1436-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="c1436-155">В разделе **Домены и URL-адреса приложения Promapp** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="c1436-155">On the **Promapp Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="c1436-157">а.</span><span class="sxs-lookup"><span data-stu-id="c1436-157">a.</span></span> <span data-ttu-id="c1436-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="c1436-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="c1436-159">b.</span><span class="sxs-lookup"><span data-stu-id="c1436-159">b.</span></span> <span data-ttu-id="c1436-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="c1436-160">In the **Identifier** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c1436-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c1436-161">These values are not real.</span></span> <span data-ttu-id="c1436-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="c1436-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c1436-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Promapp](https://www.promapp.com/about-us/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="c1436-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="c1436-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c1436-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="c1436-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c1436-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c1436-168">В разделе **Конфигурация Promapp** щелкните **Настроить Promapp**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c1436-168">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c1436-169">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="c1436-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="c1436-171">Войдите на корпоративный сайт Promapp с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="c1436-171">Sign-on to your Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="c1436-172">В верхнем меню щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="c1436-172">In the menu on the top, click **Admin**.</span></span> 
   
    ![Единый вход в Azure AD][12]

9. <span data-ttu-id="c1436-174">Нажмите **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="c1436-174">Click **Configure**.</span></span> 
   
    ![Единый вход в Azure AD][13]

10. <span data-ttu-id="c1436-176">В диалоговом окне **Security** (Безопасность) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="c1436-176">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Единый вход в Azure AD][14]
    
    <span data-ttu-id="c1436-178">а.</span><span class="sxs-lookup"><span data-stu-id="c1436-178">a.</span></span> <span data-ttu-id="c1436-179">В текстовое поле **IdP Login URL** (URL-адрес входа IdP) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c1436-179">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="c1436-180">b.</span><span class="sxs-lookup"><span data-stu-id="c1436-180">b.</span></span> <span data-ttu-id="c1436-181">В поле **SSO - Single Sign-on Mode** (SSO — режим единого входа) выберите **Optional** (Необязательно), а затем нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="c1436-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="c1436-182">c.</span><span class="sxs-lookup"><span data-stu-id="c1436-182">c.</span></span> <span data-ttu-id="c1436-183">Откройте скачанный сертификат в блокноте, скопируйте содержимое сертификата без первой строки (-----BEGIN CERTIFICATE-----) и последней строки (-----END CERTIFICATE-----), вставьте его в текстовое поле **SSO-x.509 Certificate** (Сертификат единого входа x.509) и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="c1436-183">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----BEGIN CERTIFICATE-----) and the last line (-----END CERTIFICATE-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="c1436-184">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c1436-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c1436-185">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c1436-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c1436-186">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c1436-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1436-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1436-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1436-188">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1436-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c1436-190">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c1436-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c1436-191">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c1436-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1436-193">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c1436-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1436-195">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c1436-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1436-197">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c1436-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1436-199">а.</span><span class="sxs-lookup"><span data-stu-id="c1436-199">a.</span></span> <span data-ttu-id="c1436-200">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1436-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1436-201">b.</span><span class="sxs-lookup"><span data-stu-id="c1436-201">b.</span></span> <span data-ttu-id="c1436-202">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c1436-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1436-203">c.</span><span class="sxs-lookup"><span data-stu-id="c1436-203">c.</span></span> <span data-ttu-id="c1436-204">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c1436-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c1436-205">d.</span><span class="sxs-lookup"><span data-stu-id="c1436-205">d.</span></span> <span data-ttu-id="c1436-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c1436-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="c1436-207">Создание тестового пользователя Promapp</span><span class="sxs-lookup"><span data-stu-id="c1436-207">Creating a Promapp test user</span></span>

<span data-ttu-id="c1436-208">Приложение Promapp поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="c1436-208">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="c1436-209">Это значит, что учетная запись пользователя при необходимости создается автоматически во время попытки доступа к приложению с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c1436-209">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c1436-210">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1436-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c1436-211">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Promapp.</span><span class="sxs-lookup"><span data-stu-id="c1436-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c1436-213">**Чтобы назначить пользователя Britta Simon в Promapp, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c1436-213">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="c1436-214">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c1436-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c1436-216">В списке приложений выберите **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="c1436-216">In the applications list, select **Promapp**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="c1436-218">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c1436-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c1436-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c1436-220">Click **Add** button.</span></span> <span data-ttu-id="c1436-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c1436-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c1436-223">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c1436-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c1436-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c1436-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1436-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c1436-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1436-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c1436-226">Testing single sign-on</span></span>

<span data-ttu-id="c1436-227">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c1436-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c1436-228">Щелкнув плитку Promapp на панели доступа, вы автоматически войдете в приложение Promapp.</span><span class="sxs-lookup"><span data-stu-id="c1436-228">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c1436-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c1436-229">Additional resources</span></span>

* [<span data-ttu-id="c1436-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1436-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1436-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1436-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

