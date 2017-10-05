---
title: "Руководство по интеграции Azure Active Directory с Image Relay | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в Image Relay."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="107ec-103">Руководство по интеграции Azure Active Directory с приложением Image Relay</span><span class="sxs-lookup"><span data-stu-id="107ec-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="107ec-104">В этом учебнике описано, как интегрировать Image Relay с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="107ec-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="107ec-105">Интеграция Image Relay с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="107ec-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="107ec-106">С помощью Azure AD вы можете контролировать доступ к Image Relay.</span><span class="sxs-lookup"><span data-stu-id="107ec-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="107ec-107">Вы можете включить автоматический вход пользователей в Image Relay (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="107ec-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="107ec-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="107ec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="107ec-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="107ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="107ec-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="107ec-110">Prerequisites</span></span>

<span data-ttu-id="107ec-111">Чтобы настроить интеграцию Azure AD с Image Relay, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="107ec-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="107ec-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="107ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="107ec-113">подписка Image Relay с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="107ec-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="107ec-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="107ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="107ec-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="107ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="107ec-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="107ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="107ec-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="107ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="107ec-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="107ec-118">Scenario description</span></span>
<span data-ttu-id="107ec-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="107ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="107ec-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="107ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="107ec-121">Добавление Image Relay из коллекции.</span><span class="sxs-lookup"><span data-stu-id="107ec-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="107ec-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="107ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="107ec-123">Добавление Image Relay из коллекции</span><span class="sxs-lookup"><span data-stu-id="107ec-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="107ec-124">Чтобы настроить интеграцию Image Relay с Azure AD, необходимо добавить Image Relay из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="107ec-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="107ec-125">**Чтобы добавить Image Relay из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="107ec-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="107ec-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="107ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="107ec-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="107ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="107ec-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="107ec-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="107ec-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="107ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="107ec-133">В поле поиска введите **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="107ec-133">In the search box, type **Image Relay**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="107ec-135">На панели результатов выберите **Image Relay** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="107ec-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="107ec-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="107ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="107ec-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Image Relay для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="107ec-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="107ec-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Image Relay соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="107ec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="107ec-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Image Relay.</span><span class="sxs-lookup"><span data-stu-id="107ec-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="107ec-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Image Relay.</span><span class="sxs-lookup"><span data-stu-id="107ec-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="107ec-142">Чтобы настроить и проверить единый вход Azure AD в Image Relay, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="107ec-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="107ec-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="107ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="107ec-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="107ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="107ec-145">**[Создание тестового пользователя Image Relay](#creating-an-image-relay-test-user)** требуется для создания пользователя Britta Simon в Image Relay, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="107ec-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="107ec-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="107ec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="107ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="107ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="107ec-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="107ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="107ec-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Image Relay.</span><span class="sxs-lookup"><span data-stu-id="107ec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="107ec-150">**Чтобы настроить единый вход Azure AD в Image Relay, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="107ec-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="107ec-151">На портале Azure на странице интеграции с приложением **Image Relay** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="107ec-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="107ec-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="107ec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="107ec-155">В разделе **Домены и URL-адреса Image Relay** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="107ec-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="107ec-157">а.</span><span class="sxs-lookup"><span data-stu-id="107ec-157">a.</span></span> <span data-ttu-id="107ec-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="107ec-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="107ec-159">b.</span><span class="sxs-lookup"><span data-stu-id="107ec-159">b.</span></span> <span data-ttu-id="107ec-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="107ec-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="107ec-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="107ec-161">These values are not real.</span></span> <span data-ttu-id="107ec-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="107ec-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="107ec-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Image Relay](http://support.imagerelay.com/).</span><span class="sxs-lookup"><span data-stu-id="107ec-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="107ec-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="107ec-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="107ec-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="107ec-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="107ec-168">В разделе **Настройка Image Relay** щелкните **Настроить Image Relay**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="107ec-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="107ec-169">Скопируйте **URL-адрес службы выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="107ec-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="107ec-171">В другом окне браузера войдите на сайт компании Image Relay с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="107ec-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="107ec-172">На панели инструментов вверху экрана выберите рабочую нагрузку **Users & Permissions** (Пользователи и разрешения).</span><span class="sxs-lookup"><span data-stu-id="107ec-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="107ec-174">Щелкните **Создать новое разрешение**.</span><span class="sxs-lookup"><span data-stu-id="107ec-174">Click **Create New Permission**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="107ec-176">В рабочей нагрузке **Single Sign On Settings** (Параметры единого входа) установите флажок **This Group can only sign-in via Single Sign On** (Эта группа может входить только через единый вход) и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="107ec-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="107ec-178">Откройте **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="107ec-178">Go to **Account Settings**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="107ec-180">Выберите рабочую нагрузку **Параметры единого входа** .</span><span class="sxs-lookup"><span data-stu-id="107ec-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="107ec-182">В диалоговом окне **SAML Settings** (Параметры SAML) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="107ec-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="107ec-184">а.</span><span class="sxs-lookup"><span data-stu-id="107ec-184">a.</span></span> <span data-ttu-id="107ec-185">В текстовом поле **URL-адрес входа** вставьте значение **URL-адреса службы единого входа**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="107ec-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="107ec-186">b.</span><span class="sxs-lookup"><span data-stu-id="107ec-186">b.</span></span> <span data-ttu-id="107ec-187">В текстовом поле **URL-адрес выхода** вставьте значение **URL-адреса службы единого выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="107ec-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="107ec-188">c.</span><span class="sxs-lookup"><span data-stu-id="107ec-188">c.</span></span> <span data-ttu-id="107ec-189">В поле **Name Id Format** (Формат ИД имени) выберите **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="107ec-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="107ec-190">d.</span><span class="sxs-lookup"><span data-stu-id="107ec-190">d.</span></span> <span data-ttu-id="107ec-191">В разделе **Binding Options for Requests from the Service Provider (Image Relay)** (Обязательные параметры для запросов от поставщика услуг (Image Relay)) выберите **POST Binding** (Привязка POST).</span><span class="sxs-lookup"><span data-stu-id="107ec-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="107ec-192">д.</span><span class="sxs-lookup"><span data-stu-id="107ec-192">e.</span></span> <span data-ttu-id="107ec-193">В разделе **Сертификат X.509** щелкните **Обновить сертификат**.</span><span class="sxs-lookup"><span data-stu-id="107ec-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="107ec-195">Е.</span><span class="sxs-lookup"><span data-stu-id="107ec-195">f.</span></span> <span data-ttu-id="107ec-196">Откройте скачанный сертификат в блокноте, а затем скопируйте и вставьте его содержимое в текстовое поле X.509 Certificate (Сертификат X.509).</span><span class="sxs-lookup"><span data-stu-id="107ec-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="107ec-198">ж.</span><span class="sxs-lookup"><span data-stu-id="107ec-198">g.</span></span> <span data-ttu-id="107ec-199">В разделе **Just-In-Time User Provisioning** (JIT-подготовка пользователей) выберите **Enable Just-In-Time User Provisioning** (Включить JIT-подготовку пользователей).</span><span class="sxs-lookup"><span data-stu-id="107ec-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="107ec-201">h.</span><span class="sxs-lookup"><span data-stu-id="107ec-201">h.</span></span> <span data-ttu-id="107ec-202">Выберите группу разрешений (например, **SSO Basic**(Базовый единый вход)), которой будет разрешено выполнять вход только через службу единого входа.</span><span class="sxs-lookup"><span data-stu-id="107ec-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="107ec-204">i.</span><span class="sxs-lookup"><span data-stu-id="107ec-204">i.</span></span> <span data-ttu-id="107ec-205">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="107ec-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="107ec-206">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="107ec-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="107ec-207">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="107ec-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="107ec-208">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="107ec-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="107ec-209">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="107ec-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="107ec-210">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="107ec-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="107ec-212">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="107ec-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="107ec-213">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="107ec-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="107ec-215">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="107ec-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="107ec-217">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="107ec-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="107ec-219">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="107ec-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="107ec-221">а.</span><span class="sxs-lookup"><span data-stu-id="107ec-221">a.</span></span> <span data-ttu-id="107ec-222">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="107ec-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="107ec-223">b.</span><span class="sxs-lookup"><span data-stu-id="107ec-223">b.</span></span> <span data-ttu-id="107ec-224">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="107ec-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="107ec-225">c.</span><span class="sxs-lookup"><span data-stu-id="107ec-225">c.</span></span> <span data-ttu-id="107ec-226">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="107ec-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="107ec-227">d.</span><span class="sxs-lookup"><span data-stu-id="107ec-227">d.</span></span> <span data-ttu-id="107ec-228">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="107ec-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="107ec-229">Создание тестового пользователя Image Relay</span><span class="sxs-lookup"><span data-stu-id="107ec-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="107ec-230">Цель этого раздела — создать пользователя с именем Britta Simon в Image Relay.</span><span class="sxs-lookup"><span data-stu-id="107ec-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="107ec-231">**Чтобы создать пользователя с именем Britta Simon в Image Relay, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="107ec-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="107ec-232">Войдите на cайт компании Image Relay в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="107ec-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="107ec-233">Откройте раздел **Users & Permissions** (Пользователи и разрешения) и выберите параметр **Create SSO User** (Создать пользователя единого входа).</span><span class="sxs-lookup"><span data-stu-id="107ec-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="107ec-235">Введите **Адрес электронной почты**, **Имя**, **Фамилию** и **Организацию** пользователя, которого нужно подготовить, и выберите группу разрешений (например, "Базовый единый вход"). Эта группа сможет выполнять вход только с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="107ec-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="107ec-237">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="107ec-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="107ec-238">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="107ec-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="107ec-239">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к Image Relay.</span><span class="sxs-lookup"><span data-stu-id="107ec-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="107ec-241">**Чтобы назначить пользователя Britta Simon в Image Relay, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="107ec-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="107ec-242">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="107ec-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="107ec-244">В списке приложений выберите **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="107ec-244">In the applications list, select **Image Relay**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="107ec-246">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="107ec-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="107ec-248">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="107ec-248">Click **Add** button.</span></span> <span data-ttu-id="107ec-249">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="107ec-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="107ec-251">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="107ec-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="107ec-252">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="107ec-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="107ec-253">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="107ec-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="107ec-254">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="107ec-254">Testing single sign-on</span></span>

<span data-ttu-id="107ec-255">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="107ec-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="107ec-256">Щелкнув плитку Image Relay на панели доступа, вы автоматически войдете в приложение Image Relay.</span><span class="sxs-lookup"><span data-stu-id="107ec-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="107ec-257">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="107ec-257">Additional resources</span></span>

* [<span data-ttu-id="107ec-258">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="107ec-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="107ec-259">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="107ec-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

