---
title: "Руководство по интеграции Azure Active Directory с Printix | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="932a0-103">Руководство. Интеграция Azure Active Directory с Printix</span><span class="sxs-lookup"><span data-stu-id="932a0-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="932a0-104">В этом руководстве описано, как интегрировать Printix с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="932a0-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="932a0-105">Интеграция Azure AD с приложением Printix обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="932a0-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="932a0-106">С помощью Azure AD вы можете контролировать доступ к Printix.</span><span class="sxs-lookup"><span data-stu-id="932a0-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="932a0-107">Вы можете включить автоматический вход пользователей в Printix (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="932a0-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="932a0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="932a0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="932a0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="932a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="932a0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="932a0-110">Prerequisites</span></span>

<span data-ttu-id="932a0-111">Чтобы настроить интеграцию Azure AD с Printix, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="932a0-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="932a0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="932a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="932a0-113">подписка Printix с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="932a0-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="932a0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="932a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="932a0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="932a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="932a0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="932a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="932a0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="932a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="932a0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="932a0-118">Scenario description</span></span>
<span data-ttu-id="932a0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="932a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="932a0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="932a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="932a0-121">Добавление Printix из коллекции</span><span class="sxs-lookup"><span data-stu-id="932a0-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="932a0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="932a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="932a0-123">Добавление Printix из коллекции</span><span class="sxs-lookup"><span data-stu-id="932a0-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="932a0-124">Чтобы настроить интеграцию Printix с Azure AD, необходимо добавить Printix из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="932a0-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="932a0-125">**Чтобы добавить Printix из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="932a0-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="932a0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="932a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="932a0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="932a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="932a0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="932a0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="932a0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="932a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="932a0-133">В поле поиска введите **Printix**.</span><span class="sxs-lookup"><span data-stu-id="932a0-133">In the search box, type **Printix**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="932a0-135">На панели результатов выберите **Printix** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="932a0-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="932a0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="932a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="932a0-138">В этом разделе описана настройка и проверка единого входа Azure AD в Printix с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="932a0-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="932a0-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Printix соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="932a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="932a0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем Printix.</span><span class="sxs-lookup"><span data-stu-id="932a0-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="932a0-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Printix.</span><span class="sxs-lookup"><span data-stu-id="932a0-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="932a0-142">Чтобы настроить и проверить единый вход Azure AD в Printix, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="932a0-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="932a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="932a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="932a0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="932a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="932a0-145">**[Создание тестового пользователя Printix](#creating-a-printix-test-user)** требуется для того, чтобы в Printix существовал пользователь Britta Simon, связанный с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="932a0-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="932a0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="932a0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="932a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="932a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="932a0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="932a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="932a0-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Printix.</span><span class="sxs-lookup"><span data-stu-id="932a0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="932a0-150">**Чтобы настроить единый вход Azure AD в Printix, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="932a0-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="932a0-151">На портале Azure на странице интеграции с приложением **Printix** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="932a0-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="932a0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="932a0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="932a0-155">В разделе **Домены и URL-адреса приложения Printix** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="932a0-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="932a0-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="932a0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="932a0-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="932a0-158">The value is not real.</span></span> <span data-ttu-id="932a0-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="932a0-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="932a0-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="932a0-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="932a0-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="932a0-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="932a0-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="932a0-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="932a0-165">Войдите в клиент Printix как администратор.</span><span class="sxs-lookup"><span data-stu-id="932a0-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="932a0-166">В меню вверху щелкните значок в правом верхнем углу и выберите**Authentication**(Проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="932a0-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="932a0-168">На вкладке **Setup** (Настройка) выберите **Enable Azure/Office 365 authentication** (Включить проверку подлинности Azure/Office 365).</span><span class="sxs-lookup"><span data-stu-id="932a0-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="932a0-170">На вкладке **Azure** введите URL-адрес метаданных федерации в поле ввода **Federation metadata document** (Документ метаданных федерации).</span><span class="sxs-lookup"><span data-stu-id="932a0-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="932a0-171">Вложите XML-файл метаданных, который вы скачали из Azure AD, в [службу поддержки Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="932a0-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="932a0-172">Служба отправит этот файл на сервер и предоставит вам URL-адрес метаданных федерации.</span><span class="sxs-lookup"><span data-stu-id="932a0-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="932a0-174">Нажмите кнопку **Test** (Тестировать). Если проверка будет выполнена успешно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="932a0-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="932a0-175">После нажатия кнопки **тестирования** отобразится страница Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="932a0-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="932a0-176">Если на ней есть сообщение The test was successful (Проверка выполнена успешно), введите учетные данные для тестовой учетной записи Azure. Появится окно с сообщением Settings tested OK (Параметры успешно проверены). Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="932a0-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="932a0-178">Щелкните кнопку **Save** (Сохранить) на странице **Authentication** (Проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="932a0-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="932a0-179">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="932a0-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="932a0-180">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="932a0-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="932a0-181">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="932a0-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="932a0-182">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="932a0-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="932a0-183">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="932a0-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="932a0-185">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="932a0-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="932a0-186">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="932a0-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="932a0-188">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="932a0-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="932a0-190">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="932a0-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="932a0-192">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="932a0-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="932a0-194">а.</span><span class="sxs-lookup"><span data-stu-id="932a0-194">a.</span></span> <span data-ttu-id="932a0-195">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="932a0-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="932a0-196">b.</span><span class="sxs-lookup"><span data-stu-id="932a0-196">b.</span></span> <span data-ttu-id="932a0-197">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="932a0-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="932a0-198">c.</span><span class="sxs-lookup"><span data-stu-id="932a0-198">c.</span></span> <span data-ttu-id="932a0-199">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="932a0-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="932a0-200">d.</span><span class="sxs-lookup"><span data-stu-id="932a0-200">d.</span></span> <span data-ttu-id="932a0-201">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="932a0-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="932a0-202">Создание тестового пользователя Printix</span><span class="sxs-lookup"><span data-stu-id="932a0-202">Creating a Printix test user</span></span>

<span data-ttu-id="932a0-203">Цель этого раздела — создать пользователя с именем Britta Simon в приложении Printix.</span><span class="sxs-lookup"><span data-stu-id="932a0-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="932a0-204">Приложение Printix поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="932a0-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="932a0-205">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="932a0-205">There is no action item for you in this section.</span></span> <span data-ttu-id="932a0-206">Пользователь будет создан при попытке получить доступ к приложению Printix (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="932a0-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="932a0-207">Чтобы создать пользователя вручную, необходимо обратиться в [службу поддержки Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="932a0-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="932a0-208">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="932a0-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="932a0-209">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Printix.</span><span class="sxs-lookup"><span data-stu-id="932a0-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="932a0-211">**Чтобы назначить пользователя Britta Simon в Printix, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="932a0-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="932a0-212">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="932a0-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="932a0-214">В списке приложений выберите **Printix**.</span><span class="sxs-lookup"><span data-stu-id="932a0-214">In the applications list, select **Printix**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="932a0-216">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="932a0-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="932a0-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="932a0-218">Click **Add** button.</span></span> <span data-ttu-id="932a0-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="932a0-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="932a0-221">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="932a0-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="932a0-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="932a0-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="932a0-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="932a0-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="932a0-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="932a0-224">Testing single sign-on</span></span>

<span data-ttu-id="932a0-225">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="932a0-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="932a0-226">Щелкнув плитку Printix на панели доступа, вы автоматически войдете в приложение Printix.</span><span class="sxs-lookup"><span data-stu-id="932a0-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="932a0-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="932a0-227">Additional resources</span></span>

* [<span data-ttu-id="932a0-228">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="932a0-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="932a0-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="932a0-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

