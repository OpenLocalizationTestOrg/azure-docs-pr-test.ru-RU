---
title: "Учебник. Интеграция Azure Active Directory с FreshGrade | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в FreshGrade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 3ff3e5aab679f8ee610c98f8a4089308adcce48f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="90684-103">Учебник. Интеграция Azure Active Directory с FreshGrade</span><span class="sxs-lookup"><span data-stu-id="90684-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="90684-104">В этом учебнике описано, как интегрировать FreshGrade с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90684-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90684-105">Интеграция Azure AD с приложением FreshGrade обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="90684-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="90684-106">С помощью Azure AD вы можете контролировать доступ к FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="90684-106">You can control in Azure AD who has access to FreshGrade</span></span>
- <span data-ttu-id="90684-107">Вы можете включить автоматический вход пользователей во FreshGrade (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90684-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90684-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="90684-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="90684-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90684-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90684-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90684-110">Prerequisites</span></span>

<span data-ttu-id="90684-111">Чтобы настроить интеграцию Azure AD с приложением FreshGrade, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="90684-111">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

- <span data-ttu-id="90684-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="90684-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90684-113">подписка FreshGrade с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="90684-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="90684-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="90684-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="90684-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="90684-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90684-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="90684-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="90684-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90684-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="90684-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="90684-118">Scenario description</span></span>
<span data-ttu-id="90684-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="90684-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90684-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="90684-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90684-121">Добавление FreshGrade из коллекции</span><span class="sxs-lookup"><span data-stu-id="90684-121">Adding FreshGrade from the gallery</span></span>
2. <span data-ttu-id="90684-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="90684-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-the-gallery"></a><span data-ttu-id="90684-123">Добавление FreshGrade из коллекции</span><span class="sxs-lookup"><span data-stu-id="90684-123">Adding FreshGrade from the gallery</span></span>
<span data-ttu-id="90684-124">Чтобы настроить интеграцию FreshGrade с Azure AD, необходимо добавить FreshGrade из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="90684-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="90684-125">**Чтобы добавить FreshGrade из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="90684-125">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="90684-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="90684-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="90684-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="90684-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="90684-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="90684-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="90684-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="90684-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="90684-133">В поле поиска введите **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="90684-133">In the search box, type **FreshGrade**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="90684-135">На панели результатов выберите **FreshGrade** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="90684-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90684-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="90684-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90684-138">В этом разделе описана настройка и проверка единого входа Azure AD во FreshGrade с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90684-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="90684-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь во FreshGrade соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90684-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="90684-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем во FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="90684-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="90684-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** во FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="90684-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="90684-142">Чтобы настроить и проверить единый вход Azure AD во FreshGrade, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="90684-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="90684-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="90684-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="90684-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90684-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90684-145">**[Создание тестового пользователя FreshGrade](#creating-a-freshgrade-test-user)** требуется для создания пользователя Britta Simon во FreshGrade, связанного с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90684-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="90684-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90684-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="90684-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90684-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90684-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="90684-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90684-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="90684-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="90684-150">**Чтобы настроить единый вход Azure AD во FreshGrade, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="90684-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="90684-151">На портале Azure на странице интеграции с приложением **FreshGrade** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="90684-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="90684-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="90684-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="90684-155">В разделе **Домены и URL-адреса приложения FreshGrade** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="90684-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="90684-157">а.</span><span class="sxs-lookup"><span data-stu-id="90684-157">a.</span></span> <span data-ttu-id="90684-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="90684-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="90684-159">b.</span><span class="sxs-lookup"><span data-stu-id="90684-159">b.</span></span> <span data-ttu-id="90684-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="90684-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="90684-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="90684-161">These values are not real.</span></span> <span data-ttu-id="90684-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="90684-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="90684-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов FreshGrade](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="90684-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span></span> 
 


4. <span data-ttu-id="90684-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="90684-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="90684-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="90684-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="90684-168">В разделе **Настройка FreshGrade** щелкните **Настроить FreshGrade**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="90684-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span></span> <span data-ttu-id="90684-169">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="90684-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="90684-171">Для создания URL-адреса **метаданных** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="90684-171">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="90684-172">а.</span><span class="sxs-lookup"><span data-stu-id="90684-172">a.</span></span> <span data-ttu-id="90684-173">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="90684-173">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="90684-175">b.</span><span class="sxs-lookup"><span data-stu-id="90684-175">b.</span></span> <span data-ttu-id="90684-176">Щелкните **Конечные точки**, чтобы открыть диалоговое окно **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="90684-176">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="90684-178">c.</span><span class="sxs-lookup"><span data-stu-id="90684-178">c.</span></span> <span data-ttu-id="90684-179">Нажмите кнопку "Копировать", чтобы скопировать URL-адрес **документа метаданных федерации**, а затем вставьте его в блокнот.</span><span class="sxs-lookup"><span data-stu-id="90684-179">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="90684-181">г)</span><span class="sxs-lookup"><span data-stu-id="90684-181">d.</span></span> <span data-ttu-id="90684-182">Теперь перейдите на страницу свойств **FreshGrade** и скопируйте **идентификатор приложения** с помощью кнопки **Копировать**, а затем вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="90684-182">Now go to the property page of **FreshGrade** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="90684-184">д.</span><span class="sxs-lookup"><span data-stu-id="90684-184">e.</span></span> <span data-ttu-id="90684-185">Создайте **URL-адрес метаданных** по следующему шаблону: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`.</span><span class="sxs-lookup"><span data-stu-id="90684-185">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="90684-186">Чтобы настроить единый вход на стороне **FreshGrade**, нужно отправить скачанный **URL-адрес метаданных** и **URL-адрес службы единого входа SAML** в [службу поддержки FreshGrade](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="90684-186">To configure single sign-on on **FreshGrade** side, you need to send the **Metadata URL** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="90684-187">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="90684-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="90684-188">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="90684-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="90684-189">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="90684-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="90684-190">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="90684-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90684-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="90684-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="90684-192">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="90684-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="90684-194">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="90684-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="90684-195">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="90684-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90684-197">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="90684-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90684-199">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="90684-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90684-201">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="90684-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90684-203">а.</span><span class="sxs-lookup"><span data-stu-id="90684-203">a.</span></span> <span data-ttu-id="90684-204">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90684-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90684-205">b.</span><span class="sxs-lookup"><span data-stu-id="90684-205">b.</span></span> <span data-ttu-id="90684-206">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90684-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90684-207">c.</span><span class="sxs-lookup"><span data-stu-id="90684-207">c.</span></span> <span data-ttu-id="90684-208">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="90684-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="90684-209">d.</span><span class="sxs-lookup"><span data-stu-id="90684-209">d.</span></span> <span data-ttu-id="90684-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="90684-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="90684-211">Создание тестового пользователя FreshGrade</span><span class="sxs-lookup"><span data-stu-id="90684-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="90684-212">В этом разделе описано, как создать пользователя Britta Simon в приложении FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="90684-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="90684-213">Обратитесь в [службу поддержки FreshGrade](mailTo:support@freshgrade.com), чтобы добавить пользователей на платформу FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="90684-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="90684-214">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="90684-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="90684-215">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="90684-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="90684-217">**Чтобы назначить пользователя Britta Simon во FreshGrade, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="90684-217">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="90684-218">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="90684-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="90684-220">В списке приложений выберите **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="90684-220">In the applications list, select **FreshGrade**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="90684-222">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="90684-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="90684-224">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="90684-224">Click **Add** button.</span></span> <span data-ttu-id="90684-225">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="90684-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="90684-227">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="90684-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="90684-228">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="90684-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90684-229">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="90684-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="90684-230">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="90684-230">Testing single sign-on</span></span>

<span data-ttu-id="90684-231">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="90684-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="90684-232">Щелкнув элемент FreshGrade на панели доступа, вы автоматически войдете в приложение FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="90684-232">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>
<span data-ttu-id="90684-233">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="90684-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="90684-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="90684-234">Additional resources</span></span>

* [<span data-ttu-id="90684-235">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90684-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90684-236">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="90684-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

