---
title: "Руководство по интеграции Azure Active Directory с Bambu by Sprout Social | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Bambu by Sprout Social."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="452d2-103">Руководство по интеграции Azure Active Directory с Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="452d2-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="452d2-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="452d2-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="452d2-105">Интеграция Azure AD с Bambu by Sprout Social обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="452d2-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="452d2-106">С помощью Azure AD вы можете контролировать доступ к Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="452d2-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="452d2-107">Вы можете включить автоматический вход пользователей в Bambu by Sprout Social (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="452d2-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="452d2-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="452d2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="452d2-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="452d2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="452d2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="452d2-110">Prerequisites</span></span>

<span data-ttu-id="452d2-111">Чтобы настроить интеграцию Azure AD с Bambu by Sprout Social, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="452d2-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="452d2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="452d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="452d2-113">подписка Bambu by Sprout Social с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="452d2-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="452d2-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="452d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="452d2-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="452d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="452d2-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="452d2-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="452d2-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="452d2-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="452d2-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="452d2-118">Scenario description</span></span>
<span data-ttu-id="452d2-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="452d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="452d2-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="452d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="452d2-121">Добавление Bambu by Sprout Social из коллекции</span><span class="sxs-lookup"><span data-stu-id="452d2-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="452d2-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="452d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="452d2-123">Добавление Bambu by Sprout Social из коллекции</span><span class="sxs-lookup"><span data-stu-id="452d2-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="452d2-124">Чтобы настроить интеграцию Bambu by Sprout Social с Azure AD, нужно добавить Bambu из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="452d2-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="452d2-125">**Чтобы добавить Bambu by Sprout Social из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="452d2-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="452d2-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="452d2-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="452d2-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="452d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="452d2-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="452d2-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="452d2-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="452d2-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="452d2-133">В поле поиска введите **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="452d2-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="452d2-135">На панели результатов выберите **Bambu by Sprout Social** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="452d2-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="452d2-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="452d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="452d2-138">В этом разделе описана настройка и проверка единого входа Azure AD в Bambu by Sprout Social с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="452d2-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="452d2-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Bambu by Sprout Social соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="452d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="452d2-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="452d2-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="452d2-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве **имени пользователя** в Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="452d2-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="452d2-142">Чтобы настроить и проверить единый вход Azure AD в Bambu by Sprout Social, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="452d2-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="452d2-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="452d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="452d2-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="452d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="452d2-145">**[Создание тестового пользователя Bambu by Sprout Social](#creating-a-bambu-by-sprout-social-test-user)** требуется для создания в Bambu by Sprout Social пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="452d2-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="452d2-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="452d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="452d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="452d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="452d2-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="452d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="452d2-149">В данном разделе описано, как включить единый вход в Azure AD на портале Azure и настроить его в Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="452d2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="452d2-150">**Чтобы настроить единый вход Azure AD в Bambu by Sprout Social, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="452d2-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="452d2-151">На портале Azure на странице интеграции с приложением **Bambu by Sprout Social** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="452d2-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="452d2-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="452d2-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="452d2-155">В разделе **Домен и URL-адреса единого входа в Bambu by Sprout Social** не нужно выполнять никаких действий, поскольку приложение уже предварительно интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="452d2-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="452d2-157">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="452d2-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="452d2-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="452d2-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="452d2-161">В разделе **Настройка Bambu by Sprout Social** щелкните **Настроить Bambu by Sprout Social**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="452d2-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="452d2-162">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="452d2-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="452d2-164">Чтобы настроить единый вход на стороне **Bambu by Sprout Social**, нужно отправить скачанный **XML метаданных** и **URL-адрес службы единого входа SAML** в [службу поддержки Bambu by Sprout Social](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="452d2-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="452d2-165">Это позволит службе поддержки правильно настроить подключение единого входа SAML на обоих сторонах.</span><span class="sxs-lookup"><span data-stu-id="452d2-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="452d2-166">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="452d2-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="452d2-167">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="452d2-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="452d2-168">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="452d2-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="452d2-169">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="452d2-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="452d2-170">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="452d2-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="452d2-172">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="452d2-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="452d2-173">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="452d2-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="452d2-175">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="452d2-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="452d2-177">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="452d2-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="452d2-179">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="452d2-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="452d2-181">А.</span><span class="sxs-lookup"><span data-stu-id="452d2-181">a.</span></span> <span data-ttu-id="452d2-182">В текстовом поле **Name** (Имя) введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="452d2-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="452d2-183">b.</span><span class="sxs-lookup"><span data-stu-id="452d2-183">b.</span></span> <span data-ttu-id="452d2-184">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="452d2-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="452d2-185">c.</span><span class="sxs-lookup"><span data-stu-id="452d2-185">c.</span></span> <span data-ttu-id="452d2-186">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="452d2-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="452d2-187">d.</span><span class="sxs-lookup"><span data-stu-id="452d2-187">d.</span></span> <span data-ttu-id="452d2-188">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="452d2-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="452d2-189">Создание тестового пользователя для Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="452d2-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="452d2-190">Приложение поддерживает JIT-подготовку пользователей, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="452d2-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="452d2-191">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="452d2-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="452d2-192">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="452d2-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="452d2-194">**Чтобы назначить пользователя Britta Simon в приложении Bambu by Sprout Social, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="452d2-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="452d2-195">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="452d2-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="452d2-197">В списке приложений выберите **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="452d2-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="452d2-199">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="452d2-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="452d2-201">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="452d2-201">Click **Add** button.</span></span> <span data-ttu-id="452d2-202">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="452d2-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="452d2-204">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="452d2-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="452d2-205">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="452d2-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="452d2-206">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="452d2-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="452d2-207">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="452d2-207">Testing single sign-on</span></span>

<span data-ttu-id="452d2-208">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="452d2-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="452d2-209">Щелкнув элемент Bambu by Sprout Social на панели доступа, вы автоматически войдете в приложение Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="452d2-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="452d2-210">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="452d2-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="452d2-211">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="452d2-211">Additional resources</span></span>

* [<span data-ttu-id="452d2-212">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="452d2-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="452d2-213">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="452d2-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

