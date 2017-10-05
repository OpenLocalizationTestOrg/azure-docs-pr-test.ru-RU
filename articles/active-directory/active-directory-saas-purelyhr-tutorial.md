---
title: "Руководство по интеграции Azure Active Directory с PurelyHR | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="83eb2-103">Руководство. Интеграция Azure Active Directory с PurelyHR</span><span class="sxs-lookup"><span data-stu-id="83eb2-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="83eb2-104">В этом руководстве описано, как интегрировать PurelyHR с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83eb2-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83eb2-105">Интеграция Azure AD с приложением PurelyHR обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="83eb2-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="83eb2-106">С помощью Azure AD вы можете контролировать доступ к PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="83eb2-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="83eb2-107">Вы можете включить автоматический вход пользователей в PurelyHR (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83eb2-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83eb2-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="83eb2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="83eb2-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83eb2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83eb2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83eb2-110">Prerequisites</span></span>

<span data-ttu-id="83eb2-111">Чтобы настроить интеграцию Azure AD с PurelyHR, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="83eb2-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="83eb2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="83eb2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83eb2-113">подписка PurelyHR с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="83eb2-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83eb2-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="83eb2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83eb2-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="83eb2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83eb2-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="83eb2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83eb2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83eb2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83eb2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="83eb2-118">Scenario description</span></span>
<span data-ttu-id="83eb2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="83eb2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83eb2-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="83eb2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83eb2-121">Добавление PurelyHR из коллекции</span><span class="sxs-lookup"><span data-stu-id="83eb2-121">Adding PurelyHR from the gallery</span></span>
2. <span data-ttu-id="83eb2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83eb2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="83eb2-123">Добавление PurelyHR из коллекции</span><span class="sxs-lookup"><span data-stu-id="83eb2-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="83eb2-124">Чтобы настроить интеграцию PurelyHR с Azure AD, нужно добавить PurelyHR из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="83eb2-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="83eb2-125">**Чтобы добавить PurelyHR из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="83eb2-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="83eb2-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="83eb2-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="83eb2-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="83eb2-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="83eb2-133">В поле поиска введите **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-133">In the search box, type **PurelyHR**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="83eb2-135">На панели результатов выберите **PurelyHR** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="83eb2-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83eb2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83eb2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83eb2-138">В этом разделе описана настройка и проверка единого входа Azure AD в PurelyHR с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83eb2-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="83eb2-139">Для работы единого входа в Azure AD нужно знать, какой пользователь в PurelyHR соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83eb2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="83eb2-140">Иными словами, нужно установить связь между пользователем в Azure AD и соответствующим пользователем в PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="83eb2-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="83eb2-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="83eb2-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="83eb2-142">Чтобы настроить и проверить единый вход Azure AD в PurelyHR, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="83eb2-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="83eb2-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="83eb2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="83eb2-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83eb2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83eb2-145">**[Создание тестового пользователя PurelyHR](#creating-a-purelyhr-test-user)** требуется для создания пользователя Britta Simon в PurelyHR, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83eb2-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="83eb2-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83eb2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83eb2-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="83eb2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83eb2-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83eb2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83eb2-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="83eb2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="83eb2-150">**Чтобы настроить единый вход Azure AD в PurelyHR, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="83eb2-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="83eb2-151">На портале Azure на странице интеграции с приложением **PurelyHR** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="83eb2-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="83eb2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="83eb2-155">Если вы хотите настроить приложение в режиме, инициированном **поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения PurelyHR** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="83eb2-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="83eb2-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyID>.purelyhr.com/sso-consume`.</span><span class="sxs-lookup"><span data-stu-id="83eb2-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="83eb2-158">Установите флажок **Показать дополнительные параметры URL-адресов**, если вы хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="83eb2-160">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://<companyID>.purelyhr.com/sso-initiate`.</span><span class="sxs-lookup"><span data-stu-id="83eb2-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="83eb2-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="83eb2-161">These values are not the real.</span></span> <span data-ttu-id="83eb2-162">Измените их на фактические значения URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="83eb2-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="83eb2-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов PurelyHR](http://support.purelyhr.com/).</span><span class="sxs-lookup"><span data-stu-id="83eb2-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

5. <span data-ttu-id="83eb2-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="83eb2-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="83eb2-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="83eb2-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="83eb2-168">В разделе **Конфигурация PurelyHR** щелкните **Настроить PurelyHR**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="83eb2-169">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="83eb2-171">Чтобы настроить единый вход на стороне **PurelyHR**, войдите на соответствующий сайт в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="83eb2-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

