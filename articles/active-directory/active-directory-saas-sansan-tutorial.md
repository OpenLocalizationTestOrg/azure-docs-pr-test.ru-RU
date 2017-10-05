---
title: "Руководство по интеграции Azure Active Directory с Sansan | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Sansan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e1a9653d5feea910308cefabdbdfe3a6af44bbe4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="13bcd-103">Руководство по интеграции Azure Active Directory с Sansan</span><span class="sxs-lookup"><span data-stu-id="13bcd-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="13bcd-104">В этом руководстве описано, как интегрировать Sansan с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13bcd-104">In this tutorial, you learn how to integrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13bcd-105">Интеграция Azure AD с приложением Sansan обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="13bcd-105">Integrating Sansan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="13bcd-106">С помощью Azure AD вы можете контролировать доступ к Sansan.</span><span class="sxs-lookup"><span data-stu-id="13bcd-106">You can control in Azure AD who has access to Sansan</span></span>
- <span data-ttu-id="13bcd-107">Вы можете включить автоматический вход пользователей в Sansan (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13bcd-107">You can enable your users to automatically get signed-on to Sansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13bcd-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="13bcd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="13bcd-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13bcd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13bcd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="13bcd-110">Prerequisites</span></span>

<span data-ttu-id="13bcd-111">Чтобы настроить интеграцию Azure AD с Sansan, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="13bcd-111">To configure Azure AD integration with Sansan, you need the following items:</span></span>

- <span data-ttu-id="13bcd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="13bcd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13bcd-113">подписка Sansan с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="13bcd-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13bcd-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="13bcd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13bcd-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="13bcd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13bcd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="13bcd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13bcd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13bcd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13bcd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="13bcd-118">Scenario description</span></span>
<span data-ttu-id="13bcd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="13bcd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13bcd-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="13bcd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13bcd-121">Добавление Sansan из коллекции.</span><span class="sxs-lookup"><span data-stu-id="13bcd-121">Adding Sansan from the gallery</span></span>
2. <span data-ttu-id="13bcd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="13bcd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-the-gallery"></a><span data-ttu-id="13bcd-123">Добавление Sansan из коллекции</span><span class="sxs-lookup"><span data-stu-id="13bcd-123">Adding Sansan from the gallery</span></span>
<span data-ttu-id="13bcd-124">Чтобы настроить интеграцию Sansan с Azure AD, необходимо добавить Sansan из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="13bcd-124">To configure the integration of Sansan into Azure AD, you need to add Sansan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="13bcd-125">**Чтобы добавить Sansan из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="13bcd-125">**To add Sansan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="13bcd-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13bcd-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="13bcd-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="13bcd-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="13bcd-133">В поле поиска введите **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-133">In the search box, type **Sansan**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="13bcd-135">На панели результатов выберите **Sansan** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="13bcd-135">In the results panel, select **Sansan**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13bcd-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="13bcd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13bcd-138">В этом разделе описана настройка и проверка единого входа Azure AD в Sansan с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13bcd-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="13bcd-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Sansan соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13bcd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sansan is to a user in Azure AD.</span></span> <span data-ttu-id="13bcd-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Sansan.</span><span class="sxs-lookup"><span data-stu-id="13bcd-140">In other words, a link relationship between an Azure AD user and the related user in Sansan needs to be established.</span></span>

<span data-ttu-id="13bcd-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Sansan.</span><span class="sxs-lookup"><span data-stu-id="13bcd-141">In Sansan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="13bcd-142">Чтобы настроить и проверить единый вход Azure AD в Sansan, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="13bcd-142">To configure and test Azure AD single sign-on with Sansan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="13bcd-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="13bcd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="13bcd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13bcd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13bcd-145">**[Создание тестового пользователя Sansan](#creating-a-sansan-test-user)** требуется для того, чтобы в Sansan существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13bcd-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - to have a counterpart of Britta Simon in Sansan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="13bcd-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13bcd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13bcd-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="13bcd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13bcd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="13bcd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13bcd-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Sansan.</span><span class="sxs-lookup"><span data-stu-id="13bcd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="13bcd-150">**Чтобы настроить единый вход Azure AD в Sansan, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="13bcd-150">**To configure Azure AD single sign-on with Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="13bcd-151">На портале Azure на странице интеграции с приложением **Sansan** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-151">In the Azure portal, on the **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="13bcd-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="13bcd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="13bcd-155">В разделе **Домены и URL-адреса приложения Sansan** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="13bcd-155">On the **Sansan Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="13bcd-157">а.</span><span class="sxs-lookup"><span data-stu-id="13bcd-157">a.</span></span> <span data-ttu-id="13bcd-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="13bcd-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | <span data-ttu-id="13bcd-159">Среда</span><span class="sxs-lookup"><span data-stu-id="13bcd-159">Environment</span></span> | <span data-ttu-id="13bcd-160">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="13bcd-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="13bcd-161">Компьютерная сеть</span><span class="sxs-lookup"><span data-stu-id="13bcd-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="13bcd-162">Собственное мобильное приложение</span><span class="sxs-lookup"><span data-stu-id="13bcd-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="13bcd-163">Параметры браузера для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="13bcd-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="13bcd-164">b.</span><span class="sxs-lookup"><span data-stu-id="13bcd-164">b.</span></span> <span data-ttu-id="13bcd-165">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="13bcd-165">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="13bcd-166">Среда</span><span class="sxs-lookup"><span data-stu-id="13bcd-166">Environment</span></span>             | <span data-ttu-id="13bcd-167">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="13bcd-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="13bcd-168">Компьютерная сеть</span><span class="sxs-lookup"><span data-stu-id="13bcd-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="13bcd-169">Собственное мобильное приложение</span><span class="sxs-lookup"><span data-stu-id="13bcd-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="13bcd-170">Параметры браузера для мобильных устройств</span><span class="sxs-lookup"><span data-stu-id="13bcd-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="13bcd-171">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="13bcd-171">These values are not real.</span></span> <span data-ttu-id="13bcd-172">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="13bcd-172">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="13bcd-173">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="13bcd-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) to get these values.</span></span> 

4. <span data-ttu-id="13bcd-174">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="13bcd-174">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="13bcd-176">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="13bcd-176">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="13bcd-178">В разделе **Конфигурация Sansan** щелкните **Настроить Sansan**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-178">On the **Sansan Configuration** section, click **Configure Sansan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="13bcd-179">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-179">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="13bcd-181">Чтобы настроить единый вход на стороне **Sansan**, нужно отправить скачанный **сертификат**, **URL-адрес выхода**, **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** [группе поддержки Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="13bcd-181">To configure single sign-on on **Sansan** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="13bcd-182">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="13bcd-182">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="13bcd-183">Настройка браузера ПК подходит как для мобильного приложения и браузера для мобильных устройств, так и для компьютерной сети.</span><span class="sxs-lookup"><span data-stu-id="13bcd-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="13bcd-184">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="13bcd-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="13bcd-185">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="13bcd-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="13bcd-186">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="13bcd-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13bcd-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="13bcd-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="13bcd-188">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13bcd-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="13bcd-190">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="13bcd-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="13bcd-191">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13bcd-193">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13bcd-195">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13bcd-197">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="13bcd-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13bcd-199">а.</span><span class="sxs-lookup"><span data-stu-id="13bcd-199">a.</span></span> <span data-ttu-id="13bcd-200">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13bcd-201">b.</span><span class="sxs-lookup"><span data-stu-id="13bcd-201">b.</span></span> <span data-ttu-id="13bcd-202">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="13bcd-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13bcd-203">c.</span><span class="sxs-lookup"><span data-stu-id="13bcd-203">c.</span></span> <span data-ttu-id="13bcd-204">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="13bcd-205">d.</span><span class="sxs-lookup"><span data-stu-id="13bcd-205">d.</span></span> <span data-ttu-id="13bcd-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="13bcd-207">Создание тестового пользователя Sansan</span><span class="sxs-lookup"><span data-stu-id="13bcd-207">Creating a Sansan test user</span></span>

<span data-ttu-id="13bcd-208">В этом разделе описано, как создать пользователя Britta Simon в приложении SanSan.</span><span class="sxs-lookup"><span data-stu-id="13bcd-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="13bcd-209">Перед выполнением единого входа пользователь должен быть подготовлен в приложении Sansan.</span><span class="sxs-lookup"><span data-stu-id="13bcd-209">SanSan application needs the user to be provisioned in the application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="13bcd-210">Чтобы создать пользователя или несколько пользователей вручную, обратитесь к [группе поддержки Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="13bcd-210">If you need to create a user manually or batch of users, you need to contact the [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="13bcd-211">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="13bcd-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="13bcd-212">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Sansan.</span><span class="sxs-lookup"><span data-stu-id="13bcd-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sansan.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="13bcd-214">**Чтобы назначить пользователя Britta Simon в Sansan, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="13bcd-214">**To assign Britta Simon to Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="13bcd-215">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="13bcd-217">Из списка приложений выберите **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-217">In the applications list, select **Sansan**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="13bcd-219">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="13bcd-221">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-221">Click **Add** button.</span></span> <span data-ttu-id="13bcd-222">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="13bcd-224">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="13bcd-225">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13bcd-226">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="13bcd-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13bcd-227">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="13bcd-227">Testing single sign-on</span></span>

<span data-ttu-id="13bcd-228">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="13bcd-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="13bcd-229">Щелкнув элемент "Sansan" на панели доступа, вы автоматически войдете в приложение Sansan.</span><span class="sxs-lookup"><span data-stu-id="13bcd-229">When you click the Sansan tile in the Access Panel, you should get automatically signed-on to your Sansan application.</span></span>
<span data-ttu-id="13bcd-230">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="13bcd-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13bcd-231">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="13bcd-231">Additional resources</span></span>

* [<span data-ttu-id="13bcd-232">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13bcd-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13bcd-233">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13bcd-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

