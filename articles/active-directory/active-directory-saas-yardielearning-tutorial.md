---
title: "Руководство по интеграции Azure Active Directory с Yardi eLearning | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Yardi eLearning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7ea58b54-ec5b-4576-8586-814b11d0f4fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: e7b36b692ad2a8bc3a3f5203d93882af96fd2109
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yardi-elearning"></a><span data-ttu-id="05f13-103">Учебник. Интеграция Azure Active Directory с Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="05f13-103">Tutorial: Azure Active Directory integration with Yardi eLearning</span></span>

<span data-ttu-id="05f13-104">Это руководство описывает интеграцию Azure Active Directory (Azure AD) с приложением Yardi Learning.</span><span class="sxs-lookup"><span data-stu-id="05f13-104">In this tutorial, you learn how to integrate Yardi eLearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05f13-105">Интеграция приложения Yardi eLearning с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="05f13-105">Integrating Yardi eLearning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="05f13-106">С помощью Azure AD вы можете контролировать доступ пользователей к Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="05f13-106">You can control in Azure AD who has access to Yardi eLearning</span></span>
- <span data-ttu-id="05f13-107">Вы можете включить автоматический вход пользователей в Yardi eLearning (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05f13-107">You can enable your users to automatically get signed-on to Yardi eLearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05f13-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="05f13-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="05f13-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05f13-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05f13-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="05f13-110">Prerequisites</span></span>

<span data-ttu-id="05f13-111">Чтобы настроить интеграцию Azure AD с Yardi eLearning, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="05f13-111">To configure Azure AD integration with Yardi eLearning, you need the following items:</span></span>

- <span data-ttu-id="05f13-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="05f13-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05f13-113">подписка Yardi eLearning с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="05f13-113">A Yardi eLearning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05f13-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="05f13-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05f13-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="05f13-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05f13-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="05f13-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05f13-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05f13-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05f13-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="05f13-118">Scenario description</span></span>
<span data-ttu-id="05f13-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="05f13-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05f13-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="05f13-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05f13-121">Добавление Yardi eLearning из коллекции</span><span class="sxs-lookup"><span data-stu-id="05f13-121">Adding Yardi eLearning from the gallery</span></span>
2. <span data-ttu-id="05f13-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05f13-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yardi-elearning-from-the-gallery"></a><span data-ttu-id="05f13-123">Добавление Yardi eLearning из коллекции</span><span class="sxs-lookup"><span data-stu-id="05f13-123">Adding Yardi eLearning from the gallery</span></span>
<span data-ttu-id="05f13-124">Чтобы настроить интеграцию Yardi eLearning с Azure AD, необходимо добавить Yardi eLearning из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="05f13-124">To configure the integration of Yardi eLearning into Azure AD, you need to add Yardi eLearning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05f13-125">**Чтобы добавить Yardi eLearning из коллекции, выполните указанные далее действия.**</span><span class="sxs-lookup"><span data-stu-id="05f13-125">**To add Yardi eLearning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="05f13-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05f13-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05f13-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="05f13-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="05f13-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="05f13-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="05f13-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="05f13-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="05f13-133">В поле поиска введите **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="05f13-133">In the search box, type **Yardi eLearning**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_search.png)

5. <span data-ttu-id="05f13-135">На панели результатов выберите **Yardi eLearning** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="05f13-135">In the results panel, select **Yardi eLearning**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05f13-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05f13-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05f13-138">Этот раздел описывает настройку и проверку единого входа Azure AD в Yardi eLearning с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05f13-138">In this section, you configure and test Azure AD single sign-on with Yardi eLearning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05f13-139">Для работы единого входа в Azure AD нужно знать, какой пользователь в Yardi eLearning соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05f13-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Yardi eLearning is to a user in Azure AD.</span></span> <span data-ttu-id="05f13-140">То есть необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="05f13-140">In other words, a link relationship between an Azure AD user and the related user in Yardi eLearning needs to be established.</span></span>

<span data-ttu-id="05f13-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="05f13-141">In Yardi eLearning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="05f13-142">Чтобы настроить и проверить единый вход Azure AD в Yardi eLearning, вам потребуется выполнить действия в указанных далее стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="05f13-142">To configure and test Azure AD single sign-on with Yardi eLearning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05f13-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="05f13-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="05f13-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05f13-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05f13-145">**[Создание тестового пользователя Yardi eLearning](#creating-a-yardi-elearning-test-user)** требуется для создания пользователя Britta Simon в Yardi eLearning, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05f13-145">**[Creating a Yardi eLearning test user](#creating-a-yardi-elearning-test-user)** - to have a counterpart of Britta Simon in Yardi eLearning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="05f13-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05f13-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05f13-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="05f13-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05f13-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05f13-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05f13-149">Этот раздел описывает, как включить единый вход Azure AD на портале Azure и настроить его в приложении Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="05f13-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yardi eLearning application.</span></span>

<span data-ttu-id="05f13-150">**Чтобы настроить единый вход Azure AD в Yardi eLearning, выполните указанные далее действия.**</span><span class="sxs-lookup"><span data-stu-id="05f13-150">**To configure Azure AD single sign-on with Yardi eLearning, perform the following steps:**</span></span>

1. <span data-ttu-id="05f13-151">На портале Azure на странице интеграции с приложением **Yardi eLearning**  щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="05f13-151">In the Azure portal, on the **Yardi eLearning** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="05f13-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="05f13-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_samlbase.png)

3. <span data-ttu-id="05f13-155">В разделе **Домены и URL-адреса приложения Yardi eLearning** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="05f13-155">On the **Yardi eLearning Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_url.png)

    <span data-ttu-id="05f13-157">а.</span><span class="sxs-lookup"><span data-stu-id="05f13-157">a.</span></span> <span data-ttu-id="05f13-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.yardielearning.com/login`</span><span class="sxs-lookup"><span data-stu-id="05f13-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/login`</span></span>

    <span data-ttu-id="05f13-159">b.</span><span class="sxs-lookup"><span data-stu-id="05f13-159">b.</span></span> <span data-ttu-id="05f13-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.yardielearning.com/trust`</span><span class="sxs-lookup"><span data-stu-id="05f13-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.yardielearning.com/trust`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05f13-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="05f13-161">These values are not real.</span></span> <span data-ttu-id="05f13-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="05f13-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="05f13-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Yardi eLearning](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="05f13-163">Contact [Yardi eLearning Client support team](mailto:elearning@yardi.com) to get these values.</span></span> 
 
4. <span data-ttu-id="05f13-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="05f13-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_certificate.png) 

