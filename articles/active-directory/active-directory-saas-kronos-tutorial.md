---
title: "Учебник. Интеграция Azure Active Directory с Kronos | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: eb61ec0a7d3e992a285b1af3d4a7fbe1feb8d991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="d28c9-103">Учебник. Интеграция Azure Active Directory с Kronos</span><span class="sxs-lookup"><span data-stu-id="d28c9-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="d28c9-104">В этом учебнике описано, как интегрировать приложение Kronos с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d28c9-104">In this tutorial, you learn how to integrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d28c9-105">Интеграция Azure AD с приложением Kronos обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="d28c9-105">Integrating Kronos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d28c9-106">С помощью Azure AD вы можете контролировать доступ к Kronos.</span><span class="sxs-lookup"><span data-stu-id="d28c9-106">You can control in Azure AD who has access to Kronos</span></span>
- <span data-ttu-id="d28c9-107">Вы можете включить автоматический вход пользователей в Kronos (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d28c9-107">You can enable your users to automatically get signed-on to Kronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d28c9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d28c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d28c9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d28c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d28c9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d28c9-110">Prerequisites</span></span>

<span data-ttu-id="d28c9-111">Чтобы настроить интеграцию Azure AD с Kronos, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d28c9-111">To configure Azure AD integration with Kronos, you need the following items:</span></span>

- <span data-ttu-id="d28c9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d28c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d28c9-113">подписка **Kronos Workforce Central** с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d28c9-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d28c9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d28c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d28c9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="d28c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d28c9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d28c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d28c9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d28c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d28c9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d28c9-118">Scenario description</span></span>
<span data-ttu-id="d28c9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d28c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d28c9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="d28c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d28c9-121">Добавление Kronos из коллекции</span><span class="sxs-lookup"><span data-stu-id="d28c9-121">Adding Kronos from the gallery</span></span>
2. <span data-ttu-id="d28c9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d28c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-the-gallery"></a><span data-ttu-id="d28c9-123">Добавление Kronos из коллекции</span><span class="sxs-lookup"><span data-stu-id="d28c9-123">Adding Kronos from the gallery</span></span>
<span data-ttu-id="d28c9-124">Чтобы настроить интеграцию Kronos с Azure AD, необходимо добавить Kronos из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d28c9-124">To configure the integration of Kronos into Azure AD, you need to add Kronos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d28c9-125">**Чтобы добавить Kronos из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d28c9-125">**To add Kronos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d28c9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d28c9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d28c9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d28c9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d28c9-133">В поле поиска введите **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-133">In the search box, type **Kronos**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="d28c9-135">На панели результатов выберите **Kronos** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="d28c9-135">In the results panel, select **Kronos**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d28c9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d28c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d28c9-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kronos с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d28c9-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d28c9-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Kronos соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d28c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kronos is to a user in Azure AD.</span></span> <span data-ttu-id="d28c9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Kronos.</span><span class="sxs-lookup"><span data-stu-id="d28c9-140">In other words, a link relationship between an Azure AD user and the related user in Kronos needs to be established.</span></span>

<span data-ttu-id="d28c9-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Kronos.</span><span class="sxs-lookup"><span data-stu-id="d28c9-141">In Kronos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d28c9-142">Чтобы настроить и проверить единый вход Azure AD в Kronos, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="d28c9-142">To configure and test Azure AD single sign-on with Kronos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d28c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d28c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d28c9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d28c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d28c9-145">**[Создание тестового пользователя Kronos](#creating-a-kronos-test-user)** требуется для создания в Kronos пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d28c9-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - to have a counterpart of Britta Simon in Kronos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d28c9-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d28c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d28c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d28c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d28c9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d28c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d28c9-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Kronos.</span><span class="sxs-lookup"><span data-stu-id="d28c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="d28c9-150">**Чтобы настроить единый вход Azure AD в Kronos, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d28c9-150">**To configure Azure AD single sign-on with Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="d28c9-151">На портале Azure на странице интеграции с приложением **Kronos** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-151">In the Azure portal, on the **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d28c9-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="d28c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="d28c9-155">В разделе **Домены и URL-адреса приложения Kronos** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d28c9-155">On the **Kronos Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="d28c9-157">а.</span><span class="sxs-lookup"><span data-stu-id="d28c9-157">a.</span></span> <span data-ttu-id="d28c9-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="d28c9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="d28c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="d28c9-159">b.</span></span> <span data-ttu-id="d28c9-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`.</span><span class="sxs-lookup"><span data-stu-id="d28c9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d28c9-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d28c9-161">These values are not real.</span></span> <span data-ttu-id="d28c9-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="d28c9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d28c9-163">Чтобы получить эти значения, обратитесь в [службу поддержки Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="d28c9-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) to get these values.</span></span>
 
4. <span data-ttu-id="d28c9-164">Приложение Kronos ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="d28c9-164">Your Kronos application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d28c9-165">Обратитесь в [службу поддержки Kronos](https://www.kronos.in/contact/en-in/form), чтобы определить правильный идентификатор пользователя, который будет сопоставляться в приложении.</span><span class="sxs-lookup"><span data-stu-id="d28c9-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first to identify the correct user identifier, which is mapped into the application.</span></span> <span data-ttu-id="d28c9-166">Необходимо выполнить рекомендации, касающиеся атрибута, который следует использовать для данного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="d28c9-166">Also please take the guidance about the attribute, which they want to use for this mapping.</span></span>
 
     <span data-ttu-id="d28c9-167">Корпорация Майкрософт рекомендует использовать атрибут **NameIdentifier** в качестве идентификатора пользователя.</span><span class="sxs-lookup"><span data-stu-id="d28c9-167">Microsoft recommends using the **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="d28c9-168">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="d28c9-168">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="d28c9-169">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="d28c9-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="d28c9-170">Здесь сопоставлен **идентификатор пользователя (nameid)** с функцией **ExtractMailPrefix()** атрибута **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-170">Here we have mapped the **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="d28c9-171">Таким образом получено значение префикса адреса электронной почты пользователя, которое представляет собой уникальный идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="d28c9-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="d28c9-172">Он будет отправляться в приложение Kronos в каждом успешном ответе.</span><span class="sxs-lookup"><span data-stu-id="d28c9-172">This is sent to the Kronos application in every successful response.</span></span> 
     
    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="d28c9-174">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d28c9-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="d28c9-175">а.</span><span class="sxs-lookup"><span data-stu-id="d28c9-175">a.</span></span> <span data-ttu-id="d28c9-176">В раскрывающемся списке "Идентификатор пользователя" выберите **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-176">In the User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="d28c9-177">b.</span><span class="sxs-lookup"><span data-stu-id="d28c9-177">b.</span></span> <span data-ttu-id="d28c9-178">В раскрывающемся списке **Электронная почта** выберите **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-178">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="d28c9-179">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d28c9-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="d28c9-181">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d28c9-181">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d28c9-183">Чтобы настроить единый вход на стороне **Kronos**, отправьте в [службу поддержки Kronos](https://www.kronos.in/contact/en-in/form) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-183">To configure single sign-on on **Kronos** side, you need to send the downloaded **Metadata XML** to [Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="d28c9-184">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d28c9-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d28c9-185">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d28c9-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d28c9-186">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d28c9-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d28c9-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d28c9-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="d28c9-188">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d28c9-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d28c9-190">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d28c9-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d28c9-191">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d28c9-193">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d28c9-195">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d28c9-197">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d28c9-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d28c9-199">а.</span><span class="sxs-lookup"><span data-stu-id="d28c9-199">a.</span></span> <span data-ttu-id="d28c9-200">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d28c9-201">b.</span><span class="sxs-lookup"><span data-stu-id="d28c9-201">b.</span></span> <span data-ttu-id="d28c9-202">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d28c9-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d28c9-203">c.</span><span class="sxs-lookup"><span data-stu-id="d28c9-203">c.</span></span> <span data-ttu-id="d28c9-204">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d28c9-205">d.</span><span class="sxs-lookup"><span data-stu-id="d28c9-205">d.</span></span> <span data-ttu-id="d28c9-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="d28c9-207">Создание тестового пользователя Kronos</span><span class="sxs-lookup"><span data-stu-id="d28c9-207">Creating a Kronos test user</span></span>

<span data-ttu-id="d28c9-208">В этом разделе описано, как создать пользователя Britta Simon в приложении Kronos.</span><span class="sxs-lookup"><span data-stu-id="d28c9-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="d28c9-209">Перед использованием единого входа все пользователи должны быть подготовлены в приложении Kronos.</span><span class="sxs-lookup"><span data-stu-id="d28c9-209">Kronos application needs all the users to be provisioned in the application before doing SSO.</span></span> 

<span data-ttu-id="d28c9-210">Для этого обратитесь в [службу поддержки Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="d28c9-210">Work with the [Kronos support team](https://www.kronos.in/contact/en-in/form) to provision all these users into the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d28c9-211">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d28c9-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d28c9-212">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Kronos.</span><span class="sxs-lookup"><span data-stu-id="d28c9-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kronos.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d28c9-214">**Чтобы назначить пользователя Britta Simon в Kronos, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d28c9-214">**To assign Britta Simon to Kronos, perform the following steps:**</span></span>

1. <span data-ttu-id="d28c9-215">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d28c9-217">В списке приложений выберите **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-217">In the applications list, select **Kronos**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="d28c9-219">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d28c9-221">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-221">Click **Add** button.</span></span> <span data-ttu-id="d28c9-222">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d28c9-224">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d28c9-225">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d28c9-226">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d28c9-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d28c9-227">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d28c9-227">Testing single sign-on</span></span>

<span data-ttu-id="d28c9-228">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d28c9-228">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="d28c9-229">Щелкнув элемент Kronos на панели доступа, вы автоматически войдете в приложение Kronos.</span><span class="sxs-lookup"><span data-stu-id="d28c9-229">When you click the Kronos tile in the Access Panel, you should get automatically signed-on to your Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d28c9-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d28c9-230">Additional resources</span></span>

* [<span data-ttu-id="d28c9-231">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d28c9-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d28c9-232">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d28c9-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

