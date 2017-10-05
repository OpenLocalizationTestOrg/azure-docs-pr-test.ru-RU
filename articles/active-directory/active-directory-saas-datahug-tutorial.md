---
title: "Руководство по интеграции Azure Active Directory с Datahug | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: ec431dd5ccfa53e4b975e46da247704dd1e15c2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="0b451-103">Руководство. Интеграция Azure Active Directory с Datahug</span><span class="sxs-lookup"><span data-stu-id="0b451-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="0b451-104">В этом руководстве описано, как интегрировать приложение Datahug с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b451-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b451-105">Интеграция Azure AD с приложением Datahug обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0b451-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b451-106">С помощью Azure AD вы можете контролировать доступ к Datahug.</span><span class="sxs-lookup"><span data-stu-id="0b451-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="0b451-107">Вы можете включить автоматический вход пользователей в Datahug (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b451-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b451-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0b451-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b451-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье</span><span class="sxs-lookup"><span data-stu-id="0b451-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="0b451-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b451-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b451-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0b451-111">Prerequisites</span></span>

<span data-ttu-id="0b451-112">Чтобы настроить интеграцию Azure AD с Datahug, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="0b451-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="0b451-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0b451-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0b451-114">подписка Datahug с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0b451-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b451-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0b451-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b451-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="0b451-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b451-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0b451-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b451-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b451-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b451-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0b451-119">Scenario description</span></span>
<span data-ttu-id="0b451-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0b451-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b451-121">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="0b451-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b451-122">Добавление Datahug из коллекции</span><span class="sxs-lookup"><span data-stu-id="0b451-122">Adding Datahug from the gallery</span></span>
2. <span data-ttu-id="0b451-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b451-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="0b451-124">Добавление Datahug из коллекции</span><span class="sxs-lookup"><span data-stu-id="0b451-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="0b451-125">Чтобы настроить интеграцию Datahug с Azure AD, нужно добавить Datahug из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0b451-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b451-126">**Чтобы добавить Datahug из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="0b451-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b451-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b451-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b451-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="0b451-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b451-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0b451-130">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0b451-132">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="0b451-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0b451-134">В поле поиска введите **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="0b451-134">In the search box, type **Datahug**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="0b451-136">На панели результатов выберите **Datahug** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="0b451-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b451-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b451-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b451-139">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Datahug с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b451-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0b451-140">Для работы единого входа в Azure AD нужно знать, какой пользователь в Datahug соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b451-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="0b451-141">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Datahug.</span><span class="sxs-lookup"><span data-stu-id="0b451-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="0b451-142">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Datahug.</span><span class="sxs-lookup"><span data-stu-id="0b451-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="0b451-143">Чтобы настроить и проверить единый вход Azure AD в Datahug, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="0b451-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b451-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="0b451-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b451-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b451-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b451-146">**[Создание тестового пользователя Datahug](#creating-a-datahug-test-user)** требуется для создания пользователя Britta Simon в Datahug, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b451-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b451-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b451-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b451-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b451-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b451-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b451-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b451-150">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Datahug.</span><span class="sxs-lookup"><span data-stu-id="0b451-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="0b451-151">**Чтобы настроить единый вход Azure AD в Datahug, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0b451-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="0b451-152">На портале Azure на странице интеграции с приложением **Datahug** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0b451-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0b451-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="0b451-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="0b451-156">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Datahug** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0b451-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="0b451-158">а.</span><span class="sxs-lookup"><span data-stu-id="0b451-158">a.</span></span> <span data-ttu-id="0b451-159">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="0b451-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="0b451-160">b.</span><span class="sxs-lookup"><span data-stu-id="0b451-160">b.</span></span> <span data-ttu-id="0b451-161">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://apps.datahug.com/identity/<uniqueID>/acs`.</span><span class="sxs-lookup"><span data-stu-id="0b451-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="0b451-162">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="0b451-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="0b451-163">если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="0b451-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="0b451-165">В текстовом поле **URL-адрес для входа** введите URL-адрес в формате `https://apps.datahug.com/`.</span><span class="sxs-lookup"><span data-stu-id="0b451-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0b451-166">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0b451-166">These values are not the real.</span></span> <span data-ttu-id="0b451-167">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="0b451-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="0b451-168">Мы рекомендуем использовать уникальное значение строки идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="0b451-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="0b451-169">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="0b451-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="0b451-170">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0b451-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="0b451-172">Установите флажок **Показать дополнительные параметры подписывания сертификатов** и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0b451-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="0b451-174">А.</span><span class="sxs-lookup"><span data-stu-id="0b451-174">a.</span></span> <span data-ttu-id="0b451-175">В поле **Вариант подписывания** выберите **Утверждение знака SAML**.</span><span class="sxs-lookup"><span data-stu-id="0b451-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="0b451-176">b.</span><span class="sxs-lookup"><span data-stu-id="0b451-176">b.</span></span> <span data-ttu-id="0b451-177">В поле **Алгоритм подписывания** выберите **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="0b451-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="0b451-178">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0b451-178">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="0b451-180">В разделе **Конфигурация Datahug** щелкните **Настроить Datahug**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0b451-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b451-181">Скопируйте **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="0b451-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="0b451-183">Чтобы настроить единый вход на стороне **Datahug**, нужно отправить скачанный **XML-файл метаданных**, **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** в [службу поддержки Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="0b451-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="0b451-184">Это позволит службе поддержки правильно настроить подключение единого входа SAML для приложения на обоих сторонах.</span><span class="sxs-lookup"><span data-stu-id="0b451-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0b451-185">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="0b451-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b451-186">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0b451-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b451-187">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0b451-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b451-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b451-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b451-189">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b451-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0b451-191">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0b451-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b451-192">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b451-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b451-194">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0b451-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b451-196">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0b451-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b451-198">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0b451-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b451-200">а.</span><span class="sxs-lookup"><span data-stu-id="0b451-200">a.</span></span> <span data-ttu-id="0b451-201">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b451-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b451-202">b.</span><span class="sxs-lookup"><span data-stu-id="0b451-202">b.</span></span> <span data-ttu-id="0b451-203">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0b451-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b451-204">c.</span><span class="sxs-lookup"><span data-stu-id="0b451-204">c.</span></span> <span data-ttu-id="0b451-205">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="0b451-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b451-206">d.</span><span class="sxs-lookup"><span data-stu-id="0b451-206">d.</span></span> <span data-ttu-id="0b451-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0b451-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="0b451-208">Создание тестового пользователя Datahug</span><span class="sxs-lookup"><span data-stu-id="0b451-208">Creating a Datahug test user</span></span>

