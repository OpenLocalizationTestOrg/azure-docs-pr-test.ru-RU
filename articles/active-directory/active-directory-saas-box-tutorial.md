---
title: "Руководство. Интеграция Azure Active Directory с Box | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 2cc2afe8ff3f0063224c94eb0b8135347051b0aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="44c46-103">Руководство. Интеграция Azure Active Directory с Box</span><span class="sxs-lookup"><span data-stu-id="44c46-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="44c46-104">В этом руководстве описано, как интегрировать Box с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44c46-104">In this tutorial, you learn how to integrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44c46-105">Интеграция Azure AD с приложением Box обеспечивает перечисленные ниже преимущества.</span><span class="sxs-lookup"><span data-stu-id="44c46-105">Integrating Box with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44c46-106">С помощью Azure AD вы можете контролировать доступ к Box.</span><span class="sxs-lookup"><span data-stu-id="44c46-106">You can control in Azure AD who has access to Box</span></span>
- <span data-ttu-id="44c46-107">Вы можете включить автоматический вход пользователей в Box (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44c46-107">You can enable your users to automatically get signed-on to Box (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44c46-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="44c46-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="44c46-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44c46-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44c46-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44c46-110">Prerequisites</span></span>

<span data-ttu-id="44c46-111">Чтобы настроить интеграцию Azure AD с Box, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="44c46-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="44c46-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="44c46-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44c46-113">подписка Box с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="44c46-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44c46-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="44c46-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44c46-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="44c46-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44c46-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="44c46-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44c46-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44c46-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44c46-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="44c46-118">Scenario description</span></span>
<span data-ttu-id="44c46-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="44c46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44c46-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="44c46-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44c46-121">Добавление Box из коллекции</span><span class="sxs-lookup"><span data-stu-id="44c46-121">Adding Box from the gallery</span></span>
2. <span data-ttu-id="44c46-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44c46-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-the-gallery"></a><span data-ttu-id="44c46-123">Добавление Box из коллекции</span><span class="sxs-lookup"><span data-stu-id="44c46-123">Adding Box from the gallery</span></span>
<span data-ttu-id="44c46-124">Чтобы настроить интеграцию Box с Azure AD, необходимо добавить Box из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="44c46-124">To configure the integration of Box into Azure AD, you need to add Box from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44c46-125">**Чтобы добавить Box из коллекции, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="44c46-125">**To add Box from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44c46-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44c46-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44c46-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="44c46-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44c46-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="44c46-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="44c46-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="44c46-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="44c46-133">В поле поиска введите **Box**.</span><span class="sxs-lookup"><span data-stu-id="44c46-133">In the search box, type **Box**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="44c46-135">На панели результатов выберите **Box** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="44c46-135">In the results panel, select **Box**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44c46-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44c46-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44c46-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Box с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44c46-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44c46-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Box соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44c46-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Box is to a user in Azure AD.</span></span> <span data-ttu-id="44c46-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Box.</span><span class="sxs-lookup"><span data-stu-id="44c46-140">In other words, a link relationship between an Azure AD user and the related user in Box needs to be established.</span></span>

<span data-ttu-id="44c46-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Box.</span><span class="sxs-lookup"><span data-stu-id="44c46-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Box.</span></span>

<span data-ttu-id="44c46-142">Чтобы настроить и проверить единый вход Azure AD в Box, вам потребуется выполнить действия в перечисленных ниже стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="44c46-142">To configure and test Azure AD single sign-on with Box, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44c46-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="44c46-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44c46-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44c46-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44c46-145">**[Создание тестового пользователя Box](#creating-a-box-test-user)** требуется для создания в Box пользователя Britta Simon, связанного с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44c46-145">**[Creating a Box test user](#creating-a-box-test-user)** - to have a counterpart of Britta Simon in Box that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="44c46-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44c46-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44c46-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="44c46-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44c46-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44c46-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44c46-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в Box.</span><span class="sxs-lookup"><span data-stu-id="44c46-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="44c46-150">**Чтобы настроить единый вход Azure AD в Box, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="44c46-150">**To configure Azure AD single sign-on with Box, perform the following steps:**</span></span>

1. <span data-ttu-id="44c46-151">На портале Azure на странице интеграции с приложением **Box** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="44c46-151">In the Azure portal, on the **Box** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="44c46-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="44c46-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="44c46-155">В разделе **Домены и URL-адреса приложения Box** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="44c46-155">On the **Box Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="44c46-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="44c46-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44c46-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="44c46-158">This value is not real.</span></span> <span data-ttu-id="44c46-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="44c46-159">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="44c46-160">Для получения этого значения обратитесь в [службу поддержки клиентов Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire).</span><span class="sxs-lookup"><span data-stu-id="44c46-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) to get this value.</span></span> 
 
4. <span data-ttu-id="44c46-161">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="44c46-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="44c46-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="44c46-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44c46-165">Чтобы настроить единый вход для своего приложения, обратитесь в [службу поддержки клиентов Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) и предоставьте скачанный XML-файл.</span><span class="sxs-lookup"><span data-stu-id="44c46-165">To get SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="44c46-166">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="44c46-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="44c46-167">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="44c46-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="44c46-168">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="44c46-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44c46-169">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="44c46-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="44c46-170">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44c46-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="44c46-172">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="44c46-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44c46-173">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44c46-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44c46-175">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="44c46-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44c46-177">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="44c46-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44c46-179">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="44c46-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44c46-181">а.</span><span class="sxs-lookup"><span data-stu-id="44c46-181">a.</span></span> <span data-ttu-id="44c46-182">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44c46-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44c46-183">b.</span><span class="sxs-lookup"><span data-stu-id="44c46-183">b.</span></span> <span data-ttu-id="44c46-184">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44c46-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44c46-185">c.</span><span class="sxs-lookup"><span data-stu-id="44c46-185">c.</span></span> <span data-ttu-id="44c46-186">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="44c46-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="44c46-187">d.</span><span class="sxs-lookup"><span data-stu-id="44c46-187">d.</span></span> <span data-ttu-id="44c46-188">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="44c46-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="44c46-189">Создание тестового пользователя Box</span><span class="sxs-lookup"><span data-stu-id="44c46-189">Creating a Box test user</span></span>

<span data-ttu-id="44c46-190">В этом разделе вы создадите в Box пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44c46-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="44c46-191">Приложение Box поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="44c46-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="44c46-192">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="44c46-192">There is no action item for you in this section.</span></span> <span data-ttu-id="44c46-193">Если пользователь еще не существует в Box, он создается при попытке доступа к приложению Box.</span><span class="sxs-lookup"><span data-stu-id="44c46-193">If a user doesn't already exist in Box, a new one is created when you attempt to access Box.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44c46-194">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="44c46-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44c46-195">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Box.</span><span class="sxs-lookup"><span data-stu-id="44c46-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Box.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="44c46-197">**Чтобы назначить пользователя Britta Simon в Box, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="44c46-197">**To assign Britta Simon to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="44c46-198">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="44c46-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="44c46-200">В списке приложений выберите **Box**.</span><span class="sxs-lookup"><span data-stu-id="44c46-200">In the applications list, select **Box**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="44c46-202">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="44c46-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="44c46-204">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="44c46-204">Click **Add** button.</span></span> <span data-ttu-id="44c46-205">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="44c46-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="44c46-207">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="44c46-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44c46-208">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="44c46-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44c46-209">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="44c46-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44c46-210">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="44c46-210">Testing single sign-on</span></span>

<span data-ttu-id="44c46-211">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="44c46-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44c46-212">Щелкнув плитку Box на панели доступа, вы автоматически войдете в приложение Box.</span><span class="sxs-lookup"><span data-stu-id="44c46-212">When you click the Box tile in the Access Panel, you should get login page to get signed-on to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44c46-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="44c46-213">Additional resources</span></span>

* [<span data-ttu-id="44c46-214">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44c46-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44c46-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44c46-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="44c46-216">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="44c46-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

