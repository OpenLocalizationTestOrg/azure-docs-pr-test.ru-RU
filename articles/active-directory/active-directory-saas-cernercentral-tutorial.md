---
title: "Руководство по интеграции Azure Active Directory с Cerner Central | Документы Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и Cerner Central."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="a5ef8-103">Руководство. Интеграция Azure Active Directory с Cerner Central</span><span class="sxs-lookup"><span data-stu-id="a5ef8-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="a5ef8-104">В этом руководстве описано, как интегрировать Cerner Central с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5ef8-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5ef8-105">Интеграция Azure AD с приложением Cerner Central обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a5ef8-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5ef8-106">С помощью Azure AD вы можете контролировать доступ к Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="a5ef8-107">Вы можете включить автоматический вход пользователей в Cerner Central (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5ef8-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a5ef8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5ef8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5ef8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a5ef8-110">Prerequisites</span></span>

<span data-ttu-id="a5ef8-111">Чтобы настроить интеграцию Azure AD с Cerner Central, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a5ef8-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="a5ef8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a5ef8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5ef8-113">утвержденная системная учетная запись Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="a5ef8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5ef8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a5ef8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5ef8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5ef8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5ef8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5ef8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a5ef8-118">Scenario description</span></span>
<span data-ttu-id="a5ef8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5ef8-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5ef8-121">Добавление Cerner Central из коллекции</span><span class="sxs-lookup"><span data-stu-id="a5ef8-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="a5ef8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5ef8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="a5ef8-123">Добавление Cerner Central из коллекции</span><span class="sxs-lookup"><span data-stu-id="a5ef8-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="a5ef8-124">Чтобы настроить интеграцию Cerner Central с Azure AD, необходимо добавить Cerner Central из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5ef8-125">**Чтобы добавить Cerner Central из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="a5ef8-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ef8-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a5ef8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5ef8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a5ef8-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a5ef8-133">В поле поиска введите **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-133">In the search box, type **Cerner Central**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="a5ef8-135">На панели результатов выберите **Cerner Central** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5ef8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5ef8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a5ef8-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Cerner Central с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a5ef8-139">Для работы единого входа Azure AD необходимо знать, какой пользователь в Cerner Central соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="a5ef8-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="a5ef8-141">Чтобы настроить и проверить единый вход Azure AD в Cerner Central, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5ef8-142">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5ef8-143">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5ef8-144">**[Создание тестового пользователя Cerner Central](#creating-a-cerner-central-test-user)** требуется для создания пользователя Britta Simon в Cerner Central, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="a5ef8-145">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5ef8-146">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5ef8-147">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5ef8-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5ef8-148">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="a5ef8-149">**Чтобы настроить единый вход Azure AD в Cerner Central, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="a5ef8-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ef8-150">На портале Azure на странице интеграции с приложением **Cerner Central** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a5ef8-152">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="a5ef8-154">В разделе **Домены и URL-адреса приложения Cerner Central** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="a5ef8-156">а.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-156">a.</span></span> <span data-ttu-id="a5ef8-157">В текстовое поле **Идентификатор** введите значение в приведенном ниже формате.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="a5ef8-158">b.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-158">b.</span></span> <span data-ttu-id="a5ef8-159">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="a5ef8-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="a5ef8-160">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-160">These values are not the real.</span></span> <span data-ttu-id="a5ef8-161">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a5ef8-162">Чтобы получить эти значения, обратитесь в [службу поддержки Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="a5ef8-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="a5ef8-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a5ef8-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="a5ef8-165">Для создания URL-адреса **метаданных** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="a5ef8-166">а.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-166">a.</span></span> <span data-ttu-id="a5ef8-167">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-167">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="a5ef8-169">b.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-169">b.</span></span> <span data-ttu-id="a5ef8-170">Щелкните **Конечные точки**, чтобы открыть диалоговое окно **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="a5ef8-172">c.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-172">c.</span></span> <span data-ttu-id="a5ef8-173">Нажмите кнопку "Копировать", чтобы скопировать URL-адрес **документа метаданных федерации**, а затем вставьте его в блокнот.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="a5ef8-175">г)</span><span class="sxs-lookup"><span data-stu-id="a5ef8-175">d.</span></span> <span data-ttu-id="a5ef8-176">Теперь перейдите к странице свойств **Cerner Central** и скопируйте **идентификатор приложения** с помощью кнопки **Копировать**, а затем вставьте его в блокнот.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="a5ef8-178">д.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-178">e.</span></span> <span data-ttu-id="a5ef8-179">Создайте **URL-адрес метаданных** по следующему шаблону: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="a5ef8-180">Для настройки единого входа на стороне **Cerner Central** необходимо отправить **URL-адрес метаданных** в [службу поддержки Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="a5ef8-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="a5ef8-181">Специалисты службы поддержки настроят единый вход на стороне приложения для завершения интеграции.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="a5ef8-182">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a5ef8-183">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5ef8-184">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a5ef8-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5ef8-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5ef8-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5ef8-186">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Создание пользователя Azure AD][100]

<span data-ttu-id="a5ef8-188">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a5ef8-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ef8-189">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5ef8-191">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5ef8-193">Щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5ef8-195">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5ef8-197">а.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-197">a.</span></span> <span data-ttu-id="a5ef8-198">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5ef8-199">b.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-199">b.</span></span> <span data-ttu-id="a5ef8-200">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a5ef8-201">c.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-201">c.</span></span> <span data-ttu-id="a5ef8-202">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5ef8-203">d.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-203">d.</span></span> <span data-ttu-id="a5ef8-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="a5ef8-205">Создание тестового пользователя Cerner Central</span><span class="sxs-lookup"><span data-stu-id="a5ef8-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="a5ef8-206">Приложение **Cerner Central** разрешает аутентификацию посредством любого поставщика федеративных удостоверений.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="a5ef8-207">Если пользователь может войти на домашнюю страницу приложения, то он является федеративным и не требует подготовки вручную.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a5ef8-208">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5ef8-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a5ef8-209">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a5ef8-211">**Чтобы назначить пользователя Britta Simon в Cerner Central, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="a5ef8-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="a5ef8-212">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a5ef8-214">В списке приложений выберите **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-214">In the applications list, select **Cerner Central**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="a5ef8-216">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a5ef8-218">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-218">Click **Add** button.</span></span> <span data-ttu-id="a5ef8-219">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a5ef8-221">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5ef8-222">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5ef8-223">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5ef8-224">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a5ef8-224">Testing single sign-on</span></span>

<span data-ttu-id="a5ef8-225">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5ef8-226">Щелкнув элемент Cerner Central на панели доступа, вы автоматически войдете в приложение Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="a5ef8-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="a5ef8-227">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a5ef8-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5ef8-228">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a5ef8-228">Additional resources</span></span>

* [<span data-ttu-id="a5ef8-229">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5ef8-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5ef8-230">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5ef8-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

