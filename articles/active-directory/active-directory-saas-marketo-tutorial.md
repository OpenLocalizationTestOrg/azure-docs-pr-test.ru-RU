---
title: "Учебник. Интеграция Azure Active Directory с Marketo | Документация Майкрософт"
description: "Узнайте, как настроить единый вход в Marketo через Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="0b7ba-103">Руководство. Интеграция Azure Active Directory с Marketo</span><span class="sxs-lookup"><span data-stu-id="0b7ba-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="0b7ba-104">В этом руководстве описано, как интегрировать Marketo с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b7ba-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b7ba-105">Интеграция Azure AD с приложением Marketo обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b7ba-106">С помощью Azure AD вы можете контролировать доступ к Marketo.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="0b7ba-107">Вы можете включить автоматический вход пользователей в Marketo (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b7ba-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b7ba-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b7ba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b7ba-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0b7ba-110">Prerequisites</span></span>

<span data-ttu-id="0b7ba-111">Чтобы настроить интеграцию Azure AD с Marketo, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="0b7ba-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="0b7ba-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0b7ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b7ba-113">подписка Marketo с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b7ba-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b7ba-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="0b7ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b7ba-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b7ba-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b7ba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b7ba-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0b7ba-118">Scenario description</span></span>
<span data-ttu-id="0b7ba-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b7ba-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="0b7ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b7ba-121">добавление Marketo из коллекции,</span><span class="sxs-lookup"><span data-stu-id="0b7ba-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="0b7ba-122">настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="0b7ba-123">добавление Marketo из коллекции,</span><span class="sxs-lookup"><span data-stu-id="0b7ba-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="0b7ba-124">Чтобы настроить интеграцию Marketo с Azure AD, необходимо добавить Marketo из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b7ba-125">**Чтобы добавить Marketo из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0b7ba-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b7ba-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b7ba-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b7ba-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0b7ba-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0b7ba-133">В поле поиска введите **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-133">In the search box, type **Marketo**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="0b7ba-135">На панели результатов выберите **Marketo** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b7ba-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b7ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b7ba-138">В этом разделе описана настройка и проверка единого входа Azure AD в Marketo для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0b7ba-139">Для работы единого входа Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в Marketo.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="0b7ba-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Marketo.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="0b7ba-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Marketo.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0b7ba-142">Чтобы настроить и проверить единый вход Azure AD в Marketo, вам нужно выполнить следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b7ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b7ba-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b7ba-145">**[Создание тестового пользователя Marketo](#creating-a-marketo-test-user)** требуется для создания в Marketo пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b7ba-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b7ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b7ba-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b7ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b7ba-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Marketo.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="0b7ba-150">**Чтобы настроить единый вход Azure AD в Marketo, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0b7ba-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="0b7ba-151">На портале Azure на странице интеграции с приложением **Marketo** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0b7ba-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="0b7ba-155">В разделе **Домены и URL-адреса Marketo** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0b7ba-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="0b7ba-157">а.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-157">a.</span></span> <span data-ttu-id="0b7ba-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="0b7ba-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="0b7ba-159">b.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-159">b.</span></span> <span data-ttu-id="0b7ba-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://login.marketo.com/saml/assertion/\<munchkinid\>`.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0b7ba-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-161">These values are not real.</span></span> <span data-ttu-id="0b7ba-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="0b7ba-163">Чтобы получить эти значения, обратитесь в [службу поддержки Marketo](http://investors.marketo.com/contactus.cfm).</span><span class="sxs-lookup"><span data-stu-id="0b7ba-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="0b7ba-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="0b7ba-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0b7ba-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b7ba-168">В разделе **Настройка Marketo** щелкните **Настроить Marketo**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b7ba-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="0b7ba-171">Чтобы получить идентификатор Munchkin для приложения, войдите в Marketo, используя учетные данные администратора, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="0b7ba-172">а.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-172">a.</span></span> <span data-ttu-id="0b7ba-173">Войдите в приложение Marketo, используя учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="0b7ba-174">b.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-174">b.</span></span> <span data-ttu-id="0b7ba-175">Нажмите кнопку **Администратор** в области навигации вверху.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="0b7ba-177">c.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-177">c.</span></span> <span data-ttu-id="0b7ba-178">Перейдите в меню "Интеграция" и щелкните **ссылку Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="0b7ba-180">d.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-180">d.</span></span> <span data-ttu-id="0b7ba-181">Скопируйте идентификатор Munchkin, показанный на экране, и введите URL-адрес ответа в мастере настройки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="0b7ba-183">Для настройки единого входа в приложение выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0b7ba-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="0b7ba-184">а.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-184">a.</span></span> <span data-ttu-id="0b7ba-185">Войдите в приложение Marketo, используя учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="0b7ba-186">b.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-186">b.</span></span> <span data-ttu-id="0b7ba-187">Нажмите кнопку **Администратор** в области навигации вверху.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="0b7ba-189">c.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-189">c.</span></span> <span data-ttu-id="0b7ba-190">Перейдите в меню "Интеграция" и щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="0b7ba-192">г)</span><span class="sxs-lookup"><span data-stu-id="0b7ba-192">d.</span></span> <span data-ttu-id="0b7ba-193">Чтобы включить параметры SAML, нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="0b7ba-195">д.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-195">e.</span></span> <span data-ttu-id="0b7ba-196">**Включите** параметры единого входа.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="0b7ba-197">Е.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-197">f.</span></span> <span data-ttu-id="0b7ba-198">Вставьте **идентификатор сущности SAML** в текстовое поле **Идентификатор издателя**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="0b7ba-199">g.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-199">g.</span></span> <span data-ttu-id="0b7ba-200">В текстовом поле **Идентификатор сущности** введите URL-адрес в формате `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="0b7ba-201">h.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-201">h.</span></span> <span data-ttu-id="0b7ba-202">Укажите значение **В элементе идентификатора имени** для параметра "Расположение идентификатора пользователя".</span><span class="sxs-lookup"><span data-stu-id="0b7ba-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="0b7ba-204">Если идентификатор пользователя имеет значение, отличное от имени участника-пользователя, измените это значение на вкладке Attribute (Атрибут).</span><span class="sxs-lookup"><span data-stu-id="0b7ba-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="0b7ba-205">i.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-205">i.</span></span> <span data-ttu-id="0b7ba-206">Отправьте сертификат, скачанный из мастера настройки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="0b7ba-207">**Сохраните** параметры.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="0b7ba-208">j.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-208">j.</span></span> <span data-ttu-id="0b7ba-209">Измените параметры перенаправления страниц.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="0b7ba-210">k.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-210">k.</span></span> <span data-ttu-id="0b7ba-211">Вставьте **URL-адрес службы единого входа SAML** в текстовое поле **URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="0b7ba-212">l.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-212">l.</span></span> <span data-ttu-id="0b7ba-213">Вставьте **URL-адрес выхода** в текстовое поле **URL-адрес выхода**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="0b7ba-214">m.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-214">m.</span></span> <span data-ttu-id="0b7ba-215">В поле **URL-адрес ошибки** вставьте **URL-адрес экземпляра Marketo** и нажмите кнопку **Сохранить**, чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="0b7ba-217">Чтобы включить единый вход для пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="0b7ba-218">а.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-218">a.</span></span> <span data-ttu-id="0b7ba-219">Войдите в приложение Marketo, используя учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="0b7ba-220">b.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-220">b.</span></span> <span data-ttu-id="0b7ba-221">Нажмите кнопку **Администратор** в области навигации вверху.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="0b7ba-223">c.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-223">c.</span></span> <span data-ttu-id="0b7ba-224">В меню **Безопасность** щелкните **Параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="0b7ba-226">г)</span><span class="sxs-lookup"><span data-stu-id="0b7ba-226">d.</span></span> <span data-ttu-id="0b7ba-227">Установите флажок **Требовать единый вход** и **сохраните** параметры.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="0b7ba-229">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b7ba-230">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b7ba-231">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0b7ba-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b7ba-232">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b7ba-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b7ba-233">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0b7ba-235">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0b7ba-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b7ba-236">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b7ba-238">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b7ba-240">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b7ba-242">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b7ba-244">а.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-244">a.</span></span> <span data-ttu-id="0b7ba-245">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b7ba-246">b.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-246">b.</span></span> <span data-ttu-id="0b7ba-247">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b7ba-248">c.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-248">c.</span></span> <span data-ttu-id="0b7ba-249">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b7ba-250">d.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-250">d.</span></span> <span data-ttu-id="0b7ba-251">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="0b7ba-252">Создание тестового пользователя Marketo</span><span class="sxs-lookup"><span data-stu-id="0b7ba-252">Creating a Marketo test user</span></span>

<span data-ttu-id="0b7ba-253">В этом разделе описано, как создать пользователя Britta Simon в приложении Marketo.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="0b7ba-254">Для создания пользователя на платформе Marketo выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="0b7ba-255">Войдите в приложение Marketo, используя учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="0b7ba-256">Нажмите кнопку **Администратор** в области навигации вверху.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="0b7ba-258">Откройте меню **Безопасность** и выберите **Пользователи и роли**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="0b7ba-260">На вкладке "Пользователи" щелкните **Пригласить нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="0b7ba-262">Введите следующую информацию в мастере приглашения нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="0b7ba-263">а.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-263">a.</span></span> <span data-ttu-id="0b7ba-264">Введите адрес **электронной почты** пользователя в соответствующее текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="0b7ba-266">b.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-266">b.</span></span> <span data-ttu-id="0b7ba-267">Введите **имя** .</span><span class="sxs-lookup"><span data-stu-id="0b7ba-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="0b7ba-268">В.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-268">c.</span></span> <span data-ttu-id="0b7ba-269">Введите **фамилию**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="0b7ba-270">г)</span><span class="sxs-lookup"><span data-stu-id="0b7ba-270">d.</span></span> <span data-ttu-id="0b7ba-271">Щелкните **Далее**</span><span class="sxs-lookup"><span data-stu-id="0b7ba-271">Click **Next**</span></span>

6. <span data-ttu-id="0b7ba-272">На вкладке **Разрешения** выберите **роли пользователя** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="0b7ba-274">Нажмите кнопку **Отправить**, чтобы отправить приглашение пользователю.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="0b7ba-276">Пользователь получит уведомление по электронной почте. Ему нужно будет перейти по ссылке, чтобы изменить пароль и активировать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b7ba-277">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b7ba-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b7ba-278">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon и предоставить этому пользователю доступ к Marketo.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0b7ba-280">**Чтобы назначить пользователя Britta Simon в Marketo, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0b7ba-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="0b7ba-281">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0b7ba-283">В списке приложений выберите **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-283">In the applications list, select **Marketo**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="0b7ba-285">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-285">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0b7ba-287">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-287">Click **Add** button.</span></span> <span data-ttu-id="0b7ba-288">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0b7ba-290">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b7ba-291">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b7ba-292">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b7ba-293">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0b7ba-293">Testing single sign-on</span></span>

<span data-ttu-id="0b7ba-294">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0b7ba-295">Щелкнув плитку Marketo на панели доступа, вы автоматически войдете в приложение Marketo.</span><span class="sxs-lookup"><span data-stu-id="0b7ba-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0b7ba-296">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0b7ba-296">Additional resources</span></span>

* [<span data-ttu-id="0b7ba-297">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b7ba-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b7ba-298">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b7ba-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

