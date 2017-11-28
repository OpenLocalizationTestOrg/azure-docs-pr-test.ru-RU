---
title: "Руководство по интеграции Azure Active Directory с Halogen Software | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Halogen Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="724b5-103">Учебник. Интеграция Azure Active Directory с Halogen Software</span><span class="sxs-lookup"><span data-stu-id="724b5-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="724b5-104">В этом руководстве описано, как интегрировать Halogen Software с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="724b5-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="724b5-105">Интеграция Halogen Software с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="724b5-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="724b5-106">С помощью Azure AD вы можете контролировать доступ к Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="724b5-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="724b5-107">Вы можете включить автоматический вход пользователей в Halogen Software (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="724b5-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="724b5-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="724b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="724b5-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="724b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="724b5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="724b5-110">Prerequisites</span></span>

<span data-ttu-id="724b5-111">Чтобы настроить интеграцию Azure AD с Halogen Software, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="724b5-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="724b5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="724b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="724b5-113">подписка Halogen Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="724b5-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="724b5-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="724b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="724b5-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="724b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="724b5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="724b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="724b5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="724b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="724b5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="724b5-118">Scenario description</span></span>

<span data-ttu-id="724b5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="724b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="724b5-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="724b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="724b5-121">Добавление Halogen Software из коллекции.</span><span class="sxs-lookup"><span data-stu-id="724b5-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="724b5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="724b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="724b5-123">Добавление Halogen Software из коллекции.</span><span class="sxs-lookup"><span data-stu-id="724b5-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="724b5-124">Чтобы настроить интеграцию Halogen Software с Azure AD, вам потребуется добавить Halogen Software из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="724b5-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="724b5-125">**Чтобы добавить Halogen Software из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="724b5-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="724b5-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="724b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="724b5-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="724b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="724b5-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="724b5-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="724b5-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="724b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="724b5-133">В поле поиска введите **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="724b5-133">In the search box, type **Halogen Software**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="724b5-135">В области результатов выберите **Halogen Software** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="724b5-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="724b5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="724b5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="724b5-138">В этом разделе описана настройка и проверка единого входа Azure AD в Halogen Software для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="724b5-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="724b5-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Halogen Software соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="724b5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="724b5-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="724b5-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="724b5-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="724b5-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="724b5-142">Чтобы настроить и проверить единый вход в Azure AD в Halogen Software, вам потребуется выполнить действия в следующих блоках:</span><span class="sxs-lookup"><span data-stu-id="724b5-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="724b5-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="724b5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="724b5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="724b5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="724b5-145">**[Создание тестового пользователя Halogen Software](#creating-a-halogen-software-test-user)** требуется для создания дублирующего Britta Simon пользователя в Halogen Software, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="724b5-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="724b5-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="724b5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="724b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="724b5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="724b5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="724b5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="724b5-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="724b5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="724b5-150">**Чтобы настроить единый вход в Azure AD с помощью Halogen Software, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="724b5-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="724b5-151">На портале Azure на странице интеграции с приложением **Halogen Software** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="724b5-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="724b5-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="724b5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="724b5-155">В разделе **Домены и URL-адреса Halogen Software** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="724b5-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="724b5-157">а.</span><span class="sxs-lookup"><span data-stu-id="724b5-157">a.</span></span> <span data-ttu-id="724b5-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="724b5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="724b5-159">b.</span><span class="sxs-lookup"><span data-stu-id="724b5-159">b.</span></span> <span data-ttu-id="724b5-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="724b5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="724b5-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="724b5-161">These values are not real.</span></span> <span data-ttu-id="724b5-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="724b5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="724b5-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Halogen Software](https://support.halogensoftware.com/).</span><span class="sxs-lookup"><span data-stu-id="724b5-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="724b5-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="724b5-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="724b5-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="724b5-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="724b5-168">В отдельном окне браузера войдите в приложение **Halogen Software** под учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="724b5-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="724b5-169">Откройте вкладку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="724b5-169">Click the **Options** tab.</span></span> 
   
    ![Что такое Azure AD Connect?][12]

8. <span data-ttu-id="724b5-171">На панели навигации слева щелкните **Настройка SAML**.</span><span class="sxs-lookup"><span data-stu-id="724b5-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Что такое Azure AD Connect?][13]

