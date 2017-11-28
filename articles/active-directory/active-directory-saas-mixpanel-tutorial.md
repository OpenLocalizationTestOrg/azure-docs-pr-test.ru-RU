---
title: "Руководство по интеграции Azure Active Directory с Mixpanel | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3dd11b3477de1329c1c8e45a6dbf212b1635fd95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="c0c61-103">Руководство. Интеграция Azure Active Directory с Mixpanel</span><span class="sxs-lookup"><span data-stu-id="c0c61-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="c0c61-104">В этом руководстве описано, как интегрировать Mixpanel с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c0c61-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0c61-105">Интеграция Mixpanel с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="c0c61-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0c61-106">С помощью Azure AD вы можете контролировать доступ к Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="c0c61-107">Вы можете включить автоматический вход пользователей в Mixpanel (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0c61-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0c61-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c0c61-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0c61-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c0c61-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0c61-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c0c61-110">Prerequisites</span></span>

<span data-ttu-id="c0c61-111">Чтобы настроить интеграцию Azure AD с Mixpanel, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c0c61-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="c0c61-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c0c61-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0c61-113">подписка с поддержкой единого входа Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0c61-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c0c61-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0c61-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c0c61-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0c61-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c0c61-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0c61-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0c61-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0c61-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c0c61-118">Scenario description</span></span>
<span data-ttu-id="c0c61-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c0c61-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0c61-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c0c61-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0c61-121">Добавление Mixpanel из коллекции</span><span class="sxs-lookup"><span data-stu-id="c0c61-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="c0c61-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0c61-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="c0c61-123">Добавление Mixpanel из коллекции</span><span class="sxs-lookup"><span data-stu-id="c0c61-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="c0c61-124">Чтобы настроить интеграцию Mixpanel с Azure AD, необходимо добавить Mixpanel из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c0c61-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0c61-125">**Чтобы добавить Mixpanel из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c0c61-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0c61-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0c61-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0c61-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c0c61-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c0c61-133">В поле поиска введите **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-133">In the search box, type **Mixpanel**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="c0c61-135">На панели результатов выберите **Mixpanel** и щелкните **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="c0c61-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0c61-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0c61-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0c61-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Mixpanel с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0c61-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c0c61-139">Для работы единого входа Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="c0c61-140">То есть необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="c0c61-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c0c61-142">Чтобы настроить и проверить единый вход Azure AD в Mixpanel, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="c0c61-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0c61-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c0c61-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0c61-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0c61-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0c61-145">**[Создание тестового пользователя Mixpanel](#creating-a-mixpanel-test-user)** требуется для создания в Mixpanel пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0c61-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0c61-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0c61-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0c61-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c0c61-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0c61-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0c61-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0c61-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="c0c61-150">**Чтобы настроить единый вход Azure AD в Mixpanel, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c0c61-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="c0c61-151">На портале Azure на странице интеграции с приложением **Mixpanel** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c0c61-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c0c61-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="c0c61-155">В разделе **Домены и URL-адреса приложения Mixpanel** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c0c61-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="c0c61-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в формате `https://mixpanel.com/login/`.</span><span class="sxs-lookup"><span data-stu-id="c0c61-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0c61-158">Зарегистрируйтесь на сайте [https://mixpanel.com/register/](https://mixpanel.com/register/), настройте учетные данные для входа в систему и обратитесь в [службу поддержки Mixpanel](mailto:support@mixpanel.com), чтобы включить параметры единого входа для своего клиента.</span><span class="sxs-lookup"><span data-stu-id="c0c61-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="c0c61-159">Вы также можете получить URL-адрес единого входа, обратившись в службу поддержки Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="c0c61-160">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c0c61-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="c0c61-162">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c0c61-162">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0c61-164">В разделе **Настройка Mixpanel** щелкните **Настроить Mixpanel**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c0c61-165">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="c0c61-167">В отдельном окне браузера войдите в приложение Mixpanel под учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="c0c61-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="c0c61-168">Щелкните маленький значок **шестеренки** в левом нижнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="c0c61-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Единый вход в Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="c0c61-170">Откройте вкладку **Access security** (Безопасность доступа) и щелкните **Change settings** (Изменить параметры).</span><span class="sxs-lookup"><span data-stu-id="c0c61-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Параметры Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="c0c61-172">На странице диалогового окна **Change your certificate** (Изменение сертификата) щелкните **Choose file** (Выбрать файл), чтобы передать скачанный сертификат, а затем щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="c0c61-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Параметры Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="c0c61-174">В текстовом поле URL-адреса проверки подлинности диалоговой страницы **Change your authentication URL** (Изменение URL-адреса проверки подлинности) вставьте значение **URL-адрес службы единого входа SAML**, которое скопировано с портала Azure, и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="c0c61-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Параметры Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="c0c61-176">Нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="c0c61-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="c0c61-177">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c0c61-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0c61-178">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c0c61-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0c61-179">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c0c61-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0c61-180">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0c61-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0c61-181">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c0c61-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c0c61-183">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c0c61-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0c61-184">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0c61-186">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0c61-188">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0c61-190">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c0c61-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0c61-192">а.</span><span class="sxs-lookup"><span data-stu-id="c0c61-192">a.</span></span> <span data-ttu-id="c0c61-193">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0c61-194">b.</span><span class="sxs-lookup"><span data-stu-id="c0c61-194">b.</span></span> <span data-ttu-id="c0c61-195">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c0c61-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0c61-196">c.</span><span class="sxs-lookup"><span data-stu-id="c0c61-196">c.</span></span> <span data-ttu-id="c0c61-197">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0c61-198">d.</span><span class="sxs-lookup"><span data-stu-id="c0c61-198">d.</span></span> <span data-ttu-id="c0c61-199">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="c0c61-200">Создание тестового пользователя Mixpanel</span><span class="sxs-lookup"><span data-stu-id="c0c61-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="c0c61-201">Цель этого раздела — создать пользователя с именем Britta Simon в Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="c0c61-202">Войдите на веб-сайт компании Mixpanel в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c0c61-202">Sign on to your Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="c0c61-203">Щелкните маленькую кнопку с шестеренкой в левом нижнем углу страницы, чтобы открыть окно **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="c0c61-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

3. <span data-ttu-id="c0c61-204">Откройте вкладку **Команды** .</span><span class="sxs-lookup"><span data-stu-id="c0c61-204">Click the **Team** tab.</span></span>

4. <span data-ttu-id="c0c61-205">В текстовое поле **член команды** введите электронный адрес пользователя Britta Simon на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c0c61-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Параметры Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="c0c61-207">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="c0c61-208">Пользователь получит по электронной почте письмо с предложением настроить свой профиль.</span><span class="sxs-lookup"><span data-stu-id="c0c61-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0c61-209">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0c61-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0c61-210">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c0c61-212">**Чтобы назначить пользователя Britta Simon в Mixpanel, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c0c61-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="c0c61-213">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c0c61-215">В списке приложений выберите **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-215">In the applications list, select **Mixpanel**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="c0c61-217">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c0c61-219">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-219">Click **Add** button.</span></span> <span data-ttu-id="c0c61-220">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c0c61-222">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0c61-223">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0c61-224">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c0c61-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0c61-225">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c0c61-225">Testing single sign-on</span></span>

<span data-ttu-id="c0c61-226">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c0c61-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0c61-227">Щелкнув элемент Mixpanel на панели доступа, вы автоматически войдете в приложение Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="c0c61-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="c0c61-228">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c0c61-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0c61-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c0c61-229">Additional resources</span></span>

* [<span data-ttu-id="c0c61-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0c61-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0c61-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0c61-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

