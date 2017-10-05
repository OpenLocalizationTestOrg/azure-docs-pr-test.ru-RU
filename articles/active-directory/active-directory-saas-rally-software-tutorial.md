---
title: "Учебник. Интеграция Azure Active Directory с Rally Software | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="14fe5-103">Учебник. Интеграция Azure Active Directory с Rally Software</span><span class="sxs-lookup"><span data-stu-id="14fe5-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="14fe5-104">В этом учебнике описано, как интегрировать Rally Software с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14fe5-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14fe5-105">Интеграция Rally Software с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="14fe5-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="14fe5-106">С помощью Azure AD вы можете контролировать доступ к Rally Software.</span><span class="sxs-lookup"><span data-stu-id="14fe5-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="14fe5-107">Вы можете включить автоматический вход пользователей в Rally Software (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14fe5-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="14fe5-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="14fe5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="14fe5-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="14fe5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14fe5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="14fe5-110">Prerequisites</span></span>

<span data-ttu-id="14fe5-111">Чтобы настроить интеграцию Azure AD с Rally Software, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="14fe5-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="14fe5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="14fe5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14fe5-113">подписка Rally Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="14fe5-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14fe5-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="14fe5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14fe5-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="14fe5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14fe5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="14fe5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14fe5-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="14fe5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14fe5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="14fe5-118">Scenario description</span></span>
<span data-ttu-id="14fe5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="14fe5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14fe5-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="14fe5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14fe5-121">Добавление Rally Software из коллекции</span><span class="sxs-lookup"><span data-stu-id="14fe5-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="14fe5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="14fe5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="14fe5-123">Добавление Rally Software из коллекции</span><span class="sxs-lookup"><span data-stu-id="14fe5-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="14fe5-124">Чтобы настроить интеграцию Rally Software с Azure AD, вам потребуется добавить Rally Software из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="14fe5-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="14fe5-125">**Чтобы добавить Rally Software из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="14fe5-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="14fe5-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="14fe5-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="14fe5-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="14fe5-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="14fe5-133">В поле поиска введите **Rally Software**, выберите **Rally Software** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="14fe5-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![Rally Software в списке результатов](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="14fe5-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="14fe5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="14fe5-136">В этом разделе описана настройка и проверка единого входа Azure AD в Rally Software для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14fe5-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="14fe5-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Rally Software соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14fe5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="14fe5-138">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Rally Software.</span><span class="sxs-lookup"><span data-stu-id="14fe5-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="14fe5-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Rally Software.</span><span class="sxs-lookup"><span data-stu-id="14fe5-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="14fe5-140">Чтобы настроить и проверить единый вход в Azure AD в Rally Software, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="14fe5-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="14fe5-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="14fe5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="14fe5-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14fe5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14fe5-143">**[Создание тестового пользователя Rally Software](#create-a-rally-software-test-user)** требуется для создания дублирующего Britta Simon пользователя в Rally Software, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14fe5-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="14fe5-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14fe5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14fe5-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="14fe5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="14fe5-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="14fe5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="14fe5-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Rally Software.</span><span class="sxs-lookup"><span data-stu-id="14fe5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="14fe5-148">**Чтобы настроить единый вход в Azure AD для Rally Software, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="14fe5-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="14fe5-149">На портале Azure на странице интеграции с приложением **Rally Software** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="14fe5-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="14fe5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="14fe5-153">В разделе **Домены и URL-адреса Rally Software** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="14fe5-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="14fe5-155">а.</span><span class="sxs-lookup"><span data-stu-id="14fe5-155">a.</span></span> <span data-ttu-id="14fe5-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="14fe5-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="14fe5-157">b.</span><span class="sxs-lookup"><span data-stu-id="14fe5-157">b.</span></span> <span data-ttu-id="14fe5-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="14fe5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14fe5-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="14fe5-159">These values are not real.</span></span> <span data-ttu-id="14fe5-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="14fe5-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="14fe5-161">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Rally Software](https://help.rallydev.com/).</span><span class="sxs-lookup"><span data-stu-id="14fe5-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="14fe5-162">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="14fe5-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="14fe5-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="14fe5-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="14fe5-166">В разделе **Настройка Rally Software** щелкните **Настроить Rally Software**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="14fe5-167">Скопируйте **URL-адрес выхода и идентификатор сущности SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Настройка Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="14fe5-169">Выполните вход в клиент **Rally Software** .</span><span class="sxs-lookup"><span data-stu-id="14fe5-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="14fe5-170">На панели инструментов вверху щелкните **Setup** (Настройка), затем выберите **Subscription** (Подписка).</span><span class="sxs-lookup"><span data-stu-id="14fe5-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="14fe5-171">![Подписка](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Подписка")</span><span class="sxs-lookup"><span data-stu-id="14fe5-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="14fe5-172">Нажмите кнопку **Действие**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-172">Click the **Action** button.</span></span> <span data-ttu-id="14fe5-173">В правой верхней части панели инструментов выберите **Изменение подписки**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="14fe5-174">На странице диалогового окна **Subscription** (Подписка) выполните указанные ниже действия, после чего нажмите кнопку **Save & Close** (Сохранить и закрыть).</span><span class="sxs-lookup"><span data-stu-id="14fe5-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="14fe5-175">![Аутентификация](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="14fe5-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="14fe5-176">а.</span><span class="sxs-lookup"><span data-stu-id="14fe5-176">a.</span></span> <span data-ttu-id="14fe5-177">Из раскрывающегося списка "Аутентификация" выберите пункт **Rally or SSO authentication** (Аутентификация Rally или путем единого входа).</span><span class="sxs-lookup"><span data-stu-id="14fe5-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="14fe5-178">b.</span><span class="sxs-lookup"><span data-stu-id="14fe5-178">b.</span></span> <span data-ttu-id="14fe5-179">В текстовое поле **Identity Provider URL** (URL-адрес поставщика удостоверений) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="14fe5-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="14fe5-180">c.</span><span class="sxs-lookup"><span data-stu-id="14fe5-180">c.</span></span> <span data-ttu-id="14fe5-181">В текстовое поле **SSO Logout** (Выход из службы единого входа) вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="14fe5-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="14fe5-182">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="14fe5-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="14fe5-183">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="14fe5-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="14fe5-184">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="14fe5-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="14fe5-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="14fe5-185">Create an Azure AD test user</span></span>

<span data-ttu-id="14fe5-186">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14fe5-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="14fe5-188">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="14fe5-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="14fe5-189">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="14fe5-191">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="14fe5-193">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="14fe5-195">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="14fe5-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="14fe5-197">а.</span><span class="sxs-lookup"><span data-stu-id="14fe5-197">a.</span></span> <span data-ttu-id="14fe5-198">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14fe5-199">b.</span><span class="sxs-lookup"><span data-stu-id="14fe5-199">b.</span></span> <span data-ttu-id="14fe5-200">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="14fe5-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="14fe5-201">c.</span><span class="sxs-lookup"><span data-stu-id="14fe5-201">c.</span></span> <span data-ttu-id="14fe5-202">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="14fe5-203">г)</span><span class="sxs-lookup"><span data-stu-id="14fe5-203">d.</span></span> <span data-ttu-id="14fe5-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="14fe5-205">Создание тестового пользователя Rally Software</span><span class="sxs-lookup"><span data-stu-id="14fe5-205">Create a Rally Software test user</span></span>

