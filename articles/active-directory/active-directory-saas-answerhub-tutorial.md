---
title: "Руководство. Интеграция Azure Active Directory с AnswerHub | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="70b12-103">Руководство. Интеграция Azure Active Directory с AnswerHub</span><span class="sxs-lookup"><span data-stu-id="70b12-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="70b12-104">В этом руководстве описано, как интегрировать AnswerHub с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70b12-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70b12-105">Интеграция Azure AD с AnswerHub обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="70b12-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="70b12-106">С помощью Azure AD вы можете контролировать доступ к AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="70b12-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="70b12-107">Вы можете включить автоматический вход пользователей в AnswerHub (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70b12-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70b12-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="70b12-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="70b12-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70b12-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70b12-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="70b12-110">Prerequisites</span></span>

<span data-ttu-id="70b12-111">Чтобы настроить интеграцию Azure AD с AnswerHub, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="70b12-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="70b12-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="70b12-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70b12-113">подписка AnswerHub с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="70b12-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70b12-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="70b12-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70b12-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="70b12-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70b12-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="70b12-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70b12-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70b12-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70b12-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="70b12-118">Scenario description</span></span>
<span data-ttu-id="70b12-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="70b12-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70b12-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="70b12-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70b12-121">Добавление AnswerHub из коллекции</span><span class="sxs-lookup"><span data-stu-id="70b12-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="70b12-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b12-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="70b12-123">Добавление AnswerHub из коллекции</span><span class="sxs-lookup"><span data-stu-id="70b12-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="70b12-124">Чтобы настроить интеграцию AnswerHub с Azure AD, необходимо добавить AnswerHub из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="70b12-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="70b12-125">**Чтобы добавить AnswerHub из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="70b12-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="70b12-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70b12-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70b12-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="70b12-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="70b12-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="70b12-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="70b12-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="70b12-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="70b12-133">В поле поиска введите **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="70b12-133">In the search box, type **AnswerHub**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="70b12-135">На панели результатов выберите **AnswerHub** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="70b12-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70b12-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b12-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70b12-138">В этом разделе описана настройка и проверка единого входа Azure AD в AnswerHub с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70b12-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="70b12-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в AnswerHub соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70b12-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="70b12-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="70b12-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="70b12-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="70b12-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="70b12-142">Чтобы настроить и проверить единый вход Azure AD в AnswerHub, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="70b12-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="70b12-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="70b12-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="70b12-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70b12-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70b12-145">**[Создание тестового пользователя AnswerHub](#creating-an-answerhub-test-user)** нужно для того, чтобы в AnswerHub также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70b12-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="70b12-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70b12-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70b12-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="70b12-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70b12-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b12-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70b12-149">В данном разделе описано, как включить единый вход в Azure AD на портале Azure и настроить его в приложении AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="70b12-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="70b12-150">**Чтобы настроить единый вход Azure AD в AnswerHub, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="70b12-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="70b12-151">На портале Azure на странице интеграции с приложением **AnswerHub** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="70b12-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="70b12-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="70b12-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="70b12-155">В разделе **Домены и URL-адреса приложения AnswerHub** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="70b12-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="70b12-157">а.</span><span class="sxs-lookup"><span data-stu-id="70b12-157">a.</span></span> <span data-ttu-id="70b12-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="70b12-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="70b12-159">b.</span><span class="sxs-lookup"><span data-stu-id="70b12-159">b.</span></span> <span data-ttu-id="70b12-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="70b12-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70b12-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="70b12-161">These values are not real.</span></span> <span data-ttu-id="70b12-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="70b12-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="70b12-163">Чтобы получить эти значения, обратитесь к [группе поддержки AnswerHub](mailto:success@answerhub.com).</span><span class="sxs-lookup"><span data-stu-id="70b12-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="70b12-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="70b12-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="70b12-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="70b12-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="70b12-168">В разделе **Настройка AnswerHub** щелкните **Настроить AnswerHub**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="70b12-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="70b12-169">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="70b12-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="70b12-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт AnswerHub в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="70b12-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="70b12-172">Если вам нужна помощь в настройке AnswerHub, обратитесь в [службу поддержки AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="70b12-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="70b12-173">Перейдите в раздел **Administration**(Администрирование).</span><span class="sxs-lookup"><span data-stu-id="70b12-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="70b12-174">Откройте вкладку **User and Group** (Пользователь и группа).</span><span class="sxs-lookup"><span data-stu-id="70b12-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="70b12-175">В разделе **Social Settings** (Параметры социальных сетей) в области навигации слева выберите пункт **SAML Setup** (Настройка SAML).</span><span class="sxs-lookup"><span data-stu-id="70b12-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="70b12-176">Откройте вкладку **IDP Config** (Настройка IDP).</span><span class="sxs-lookup"><span data-stu-id="70b12-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="70b12-177">На вкладке **IDP Config** (Настройка IDP) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="70b12-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="70b12-178">![Настройка SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="70b12-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="70b12-179">а.</span><span class="sxs-lookup"><span data-stu-id="70b12-179">a.</span></span> <span data-ttu-id="70b12-180">В текстовое поле **IDP Login URL** (URL-адрес входа IdP) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="70b12-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="70b12-181">b.</span><span class="sxs-lookup"><span data-stu-id="70b12-181">b.</span></span> <span data-ttu-id="70b12-182">В текстовое поле **IDP Logout URL** (URL-адрес выхода IdP) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="70b12-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="70b12-183">c.</span><span class="sxs-lookup"><span data-stu-id="70b12-183">c.</span></span> <span data-ttu-id="70b12-184">В текстовое поле **IDP Name Identifier Format** (Формат идентификатора имени IdP) введите значение идентификатора имени пользователя, выбранное на портале Azure в разделе **Атрибуты пользователя**.</span><span class="sxs-lookup"><span data-stu-id="70b12-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="70b12-185">г)</span><span class="sxs-lookup"><span data-stu-id="70b12-185">d.</span></span> <span data-ttu-id="70b12-186">Щелкните **Ключи и сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="70b12-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="70b12-187">На вкладке «Ключи и сертификаты» выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="70b12-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="70b12-188">![Ключи и сертификаты](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Ключи и сертификаты")</span><span class="sxs-lookup"><span data-stu-id="70b12-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="70b12-189">а.</span><span class="sxs-lookup"><span data-stu-id="70b12-189">a.</span></span> <span data-ttu-id="70b12-190">Откройте в Блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **IDP Public Key (x509 Format)** (Открытый ключ IdP (формат x509)).</span><span class="sxs-lookup"><span data-stu-id="70b12-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="70b12-191">b.</span><span class="sxs-lookup"><span data-stu-id="70b12-191">b.</span></span> <span data-ttu-id="70b12-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="70b12-192">Click **Save**.</span></span>

