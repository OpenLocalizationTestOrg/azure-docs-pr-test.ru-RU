---
title: "Руководство по интеграции Azure Active Directory с Novatus | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: ec67e96309a8877e6fb65b30da1501e4f34a9ee4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="21598-103">Руководство по интеграции Azure Active Directory с Novatus</span><span class="sxs-lookup"><span data-stu-id="21598-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="21598-104">В этом руководстве описано, как интегрировать приложение Novatus с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="21598-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="21598-105">Интеграция Azure AD с приложением Novatus обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="21598-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="21598-106">С помощью Azure AD вы можете контролировать доступ к Novatus.</span><span class="sxs-lookup"><span data-stu-id="21598-106">You can control in Azure AD who has access to Novatus</span></span>
- <span data-ttu-id="21598-107">Вы можете включить автоматический вход пользователей в Novatus (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21598-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="21598-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="21598-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="21598-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="21598-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21598-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="21598-110">Prerequisites</span></span>

<span data-ttu-id="21598-111">Чтобы настроить интеграцию Azure AD с Novatus, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="21598-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

- <span data-ttu-id="21598-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="21598-112">An Azure AD subscription</span></span>
- <span data-ttu-id="21598-113">подписка Novatus с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="21598-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="21598-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="21598-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="21598-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="21598-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="21598-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="21598-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="21598-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21598-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="21598-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="21598-118">Scenario description</span></span>
<span data-ttu-id="21598-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="21598-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="21598-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="21598-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="21598-121">Добавление Novatus из коллекции</span><span class="sxs-lookup"><span data-stu-id="21598-121">Adding Novatus from the gallery</span></span>
2. <span data-ttu-id="21598-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="21598-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-the-gallery"></a><span data-ttu-id="21598-123">Добавление Novatus из коллекции</span><span class="sxs-lookup"><span data-stu-id="21598-123">Adding Novatus from the gallery</span></span>
<span data-ttu-id="21598-124">Чтобы настроить интеграцию Novatus с Azure AD, необходимо добавить Novatus из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="21598-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="21598-125">**Чтобы добавить Novatus из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="21598-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="21598-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="21598-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="21598-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="21598-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="21598-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="21598-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="21598-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="21598-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="21598-133">В поле поиска введите **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="21598-133">In the search box, type **Novatus**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="21598-135">На панели результатов выберите **Novatus** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="21598-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="21598-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="21598-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="21598-138">В этом разделе описана настройка и проверка единого входа Azure AD в Novatus с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21598-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="21598-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Novatus соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21598-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span></span> <span data-ttu-id="21598-140">То есть необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Novatus.</span><span class="sxs-lookup"><span data-stu-id="21598-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="21598-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Novatus.</span><span class="sxs-lookup"><span data-stu-id="21598-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="21598-142">Чтобы настроить и проверить единый вход Azure AD в Novatus, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="21598-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="21598-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="21598-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="21598-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21598-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="21598-145">**[Создание тестового пользователя Novatus](#creating-a-novatus-test-user)** требуется для того, чтобы в Novatus существовал пользователь Britta Simon, связанный с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21598-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="21598-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="21598-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="21598-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="21598-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="21598-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="21598-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="21598-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Novatus.</span><span class="sxs-lookup"><span data-stu-id="21598-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="21598-150">**Чтобы настроить единый вход Azure AD в Novatus, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="21598-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="21598-151">На портале Azure на странице интеграции с приложением **Novatus** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="21598-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="21598-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="21598-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="21598-155">В разделе **Домены и URL-адреса приложения Novatus** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="21598-155">On the **Novatus Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="21598-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="21598-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="21598-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="21598-158">This value is not real.</span></span> <span data-ttu-id="21598-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="21598-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="21598-160">Для получения данного значения обратитесь в [службу поддержки клиентов Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="21598-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span></span> 
 


4. <span data-ttu-id="21598-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="21598-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="21598-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="21598-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="21598-165">В разделе **Настройка Novatus** щелкните **Настроить Novatus**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="21598-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span></span> <span data-ttu-id="21598-166">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="21598-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="21598-168">Чтобы настроить единый вход для своего приложения, обратитесь в [службу поддержки Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="21598-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="21598-169">Прикрепите к сообщению **скачанный файл сертификата** и укажите **URL-адреса метаданных** (**URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**), чтобы специалисты Novatus смогли настроить единый вход со своей стороны.</span><span class="sxs-lookup"><span data-stu-id="21598-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="21598-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="21598-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="21598-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="21598-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="21598-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="21598-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="21598-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="21598-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="21598-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="21598-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="21598-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="21598-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="21598-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="21598-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="21598-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="21598-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="21598-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="21598-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="21598-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="21598-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="21598-185">а.</span><span class="sxs-lookup"><span data-stu-id="21598-185">a.</span></span> <span data-ttu-id="21598-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="21598-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="21598-187">b.</span><span class="sxs-lookup"><span data-stu-id="21598-187">b.</span></span> <span data-ttu-id="21598-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="21598-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="21598-189">c.</span><span class="sxs-lookup"><span data-stu-id="21598-189">c.</span></span> <span data-ttu-id="21598-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="21598-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="21598-191">d.</span><span class="sxs-lookup"><span data-stu-id="21598-191">d.</span></span> <span data-ttu-id="21598-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="21598-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="21598-193">Создание тестового пользователя Novatus</span><span class="sxs-lookup"><span data-stu-id="21598-193">Creating a Novatus test user</span></span>

<span data-ttu-id="21598-194">Цель этого раздела — создать пользователя с именем Britta Simon в Novatus.</span><span class="sxs-lookup"><span data-stu-id="21598-194">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="21598-195">Приложение Novatus поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="21598-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="21598-196">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="21598-196">There is no action item for you in this section.</span></span> <span data-ttu-id="21598-197">При попытке получить доступ к Novatus будет создан пользователь (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="21598-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="21598-198">Чтобы создать пользователя вручную, обратитесь в [службу поддержки Novatus](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="21598-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="21598-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="21598-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="21598-200">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Novatus, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="21598-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="21598-202">**Чтобы назначить пользователя Britta Simon в Novatus, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="21598-202">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="21598-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="21598-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="21598-205">Из списка приложений выберите **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="21598-205">In the applications list, select **Novatus**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="21598-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="21598-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="21598-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="21598-209">Click **Add** button.</span></span> <span data-ttu-id="21598-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="21598-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="21598-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="21598-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="21598-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="21598-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="21598-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="21598-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="21598-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="21598-215">Testing single sign-on</span></span>

<span data-ttu-id="21598-216">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="21598-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="21598-217">Щелкнув плитку Novatus на панели доступа, вы автоматически войдете в приложение Novatus.</span><span class="sxs-lookup"><span data-stu-id="21598-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span> <span data-ttu-id="21598-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="21598-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="21598-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="21598-219">Additional resources</span></span>

* [<span data-ttu-id="21598-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="21598-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="21598-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="21598-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