<span data-ttu-id="14fe5-206">Чтобы пользователи Azure AD могли войти систему, их необходимо подготовить для приложения Rally Software, используя их имена пользователей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="14fe5-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="14fe5-207">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="14fe5-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="14fe5-208">Выполните вход в клиент Rally Software.</span><span class="sxs-lookup"><span data-stu-id="14fe5-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="14fe5-209">Щелкните **Setup \> USERS** ("Настройка" > "ПОЛЬЗОВАТЕЛИ"), затем выберите **+ Add New** (+ Добавить).</span><span class="sxs-lookup"><span data-stu-id="14fe5-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="14fe5-210">![Пользователи](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="14fe5-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="14fe5-211">Введите имя в текстовом поле "Новый пользователь" и щелкните **Добавить со сведениями**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="14fe5-212">В разделе **Создание пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="14fe5-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="14fe5-213">![Создание пользователя](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="14fe5-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="14fe5-214">а.</span><span class="sxs-lookup"><span data-stu-id="14fe5-214">a.</span></span> <span data-ttu-id="14fe5-215">В текстовое поле **Имя пользователя** введите имя пользователя, например **Brittsimon**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="14fe5-216">b.</span><span class="sxs-lookup"><span data-stu-id="14fe5-216">b.</span></span> <span data-ttu-id="14fe5-217">В текстовое поле **Email address** (Адрес электронной почты) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="14fe5-218">c.</span><span class="sxs-lookup"><span data-stu-id="14fe5-218">c.</span></span> <span data-ttu-id="14fe5-219">В текстовое поле **First Name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="14fe5-220">d.</span><span class="sxs-lookup"><span data-stu-id="14fe5-220">d.</span></span> <span data-ttu-id="14fe5-221">В текстовое поле **Last Name** (Фамилия) введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="14fe5-222">д.</span><span class="sxs-lookup"><span data-stu-id="14fe5-222">e.</span></span> <span data-ttu-id="14fe5-223">Щелкните **Save & Close** (Сохранить и закрыть).</span><span class="sxs-lookup"><span data-stu-id="14fe5-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="14fe5-224">Вы можете использовать любые другие инструменты создания учетных записей пользователя Rally Software или API, предоставляемые Rally Software для подготовки учетных записей пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14fe5-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="14fe5-225">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="14fe5-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="14fe5-226">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon и предоставить этому пользователю доступ к Rally Software.</span><span class="sxs-lookup"><span data-stu-id="14fe5-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="14fe5-228">**Чтобы назначить Britta Simon для Rally Software, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="14fe5-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="14fe5-229">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="14fe5-231">В списке приложений выберите **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-231">In the applications list, select **Rally Software**.</span></span>

    ![Ссылка на Rally Software в списке "Приложения"](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="14fe5-233">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="14fe5-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-235">Click **Add** button.</span></span> <span data-ttu-id="14fe5-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="14fe5-238">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="14fe5-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14fe5-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="14fe5-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="14fe5-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="14fe5-241">Test single sign-on</span></span>

<span data-ttu-id="14fe5-242">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="14fe5-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="14fe5-243">Щелкнув элемент Rally Software на панели доступа, вы автоматически войдете в приложение Rally Software.</span><span class="sxs-lookup"><span data-stu-id="14fe5-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14fe5-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="14fe5-244">Additional resources</span></span>

* [<span data-ttu-id="14fe5-245">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="14fe5-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14fe5-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="14fe5-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

