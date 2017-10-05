---
title: "Руководство по интеграции Azure Active Directory с Dropbox for Business | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="7045a-103">Руководство. Интеграция Azure Active Directory с Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="7045a-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="7045a-104">В этом руководстве описано, как интегрировать Dropbox for Business с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7045a-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7045a-105">Интеграция Dropbox for Business с Azure AD обеспечивает перечисленные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="7045a-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7045a-106">С помощью Azure AD вы можете контролировать доступ к приложению Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="7045a-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="7045a-107">Вы можете включить автоматический вход пользователей в Dropbox for Business (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7045a-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7045a-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7045a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7045a-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7045a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7045a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7045a-110">Prerequisites</span></span>

<span data-ttu-id="7045a-111">Чтобы настроить интеграцию Azure AD с Dropbox for Business, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="7045a-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="7045a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7045a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7045a-113">подписка Dropbox for Business с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7045a-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7045a-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7045a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7045a-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7045a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7045a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7045a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7045a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7045a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7045a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7045a-118">Scenario description</span></span>
<span data-ttu-id="7045a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7045a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7045a-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="7045a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7045a-121">Добавление Dropbox for Business из коллекции</span><span class="sxs-lookup"><span data-stu-id="7045a-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="7045a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7045a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="7045a-123">Добавление Dropbox for Business из коллекции</span><span class="sxs-lookup"><span data-stu-id="7045a-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="7045a-124">Чтобы настроить интеграцию Dropbox for Business с Azure AD, необходимо добавить Dropbox for Business из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7045a-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7045a-125">**Чтобы добавить Dropbox for Business из коллекции, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="7045a-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7045a-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7045a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7045a-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="7045a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7045a-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7045a-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7045a-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="7045a-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7045a-133">В поле поиска введите **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="7045a-133">In the search box, type **Dropbox for Business**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="7045a-135">В области результатов выберите **Dropbox for Business** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="7045a-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7045a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7045a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7045a-138">В этом разделе описана настройка и проверка единого входа Azure AD в Dropbox for Business с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7045a-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7045a-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Dropbox for Business соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7045a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="7045a-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="7045a-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="7045a-141">Чтобы установить эту связь, следует указать **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="7045a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="7045a-142">Чтобы настроить и проверить единый вход Azure AD в Dropbox for Business, вам потребуется выполнить действия в перечисленных ниже стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="7045a-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7045a-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7045a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7045a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7045a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7045a-145">**[Создание тестового пользователя Dropbox for Business](#creating-a-dropbox-for-business-test-user)** требуется для создания пользователя Britta Simon в Dropbox for Business, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7045a-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7045a-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7045a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7045a-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7045a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7045a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7045a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7045a-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="7045a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="7045a-150">**Чтобы настроить единый вход Azure AD в Dropbox for Business, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="7045a-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="7045a-151">На портале Azure на странице интеграции с приложением **Dropbox for Business** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7045a-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7045a-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="7045a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="7045a-155">В разделе **Домены и URL-адреса приложения Dropbox for Business** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="7045a-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="7045a-156">а.</span><span class="sxs-lookup"><span data-stu-id="7045a-156">a.</span></span> <span data-ttu-id="7045a-157">Войдите в клиент Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="7045a-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="7045a-158">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="7045a-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7045a-159">b.</span><span class="sxs-lookup"><span data-stu-id="7045a-159">b.</span></span> <span data-ttu-id="7045a-160">На панели навигации слева щелкните **Консоль администрирования**.</span><span class="sxs-lookup"><span data-stu-id="7045a-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="7045a-161">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="7045a-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7045a-162">c.</span><span class="sxs-lookup"><span data-stu-id="7045a-162">c.</span></span> <span data-ttu-id="7045a-163">В **консоли администрирования** выберите пункт **Проверка подлинности** в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="7045a-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="7045a-164">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="7045a-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7045a-165">г)</span><span class="sxs-lookup"><span data-stu-id="7045a-165">d.</span></span> <span data-ttu-id="7045a-166">В разделе **Единый вход** установите флажок **Включить единый вход** и нажмите кнопку **Дополнительно**, чтобы развернуть этот раздел.</span><span class="sxs-lookup"><span data-stu-id="7045a-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="7045a-167">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="7045a-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7045a-168">д.</span><span class="sxs-lookup"><span data-stu-id="7045a-168">e.</span></span> <span data-ttu-id="7045a-169">Скопируйте URL-адрес рядом с пунктом **Users can sign in by entering their email address or they can go directly to**(Пользователи могут входить, указывая адрес электронной почты, или напрямую переходить по адресу).</span><span class="sxs-lookup"><span data-stu-id="7045a-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="7045a-171">f.</span><span class="sxs-lookup"><span data-stu-id="7045a-171">f.</span></span> <span data-ttu-id="7045a-172">На портале Azure в текстовом поле **URL-адрес входа** вставьте URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="7045a-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="7045a-174">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="7045a-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7045a-175">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="7045a-175">This value is not real value.</span></span> <span data-ttu-id="7045a-176">Измените его на фактический URL-адрес входа, полученный в разделе "Единый вход".</span><span class="sxs-lookup"><span data-stu-id="7045a-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="7045a-177">Для получения этого значения обратитесь в [службу поддержки клиентов Dropbox for Business](https://www.dropbox.com/business/contact).</span><span class="sxs-lookup"><span data-stu-id="7045a-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="7045a-178">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7045a-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="7045a-180">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7045a-180">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7045a-182">В разделе **Настройка Dropbox for Business** щелкните **Настроить Dropbox for Business**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7045a-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7045a-183">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="7045a-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="7045a-185">Чтобы настроить единый вход на стороне **Dropbox for Business**, перейдите в клиент Dropbox for Business, а затем в разделе **Единый вход** на странице **Проверка подлинности** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="7045a-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="7045a-186">![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="7045a-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="7045a-187">а.</span><span class="sxs-lookup"><span data-stu-id="7045a-187">a.</span></span> <span data-ttu-id="7045a-188">Установите флажок **Обязательно**.</span><span class="sxs-lookup"><span data-stu-id="7045a-188">Click **Required**.</span></span>
   
    <span data-ttu-id="7045a-189">b.</span><span class="sxs-lookup"><span data-stu-id="7045a-189">b.</span></span> <span data-ttu-id="7045a-190">На портале Azure в окне **Настройка единого входа** скопируйте значение в поле **URL-адрес службы единого входа SAML** и вставьте его в текстовое поле **Sign-in URL** (URL-адрес для входа).</span><span class="sxs-lookup"><span data-stu-id="7045a-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="7045a-191">c.</span><span class="sxs-lookup"><span data-stu-id="7045a-191">c.</span></span> <span data-ttu-id="7045a-192">Щелкните **Choose certificate** (Выбрать сертификат), а затем выберите **файл сертификата в кодировке Base64**.</span><span class="sxs-lookup"><span data-stu-id="7045a-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="7045a-193">г)</span><span class="sxs-lookup"><span data-stu-id="7045a-193">d.</span></span> <span data-ttu-id="7045a-194">Щелкните **Сохранить изменения**, чтобы завершить настройку клиента Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="7045a-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="7045a-195">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="7045a-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7045a-196">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="7045a-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7045a-197">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="7045a-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7045a-198">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7045a-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="7045a-199">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7045a-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7045a-201">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7045a-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7045a-202">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7045a-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="7045a-204">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7045a-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7045a-206">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="7045a-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7045a-208">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7045a-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7045a-210">а.</span><span class="sxs-lookup"><span data-stu-id="7045a-210">a.</span></span> <span data-ttu-id="7045a-211">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7045a-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7045a-212">b.</span><span class="sxs-lookup"><span data-stu-id="7045a-212">b.</span></span> <span data-ttu-id="7045a-213">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7045a-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7045a-214">c.</span><span class="sxs-lookup"><span data-stu-id="7045a-214">c.</span></span> <span data-ttu-id="7045a-215">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="7045a-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7045a-216">d.</span><span class="sxs-lookup"><span data-stu-id="7045a-216">d.</span></span> <span data-ttu-id="7045a-217">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7045a-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="7045a-218">Создание тестового пользователя Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="7045a-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="7045a-219">В этом разделе вы создадите в Dropbox for Business пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7045a-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="7045a-220">Приложение Dropbox for Business поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7045a-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="7045a-221">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="7045a-221">There is no action item for you in this section.</span></span> <span data-ttu-id="7045a-222">Если пользователь в Dropbox for Business еще не существует, он создается при попытке доступа к приложению Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="7045a-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="7045a-223">Если вам нужно вручную создать пользователя, обратитесь в [службу поддержки клиентов Dropbox for Business](https://www.dropbox.com/business/contact).</span><span class="sxs-lookup"><span data-stu-id="7045a-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7045a-224">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7045a-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7045a-225">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Dropbox for Business, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="7045a-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7045a-227">**Чтобы назначить пользователя Britta Simon приложению Dropbox for Business, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="7045a-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="7045a-228">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7045a-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7045a-230">В списке приложений выберите **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="7045a-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="7045a-232">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7045a-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7045a-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7045a-234">Click **Add** button.</span></span> <span data-ttu-id="7045a-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7045a-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7045a-237">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7045a-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7045a-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7045a-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7045a-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7045a-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7045a-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7045a-240">Testing single sign-on</span></span>

<span data-ttu-id="7045a-241">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7045a-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7045a-242">При выборе плитки Dropbox for Business на панели доступа должна появиться страница входа приложения Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="7045a-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7045a-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7045a-243">Additional resources</span></span>

* [<span data-ttu-id="7045a-244">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7045a-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7045a-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7045a-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7045a-246">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="7045a-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