<span data-ttu-id="0b451-209">Чтобы пользователи Azure AD могли выполнять вход в Datahug, они должны быть подготовлены для Datahug.</span><span class="sxs-lookup"><span data-stu-id="0b451-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="0b451-210">Эта подготовка для Datahug выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="0b451-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="0b451-211">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="0b451-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0b451-212">Войдите на веб-сайт организации Datahug в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="0b451-212">Log in to your Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="0b451-213">Наведите указатель мыши на **шестеренку** в верхнем правом углу и выберите **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="0b451-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![Добавление сотрудника](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="0b451-215">Выберите элемент **People** (Люди) и откройте вкладку **Add Users** (Добавление пользователей).</span><span class="sxs-lookup"><span data-stu-id="0b451-215">Choose **People** and click the **Add Users** tab</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="0b451-217">Введите адрес электронной почты человека, для которого вы хотите создать учетную запись, и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0b451-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="0b451-219">Вы можете отправить пользователю сообщение о регистрации, установив флажок **Send welcome email** (Отправить приветственное сообщение).</span><span class="sxs-lookup"><span data-stu-id="0b451-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="0b451-220">При создании учетной записи для Salesforce не отправляйте приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="0b451-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b451-221">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b451-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b451-222">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Datahug.</span><span class="sxs-lookup"><span data-stu-id="0b451-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0b451-224">**Чтобы назначить пользователя Britta Simon в Datahug, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0b451-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="0b451-225">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0b451-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0b451-227">В списке приложений выберите **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="0b451-227">In the applications list, select **Datahug**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="0b451-229">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0b451-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0b451-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0b451-231">Click **Add** button.</span></span> <span data-ttu-id="0b451-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0b451-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0b451-234">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0b451-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b451-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0b451-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b451-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0b451-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b451-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0b451-237">Testing single sign-on</span></span>

<span data-ttu-id="0b451-238">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="0b451-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="0b451-239">Щелкнув элемент Datahug на панели доступа, вы автоматически войдете в приложение Datahug.</span><span class="sxs-lookup"><span data-stu-id="0b451-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="0b451-240">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0b451-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0b451-241">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0b451-241">Additional resources</span></span>

* [<span data-ttu-id="0b451-242">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b451-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b451-243">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0b451-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

