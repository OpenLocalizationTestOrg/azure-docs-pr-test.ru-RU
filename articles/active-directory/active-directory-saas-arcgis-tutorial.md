---
title: "Руководство по интеграции Azure Active Directory с ArcGIS Online | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="a532d-103">Руководство по интеграции Azure Active Directory с ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="a532d-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="a532d-104">В этом руководстве описано, как интегрировать ArcGIS Online с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a532d-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a532d-105">Интеграция ArcGIS Online с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a532d-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a532d-106">С помощью Azure AD вы можете контролировать доступ к ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="a532d-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="a532d-107">Вы можете включить автоматический вход пользователей в ArcGIS Online (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a532d-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a532d-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a532d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a532d-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a532d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="a532d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a532d-110">Prerequisites</span></span>

<span data-ttu-id="a532d-111">Чтобы настроить интеграцию Azure AD с ArcGIS Online, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a532d-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="a532d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a532d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a532d-113">подписка ArcGIS Online с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a532d-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a532d-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a532d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a532d-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a532d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a532d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a532d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a532d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a532d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a532d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a532d-118">Scenario description</span></span>
<span data-ttu-id="a532d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a532d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a532d-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a532d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a532d-121">Добавление ArcGIS Online из коллекции</span><span class="sxs-lookup"><span data-stu-id="a532d-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="a532d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a532d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="a532d-123">Добавление ArcGIS Online из коллекции</span><span class="sxs-lookup"><span data-stu-id="a532d-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="a532d-124">Чтобы настроить интеграцию ArcGIS Online с Azure AD, необходимо добавить ArcGIS Online из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a532d-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a532d-125">**Чтобы добавить ArcGIS Online из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a532d-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a532d-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a532d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a532d-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a532d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a532d-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a532d-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a532d-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a532d-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a532d-133">В поле поиска введите **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="a532d-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="a532d-135">На панели результатов выберите **ArcGIS Online** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="a532d-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a532d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a532d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a532d-138">В этом разделе описана настройка и проверка единого входа Azure AD в ArcGIS Online с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a532d-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a532d-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в ArcGIS Online соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a532d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="a532d-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="a532d-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="a532d-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве **имени пользователя** в ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="a532d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="a532d-142">Чтобы настроить и проверить единый вход Azure AD в ArcGIS Online, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="a532d-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a532d-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a532d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a532d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a532d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a532d-145">**[Создание тестового пользователя ArcGIS Online](#creating-an-arcgis-online-test-user)** нужно для того, чтобы в ArcGIS Online также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a532d-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a532d-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a532d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a532d-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a532d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a532d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a532d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a532d-149">В этом разделе описано, как на портале Azure включить единый вход Azure AD и настроить его в приложении ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="a532d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="a532d-150">**Чтобы настроить единый вход Azure AD в ArcGIS Online, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a532d-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="a532d-151">На портале Azure на странице интеграции с приложением **ArcGIS Online** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a532d-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a532d-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a532d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="a532d-155">В разделе **Домены и URL-адреса приложения ArcGIS Online** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a532d-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="a532d-157">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://<company>.maps.arcgis.com`.</span><span class="sxs-lookup"><span data-stu-id="a532d-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a532d-158">Это значение приведено только для примера.</span><span class="sxs-lookup"><span data-stu-id="a532d-158">This value is not the real.</span></span> <span data-ttu-id="a532d-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a532d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a532d-160">Для получения этого значения обратитесь к [группе поддержки ArcGIS Online](http://support.esri.com/).</span><span class="sxs-lookup"><span data-stu-id="a532d-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="a532d-161">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a532d-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="a532d-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a532d-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a532d-165">В другом окне веб-браузера войдите на свой корпоративный веб-сайт ArcGIS в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="a532d-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="a532d-166">Щелкните **EDIT SETTINGS** (Изменить параметры).</span><span class="sxs-lookup"><span data-stu-id="a532d-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="a532d-167">![Изменение параметров](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Изменение параметров")</span><span class="sxs-lookup"><span data-stu-id="a532d-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="a532d-168">Щелкните **Security**(Безопасность).</span><span class="sxs-lookup"><span data-stu-id="a532d-168">Click **Security**.</span></span>

    <span data-ttu-id="a532d-169">![Безопасность](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="a532d-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="a532d-170">В разделе **Enterprise Logins** (Корпоративные имена для входа) установите флажок **Set Identity Provider** (Задать поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="a532d-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="a532d-171">![Корпоративные имена входа](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Корпоративные имена входа")</span><span class="sxs-lookup"><span data-stu-id="a532d-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="a532d-172">На странице **Назначение поставщика удостоверений** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a532d-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="a532d-173">![Назначение поставщика удостоверений](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Назначение поставщика удостоверений")</span><span class="sxs-lookup"><span data-stu-id="a532d-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="a532d-174">а.</span><span class="sxs-lookup"><span data-stu-id="a532d-174">a.</span></span> <span data-ttu-id="a532d-175">В текстовое поле **Name** (Имя) введите название своей организации.</span><span class="sxs-lookup"><span data-stu-id="a532d-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="a532d-176">b.</span><span class="sxs-lookup"><span data-stu-id="a532d-176">b.</span></span> <span data-ttu-id="a532d-177">Для параметра **Metadata for the Enterprise Identity Provider will be supplied using** (В предоставлении метаданных для корпоративного поставщика удостоверений будет использоваться) выберите значение **Файл**.</span><span class="sxs-lookup"><span data-stu-id="a532d-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="a532d-178">c.</span><span class="sxs-lookup"><span data-stu-id="a532d-178">c.</span></span> <span data-ttu-id="a532d-179">Чтобы отправить загруженный файл метаданных, нажмите кнопку **Выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="a532d-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="a532d-180">г)</span><span class="sxs-lookup"><span data-stu-id="a532d-180">d.</span></span> <span data-ttu-id="a532d-181">Щелкните **SET IDENTITY PROVIDER** (Задать поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="a532d-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="a532d-182">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a532d-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a532d-183">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a532d-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a532d-184">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a532d-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a532d-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a532d-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="a532d-186">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a532d-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a532d-188">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a532d-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a532d-189">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a532d-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a532d-191">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="a532d-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a532d-193">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="a532d-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a532d-195">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a532d-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a532d-197">а.</span><span class="sxs-lookup"><span data-stu-id="a532d-197">a.</span></span> <span data-ttu-id="a532d-198">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a532d-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a532d-199">b.</span><span class="sxs-lookup"><span data-stu-id="a532d-199">b.</span></span> <span data-ttu-id="a532d-200">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a532d-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a532d-201">c.</span><span class="sxs-lookup"><span data-stu-id="a532d-201">c.</span></span> <span data-ttu-id="a532d-202">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a532d-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a532d-203">d.</span><span class="sxs-lookup"><span data-stu-id="a532d-203">d.</span></span> <span data-ttu-id="a532d-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a532d-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="a532d-205">Создание тестового пользователя ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="a532d-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="a532d-206">Чтобы пользователи Azure AD могли выполнять вход в ArcGIS Online, они должны быть подготовлены в ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="a532d-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="a532d-207">В случае ArcGIS Online подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="a532d-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="a532d-208">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="a532d-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a532d-209">Войдите в клиент **ArcGIS** .</span><span class="sxs-lookup"><span data-stu-id="a532d-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="a532d-210">Щелкните **INVITE MEMBERS** (Пригласить участников).</span><span class="sxs-lookup"><span data-stu-id="a532d-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="a532d-211">![Приглашение участников](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="a532d-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="a532d-212">Щелкните переключатель **Add members automatically without sending an email** (Добавлять участников автоматически без отправки электронного сообщения) и нажмите кнопку **NEXT** (Далее).</span><span class="sxs-lookup"><span data-stu-id="a532d-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="a532d-213">![Автоматическое добавление участников](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Автоматическое добавление участников")</span><span class="sxs-lookup"><span data-stu-id="a532d-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="a532d-214">На странице диалогового окна **Участники** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a532d-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="a532d-215">![Добавление и просмотр](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Добавление и просмотр")</span><span class="sxs-lookup"><span data-stu-id="a532d-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="a532d-216">а.</span><span class="sxs-lookup"><span data-stu-id="a532d-216">a.</span></span> <span data-ttu-id="a532d-217">Введите в поля **Email** (Адрес электронной почты), **First name** (Имя) и **Last name** (Фамилия) соответствующие данные действующей учетной записи Azure AD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="a532d-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="a532d-218">b.</span><span class="sxs-lookup"><span data-stu-id="a532d-218">b.</span></span> <span data-ttu-id="a532d-219">Нажмите кнопку **ADD AND REVIEW** (Добавить и просмотреть).</span><span class="sxs-lookup"><span data-stu-id="a532d-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="a532d-220">Просмотрите введенные данные и нажмите кнопку **ADD MEMBERS** (Добавить участников).</span><span class="sxs-lookup"><span data-stu-id="a532d-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="a532d-221">![Добавление участника](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Добавление участника")</span><span class="sxs-lookup"><span data-stu-id="a532d-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="a532d-222">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a532d-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a532d-223">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a532d-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a532d-224">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="a532d-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a532d-226">**Чтобы назначить пользователя Britta Simon в ArcGIS Online, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a532d-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="a532d-227">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a532d-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a532d-229">Из списка приложений выберите **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="a532d-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="a532d-231">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a532d-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a532d-233">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a532d-233">Click **Add** button.</span></span> <span data-ttu-id="a532d-234">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a532d-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a532d-236">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a532d-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a532d-237">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a532d-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a532d-238">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a532d-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a532d-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a532d-239">Testing single sign-on</span></span>

<span data-ttu-id="a532d-240">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a532d-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a532d-241">Щелкнув элемент "ArcGIS Online" на панели доступа, вы автоматически войдете в приложение ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="a532d-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="a532d-242">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a532d-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a532d-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a532d-243">Additional resources</span></span>

* [<span data-ttu-id="a532d-244">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a532d-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a532d-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a532d-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

