---
title: "Руководство по интеграции Azure Active Directory с Pantheon | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3f4ac1db2ee83d9f9fcb375d0fb7c40ad21c4688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="8dad9-103">Руководство по интеграции Azure Active Directory с Pantheon</span><span class="sxs-lookup"><span data-stu-id="8dad9-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="8dad9-104">В этом руководстве описано, как интегрировать Pantheon с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8dad9-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8dad9-105">Интеграция Azure AD с приложением Pantheon обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8dad9-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8dad9-106">С помощью Azure AD вы можете контролировать доступ к Pantheon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="8dad9-107">Вы можете включить автоматический вход пользователей в Pantheon (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dad9-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8dad9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8dad9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8dad9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8dad9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dad9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8dad9-110">Prerequisites</span></span>

<span data-ttu-id="8dad9-111">Чтобы настроить интеграцию Azure AD с Pantheon, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8dad9-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="8dad9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8dad9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8dad9-113">подписка Pantheon с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8dad9-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8dad9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8dad9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8dad9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8dad9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8dad9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8dad9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8dad9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8dad9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8dad9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8dad9-118">Scenario description</span></span>
<span data-ttu-id="8dad9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8dad9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8dad9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8dad9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8dad9-121">Добавление Pantheon из коллекции</span><span class="sxs-lookup"><span data-stu-id="8dad9-121">Adding Pantheon from the gallery</span></span>
2. <span data-ttu-id="8dad9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dad9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="8dad9-123">Добавление Pantheon из коллекции</span><span class="sxs-lookup"><span data-stu-id="8dad9-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="8dad9-124">Чтобы настроить интеграцию Pantheon с Azure AD, необходимо добавить Pantheon из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8dad9-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8dad9-125">**Чтобы добавить Pantheon из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8dad9-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8dad9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8dad9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8dad9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8dad9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8dad9-133">В поле поиска введите **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-133">In the search box, type **Pantheon**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="8dad9-135">На панели результатов выберите **Pantheon** и щелкните **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8dad9-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8dad9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dad9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8dad9-138">В этом разделе описана настройка и проверка единого входа Azure AD в Pantheon с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8dad9-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Pantheon соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dad9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="8dad9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Pantheon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="8dad9-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Pantheon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8dad9-142">Чтобы настроить и проверить единый вход Azure AD в Pantheon, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="8dad9-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8dad9-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8dad9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8dad9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8dad9-145">**[Создание тестового пользователя Pantheon](#creating-a-pantheon-test-user)** требуется для создания в Pantheon пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dad9-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8dad9-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8dad9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8dad9-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8dad9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8dad9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dad9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8dad9-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Pantheon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="8dad9-150">**Чтобы настроить единый вход Azure AD в Pantheon, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8dad9-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="8dad9-151">На портале Azure на странице интеграции с приложением **Pantheon** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8dad9-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8dad9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="8dad9-155">В разделе **Домены и URL-адреса приложения Pantheon** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="8dad9-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="8dad9-157">а.</span><span class="sxs-lookup"><span data-stu-id="8dad9-157">a.</span></span> <span data-ttu-id="8dad9-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="8dad9-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="8dad9-159">b.</span><span class="sxs-lookup"><span data-stu-id="8dad9-159">b.</span></span> <span data-ttu-id="8dad9-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`.</span><span class="sxs-lookup"><span data-stu-id="8dad9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8dad9-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8dad9-161">These values are not real.</span></span> <span data-ttu-id="8dad9-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="8dad9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="8dad9-163">Чтобы получить эти значения, обратитесь в [службу поддержки Pantheon](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="8dad9-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span></span>

4. <span data-ttu-id="8dad9-164">Приложение Pantheon ожидает получить утверждение SAML в определенном формате. Для этого формата потребуется указать адрес электронной почты пользователя в качестве значения атрибута UserIdentifier.</span><span class="sxs-lookup"><span data-stu-id="8dad9-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="8dad9-165">По умолчанию Azure AD использует для этого атрибута значение UserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="8dad9-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="8dad9-166">Для успешной интеграции это значение следует изменить так, чтобы оно совпадало с адресом электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="8dad9-166">But for successful integration you need to adjust this value to match with user’s email address.</span></span> <span data-ttu-id="8dad9-167">Интеграция будет работать только после выполнения правильного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="8dad9-167">The integration will only work after doing the correct mapping.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="8dad9-169">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8dad9-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="8dad9-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8dad9-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="8dad9-173">В разделе **Настройка Pantheon** выберите **Настроить Pantheon**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8dad9-174">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="8dad9-176">Чтобы настроить единый вход на стороне **Pantheon**, нужно отправить скачанный **сертификат** и **URL-адрес службы единого входа SAML** в [службу поддержки Pantheon](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="8dad9-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="8dad9-177">Чтобы включить эту связь, необходимо также предоставить сведения о доменах электронной почты и о формате даты и времени.</span><span class="sxs-lookup"><span data-stu-id="8dad9-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="8dad9-178">Дополнительные сведения см. [здесь](https://pantheon.io/docs/sso-organizations/).</span><span class="sxs-lookup"><span data-stu-id="8dad9-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="8dad9-179">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8dad9-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8dad9-180">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8dad9-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8dad9-181">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8dad9-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8dad9-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dad9-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="8dad9-183">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8dad9-185">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8dad9-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8dad9-186">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8dad9-188">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8dad9-190">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8dad9-192">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8dad9-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8dad9-194">а.</span><span class="sxs-lookup"><span data-stu-id="8dad9-194">a.</span></span> <span data-ttu-id="8dad9-195">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8dad9-196">b.</span><span class="sxs-lookup"><span data-stu-id="8dad9-196">b.</span></span> <span data-ttu-id="8dad9-197">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8dad9-198">c.</span><span class="sxs-lookup"><span data-stu-id="8dad9-198">c.</span></span> <span data-ttu-id="8dad9-199">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8dad9-200">d.</span><span class="sxs-lookup"><span data-stu-id="8dad9-200">d.</span></span> <span data-ttu-id="8dad9-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="8dad9-202">Создание тестового пользователя Pantheon</span><span class="sxs-lookup"><span data-stu-id="8dad9-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="8dad9-203">В этом разделе описано, как создать пользователя Britta Simon в приложении Pantheon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="8dad9-204">Выполните следующие ниже действия, чтобы добавить пользователя в Pantheon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-204">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="8dad9-205">Чтобы единый вход начал работать, необходимо сначала создать пользователя в Pantheon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-205">For SSO to work user needs to be created first in Pantheon.</span></span>

1. <span data-ttu-id="8dad9-206">Войдите в Pantheon с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="8dad9-206">Login to Pantheon with admin credentials.</span></span>

2. <span data-ttu-id="8dad9-207">Перейдите на страницу **Organization** (Организация) панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8dad9-207">Navigate to **Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="8dad9-208">Выберите параметр **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-208">Click **People**.</span></span>

4. <span data-ttu-id="8dad9-209">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-209">Click **Add user**.</span></span>

5. <span data-ttu-id="8dad9-210">Введите адрес электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="8dad9-210">Enter the user's email address.</span></span>

6. <span data-ttu-id="8dad9-211">Выберите роль пользователя.</span><span class="sxs-lookup"><span data-stu-id="8dad9-211">Choose the user's role.</span></span>

7. <span data-ttu-id="8dad9-212">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-212">Click **Add user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8dad9-213">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8dad9-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8dad9-214">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Pantheon, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="8dad9-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8dad9-216">**Чтобы назначить пользователя Britta Simon в Pantheon, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8dad9-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="8dad9-217">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8dad9-219">В списке приложений выберите **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-219">In the applications list, select **Pantheon**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="8dad9-221">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8dad9-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-223">Click **Add** button.</span></span> <span data-ttu-id="8dad9-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8dad9-226">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8dad9-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8dad9-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8dad9-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8dad9-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8dad9-229">Testing single sign-on</span></span>

<span data-ttu-id="8dad9-230">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8dad9-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8dad9-231">Щелкнув элемент Pantheon на панели доступа, вы автоматически войдете в приложение Pantheon.</span><span class="sxs-lookup"><span data-stu-id="8dad9-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>
<span data-ttu-id="8dad9-232">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8dad9-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8dad9-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8dad9-233">Additional resources</span></span>

* [<span data-ttu-id="8dad9-234">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8dad9-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8dad9-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8dad9-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

