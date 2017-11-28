---
title: "Руководство по интеграции Azure Active Directory с Collaborative Innovation | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Collaborative Innovation."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 5706ba9f4e7c92de77a0edc5146aa150de379c9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="ca152-103">Руководство по интеграции Azure Active Directory с Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="ca152-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="ca152-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="ca152-104">In this tutorial, you learn how to integrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca152-105">Интеграция Azure AD с приложением Collaborative Innovation обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="ca152-105">Integrating Collaborative Innovation with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ca152-106">С помощью Azure AD вы можете контролировать доступ к Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="ca152-106">You can control in Azure AD who has access to Collaborative Innovation</span></span>
- <span data-ttu-id="ca152-107">Вы можете включить автоматический вход пользователей в Collaborative Innovation (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca152-107">You can enable your users to automatically get signed-on to Collaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ca152-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ca152-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ca152-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ca152-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca152-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ca152-110">Prerequisites</span></span>

<span data-ttu-id="ca152-111">Чтобы настроить интеграцию Azure AD с Collaborative Innovation, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ca152-111">To configure Azure AD integration with Collaborative Innovation, you need the following items:</span></span>

- <span data-ttu-id="ca152-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ca152-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca152-113">подписка на Collaborative Innovation с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ca152-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca152-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ca152-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca152-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ca152-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca152-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ca152-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca152-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca152-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca152-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ca152-118">Scenario description</span></span>
<span data-ttu-id="ca152-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ca152-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca152-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ca152-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca152-121">Добавление Collaborative Innovation из галереи</span><span class="sxs-lookup"><span data-stu-id="ca152-121">Adding Collaborative Innovation from the gallery</span></span>
2. <span data-ttu-id="ca152-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca152-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-the-gallery"></a><span data-ttu-id="ca152-123">Добавление Collaborative Innovation из галереи</span><span class="sxs-lookup"><span data-stu-id="ca152-123">Adding Collaborative Innovation from the gallery</span></span>
<span data-ttu-id="ca152-124">Чтобы настроить интеграцию Collaborative Innovation с Azure AD, вам потребуется добавить Collaborative Innovation из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ca152-124">To configure the integration of Collaborative Innovation into Azure AD, you need to add Collaborative Innovation from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ca152-125">**Чтобы добавить Collaborative Innovation из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ca152-125">**To add Collaborative Innovation from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ca152-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ca152-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ca152-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ca152-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ca152-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ca152-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ca152-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ca152-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ca152-133">В поле поиска введите **Collaborative Innovation**.</span><span class="sxs-lookup"><span data-stu-id="ca152-133">In the search box, type **Collaborative Innovation**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="ca152-135">На панели результатов выберите **Collaborative Innovation** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="ca152-135">In the results panel, select **Collaborative Innovation**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ca152-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca152-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ca152-138">В этом разделе описана настройка и проверка единого входа Azure AD в Collaborative Innovation с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca152-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ca152-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Collaborative Innovation соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca152-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Collaborative Innovation is to a user in Azure AD.</span></span> <span data-ttu-id="ca152-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="ca152-140">In other words, a link relationship between an Azure AD user and the related user in Collaborative Innovation needs to be established.</span></span>

<span data-ttu-id="ca152-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="ca152-141">In Collaborative Innovation, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ca152-142">Чтобы настроить и проверить единый вход Azure AD в Collaborative Innovation, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ca152-142">To configure and test Azure AD single sign-on with Collaborative Innovation, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ca152-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ca152-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ca152-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca152-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca152-145">**[Создание тестового пользователя Collaborative Innovation](#creating-a-collaborative-innovation-test-user)** требуется для создания в Collaborative Innovation пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca152-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - to have a counterpart of Britta Simon in Collaborative Innovation that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca152-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca152-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca152-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ca152-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ca152-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca152-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ca152-149">В данном разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="ca152-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="ca152-150">**Чтобы настроить единый вход Azure AD в Collaborative Innovation, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ca152-150">**To configure Azure AD single sign-on with Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="ca152-151">На портале Azure на странице интеграции с приложением **Collaborative Innovation** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ca152-151">In the Azure portal, on the **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ca152-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ca152-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="ca152-155">В разделе **Домены и URL-адреса приложения Collaborative Innovation** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ca152-155">On the **Collaborative Innovation Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="ca152-157">а.</span><span class="sxs-lookup"><span data-stu-id="ca152-157">a.</span></span> <span data-ttu-id="ca152-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="ca152-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="ca152-159">b.</span><span class="sxs-lookup"><span data-stu-id="ca152-159">b.</span></span> <span data-ttu-id="ca152-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="ca152-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ca152-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ca152-161">These values are not real.</span></span> <span data-ttu-id="ca152-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="ca152-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ca152-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Collaborative Innovation](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="ca152-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) to get these values.</span></span>  

4. <span data-ttu-id="ca152-164">Приложение Collaborative Innovation ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="ca152-164">Collaborative Innovation application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ca152-165">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="ca152-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="ca152-166">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="ca152-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ca152-167">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="ca152-167">The following screenshot shows an example for this.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="ca152-169">В разделе **Атрибуты пользователя** установите флажок **Просмотреть и изменить все другие атрибуты пользователей**, чтобы развернуть атрибуты.</span><span class="sxs-lookup"><span data-stu-id="ca152-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="ca152-170">Выполните следующие действия для каждого отображаемого атрибута.</span><span class="sxs-lookup"><span data-stu-id="ca152-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="ca152-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="ca152-171">Attribute Name</span></span> | <span data-ttu-id="ca152-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="ca152-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="ca152-173">givenname</span><span class="sxs-lookup"><span data-stu-id="ca152-173">givenname</span></span> | <span data-ttu-id="ca152-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="ca152-174">user.givenname</span></span> |
    | <span data-ttu-id="ca152-175">surname</span><span class="sxs-lookup"><span data-stu-id="ca152-175">surname</span></span> | <span data-ttu-id="ca152-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="ca152-176">user.surname</span></span> |
    | <span data-ttu-id="ca152-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="ca152-177">emailaddress</span></span> | <span data-ttu-id="ca152-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ca152-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="ca152-179">name</span><span class="sxs-lookup"><span data-stu-id="ca152-179">name</span></span> | <span data-ttu-id="ca152-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="ca152-180">user.userprincipalname</span></span> |

    <span data-ttu-id="ca152-181">а.</span><span class="sxs-lookup"><span data-stu-id="ca152-181">a.</span></span> <span data-ttu-id="ca152-182">Щелкните атрибут, чтобы открыть окно **Изменить атрибут**.</span><span class="sxs-lookup"><span data-stu-id="ca152-182">Click the attribute to open the **Edit Attribute** window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="ca152-184">b.</span><span class="sxs-lookup"><span data-stu-id="ca152-184">b.</span></span> <span data-ttu-id="ca152-185">Удалите значение URL-адреса из **пространства имен**.</span><span class="sxs-lookup"><span data-stu-id="ca152-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="ca152-186">c.</span><span class="sxs-lookup"><span data-stu-id="ca152-186">c.</span></span> <span data-ttu-id="ca152-187">Нажмите кнопку **ОК**, чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="ca152-187">Click **Ok** to save the setting.</span></span>

6. <span data-ttu-id="ca152-188">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ca152-188">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="ca152-190">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ca152-190">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ca152-192">Чтобы настроить единый вход на стороне **Collaborative Innovation**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Collaborative Innovation](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="ca152-192">To configure single sign-on on **Collaborative Innovation** side, you need to send the downloaded **Metadata XML** to [Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="ca152-193">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="ca152-193">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ca152-194">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ca152-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ca152-195">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ca152-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ca152-196">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ca152-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ca152-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca152-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ca152-198">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ca152-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ca152-200">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ca152-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ca152-201">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ca152-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ca152-203">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ca152-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ca152-205">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ca152-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ca152-207">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ca152-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ca152-209">а.</span><span class="sxs-lookup"><span data-stu-id="ca152-209">a.</span></span> <span data-ttu-id="ca152-210">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca152-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca152-211">b.</span><span class="sxs-lookup"><span data-stu-id="ca152-211">b.</span></span> <span data-ttu-id="ca152-212">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ca152-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ca152-213">c.</span><span class="sxs-lookup"><span data-stu-id="ca152-213">c.</span></span> <span data-ttu-id="ca152-214">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ca152-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ca152-215">d.</span><span class="sxs-lookup"><span data-stu-id="ca152-215">d.</span></span> <span data-ttu-id="ca152-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ca152-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="ca152-217">Создание тестового пользователя Collaborative Innovation</span><span class="sxs-lookup"><span data-stu-id="ca152-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="ca152-218">Чтобы пользователи Azure AD могли выполнять вход в Collaborative Innovation, они должны быть подготовлены для Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="ca152-218">To enable Azure AD users to log in to Collaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="ca152-219">Для этого приложения подготовка выполняется автоматически, так как приложение поддерживает JIT-подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="ca152-219">In case of this application provisioning is automatic as the application supports just in time user provisioning.</span></span> <span data-ttu-id="ca152-220">Поэтому в данном случае никакие действия выполнять не нужно.</span><span class="sxs-lookup"><span data-stu-id="ca152-220">So there is no need to perform any steps here.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ca152-221">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca152-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ca152-222">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="ca152-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Collaborative Innovation.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ca152-224">**Чтобы назначить пользователя Britta Simon в Collaborative Innovation, выполните следующее:**</span><span class="sxs-lookup"><span data-stu-id="ca152-224">**To assign Britta Simon to Collaborative Innovation, perform the following steps:**</span></span>

1. <span data-ttu-id="ca152-225">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ca152-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ca152-227">В списке приложений выберите **Collaborative Innovation**.</span><span class="sxs-lookup"><span data-stu-id="ca152-227">In the applications list, select **Collaborative Innovation**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="ca152-229">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ca152-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ca152-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ca152-231">Click **Add** button.</span></span> <span data-ttu-id="ca152-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ca152-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ca152-234">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ca152-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ca152-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ca152-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca152-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ca152-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ca152-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ca152-237">Testing single sign-on</span></span>

<span data-ttu-id="ca152-238">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ca152-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ca152-239">При нажатии элемента "Collaborative Innovation" на панели доступа, должна появиться страница приложения Collaborative Innovation.</span><span class="sxs-lookup"><span data-stu-id="ca152-239">When you click the Collaborative Innovation tile in the Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="ca152-240">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca152-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ca152-241">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ca152-241">Additional resources</span></span>

* [<span data-ttu-id="ca152-242">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca152-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca152-243">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ca152-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

