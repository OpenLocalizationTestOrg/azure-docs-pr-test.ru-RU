---
title: "Учебник. Интеграция Azure Active Directory с Kindling | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в Kindling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 131c2c3f46c60193d512b1779e917c8322732fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="c7147-103">Учебник. Интеграция Azure Active Directory с Kindling</span><span class="sxs-lookup"><span data-stu-id="c7147-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="c7147-104">В этом руководстве описано, как интегрировать Kindling с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c7147-104">In this tutorial, you learn how to integrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7147-105">Интеграция Azure AD с приложением Kindling дает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="c7147-105">Integrating Kindling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c7147-106">с помощью Azure AD вы можете контролировать доступ к Kindling;</span><span class="sxs-lookup"><span data-stu-id="c7147-106">You can control in Azure AD who has access to Kindling</span></span>
- <span data-ttu-id="c7147-107">вы можете включить автоматический вход пользователей в Kindling (единый вход) с использованием учетных записей Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c7147-107">You can enable your users to automatically get signed-on to Kindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7147-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c7147-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c7147-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье</span><span class="sxs-lookup"><span data-stu-id="c7147-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="c7147-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c7147-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7147-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7147-111">Prerequisites</span></span>

<span data-ttu-id="c7147-112">Чтобы настроить интеграцию Azure AD с Kindling, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c7147-112">To configure Azure AD integration with Kindling, you need the following items:</span></span>

- <span data-ttu-id="c7147-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c7147-113">An Azure AD subscription</span></span>
- <span data-ttu-id="c7147-114">подписка Kindling с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c7147-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7147-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c7147-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7147-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c7147-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7147-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c7147-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7147-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7147-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7147-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c7147-119">Scenario description</span></span>
<span data-ttu-id="c7147-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c7147-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7147-121">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c7147-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7147-122">Добавление Kindling из коллекции</span><span class="sxs-lookup"><span data-stu-id="c7147-122">Adding Kindling from the gallery</span></span>
2. <span data-ttu-id="c7147-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7147-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-the-gallery"></a><span data-ttu-id="c7147-124">Добавление Kindling из коллекции</span><span class="sxs-lookup"><span data-stu-id="c7147-124">Adding Kindling from the gallery</span></span>
<span data-ttu-id="c7147-125">Чтобы настроить интеграцию Kindling с Azure AD, необходимо добавить Kindling из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c7147-125">To configure the integration of Kindling into Azure AD, you need to add Kindling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c7147-126">**Чтобы добавить Kindling из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c7147-126">**To add Kindling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c7147-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7147-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7147-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7147-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c7147-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7147-130">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c7147-132">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c7147-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c7147-134">В поле поиска введите **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="c7147-134">In the search box, type **Kindling**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="c7147-136">На панели результатов выберите **Kindling** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="c7147-136">In the results panel, select **Kindling**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7147-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7147-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7147-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Kindling для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7147-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7147-140">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Kindling соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7147-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Kindling is to a user in Azure AD.</span></span> <span data-ttu-id="c7147-141">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Kindling.</span><span class="sxs-lookup"><span data-stu-id="c7147-141">In other words, a link relationship between an Azure AD user and the related user in Kindling needs to be established.</span></span>

<span data-ttu-id="c7147-142">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Kindling.</span><span class="sxs-lookup"><span data-stu-id="c7147-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kindling.</span></span>

