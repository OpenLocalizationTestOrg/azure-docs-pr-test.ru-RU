---
title: "Руководство по интеграции Azure Active Directory с SAP NetWeaver | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в SAP NetWeaver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: ad4140eb1183094a67822ad92eabcd35101360b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="023f1-103">Руководство. Интеграция Azure Active Directory с SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="023f1-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="023f1-104">В этом руководстве описано, как интегрировать SAP NetWeaver с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="023f1-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="023f1-105">Интеграция SAP NetWeaver с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="023f1-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="023f1-106">С помощью Azure AD вы можете контролировать доступ к приложению SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="023f1-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
- <span data-ttu-id="023f1-107">Вы можете включить автоматический вход пользователей в SAP NetWeaver (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="023f1-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="023f1-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="023f1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="023f1-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="023f1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="023f1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="023f1-110">Prerequisites</span></span>

<span data-ttu-id="023f1-111">Чтобы настроить интеграцию Azure AD с SAP NetWeaver, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="023f1-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

- <span data-ttu-id="023f1-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="023f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="023f1-113">подписка SAP NetWeaver с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="023f1-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="023f1-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="023f1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="023f1-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="023f1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="023f1-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="023f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="023f1-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="023f1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="023f1-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="023f1-118">Scenario description</span></span>
<span data-ttu-id="023f1-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="023f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="023f1-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="023f1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="023f1-121">Добавление SAP NetWeaver из коллекции</span><span class="sxs-lookup"><span data-stu-id="023f1-121">Adding SAP NetWeaver from the gallery</span></span>
2. <span data-ttu-id="023f1-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="023f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="023f1-123">Добавление SAP NetWeaver из коллекции</span><span class="sxs-lookup"><span data-stu-id="023f1-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="023f1-124">Чтобы настроить интеграцию SAP NetWeaver с Azure AD, необходимо добавить SAP NetWeaver из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="023f1-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="023f1-125">**Чтобы добавить SAP NetWeaver из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="023f1-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="023f1-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="023f1-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="023f1-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="023f1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="023f1-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="023f1-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="023f1-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="023f1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="023f1-133">В поле поиска введите **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="023f1-133">In the search box, type **SAP NetWeaver**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="023f1-135">На панели результатов выберите **SAP NetWeaver** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="023f1-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="023f1-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="023f1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="023f1-138">В этом разделе описана настройка и проверка единого входа Azure AD в SAP NetWeaver с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="023f1-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="023f1-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в SAP NetWeaver соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="023f1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="023f1-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="023f1-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="023f1-141">Чтобы установить эту связь, следует указать **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="023f1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="023f1-142">Чтобы настроить и проверить единый вход Azure AD в SAP NetWeaver, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="023f1-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="023f1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="023f1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="023f1-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="023f1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="023f1-145">**[Создание тестового пользователя SAP NetWeaver](#creating-an-sap-netweaver-test-user)** требуется для создания пользователя Britta Simon в SAP NetWeaver, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="023f1-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="023f1-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="023f1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="023f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="023f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="023f1-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="023f1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="023f1-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="023f1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="023f1-150">**Чтобы настроить единый вход Azure AD в SAP NetWeaver, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="023f1-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="023f1-151">На портале Azure на странице интеграции с приложением **SAP NetWeaver** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="023f1-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="023f1-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="023f1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="023f1-155">В разделе **Домен и URL-адреса приложения SAP NetWeaver** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="023f1-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="023f1-157">а.</span><span class="sxs-lookup"><span data-stu-id="023f1-157">a.</span></span> <span data-ttu-id="023f1-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="023f1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="023f1-159">b.</span><span class="sxs-lookup"><span data-stu-id="023f1-159">b.</span></span> <span data-ttu-id="023f1-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="023f1-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="023f1-161">c.</span><span class="sxs-lookup"><span data-stu-id="023f1-161">c.</span></span> <span data-ttu-id="023f1-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`.</span><span class="sxs-lookup"><span data-stu-id="023f1-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="023f1-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="023f1-163">These values are not the real.</span></span> <span data-ttu-id="023f1-164">Измените их на фактические значения идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="023f1-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="023f1-165">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="023f1-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="023f1-166">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="023f1-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span></span> 

4. <span data-ttu-id="023f1-167">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="023f1-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="023f1-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="023f1-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="023f1-171">В разделе **Настройка SAP NetWeaver** щелкните **Настроить SAP NetWeaver**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="023f1-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span></span> <span data-ttu-id="023f1-172">Скопируйте **идентификатор сущности SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="023f1-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="023f1-174">Для настройки единого входа на стороне приложения **SAP NetWeaver** необходимо отправить скачанные **метаданные в формате XML** и **идентификатор сущности SAML** в [службу поддержки SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="023f1-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="023f1-175">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="023f1-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="023f1-176">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="023f1-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="023f1-177">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="023f1-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="023f1-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="023f1-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="023f1-179">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="023f1-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="023f1-181">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="023f1-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="023f1-182">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="023f1-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="023f1-184">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="023f1-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="023f1-186">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="023f1-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="023f1-188">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="023f1-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="023f1-190">А.</span><span class="sxs-lookup"><span data-stu-id="023f1-190">a.</span></span> <span data-ttu-id="023f1-191">В текстовом поле **Name** (Имя) введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="023f1-191">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="023f1-192">b.</span><span class="sxs-lookup"><span data-stu-id="023f1-192">b.</span></span> <span data-ttu-id="023f1-193">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="023f1-193">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="023f1-194">c.</span><span class="sxs-lookup"><span data-stu-id="023f1-194">c.</span></span> <span data-ttu-id="023f1-195">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="023f1-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="023f1-196">d.</span><span class="sxs-lookup"><span data-stu-id="023f1-196">d.</span></span> <span data-ttu-id="023f1-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="023f1-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="023f1-198">Создание тестового пользователя SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="023f1-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="023f1-199">В этом разделе описано, как создать пользователя Britta Simon в приложении SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="023f1-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="023f1-200">Чтобы добавить пользователей на платформу SAP NetWeaver, обратитесь в [службу поддержки SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="023f1-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="023f1-201">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="023f1-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="023f1-202">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="023f1-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="023f1-204">**Чтобы назначить пользователя Britta Simon в приложении SAP NetWeaver, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="023f1-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="023f1-205">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="023f1-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="023f1-207">В списке приложений выберите **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="023f1-207">In the applications list, select **SAP NetWeaver**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="023f1-209">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="023f1-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="023f1-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="023f1-211">Click **Add** button.</span></span> <span data-ttu-id="023f1-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="023f1-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="023f1-214">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="023f1-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="023f1-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="023f1-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="023f1-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="023f1-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="023f1-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="023f1-217">Testing single sign-on</span></span>

<span data-ttu-id="023f1-218">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="023f1-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="023f1-219">Щелкнув плитку SAP NetWeaver на панели доступа, вы автоматически войдете в приложение SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="023f1-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="023f1-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="023f1-220">Additional resources</span></span>

* [<span data-ttu-id="023f1-221">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="023f1-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="023f1-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="023f1-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