5. <span data-ttu-id="05f13-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="05f13-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="05f13-168">Чтобы настроить единый вход на стороне **Yardi eLearning** , отправьте скачанный **XML-файл метаданных** в [службу поддержки Yardi eLearning](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="05f13-168">To configure single sign-on on **Yardi eLearning** side, you need to send the downloaded **Metadata XML** to [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span> 

> [!TIP]
> <span data-ttu-id="05f13-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="05f13-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="05f13-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="05f13-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="05f13-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="05f13-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05f13-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="05f13-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="05f13-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05f13-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="05f13-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="05f13-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="05f13-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05f13-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05f13-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="05f13-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05f13-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="05f13-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05f13-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="05f13-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-yardielearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05f13-184">а.</span><span class="sxs-lookup"><span data-stu-id="05f13-184">a.</span></span> <span data-ttu-id="05f13-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05f13-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05f13-186">b.</span><span class="sxs-lookup"><span data-stu-id="05f13-186">b.</span></span> <span data-ttu-id="05f13-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05f13-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05f13-188">c.</span><span class="sxs-lookup"><span data-stu-id="05f13-188">c.</span></span> <span data-ttu-id="05f13-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="05f13-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="05f13-190">d.</span><span class="sxs-lookup"><span data-stu-id="05f13-190">d.</span></span> <span data-ttu-id="05f13-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="05f13-191">Click **Create**.</span></span>
 
### <a name="creating-a-yardi-elearning-test-user"></a><span data-ttu-id="05f13-192">Создание тестового пользователя Yardi eLearning</span><span class="sxs-lookup"><span data-stu-id="05f13-192">Creating a Yardi eLearning test user</span></span>

<span data-ttu-id="05f13-193">Цель этого раздела — создать в приложении Yardi eLearning пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05f13-193">The objective of this section is to create a user called Britta Simon in Yardi eLearning.</span></span> <span data-ttu-id="05f13-194">Приложение Yardi eLearning поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="05f13-194">Yardi eLearning supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="05f13-195">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="05f13-195">There is no action item for you in this section.</span></span> <span data-ttu-id="05f13-196">Пользователь создается при попытке получить доступ к приложению Yardi eLearning (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="05f13-196">A new user is created during an attempt to access Yardi eLearning if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="05f13-197">Если вам требуется вручную создать пользователя, нужно обратиться в [службу поддержки Yardi eLearning](mailto:elearning@yardi.com).</span><span class="sxs-lookup"><span data-stu-id="05f13-197">If you need to create a user manually, you need to contact the [Yardi eLearning support team](mailto:elearning@yardi.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="05f13-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="05f13-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="05f13-199">Этот раздел описывает, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="05f13-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yardi eLearning.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="05f13-201">**Чтобы назначить пользователя Britta Simon приложению Yardi eLearning, выполните указанные далее действия.**</span><span class="sxs-lookup"><span data-stu-id="05f13-201">**To assign Britta Simon to Yardi eLearning, perform the following steps:**</span></span>

1. <span data-ttu-id="05f13-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="05f13-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="05f13-204">Из списка приложений выберите **Yardi eLearning**.</span><span class="sxs-lookup"><span data-stu-id="05f13-204">In the applications list, select **Yardi eLearning**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-yardielearning-tutorial/tutorial_yardielearning_app.png) 

3. <span data-ttu-id="05f13-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="05f13-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="05f13-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="05f13-208">Click **Add** button.</span></span> <span data-ttu-id="05f13-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="05f13-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="05f13-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="05f13-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="05f13-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="05f13-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05f13-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="05f13-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05f13-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="05f13-214">Testing single sign-on</span></span>

<span data-ttu-id="05f13-215">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="05f13-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="05f13-216">Щелкнув элемент Yardi eLearning на панели доступа, вы автоматически войдете в приложение Yardi eLearning.</span><span class="sxs-lookup"><span data-stu-id="05f13-216">When you click the Yardi eLearning tile in the Access Panel, you should get automatically signed-on to your Yardi eLearning application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="05f13-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="05f13-217">Additional resources</span></span>

* [<span data-ttu-id="05f13-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05f13-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05f13-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05f13-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yardielearning-tutorial/tutorial_general_203.png

