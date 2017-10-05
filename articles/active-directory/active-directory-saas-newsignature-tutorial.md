---
title: "Руководство по интеграции Azure Active Directory с порталом управления облачными службами для Microsoft Azure | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и порталом управления облачными службами для Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: bae5f05a161b2730bf662bcb47f20ab3e1799951
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="be975-103">Учебник. Интеграция Azure Active Directory с порталом управления облачными службами для Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="be975-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="be975-104">В этом учебнике описано, как интегрировать портал управления облачными службами для Microsoft Azure с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be975-104">In this tutorial, you learn how to integrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be975-105">Интеграция портала управления облачными службами для Microsoft Azure с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="be975-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="be975-106">С помощью Azure AD вы можете контролировать доступ пользователей к порталу управления облачными службами для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="be975-106">You can control in Azure AD who has access to Cloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="be975-107">Вы можете включить автоматический вход пользователей в портал управления облачными службами (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be975-107">You can enable your users to automatically get signed-on to Cloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="be975-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="be975-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="be975-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be975-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be975-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be975-110">Prerequisites</span></span>

<span data-ttu-id="be975-111">Чтобы настроить интеграцию Azure AD с порталом управления облачными службами для Microsoft Azure, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="be975-111">To configure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need the following items:</span></span>

- <span data-ttu-id="be975-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="be975-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be975-113">подписка портала управления облачными службами для Microsoft Azure с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="be975-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="be975-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="be975-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be975-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="be975-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be975-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="be975-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be975-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be975-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be975-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="be975-118">Scenario description</span></span>
<span data-ttu-id="be975-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="be975-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be975-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="be975-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be975-121">Добавление портала управления облачными службами для Microsoft Azure из коллекции</span><span class="sxs-lookup"><span data-stu-id="be975-121">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
2. <span data-ttu-id="be975-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be975-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-the-gallery"></a><span data-ttu-id="be975-123">Добавление портала управления облачными службами для Microsoft Azure из коллекции</span><span class="sxs-lookup"><span data-stu-id="be975-123">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
<span data-ttu-id="be975-124">Чтобы настроить интеграцию с портала управления облачными службами для Microsoft Azure с Azure AD, необходимо добавить портал управления облачными службами для Microsoft Azure из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="be975-124">To configure the integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need to add Cloud Management Portal for Microsoft Azure from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="be975-125">**Чтобы добавить портал управления облачными службами для Microsoft Azure из коллекции, выполните приведенные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="be975-125">**To add Cloud Management Portal for Microsoft Azure from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="be975-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="be975-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="be975-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="be975-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="be975-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="be975-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="be975-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="be975-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="be975-133">В поле поиска введите **Портал управления облачными службами для Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="be975-133">In the search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="be975-135">В области результатов выберите **Портал управления облачными службами для Microsoft Azure** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="be975-135">In the results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="be975-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="be975-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="be975-138">В этом разделе описывается настройка и проверка единого входа Azure AD на портале управления облачными службами в Microsoft Azure с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be975-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="be975-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь на портале управления облачными службами для Microsoft Azure соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be975-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cloud Management Portal for Microsoft Azure is to a user in Azure AD.</span></span> <span data-ttu-id="be975-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем на портале управления облачными службами для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="be975-140">In other words, a link relationship between an Azure AD user and the related user in Cloud Management Portal for Microsoft Azure needs to be established.</span></span>

<span data-ttu-id="be975-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** на портале управления облачными службами для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="be975-141">In Cloud Management Portal for Microsoft Azure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="be975-142">Чтобы настроить и проверить единый вход Azure AD на портал управления облачными службами для Microsoft Azure, вам потребуется выполнить приведенные далее действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="be975-142">To configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="be975-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="be975-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="be975-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be975-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be975-145">**[Создание тестового пользователя портала управления облачными службами для Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** требуется для создания пользователя Britta Simon на портале управления облачными службами для Microsoft Azure, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be975-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - to have a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="be975-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be975-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be975-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="be975-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="be975-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="be975-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="be975-149">В этом разделе описывается, как включить единый вход Azure AD на портале Azure и настроить его на портале управления облачными службами для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="be975-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="be975-150">**Чтобы настроить единый вход Azure AD на портал управления облачными службами для Microsoft Azure, вам потребуется выполнить приведенные далее действия.**</span><span class="sxs-lookup"><span data-stu-id="be975-150">**To configure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="be975-151">На портале управления Azure на странице интеграции с приложением **Портал управления облачными службами Microsoft Azure** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="be975-151">In the Azure portal, on the **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="be975-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="be975-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="be975-155">В разделе **Домен и URL-адреса портала управления облачными службами для Microsoft Azure** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="be975-155">On the **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="be975-157">а.</span><span class="sxs-lookup"><span data-stu-id="be975-157">a.</span></span> <span data-ttu-id="be975-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="be975-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="be975-159">b.</span><span class="sxs-lookup"><span data-stu-id="be975-159">b.</span></span> <span data-ttu-id="be975-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="be975-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="be975-161">c.</span><span class="sxs-lookup"><span data-stu-id="be975-161">c.</span></span> <span data-ttu-id="be975-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="be975-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="be975-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="be975-163">These values are not real.</span></span> <span data-ttu-id="be975-164">Укажите вместо них фактические значения URL-адреса для входа, идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="be975-164">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="be975-165">Чтобы получить эти значения, обратитесь в [службу поддержки портала управления облачными службами для Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="be975-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) to get these values.</span></span> 
 