14. <span data-ttu-id="70b12-193">На вкладке **IDP Config** (Настройка IDP) нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="70b12-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="70b12-194">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="70b12-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="70b12-195">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="70b12-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="70b12-196">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="70b12-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70b12-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b12-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="70b12-198">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70b12-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="70b12-200">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="70b12-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="70b12-201">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70b12-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70b12-203">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="70b12-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70b12-205">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="70b12-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70b12-207">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="70b12-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70b12-209">а.</span><span class="sxs-lookup"><span data-stu-id="70b12-209">a.</span></span> <span data-ttu-id="70b12-210">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70b12-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70b12-211">b.</span><span class="sxs-lookup"><span data-stu-id="70b12-211">b.</span></span> <span data-ttu-id="70b12-212">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="70b12-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70b12-213">c.</span><span class="sxs-lookup"><span data-stu-id="70b12-213">c.</span></span> <span data-ttu-id="70b12-214">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="70b12-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="70b12-215">d.</span><span class="sxs-lookup"><span data-stu-id="70b12-215">d.</span></span> <span data-ttu-id="70b12-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="70b12-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="70b12-217">Создание тестового пользователя AnswerHub</span><span class="sxs-lookup"><span data-stu-id="70b12-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="70b12-218">Чтобы пользователи Azure AD могли выполнять вход в AnswerHub, они должны быть подготовлены для AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="70b12-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="70b12-219">В случае с AnswerHub подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="70b12-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="70b12-220">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="70b12-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="70b12-221">Выполните вход на корпоративном веб-сайте **AnswerHub** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="70b12-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="70b12-222">Перейдите в раздел **Administration**(Администрирование).</span><span class="sxs-lookup"><span data-stu-id="70b12-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="70b12-223">Откройте вкладку **Users & Groups** (Пользователи и группы).</span><span class="sxs-lookup"><span data-stu-id="70b12-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="70b12-224">В разделе **Manage Users** (Управление пользователями) в области навигации слева выберите пункт **Create or import users** (Создать или импортировать пользователей).</span><span class="sxs-lookup"><span data-stu-id="70b12-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="70b12-225">![Пользователи и группы](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Пользователи и группы")</span><span class="sxs-lookup"><span data-stu-id="70b12-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="70b12-226">Введите в текстовые поля **Email address** (Адрес электронной почты), **Username** (Имя пользователя) и **Password** (Пароль) соответствующие данные действующей учетной записи Azure Active Directory, которую нужно подготовить, и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="70b12-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="70b12-227">Вы можете использовать любые другие средства создания учетной записи пользователя AnswerHub или API, предоставляемые AnswerHub для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="70b12-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="70b12-228">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="70b12-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="70b12-229">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="70b12-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="70b12-231">**Чтобы назначить пользователя Britta Simon в AnswerHub, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="70b12-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="70b12-232">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="70b12-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="70b12-234">Из списка приложений выберите **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="70b12-234">In the applications list, select **AnswerHub**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="70b12-236">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="70b12-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="70b12-238">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="70b12-238">Click **Add** button.</span></span> <span data-ttu-id="70b12-239">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="70b12-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="70b12-241">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="70b12-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="70b12-242">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="70b12-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70b12-243">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="70b12-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70b12-244">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="70b12-244">Testing single sign-on</span></span>

<span data-ttu-id="70b12-245">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="70b12-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="70b12-246">Щелкнув элемент "AnswerHub" на панели доступа, вы автоматически войдете в приложение Anaplan.</span><span class="sxs-lookup"><span data-stu-id="70b12-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="70b12-247">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="70b12-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70b12-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="70b12-248">Additional resources</span></span>

* [<span data-ttu-id="70b12-249">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70b12-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70b12-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="70b12-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

