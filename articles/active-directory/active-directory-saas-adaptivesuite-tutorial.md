---
title: "Руководство по интеграции Azure Active Directory с Adaptive Suite | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Adaptive Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="0c71b-103">Руководство. Интеграция Azure Active Directory с Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="0c71b-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="0c71b-104">В этом руководстве описано, как интегрировать Adaptive Suite с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c71b-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c71b-105">Интеграция приложения Adaptive Suite с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="0c71b-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0c71b-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0c71b-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="0c71b-107">Вы можете включить автоматический вход пользователей в Adaptive Suite (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c71b-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0c71b-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0c71b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0c71b-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0c71b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c71b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0c71b-110">Prerequisites</span></span>

<span data-ttu-id="0c71b-111">Чтобы настроить интеграцию Azure AD с Adaptive Suite, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="0c71b-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="0c71b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0c71b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c71b-113">подписка Adaptive Suite с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0c71b-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c71b-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0c71b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c71b-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="0c71b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c71b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0c71b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0c71b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c71b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c71b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0c71b-118">Scenario description</span></span>
<span data-ttu-id="0c71b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0c71b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c71b-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="0c71b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c71b-121">Добавление Adaptive Suite из коллекции.</span><span class="sxs-lookup"><span data-stu-id="0c71b-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="0c71b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c71b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="0c71b-123">Добавление Adaptive Suite из коллекции</span><span class="sxs-lookup"><span data-stu-id="0c71b-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="0c71b-124">Чтобы настроить интеграцию приложения Adaptive Suite с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0c71b-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0c71b-125">**Добавление приложения Adaptive Suite из коллекции**</span><span class="sxs-lookup"><span data-stu-id="0c71b-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0c71b-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0c71b-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0c71b-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0c71b-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0c71b-133">В поле поиска введите **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-133">In the search box, type **Adaptive Suite**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="0c71b-135">На панели результатов выберите **Adaptive Suite** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="0c71b-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0c71b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c71b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0c71b-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Adaptive Suite с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c71b-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0c71b-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в Adaptive Suite соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c71b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="0c71b-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0c71b-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="0c71b-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0c71b-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0c71b-142">Чтобы настроить и проверить единый вход Azure AD в Adaptive Suite, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0c71b-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0c71b-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="0c71b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0c71b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c71b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0c71b-145">**[Создание тестового пользователя Adaptive Suite](#creating-an-adaptive-suite-test-user)** требуется для создания в Adaptive Suite пользователя Britta Simon, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c71b-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0c71b-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c71b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0c71b-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0c71b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0c71b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c71b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0c71b-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0c71b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="0c71b-150">**Настройка единого входа Azure AD в Adaptive Suite**</span><span class="sxs-lookup"><span data-stu-id="0c71b-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="0c71b-151">На портале Azure на странице интеграции с приложением **Adaptive Suite** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0c71b-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="0c71b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="0c71b-155">В разделе **Домены и URL-адреса приложения Adaptive Suite** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="0c71b-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="0c71b-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`.</span><span class="sxs-lookup"><span data-stu-id="0c71b-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="0c71b-158">Этот адрес можно узнать на странице **Параметры единого входа SAML** клиента Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0c71b-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="0c71b-159">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0c71b-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="0c71b-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0c71b-161">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0c71b-163">В разделе **Настройка Adaptive Suite** щелкните **Настроить Adaptive Suite**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0c71b-164">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Quick Reference** (Краткий справочник).</span><span class="sxs-lookup"><span data-stu-id="0c71b-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="0c71b-166">В другом окне веб-браузера войдите на корпоративный сайт Adaptive Suite с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="0c71b-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="0c71b-167">Откройте страницу **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="0c71b-168">![Администратор](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="0c71b-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="0c71b-169">В разделе **Users and Roles** (Пользователи и роли) щелкните **Manage SAML SSO Settings** (Управление параметрами единого входа SAML).</span><span class="sxs-lookup"><span data-stu-id="0c71b-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="0c71b-170">![Управление параметрами единого входа SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Управление параметрами единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="0c71b-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="0c71b-171">На странице **SAML SSO Settings** (Параметры единого входа SAML) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0c71b-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="0c71b-172">![Параметры единого входа SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="0c71b-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="0c71b-173">а.</span><span class="sxs-lookup"><span data-stu-id="0c71b-173">a.</span></span> <span data-ttu-id="0c71b-174">Введите имя конфигурации в текстовое поле **Identity provider name** (Имя поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="0c71b-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="0c71b-175">b.</span><span class="sxs-lookup"><span data-stu-id="0c71b-175">b.</span></span> <span data-ttu-id="0c71b-176">Вставьте значение **идентификатора сущности SAML**, скопированное с портала Azure, в текстовое поле **Identity provider Entity ID** (Идентификатор сущности поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="0c71b-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="0c71b-177">c.</span><span class="sxs-lookup"><span data-stu-id="0c71b-177">c.</span></span> <span data-ttu-id="0c71b-178">Вставьте значение **URL-адреса службы единого входа SAML**, скопированное с портала Azure, в текстовое поле **Identity provider SSO URL** (URL-адрес единого входа поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="0c71b-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="0c71b-179">г)</span><span class="sxs-lookup"><span data-stu-id="0c71b-179">d.</span></span> <span data-ttu-id="0c71b-180">Вставьте значение **URL-адреса службы единого входа SAML**, скопированное с портала Azure, в текстовое поле **Custom logout URL** (Пользовательский URL-адрес для выхода).</span><span class="sxs-lookup"><span data-stu-id="0c71b-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="0c71b-181">д.</span><span class="sxs-lookup"><span data-stu-id="0c71b-181">e.</span></span> <span data-ttu-id="0c71b-182">Чтобы отправить загруженный сертификат, нажмите кнопку **Выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="0c71b-183">f.</span><span class="sxs-lookup"><span data-stu-id="0c71b-183">f.</span></span> <span data-ttu-id="0c71b-184">Выберите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="0c71b-184">Select the following, for:</span></span>
    * <span data-ttu-id="0c71b-185">Для параметра **SAML user id** (Идентификатор пользователя SAML) выберите значение **User’s Adaptive Insights user name** (Имя пользователя Adaptive Insights).</span><span class="sxs-lookup"><span data-stu-id="0c71b-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="0c71b-186">Для параметра **SAML user id location** (Расположение идентификатора пользователя SAML) выберите значение **User id in NameID of Subject** (Идентификатор пользователя из NameID в Subject).</span><span class="sxs-lookup"><span data-stu-id="0c71b-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="0c71b-187">Для параметра **SAML NameID format** (Формат NameID SAML) выберите значение **Адрес электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="0c71b-188">Для параметра **Включить SAML** выберите значение **Allow SAML SSO and direct Adaptive Insights login** (Разрешить единый вход SAML и прямой вход Adaptive Insights).</span><span class="sxs-lookup"><span data-stu-id="0c71b-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="0c71b-189">g.</span><span class="sxs-lookup"><span data-stu-id="0c71b-189">g.</span></span> <span data-ttu-id="0c71b-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0c71b-191">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="0c71b-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0c71b-192">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0c71b-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0c71b-193">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0c71b-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0c71b-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c71b-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="0c71b-195">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c71b-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0c71b-197">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0c71b-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0c71b-198">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0c71b-200">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0c71b-202">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0c71b-204">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0c71b-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0c71b-206">а.</span><span class="sxs-lookup"><span data-stu-id="0c71b-206">a.</span></span> <span data-ttu-id="0c71b-207">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c71b-208">b.</span><span class="sxs-lookup"><span data-stu-id="0c71b-208">b.</span></span> <span data-ttu-id="0c71b-209">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0c71b-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0c71b-210">c.</span><span class="sxs-lookup"><span data-stu-id="0c71b-210">c.</span></span> <span data-ttu-id="0c71b-211">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0c71b-212">d.</span><span class="sxs-lookup"><span data-stu-id="0c71b-212">d.</span></span> <span data-ttu-id="0c71b-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="0c71b-214">Создание тестового пользователя Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="0c71b-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="0c71b-215">Чтобы пользователи Azure AD могли выполнять вход в Adaptive Suite, их следует подготовить в Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0c71b-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="0c71b-216">В случае Adaptive Suite подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="0c71b-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="0c71b-217">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0c71b-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="0c71b-218">Выполните вход на корпоративный веб-сайт **Adaptive Suite** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="0c71b-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="0c71b-219">Перейдите на страницу **Admin**(Администратор).</span><span class="sxs-lookup"><span data-stu-id="0c71b-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="0c71b-220">![Администратор](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="0c71b-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="0c71b-221">В разделе **Users and Roles** (Пользователи и роли) щелкните **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="0c71b-222">![Добавление пользователя](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="0c71b-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="0c71b-223">В разделе **New User** (Новый пользователь) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0c71b-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="0c71b-224">![Отправка](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Отправка")</span><span class="sxs-lookup"><span data-stu-id="0c71b-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="0c71b-225">а.</span><span class="sxs-lookup"><span data-stu-id="0c71b-225">a.</span></span> <span data-ttu-id="0c71b-226">Введите в текстовые поля **Name** (Имя), **Login** (Имя для входа), **Email** (Адрес электронной почты) и **Password** (Пароль) соответствующие данные действующего пользователя Azure Active Directory, для которого выполняется подготовка.</span><span class="sxs-lookup"><span data-stu-id="0c71b-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="0c71b-227">b.</span><span class="sxs-lookup"><span data-stu-id="0c71b-227">b.</span></span> <span data-ttu-id="0c71b-228">Выберите **Роль**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="0c71b-229">c.</span><span class="sxs-lookup"><span data-stu-id="0c71b-229">c.</span></span> <span data-ttu-id="0c71b-230">Нажмите кнопку **Submit**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="0c71b-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="0c71b-231">Вы можете использовать любые другие средства создания учетной записи пользователя Adaptive Suite или API, предоставляемые Adaptive Suite для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="0c71b-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0c71b-232">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c71b-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0c71b-233">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0c71b-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0c71b-235">**Назначение пользователя Britta Simon приложению Adaptive Suite**</span><span class="sxs-lookup"><span data-stu-id="0c71b-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="0c71b-236">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0c71b-238">В списке приложений выберите **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="0c71b-240">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0c71b-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-242">Click **Add** button.</span></span> <span data-ttu-id="0c71b-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0c71b-245">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0c71b-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0c71b-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0c71b-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0c71b-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0c71b-248">Testing single sign-on</span></span>

<span data-ttu-id="0c71b-249">Цель этого раздела — проверить конфигурацию единого входа Microsoft Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="0c71b-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="0c71b-250">Щелкнув плитку Adaptive Suite на панели доступа, вы автоматически войдете в приложение Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="0c71b-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0c71b-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0c71b-251">Additional resources</span></span>

* [<span data-ttu-id="0c71b-252">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c71b-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c71b-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c71b-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