9. <span data-ttu-id="724b5-173">На странице **Настройка SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="724b5-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![Что такое Azure AD Connect?][14]

     <span data-ttu-id="724b5-175">а.</span><span class="sxs-lookup"><span data-stu-id="724b5-175">a.</span></span> <span data-ttu-id="724b5-176">В качестве значения поля **Уникальный идентификатор** выберите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="724b5-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="724b5-177">b.</span><span class="sxs-lookup"><span data-stu-id="724b5-177">b.</span></span> <span data-ttu-id="724b5-178">В качестве значения поля **Unique Identifier Maps To** (Уникальный идентификатор сопоставляется с) выберите **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="724b5-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="724b5-179">c.</span><span class="sxs-lookup"><span data-stu-id="724b5-179">c.</span></span> <span data-ttu-id="724b5-180">Для отправки скачанного файла метаданных нажмите кнопку **Обзор**, чтобы выбрать файл, а затем щелкните **Отправить файл**.</span><span class="sxs-lookup"><span data-stu-id="724b5-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="724b5-181">d.</span><span class="sxs-lookup"><span data-stu-id="724b5-181">d.</span></span> <span data-ttu-id="724b5-182">Чтобы проверить конфигурацию, нажмите кнопку **Запустить тест**.</span><span class="sxs-lookup"><span data-stu-id="724b5-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="724b5-183">Подождите, пока не появится сообщение "*Проверка SAML завершена. Закройте это окно*".</span><span class="sxs-lookup"><span data-stu-id="724b5-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="724b5-184">Закройте окно браузера.</span><span class="sxs-lookup"><span data-stu-id="724b5-184">Then, close the opened browser window.</span></span> <span data-ttu-id="724b5-185">Флажок **Включить SAML** установлен, только если проверка завершена.</span><span class="sxs-lookup"><span data-stu-id="724b5-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="724b5-186">д.</span><span class="sxs-lookup"><span data-stu-id="724b5-186">e.</span></span> <span data-ttu-id="724b5-187">Выберите **Включить SAML**.</span><span class="sxs-lookup"><span data-stu-id="724b5-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="724b5-188">Е.</span><span class="sxs-lookup"><span data-stu-id="724b5-188">f.</span></span> <span data-ttu-id="724b5-189">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="724b5-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="724b5-190">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="724b5-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="724b5-191">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="724b5-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="724b5-192">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="724b5-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="724b5-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="724b5-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="724b5-194">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="724b5-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="724b5-196">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="724b5-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="724b5-197">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="724b5-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="724b5-199">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="724b5-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="724b5-201">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="724b5-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="724b5-203">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="724b5-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="724b5-205">а.</span><span class="sxs-lookup"><span data-stu-id="724b5-205">a.</span></span> <span data-ttu-id="724b5-206">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="724b5-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="724b5-207">b.</span><span class="sxs-lookup"><span data-stu-id="724b5-207">b.</span></span> <span data-ttu-id="724b5-208">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="724b5-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="724b5-209">c.</span><span class="sxs-lookup"><span data-stu-id="724b5-209">c.</span></span> <span data-ttu-id="724b5-210">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="724b5-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="724b5-211">d.</span><span class="sxs-lookup"><span data-stu-id="724b5-211">d.</span></span> <span data-ttu-id="724b5-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="724b5-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="724b5-213">Создание тестового пользователя Halogen Software</span><span class="sxs-lookup"><span data-stu-id="724b5-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="724b5-214">Цель этого раздела — создать пользователя с именем Britta Simon в Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="724b5-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="724b5-215">**Чтобы создать пользователя с именем Britta Simon в Halogen Software, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="724b5-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="724b5-216">Войдите в приложение **Halogen Software** под учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="724b5-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="724b5-217">Щелкните вкладку **Центр пользователей**, затем щелкните **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="724b5-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![Что такое Azure AD Connect?][300]  

3. <span data-ttu-id="724b5-219">На странице диалогового окна **Новый пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="724b5-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![Что такое Azure AD Connect?][301]

    <span data-ttu-id="724b5-221">а.</span><span class="sxs-lookup"><span data-stu-id="724b5-221">a.</span></span> <span data-ttu-id="724b5-222">В текстовом поле **Имя** введите имя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="724b5-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="724b5-223">b.</span><span class="sxs-lookup"><span data-stu-id="724b5-223">b.</span></span> <span data-ttu-id="724b5-224">В текстовом поле **Фамилия** введите фамилию, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="724b5-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="724b5-225">c.</span><span class="sxs-lookup"><span data-stu-id="724b5-225">c.</span></span> <span data-ttu-id="724b5-226">В текстовом поле **Имя пользователя** введите **Britta Simon**, имя пользователя на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="724b5-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="724b5-227">г)</span><span class="sxs-lookup"><span data-stu-id="724b5-227">d.</span></span> <span data-ttu-id="724b5-228">В текстовом поле **Пароль** введите пароль для пользователя Britta.</span><span class="sxs-lookup"><span data-stu-id="724b5-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="724b5-229">д.</span><span class="sxs-lookup"><span data-stu-id="724b5-229">e.</span></span> <span data-ttu-id="724b5-230">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="724b5-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="724b5-231">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="724b5-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="724b5-232">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon и предоставить этому пользователю доступ к Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="724b5-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="724b5-234">**Чтобы назначить Britta Simon в Halogen Software, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="724b5-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="724b5-235">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="724b5-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="724b5-237">В списке приложений выберите **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="724b5-237">In the applications list, select **Halogen Software**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="724b5-239">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="724b5-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="724b5-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="724b5-241">Click **Add** button.</span></span> <span data-ttu-id="724b5-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="724b5-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="724b5-244">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="724b5-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="724b5-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="724b5-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="724b5-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="724b5-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="724b5-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="724b5-247">Testing single sign-on</span></span>

<span data-ttu-id="724b5-248">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="724b5-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="724b5-249">Нажав элемент Halogen Software на панели доступа, вы автоматически войдете в приложение Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="724b5-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="724b5-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="724b5-250">Additional resources</span></span>

* [<span data-ttu-id="724b5-251">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="724b5-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="724b5-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="724b5-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