9. <span data-ttu-id="83eb2-172">Откройте **Панель мониторинга** в параметрах на панели инструментов и щелкните **SSO Settings** (Параметры единого входа).</span><span class="sxs-lookup"><span data-stu-id="83eb2-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="83eb2-173">Вставьте в поля нужные значения, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="83eb2-173">Paste the values in the boxes as described below-</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="83eb2-175">а.</span><span class="sxs-lookup"><span data-stu-id="83eb2-175">a.</span></span> <span data-ttu-id="83eb2-176">Откройте **Сертификат (Base64)**, скачанный на портале Azure, в Блокноте и скопируйте значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="83eb2-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="83eb2-177">Вставьте это значение в поле **Сертификат X.509**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="83eb2-178">b.</span><span class="sxs-lookup"><span data-stu-id="83eb2-178">b.</span></span> <span data-ttu-id="83eb2-179">В поле **Idp Issuer URL** (URL-адрес издателя поставщика удостоверений) вставьте **идентификатор сущности SAML**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="83eb2-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="83eb2-180">c.</span><span class="sxs-lookup"><span data-stu-id="83eb2-180">c.</span></span> <span data-ttu-id="83eb2-181">В поле **Idp Endpoint URL** (URL-адрес конечной точки поставщика удостоверений) вставьте **URL-адрес службы единого входа SAML**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="83eb2-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="83eb2-182">d.</span><span class="sxs-lookup"><span data-stu-id="83eb2-182">d.</span></span> <span data-ttu-id="83eb2-183">Установите флажок **Auto-Create Users** (Автоматическое создание пользователей), чтобы включить автоматическую подготовку пользователей в PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="83eb2-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="83eb2-184">д.</span><span class="sxs-lookup"><span data-stu-id="83eb2-184">e.</span></span> <span data-ttu-id="83eb2-185">Нажмите кнопку **Сохранить изменения**, чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="83eb2-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="83eb2-186">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="83eb2-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="83eb2-187">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="83eb2-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="83eb2-188">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="83eb2-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83eb2-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="83eb2-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="83eb2-190">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="83eb2-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="83eb2-192">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="83eb2-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="83eb2-193">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83eb2-195">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83eb2-197">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83eb2-199">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="83eb2-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83eb2-201">а.</span><span class="sxs-lookup"><span data-stu-id="83eb2-201">a.</span></span> <span data-ttu-id="83eb2-202">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83eb2-203">b.</span><span class="sxs-lookup"><span data-stu-id="83eb2-203">b.</span></span> <span data-ttu-id="83eb2-204">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="83eb2-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83eb2-205">c.</span><span class="sxs-lookup"><span data-stu-id="83eb2-205">c.</span></span> <span data-ttu-id="83eb2-206">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="83eb2-207">d.</span><span class="sxs-lookup"><span data-stu-id="83eb2-207">d.</span></span> <span data-ttu-id="83eb2-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="83eb2-209">Создание тестового пользователя PurelyHR</span><span class="sxs-lookup"><span data-stu-id="83eb2-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="83eb2-210">Чтобы пользователи Azure AD могли выполнять вход в PurelyHR, они должны быть подготовлены для PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="83eb2-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="83eb2-211">В PurelyHR подготовка пользователей осуществляется автоматически, при этом никакие ручные действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="83eb2-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="83eb2-212">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="83eb2-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="83eb2-213">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="83eb2-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="83eb2-215">**Чтобы назначить пользователя Britta Simon в PurelyHR, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="83eb2-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="83eb2-216">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="83eb2-218">В списке приложений выберите **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-218">In the applications list, select **PurelyHR**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="83eb2-220">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="83eb2-222">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-222">Click **Add** button.</span></span> <span data-ttu-id="83eb2-223">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="83eb2-225">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="83eb2-226">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83eb2-227">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="83eb2-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83eb2-228">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="83eb2-228">Testing single sign-on</span></span>

<span data-ttu-id="83eb2-229">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="83eb2-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="83eb2-230">Щелкнув элемент Absorb LMS на панели доступа, вы автоматически входите в приложение Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="83eb2-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="83eb2-231">Дополнительные сведения о панели доступа см. в статье</span><span class="sxs-lookup"><span data-stu-id="83eb2-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="83eb2-232">[Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="83eb2-232">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83eb2-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="83eb2-233">Additional resources</span></span>

* [<span data-ttu-id="83eb2-234">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83eb2-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83eb2-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83eb2-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

