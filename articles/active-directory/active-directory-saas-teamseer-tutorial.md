---
title: "Руководство по интеграции Azure Active Directory с TeamSeer | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="e9b12-103">Учебник. Интеграция Azure Active Directory с TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e9b12-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="e9b12-104">В этом руководстве описано, как интегрировать TeamSeer с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9b12-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9b12-105">Интеграция Azure AD с приложением TeamSeer обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e9b12-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9b12-106">С помощью Azure AD вы можете контролировать доступ к TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e9b12-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="e9b12-107">Вы можете включить автоматический вход пользователей в TeamSeer (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9b12-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9b12-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e9b12-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e9b12-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9b12-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9b12-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e9b12-110">Prerequisites</span></span>

<span data-ttu-id="e9b12-111">Чтобы настроить интеграцию Azure AD с TeamSeer, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e9b12-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="e9b12-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e9b12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9b12-113">подписка TeamSeer с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e9b12-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9b12-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e9b12-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9b12-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e9b12-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9b12-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e9b12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9b12-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9b12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9b12-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e9b12-118">Scenario description</span></span>
<span data-ttu-id="e9b12-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e9b12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9b12-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e9b12-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9b12-121">Добавление TeamSeer из коллекции</span><span class="sxs-lookup"><span data-stu-id="e9b12-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="e9b12-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9b12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="e9b12-123">Добавление TeamSeer из коллекции</span><span class="sxs-lookup"><span data-stu-id="e9b12-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="e9b12-124">Чтобы настроить интеграцию TeamSeer с Azure AD, нужно добавить TeamSeer из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e9b12-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9b12-125">**Чтобы добавить TeamSeer из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e9b12-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b12-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9b12-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9b12-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e9b12-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e9b12-133">В поле поиска введите **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-133">In the search box, type **TeamSeer**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="e9b12-135">На панели результатов выберите **TeamSeer** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e9b12-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9b12-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9b12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9b12-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение TeamSeer с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9b12-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e9b12-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в TeamSeer соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9b12-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="e9b12-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e9b12-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="e9b12-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e9b12-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e9b12-142">Чтобы настроить и проверить единый вход Azure AD в TeamSeer, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="e9b12-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9b12-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e9b12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9b12-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9b12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9b12-145">**[Создание тестового пользователя TeamSeer](#creating-a-teamseer-test-user)** требуется для создания пользователя Britta Simon в TeamSeer, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9b12-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9b12-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9b12-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9b12-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e9b12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9b12-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9b12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9b12-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e9b12-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="e9b12-150">**Чтобы настроить единый вход Azure AD в TeamSeer, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e9b12-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b12-151">На портале Azure на странице интеграции с приложением **TeamSeer** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e9b12-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e9b12-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="e9b12-155">В разделе **Домены и URL-адреса приложения TeamSeer** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="e9b12-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="e9b12-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="e9b12-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e9b12-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="e9b12-158">The value is not real.</span></span> <span data-ttu-id="e9b12-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="e9b12-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="e9b12-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html).</span><span class="sxs-lookup"><span data-stu-id="e9b12-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="e9b12-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e9b12-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="e9b12-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e9b12-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9b12-165">В разделе **Конфигурация TeamSeer** щелкните **Настроить TeamSeer**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e9b12-166">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="e9b12-168">В другом окне веб-браузера войдите на свой корпоративный веб-сайт TeamSeer в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e9b12-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="e9b12-169">Перейдите в раздел **Администратор отдела кадров**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="e9b12-170">![Администратор отдела кадров](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Администратор отдела кадров")</span><span class="sxs-lookup"><span data-stu-id="e9b12-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="e9b12-171">Щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="e9b12-172">![Настройка](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="e9b12-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="e9b12-173">Щелкните **Задать данные о поставщике SAML**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="e9b12-174">![Параметры SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Параметры SAML")</span><span class="sxs-lookup"><span data-stu-id="e9b12-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="e9b12-175">В разделе сведений о поставщике SAML выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e9b12-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="e9b12-176">![Параметры SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Параметры SAML")</span><span class="sxs-lookup"><span data-stu-id="e9b12-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="e9b12-177">а.</span><span class="sxs-lookup"><span data-stu-id="e9b12-177">a.</span></span> <span data-ttu-id="e9b12-178">Вставьте значение **URL-адреса службы единого входа** в текстовое поле **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="e9b12-179">b.</span><span class="sxs-lookup"><span data-stu-id="e9b12-179">b.</span></span> <span data-ttu-id="e9b12-180">Откройте сертификат в кодировке Base-64 в блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Общий сертификат поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="e9b12-181">Чтобы завершить настройку поставщика SAML, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e9b12-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="e9b12-182">![Параметры SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Параметры SAML")</span><span class="sxs-lookup"><span data-stu-id="e9b12-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="e9b12-183">а.</span><span class="sxs-lookup"><span data-stu-id="e9b12-183">a.</span></span> <span data-ttu-id="e9b12-184">В разделе **Тестовые адреса электронной почты**введите адрес электронной почты для тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9b12-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="e9b12-185">b.</span><span class="sxs-lookup"><span data-stu-id="e9b12-185">b.</span></span> <span data-ttu-id="e9b12-186">В текстовом поле **Издатель** введите URL-адрес издателя поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="e9b12-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="e9b12-187">c.</span><span class="sxs-lookup"><span data-stu-id="e9b12-187">c.</span></span> <span data-ttu-id="e9b12-188">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e9b12-189">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e9b12-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e9b12-190">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e9b12-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e9b12-191">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e9b12-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9b12-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9b12-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9b12-193">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9b12-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e9b12-195">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e9b12-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b12-196">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9b12-198">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9b12-200">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9b12-202">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e9b12-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9b12-204">а.</span><span class="sxs-lookup"><span data-stu-id="e9b12-204">a.</span></span> <span data-ttu-id="e9b12-205">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9b12-206">b.</span><span class="sxs-lookup"><span data-stu-id="e9b12-206">b.</span></span> <span data-ttu-id="e9b12-207">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e9b12-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9b12-208">c.</span><span class="sxs-lookup"><span data-stu-id="e9b12-208">c.</span></span> <span data-ttu-id="e9b12-209">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e9b12-210">d.</span><span class="sxs-lookup"><span data-stu-id="e9b12-210">d.</span></span> <span data-ttu-id="e9b12-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="e9b12-212">Создание тестового пользователя TeamSeer</span><span class="sxs-lookup"><span data-stu-id="e9b12-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="e9b12-213">Чтобы пользователи Azure AD могли выполнить вход в TeamSeer, они должны быть подготовлены в TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e9b12-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="e9b12-214">В случае с TeamSeer подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="e9b12-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="e9b12-215">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e9b12-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b12-216">Войдите на веб-сайт **TeamSeer** вашей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e9b12-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="e9b12-217">Выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e9b12-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="e9b12-218">![Администратор отдела кадров](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Администратор отдела кадров")</span><span class="sxs-lookup"><span data-stu-id="e9b12-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="e9b12-219">а.</span><span class="sxs-lookup"><span data-stu-id="e9b12-219">a.</span></span> <span data-ttu-id="e9b12-220">Выберите **HR Admin (Администратор отдела кадров) \> Users (Пользователи)**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="e9b12-221">b.</span><span class="sxs-lookup"><span data-stu-id="e9b12-221">b.</span></span> <span data-ttu-id="e9b12-222">Щелкните **Запустить мастер нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="e9b12-223">В разделе **Сведения о пользователе** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e9b12-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e9b12-224">![Сведения о пользователе](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Сведения о пользователе")</span><span class="sxs-lookup"><span data-stu-id="e9b12-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="e9b12-225">а.</span><span class="sxs-lookup"><span data-stu-id="e9b12-225">a.</span></span> <span data-ttu-id="e9b12-226">Введите в текстовые поля **First Name** (Имя), **Surname** (Фамилия), **User name (Email address)** (Имя пользователя (адрес электронной почты)) соответствующие данные действующей учетной записи AAD, которую нужно подготовить.</span><span class="sxs-lookup"><span data-stu-id="e9b12-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="e9b12-227">b.</span><span class="sxs-lookup"><span data-stu-id="e9b12-227">b.</span></span> <span data-ttu-id="e9b12-228">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-228">Click **Next**.</span></span>

4. <span data-ttu-id="e9b12-229">Чтобы добавить нового пользователя, следуйте указаниям на экране и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="e9b12-230">Вы можете использовать любые другие средства создания учетной записи пользователя TeamSeer или API-интерфейсы, предоставляемые TeamSeer, для подготовки учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9b12-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e9b12-231">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9b12-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e9b12-232">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="e9b12-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e9b12-234">**Чтобы назначить пользователя Britta Simon приложению TeamSeer, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e9b12-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="e9b12-235">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e9b12-237">В списке приложений выберите **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-237">In the applications list, select **TeamSeer**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="e9b12-239">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e9b12-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-241">Click **Add** button.</span></span> <span data-ttu-id="e9b12-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e9b12-244">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e9b12-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9b12-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e9b12-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9b12-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e9b12-247">Testing single sign-on</span></span>

<span data-ttu-id="e9b12-248">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="e9b12-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="e9b12-249">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9b12-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9b12-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e9b12-250">Additional resources</span></span>

* [<span data-ttu-id="e9b12-251">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9b12-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9b12-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9b12-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