4. <span data-ttu-id="be975-166">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="be975-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="be975-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="be975-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="be975-170">В разделе **Настройка портала управления облачными службами для Microsoft Azure** щелкните **Настроить портал управления облачными службами для Microsoft Azure**, чтобы открыть окно **Настройка входа**.</span><span class="sxs-lookup"><span data-stu-id="be975-170">On the **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** to open **Configure sign-on** window.</span></span> <span data-ttu-id="be975-171">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="be975-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="be975-173">Для настройки единого входа на стороне **портала управления облачными службами для Microsoft Azure** необходимо отправить загруженный **сертификат**, **URL-адрес выхода**, **URL-адрес службы единого входа SAML** и **идентификатор сущности SAML** в [службу поддержки портала управления облачными службами для Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="be975-173">To configure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="be975-174">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="be975-174">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="be975-175">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="be975-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="be975-176">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="be975-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="be975-177">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="be975-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="be975-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="be975-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="be975-179">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="be975-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="be975-181">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="be975-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="be975-182">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="be975-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="be975-184">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="be975-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="be975-186">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="be975-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="be975-188">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="be975-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="be975-190">а.</span><span class="sxs-lookup"><span data-stu-id="be975-190">a.</span></span> <span data-ttu-id="be975-191">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be975-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be975-192">b.</span><span class="sxs-lookup"><span data-stu-id="be975-192">b.</span></span> <span data-ttu-id="be975-193">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="be975-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="be975-194">c.</span><span class="sxs-lookup"><span data-stu-id="be975-194">c.</span></span> <span data-ttu-id="be975-195">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="be975-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="be975-196">d.</span><span class="sxs-lookup"><span data-stu-id="be975-196">d.</span></span> <span data-ttu-id="be975-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="be975-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="be975-198">Создание тестового пользователя портала управления облачными службами для Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="be975-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="be975-199">Цель этого раздела — создать пользователя с именем Britta Simon на портале управления облачными службами для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="be975-199">The objective of this section is to create a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="be975-200">Обратитесь в [службу поддержки портала управления облачными службами для Microsoft Azure](mailto:jczernuszka@newsignature.com), чтобы добавить пользователей в учетную запись портала.</span><span class="sxs-lookup"><span data-stu-id="be975-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) to add the users in the Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="be975-201">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="be975-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="be975-202">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к порталу управления облачными службами для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="be975-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cloud Management Portal for Microsoft Azure.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="be975-204">**Чтобы назначить пользователя Britta Simon порталу управления облачными службами для Microsoft Azure, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="be975-204">**To assign Britta Simon to Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="be975-205">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="be975-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="be975-207">В списке приложений выберите **портал управления облачными службами для Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="be975-207">In the applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="be975-209">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="be975-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="be975-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="be975-211">Click **Add** button.</span></span> <span data-ttu-id="be975-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="be975-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="be975-214">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="be975-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="be975-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="be975-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be975-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="be975-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="be975-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="be975-217">Testing single sign-on</span></span>

<span data-ttu-id="be975-218">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="be975-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="be975-219">Щелкнув элемент портала управления облачными службами для Microsoft Azure на панели доступа, вы автоматически войдете в приложение портала управления облачными службами для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="be975-219">When you click the Cloud Management Portal for Microsoft Azure tile in the Access Panel, you should get automatically signed-on to your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="be975-220">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be975-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="be975-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="be975-221">Additional resources</span></span>

* [<span data-ttu-id="be975-222">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be975-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be975-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="be975-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

