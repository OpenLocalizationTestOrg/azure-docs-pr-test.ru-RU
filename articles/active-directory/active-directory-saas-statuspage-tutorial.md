---
title: "Руководство по интеграции Azure Active Directory и StatusPage | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и StatusPage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="e0ba8-103">Руководство. Интеграция Azure Active Directory и StatusPage</span><span class="sxs-lookup"><span data-stu-id="e0ba8-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="e0ba8-104">В этом руководстве описано, как интегрировать StatusPage с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e0ba8-105">Интеграция приложения StatusPage с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0ba8-106">С помощью Azure AD вы можете контролировать доступ к приложению StatusPage.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="e0ba8-107">Вы можете включить автоматический вход пользователей в StatusPage (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0ba8-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e0ba8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0ba8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e0ba8-110">Prerequisites</span></span>

<span data-ttu-id="e0ba8-111">Чтобы настроить интеграцию Azure AD с приложением StatusPage, вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="e0ba8-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="e0ba8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e0ba8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0ba8-113">подписка StatusPage с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e0ba8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e0ba8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e0ba8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0ba8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e0ba8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e0ba8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e0ba8-118">Scenario description</span></span>
<span data-ttu-id="e0ba8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e0ba8-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e0ba8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0ba8-121">Добавление StatusPage из коллекции.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="e0ba8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0ba8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="e0ba8-123">Добавление StatusPage из коллекции.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="e0ba8-124">Чтобы настроить интеграцию приложения StatusPage с Azure AD, вам нужно добавить StatusPage из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0ba8-125">**Чтобы добавить StatusPage из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e0ba8-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ba8-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0ba8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e0ba8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e0ba8-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e0ba8-133">В поле поиска введите **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-133">In the search box, type **StatusPage**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="e0ba8-135">На панели результатов выберите **StatusPage** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0ba8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0ba8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0ba8-138">В этом разделе описана настройка и проверка единого входа Azure AD в StatusPage с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e0ba8-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в StatusPage соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="e0ba8-140">То есть необходимо установить связь между пользователем Azure AD и соответствующим пользователем в StatusPage.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="e0ba8-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в StatusPage.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e0ba8-142">Чтобы настроить и проверить единый вход Azure AD в приложении StatusPage, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0ba8-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0ba8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0ba8-145">**[Создание тестового пользователя StatusPage](#creating-a-statuspage-test-user)** требуется для того, чтобы в StatusPage существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e0ba8-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0ba8-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0ba8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0ba8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0ba8-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении StatusPage.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="e0ba8-150">**Чтобы настроить единый вход Azure AD в StatusPage, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e0ba8-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ba8-151">На портале Azure на странице интеграции с приложением **StatusPage** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e0ba8-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="e0ba8-155">В разделе **Домены и URL-адреса приложения StatusPage** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="e0ba8-157">а.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-157">a.</span></span> <span data-ttu-id="e0ba8-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="e0ba8-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="e0ba8-159">b.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-159">b.</span></span> <span data-ttu-id="e0ba8-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="e0ba8-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="e0ba8-161">Обратитесь в службу поддержки StatusPage по адресу [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io), чтобы запросить метаданные, необходимые для настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="e0ba8-162">а.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-162">a.</span></span> <span data-ttu-id="e0ba8-163">В метаданных скопируйте значение издателя и вставьте его в текстовое поле **Идентификатор** .</span><span class="sxs-lookup"><span data-stu-id="e0ba8-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="e0ba8-164">b.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-164">b.</span></span> <span data-ttu-id="e0ba8-165">В полученных метаданных скопируйте значение URL-адреса ответа и вставьте его в текстовое поле **URL-адрес ответа** .</span><span class="sxs-lookup"><span data-stu-id="e0ba8-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="e0ba8-166">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="e0ba8-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e0ba8-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e0ba8-170">В разделе **Конфигурация StatusPage** щелкните **Настроить StatusPage**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e0ba8-171">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="e0ba8-173">В другом окне браузера войдите на корпоративный сайт StatusPage с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="e0ba8-174">На главной панели инструментов щелкните **Manage Account**(Управление учетной записью).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="e0ba8-176">Выберите вкладку **Single Sign-on** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="e0ba8-178">На странице настройки единого входа выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="e0ba8-181">а.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-181">a.</span></span> <span data-ttu-id="e0ba8-182">В текстовое поле **SSO Target URL** (Целевой URL-адрес единого входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e0ba8-183">b.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-183">b.</span></span> <span data-ttu-id="e0ba8-184">Откройте скачанный сертификат в блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Certificate** (Сертификат).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="e0ba8-185">c.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-185">c.</span></span> <span data-ttu-id="e0ba8-186">Щелкните **SAVE CONFIGURATION** (Сохранить конфигурацию).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="e0ba8-187">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e0ba8-188">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e0ba8-189">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0ba8-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0ba8-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0ba8-191">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e0ba8-193">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e0ba8-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ba8-194">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e0ba8-196">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e0ba8-198">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0ba8-200">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e0ba8-202">а.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-202">a.</span></span> <span data-ttu-id="e0ba8-203">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e0ba8-204">b.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-204">b.</span></span> <span data-ttu-id="e0ba8-205">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e0ba8-206">c.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-206">c.</span></span> <span data-ttu-id="e0ba8-207">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e0ba8-208">d.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-208">d.</span></span> <span data-ttu-id="e0ba8-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="e0ba8-210">Создание тестового пользователя в приложении StatusPage</span><span class="sxs-lookup"><span data-stu-id="e0ba8-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="e0ba8-211">Цель этого раздела — создать в приложении StatusPage пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="e0ba8-212">Приложение StatusPage поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="e0ba8-213">Эта функция уже включена в ходе [настройки единого входа в Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="e0ba8-214">**Чтобы создать в приложении StatusPage пользователя с именем Britta Simon, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e0ba8-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ba8-215">Войдите на корпоративный сайт StatusPage с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="e0ba8-216">В меню вверху щелкните **Manage Account**(Управление учетной записью).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="e0ba8-218">Перейдите на вкладку **Team Members** (Участники команды).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-218">Click the **Team Members** tab.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="e0ba8-220">Щелкните **ADD TEAM MEMBER** (Добавить участника команды).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="e0ba8-222">Введите в текстовые поля **Email Address** (Электронный адрес), **First Name** (Имя) и **Sur Name** (Фамилия) соответствующие данные действительного пользователя, которого вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="e0ba8-224">Для параметра **Role** (Роль) выберите значение **Client Administrator** (Администратор клиента).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="e0ba8-225">Щелкните **CREATE ACCOUNT** (Создать учетную запись).</span><span class="sxs-lookup"><span data-stu-id="e0ba8-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0ba8-226">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0ba8-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0ba8-227">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к StatusPage.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e0ba8-229">**Чтобы назначить пользователя Britta Simon приложению StatusPage, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e0ba8-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="e0ba8-230">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e0ba8-232">Из списка приложений выберите **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-232">In the applications list, select **StatusPage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="e0ba8-234">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e0ba8-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-236">Click **Add** button.</span></span> <span data-ttu-id="e0ba8-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e0ba8-239">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e0ba8-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e0ba8-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e0ba8-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e0ba8-242">Testing single sign-on</span></span>

<span data-ttu-id="e0ba8-243">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e0ba8-244">Щелкнув элемент StatusPage на панели доступа, вы автоматически войдете в приложение StatusPage.</span><span class="sxs-lookup"><span data-stu-id="e0ba8-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0ba8-245">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e0ba8-245">Additional resources</span></span>

* [<span data-ttu-id="e0ba8-246">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0ba8-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0ba8-247">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e0ba8-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

