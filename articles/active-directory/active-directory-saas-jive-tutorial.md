---
title: "Руководство по интеграции Azure Active Directory с Jive | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="a0903-103">Руководство. Интеграция Azure Active Directory с Jive</span><span class="sxs-lookup"><span data-stu-id="a0903-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="a0903-104">В этом руководстве описано, как интегрировать Jive с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0903-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0903-105">Интеграция Azure AD с приложением Jive обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="a0903-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a0903-106">С помощью Azure AD вы можете контролировать доступ к Jive.</span><span class="sxs-lookup"><span data-stu-id="a0903-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="a0903-107">Вы можете включить автоматический вход пользователей в Jive (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0903-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0903-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a0903-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a0903-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0903-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0903-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a0903-110">Prerequisites</span></span>

<span data-ttu-id="a0903-111">Чтобы настроить интеграцию Azure AD с Jive, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a0903-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="a0903-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a0903-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0903-113">подписка Jive с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a0903-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a0903-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a0903-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a0903-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a0903-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0903-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a0903-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0903-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0903-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a0903-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a0903-118">Scenario description</span></span>
<span data-ttu-id="a0903-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a0903-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0903-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a0903-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0903-121">Добавление Jive из коллекции.</span><span class="sxs-lookup"><span data-stu-id="a0903-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="a0903-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0903-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="a0903-123">Добавление Jive из коллекции.</span><span class="sxs-lookup"><span data-stu-id="a0903-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="a0903-124">Чтобы настроить интеграцию Jive с Azure AD, необходимо добавить Jive из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a0903-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a0903-125">**Чтобы добавить Jive из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="a0903-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a0903-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a0903-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0903-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a0903-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a0903-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a0903-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a0903-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a0903-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a0903-133">В поле поиска введите **Jive**.</span><span class="sxs-lookup"><span data-stu-id="a0903-133">In the search box, type **Jive**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="a0903-135">На панели результатов выберите **Jive** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="a0903-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0903-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0903-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0903-138">В этом разделе описана настройка и проверка единого входа Azure AD в Jive с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0903-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a0903-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Jive соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0903-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="a0903-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Jive.</span><span class="sxs-lookup"><span data-stu-id="a0903-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="a0903-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Jive.</span><span class="sxs-lookup"><span data-stu-id="a0903-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="a0903-142">Чтобы настроить и проверить единый вход Azure AD в Jive, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="a0903-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a0903-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a0903-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a0903-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0903-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0903-145">**[Создание тестового пользователя Jive](#creating-a-jive-test-user)** требуется для того, чтобы в Jive существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0903-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0903-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0903-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0903-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a0903-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0903-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0903-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0903-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Jive.</span><span class="sxs-lookup"><span data-stu-id="a0903-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="a0903-150">**Чтобы настроить единый вход Azure AD в Jive, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="a0903-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="a0903-151">На портале Azure на странице интеграции с приложением **Jive** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a0903-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a0903-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a0903-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="a0903-155">В разделе **Домены и URL-адреса приложения Jive** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a0903-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="a0903-157">а.</span><span class="sxs-lookup"><span data-stu-id="a0903-157">a.</span></span> <span data-ttu-id="a0903-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="a0903-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="a0903-159">b.</span><span class="sxs-lookup"><span data-stu-id="a0903-159">b.</span></span> <span data-ttu-id="a0903-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="a0903-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0903-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a0903-161">These values are not the real.</span></span> <span data-ttu-id="a0903-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="a0903-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="a0903-163">Чтобы получить эти значения, обратитесь к [группе поддержки Jive](https://www.jivesoftware.com/services-support/).</span><span class="sxs-lookup"><span data-stu-id="a0903-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="a0903-164">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a0903-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="a0903-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a0903-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a0903-168">Чтобы настроить единый вход на стороне **Jive**, войдите в свой клиент Jive в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="a0903-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="a0903-169">В меню вверху щелкните**SAML**.</span><span class="sxs-lookup"><span data-stu-id="a0903-169">In the menu on the top, Click "**Saml**."</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="a0903-171">а.</span><span class="sxs-lookup"><span data-stu-id="a0903-171">a.</span></span> <span data-ttu-id="a0903-172">На вкладке **General** (Общие) установите флажок **Enabled** (Включено).</span><span class="sxs-lookup"><span data-stu-id="a0903-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="a0903-173">b.</span><span class="sxs-lookup"><span data-stu-id="a0903-173">b.</span></span> <span data-ttu-id="a0903-174">Нажмите кнопку**Save all saml settings**(Сохранить все параметры SAML).</span><span class="sxs-lookup"><span data-stu-id="a0903-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="a0903-175">Перейдите на вкладку**IdP Metadata**(Метаданные IdP).</span><span class="sxs-lookup"><span data-stu-id="a0903-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="a0903-177">а.</span><span class="sxs-lookup"><span data-stu-id="a0903-177">a.</span></span> <span data-ttu-id="a0903-178">Скопируйте содержимое скачанного XML-файла с метаданными и вставьте его в текстовое поле **Identity Provider (IDP) Metadata** (Метаданные поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="a0903-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="a0903-179">b.</span><span class="sxs-lookup"><span data-stu-id="a0903-179">b.</span></span> <span data-ttu-id="a0903-180">Нажмите кнопку**Save all saml settings**(Сохранить все параметры SAML).</span><span class="sxs-lookup"><span data-stu-id="a0903-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="a0903-181">Перейдите на вкладку**User Attribute Mapping**(Сопоставление атрибутов пользователей).</span><span class="sxs-lookup"><span data-stu-id="a0903-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="a0903-183">а.</span><span class="sxs-lookup"><span data-stu-id="a0903-183">a.</span></span> <span data-ttu-id="a0903-184">В текстовом поле **Email** (Электронная почта) скопируйте и вставьте имя атрибута значения **mail**.</span><span class="sxs-lookup"><span data-stu-id="a0903-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="a0903-185">b.</span><span class="sxs-lookup"><span data-stu-id="a0903-185">b.</span></span> <span data-ttu-id="a0903-186">В текстовом поле **First Name** (Имя) скопируйте и вставьте имя атрибута значения **givenname**.</span><span class="sxs-lookup"><span data-stu-id="a0903-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="a0903-187">c.</span><span class="sxs-lookup"><span data-stu-id="a0903-187">c.</span></span> <span data-ttu-id="a0903-188">В текстовом поле **Last Name** (Фамилия) скопируйте и вставьте имя атрибута значения **surname**.</span><span class="sxs-lookup"><span data-stu-id="a0903-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="a0903-189">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a0903-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a0903-190">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a0903-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a0903-191">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a0903-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0903-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0903-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0903-193">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0903-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a0903-195">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a0903-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a0903-196">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a0903-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0903-198">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a0903-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0903-200">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a0903-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0903-202">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a0903-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0903-204">а.</span><span class="sxs-lookup"><span data-stu-id="a0903-204">a.</span></span> <span data-ttu-id="a0903-205">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0903-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0903-206">b.</span><span class="sxs-lookup"><span data-stu-id="a0903-206">b.</span></span> <span data-ttu-id="a0903-207">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0903-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0903-208">c.</span><span class="sxs-lookup"><span data-stu-id="a0903-208">c.</span></span> <span data-ttu-id="a0903-209">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a0903-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a0903-210">d.</span><span class="sxs-lookup"><span data-stu-id="a0903-210">d.</span></span> <span data-ttu-id="a0903-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a0903-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="a0903-212">Создание тестового пользователя приложения Jive</span><span class="sxs-lookup"><span data-stu-id="a0903-212">Creating a Jive test user</span></span>

<span data-ttu-id="a0903-213">Обратитесь к [группе поддержки клиентов Jive](https://www.jivesoftware.com/services-support/), чтобы добавить пользователей на платформу Jive.</span><span class="sxs-lookup"><span data-stu-id="a0903-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a0903-214">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0903-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a0903-215">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Jive.</span><span class="sxs-lookup"><span data-stu-id="a0903-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a0903-217">**Чтобы назначить пользователя Britta Simon в Jive, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="a0903-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="a0903-218">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a0903-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a0903-220">В списке приложений выберите **Jive**.</span><span class="sxs-lookup"><span data-stu-id="a0903-220">In the applications list, select **Jive**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="a0903-222">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a0903-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a0903-224">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a0903-224">Click **Add** button.</span></span> <span data-ttu-id="a0903-225">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a0903-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a0903-227">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a0903-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a0903-228">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a0903-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0903-229">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a0903-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0903-230">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a0903-230">Testing single sign-on</span></span>

<span data-ttu-id="a0903-231">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a0903-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a0903-232">Щелкнув элемент Jive на панели доступа, вы автоматически войдете в приложение Jive.</span><span class="sxs-lookup"><span data-stu-id="a0903-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0903-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a0903-233">Additional resources</span></span>

* [<span data-ttu-id="a0903-234">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0903-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0903-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a0903-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a0903-236">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="a0903-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

