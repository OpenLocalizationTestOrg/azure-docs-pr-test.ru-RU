---
title: "Учебник. Интеграция Azure Active Directory с GaggleAMP | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: c591cf99aecc4153e378c42a530b80deeca63158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="9f997-103">Руководство. Интеграция Azure Active Directory с GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="9f997-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="9f997-104">В этом руководстве описано, как интегрировать GaggleAMP с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9f997-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f997-105">Интеграция Azure AD с приложением GaggleAMP обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9f997-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9f997-106">С помощью Azure AD вы можете контролировать доступ к приложению GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9f997-106">You can control in Azure AD who has access to GaggleAMP</span></span>
- <span data-ttu-id="9f997-107">Вы можете включить автоматический вход пользователей в GaggleAMP (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f997-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f997-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9f997-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9f997-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f997-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f997-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9f997-110">Prerequisites</span></span>

<span data-ttu-id="9f997-111">Чтобы настроить интеграцию Azure AD с GaggleAMP, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9f997-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

- <span data-ttu-id="9f997-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9f997-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f997-113">подписка на GaggleAMP с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9f997-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f997-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9f997-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f997-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9f997-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f997-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9f997-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f997-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f997-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f997-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9f997-118">Scenario description</span></span>
<span data-ttu-id="9f997-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9f997-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f997-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9f997-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f997-121">Добавление GaggleAMP из коллекции</span><span class="sxs-lookup"><span data-stu-id="9f997-121">Adding GaggleAMP from the gallery</span></span>
2. <span data-ttu-id="9f997-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f997-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-the-gallery"></a><span data-ttu-id="9f997-123">Добавление GaggleAMP из коллекции</span><span class="sxs-lookup"><span data-stu-id="9f997-123">Adding GaggleAMP from the gallery</span></span>
<span data-ttu-id="9f997-124">Чтобы настроить интеграцию GaggleAMP с Azure AD, необходимо добавить GaggleAMP из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9f997-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9f997-125">**Чтобы добавить GaggleAMP из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9f997-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9f997-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f997-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f997-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f997-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9f997-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f997-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9f997-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="9f997-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9f997-133">В поле поиска введите **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="9f997-133">In the search box, type **GaggleAMP**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="9f997-135">На панели результатов выберите **GaggleAMP** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="9f997-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f997-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f997-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f997-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение GaggleAMP для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f997-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f997-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в GaggleAMP соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f997-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span></span> <span data-ttu-id="9f997-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9f997-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="9f997-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9f997-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9f997-142">Чтобы настроить и проверить единый вход Azure AD в GaggleAMP, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="9f997-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9f997-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9f997-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9f997-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f997-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f997-145">**[Создание тестового пользователя GaggleAMP](#creating-a-gaggleamp-test-user)** требуется для создания пользователя Britta Simon в GaggleAMP, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f997-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f997-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f997-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f997-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9f997-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f997-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f997-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f997-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9f997-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="9f997-150">**Чтобы настроить единый вход Azure AD в GaggleAMP, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9f997-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="9f997-151">На портале Azure на странице интеграции с приложением **GaggleAMP** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9f997-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9f997-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9f997-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="9f997-155">В разделе **Домены и URL-адреса GaggleAMP** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9f997-155">On the **GaggleAMP Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="9f997-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="9f997-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f997-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="9f997-158">The value is not real.</span></span> <span data-ttu-id="9f997-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="9f997-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="9f997-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="9f997-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get the value.</span></span> 
 
4. <span data-ttu-id="9f997-161">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9f997-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="9f997-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9f997-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9f997-165">В разделе **Настройка GaggleAMP** щелкните **Настроить GaggleAMP**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9f997-165">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9f997-166">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="9f997-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="9f997-168">В другом окне браузера перейдите на страницу единого входа SAML, созданную для вас группой поддержки Gaggle (например, *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="9f997-168">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="9f997-169">На странице **Единый вход SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9f997-169">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![Единый вход в GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="9f997-171">а.</span><span class="sxs-lookup"><span data-stu-id="9f997-171">a.</span></span> <span data-ttu-id="9f997-172">В текстовое поле **Издатель поставщика удостоверений** вставьте значение **URL-адреса издателя**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9f997-172">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="9f997-173">b.</span><span class="sxs-lookup"><span data-stu-id="9f997-173">b.</span></span> <span data-ttu-id="9f997-174">В текстовое поле **URL-адрес единого входа поставщика удостоверений** вставьте значение **URL-адреса службы единого входа**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9f997-174">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="9f997-175">c.</span><span class="sxs-lookup"><span data-stu-id="9f997-175">c.</span></span> <span data-ttu-id="9f997-176">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="9f997-176">Click **Save**</span></span>      

    <span data-ttu-id="9f997-177">г)</span><span class="sxs-lookup"><span data-stu-id="9f997-177">d.</span></span> <span data-ttu-id="9f997-178">Отправьте **Сертификат (в кодировке Base64)** в [службу поддержки GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="9f997-178">Send the **Certificate (Base64)** certificate to your [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="9f997-179">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="9f997-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9f997-180">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="9f997-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9f997-181">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9f997-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f997-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f997-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f997-183">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f997-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9f997-185">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9f997-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9f997-186">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f997-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f997-188">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="9f997-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f997-190">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9f997-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f997-192">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9f997-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f997-194">а.</span><span class="sxs-lookup"><span data-stu-id="9f997-194">a.</span></span> <span data-ttu-id="9f997-195">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f997-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f997-196">b.</span><span class="sxs-lookup"><span data-stu-id="9f997-196">b.</span></span> <span data-ttu-id="9f997-197">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f997-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f997-198">c.</span><span class="sxs-lookup"><span data-stu-id="9f997-198">c.</span></span> <span data-ttu-id="9f997-199">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9f997-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9f997-200">d.</span><span class="sxs-lookup"><span data-stu-id="9f997-200">d.</span></span> <span data-ttu-id="9f997-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9f997-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="9f997-202">Создание тестового пользователя GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="9f997-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="9f997-203">Цель этого раздела — создать в приложении GaggleAMP пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9f997-203">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="9f997-204">Приложение GaggleAMP поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9f997-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9f997-205">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="9f997-205">There is no action item for you in this section.</span></span> <span data-ttu-id="9f997-206">Новый пользователь будет создан при попытке получить доступ к GaggleAMP (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="9f997-206">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9f997-207">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f997-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9f997-208">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9f997-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9f997-210">**Чтобы назначить пользователя Britta Simon в GaggleAMP, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9f997-210">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="9f997-211">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9f997-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9f997-213">В списке приложений выберите **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="9f997-213">In the applications list, select **GaggleAMP**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="9f997-215">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9f997-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9f997-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9f997-217">Click **Add** button.</span></span> <span data-ttu-id="9f997-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9f997-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9f997-220">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9f997-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9f997-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9f997-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f997-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9f997-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f997-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9f997-223">Testing single sign-on</span></span>

<span data-ttu-id="9f997-224">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9f997-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="9f997-225">Щелкнув элемент GaggleAMP на панели доступа, вы автоматически войдете в приложение GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="9f997-225">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f997-226">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9f997-226">Additional resources</span></span>

* [<span data-ttu-id="9f997-227">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f997-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f997-228">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f997-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