<span data-ttu-id="c7147-143">Чтобы настроить и проверить единый вход Azure AD в Kindling, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="c7147-143">To configure and test Azure AD single sign-on with Kindling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c7147-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c7147-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c7147-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7147-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7147-146">**[Создание тестового пользователя Kindling](#creating-a-kindling-test-user)** требуется для создания пользователя Britta Simon в Kindling, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7147-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - to have a counterpart of Britta Simon in Kindling that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7147-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c7147-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7147-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c7147-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7147-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7147-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7147-150">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Kindling.</span><span class="sxs-lookup"><span data-stu-id="c7147-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="c7147-151">**Чтобы настроить единый вход Azure AD в Kindling, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c7147-151">**To configure Azure AD single sign-on with Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="c7147-152">На портале Azure на странице интеграции с приложением **Kindling** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c7147-152">In the Azure portal, on the **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c7147-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c7147-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="c7147-156">В разделе **Домены и URL-адреса Kindling** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c7147-156">On the **Kindling Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="c7147-158">а.</span><span class="sxs-lookup"><span data-stu-id="c7147-158">a.</span></span> <span data-ttu-id="c7147-159">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="c7147-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="c7147-160">b.</span><span class="sxs-lookup"><span data-stu-id="c7147-160">b.</span></span>  <span data-ttu-id="c7147-161">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="c7147-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7147-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c7147-162">These values are not the real.</span></span> <span data-ttu-id="c7147-163">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="c7147-163">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="c7147-164">Чтобы получить эти значения, обратитесь в [службу поддержки Kindling](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="c7147-164">Contact [Kindling support team](mailto:support@kindlingapp.com) to get these values.</span></span>
 
4. <span data-ttu-id="c7147-165">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c7147-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="c7147-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c7147-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7147-169">В разделе **Настройка Kindling** щелкните **Настроить Kindling**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c7147-169">On the **Kindling Configuration** section, click **Configure Kindling** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c7147-170">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="c7147-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="c7147-172">Чтобы настроить единый вход на стороне **Kindling**, нужно отправить скачанный **сертификат (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** в [службу поддержки Kindling](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="c7147-172">To configure single sign-on on **Kindling** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="c7147-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c7147-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c7147-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c7147-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c7147-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c7147-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7147-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7147-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7147-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7147-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c7147-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c7147-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c7147-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c7147-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7147-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c7147-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7147-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7147-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7147-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c7147-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7147-188">а.</span><span class="sxs-lookup"><span data-stu-id="c7147-188">a.</span></span> <span data-ttu-id="c7147-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7147-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7147-190">b.</span><span class="sxs-lookup"><span data-stu-id="c7147-190">b.</span></span> <span data-ttu-id="c7147-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7147-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7147-192">c.</span><span class="sxs-lookup"><span data-stu-id="c7147-192">c.</span></span> <span data-ttu-id="c7147-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c7147-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c7147-194">d.</span><span class="sxs-lookup"><span data-stu-id="c7147-194">d.</span></span> <span data-ttu-id="c7147-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c7147-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="c7147-196">Создание тестового пользователя Kindling</span><span class="sxs-lookup"><span data-stu-id="c7147-196">Creating a Kindling test user</span></span>

<span data-ttu-id="c7147-197">Цель этого раздела — создать пользователя с именем Britta Simon в Kindling.</span><span class="sxs-lookup"><span data-stu-id="c7147-197">The objective of this section is to create a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="c7147-198">Приложение Kindling поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="c7147-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="c7147-199">Эта функция уже включена в ходе [настройки единого входа Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c7147-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="c7147-200">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="c7147-200">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c7147-201">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7147-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c7147-202">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к Kindling.</span><span class="sxs-lookup"><span data-stu-id="c7147-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kindling.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c7147-204">**Чтобы назначить пользователя Britta Simon приложению Kindling, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c7147-204">**To assign Britta Simon to Kindling, perform the following steps:**</span></span>

1. <span data-ttu-id="c7147-205">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7147-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c7147-207">В списке приложений выберите **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="c7147-207">In the applications list, select **Kindling**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="c7147-209">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c7147-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c7147-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7147-211">Click **Add** button.</span></span> <span data-ttu-id="c7147-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c7147-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c7147-214">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c7147-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c7147-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c7147-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7147-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c7147-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7147-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c7147-217">Testing single sign-on</span></span>

<span data-ttu-id="c7147-218">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c7147-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c7147-219">Щелкнув плитку Kindling на панели доступа, вы автоматически войдете в приложение Kindling.</span><span class="sxs-lookup"><span data-stu-id="c7147-219">When you click the Kindling tile in the Access Panel, you should get automatically signed-on to your Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c7147-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c7147-220">Additional resources</span></span>

* [<span data-ttu-id="c7147-221">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7147-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7147-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7147-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

