---
title: "Руководство по интеграции Azure Active Directory с Teamphoria | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="2169c-103">Руководство по интеграции Azure Active Directory с Teamphoria</span><span class="sxs-lookup"><span data-stu-id="2169c-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="2169c-104">В этом руководстве описано, как интегрировать приложение Teamphoria с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2169c-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2169c-105">Интеграция Azure AD с приложением Teamphoria обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="2169c-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2169c-106">С помощью Azure AD вы можете контролировать доступ к Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="2169c-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="2169c-107">Вы можете включить автоматический вход пользователей в Teamphoria (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2169c-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2169c-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="2169c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2169c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2169c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="2169c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2169c-110">Prerequisites</span></span>

<span data-ttu-id="2169c-111">Чтобы настроить интеграцию Azure AD с Teamphoria, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="2169c-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="2169c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2169c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2169c-113">подписка Teamphoria с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="2169c-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2169c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="2169c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2169c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="2169c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2169c-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="2169c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2169c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2169c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2169c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2169c-118">Scenario description</span></span>
<span data-ttu-id="2169c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2169c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2169c-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="2169c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2169c-121">Добавление Teamphoria из коллекции</span><span class="sxs-lookup"><span data-stu-id="2169c-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="2169c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2169c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="2169c-123">Добавление Teamphoria из коллекции</span><span class="sxs-lookup"><span data-stu-id="2169c-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="2169c-124">Чтобы настроить интеграцию Teamphoria с Azure AD, необходимо добавить Teamphoria из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2169c-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2169c-125">**Чтобы добавить Teamphoria из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2169c-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2169c-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2169c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2169c-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="2169c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2169c-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2169c-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="2169c-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="2169c-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="2169c-133">В поле поиска введите **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="2169c-133">In the search box, type **Teamphoria**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="2169c-135">На панели результатов выберите **Teamphoria** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="2169c-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2169c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2169c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2169c-138">В этом разделе описана настройка и проверка единого входа Azure AD в Teamphoria с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2169c-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2169c-139">Чтобы единый вход работал, в Azure AD необходимо указать, какой пользователь в Teamphoria соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2169c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="2169c-140">Иными словами, необходимо установить связь между пользователем в Azure AD и соответствующим пользователем в Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="2169c-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="2169c-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="2169c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="2169c-142">Чтобы настроить и проверить единый вход Azure AD в Teamphoria, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="2169c-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2169c-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="2169c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2169c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2169c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2169c-145">**[Создание тестового пользователя Teamphoria](#creating-a-teamphoria-test-user)** требуется для создания пользователя Britta Simon в Teamphoria, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2169c-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2169c-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2169c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2169c-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2169c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2169c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2169c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2169c-149">В данном разделе описано, как включить единый вход Azure AD на портале управления Azure, а также как его настроить в приложении Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="2169c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="2169c-150">**Чтобы настроить единый вход Azure AD в Teamphoria, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2169c-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="2169c-151">На портале управления Azure на странице интеграции с приложением **Teamphoria** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="2169c-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="2169c-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="2169c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="2169c-155">В разделе **Домены и URL-адреса приложения Teamphoria** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="2169c-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="2169c-157">А.</span><span class="sxs-lookup"><span data-stu-id="2169c-157">a.</span></span> <span data-ttu-id="2169c-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<sub-domain>.teamphoria.com/login`.</span><span class="sxs-lookup"><span data-stu-id="2169c-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="2169c-159">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="2169c-159">Please note that these are not the real values.</span></span> <span data-ttu-id="2169c-160">Их необходимо заменить фактическим URL-адресом входа.</span><span class="sxs-lookup"><span data-stu-id="2169c-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="2169c-161">Чтобы получить его, обратитесь в [службу поддержки клиентов Teamphoria](https://www.teamphoria.com/).</span><span class="sxs-lookup"><span data-stu-id="2169c-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="2169c-162">В разделе **Сертификат подписи SAML** щелкните **(Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2169c-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="2169c-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2169c-164">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2169c-166">В разделе **Настройка Teamphoria** щелкните **Настройка Teamphoria**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="2169c-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2169c-167">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="2169c-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="2169c-169">Для настройки единого входа в **Teamphoria** войдите в приложение Teamphoria с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="2169c-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="2169c-170">Перейдите к пункту **Параметры администратора** в левой панели инструментов и в области вкладки настройки щелкните **Единый вход**, чтобы открыть окно настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="2169c-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="2169c-172">Щелкните параметр **ADD NEW IDENTITY PROVIDER** (Добавить нового поставщика удостоверений) в верхнем правом углу, чтобы открыть форму для добавления параметров единого входа.</span><span class="sxs-lookup"><span data-stu-id="2169c-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="2169c-174">Введите сведения в полях, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="2169c-174">Enter the details in the fields as described below-</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="2169c-176">А.</span><span class="sxs-lookup"><span data-stu-id="2169c-176">a.</span></span> <span data-ttu-id="2169c-177">**Отображаемое имя.** Введите отображаемое имя подключаемого модуля на странице администрирования.</span><span class="sxs-lookup"><span data-stu-id="2169c-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="2169c-178">b.</span><span class="sxs-lookup"><span data-stu-id="2169c-178">b.</span></span> <span data-ttu-id="2169c-179">**BUTTON NAME** (Имя кнопки). Имя вкладки, которая будет отображаться на странице входа при едином входе.</span><span class="sxs-lookup"><span data-stu-id="2169c-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="2169c-180">c.</span><span class="sxs-lookup"><span data-stu-id="2169c-180">c.</span></span> <span data-ttu-id="2169c-181">**Сертификат.** Откройте сертификат, скачанный ранее, на портале Azure в блокноте, скопируйте его содержимое и вставьте в поле.</span><span class="sxs-lookup"><span data-stu-id="2169c-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="2169c-182">d.</span><span class="sxs-lookup"><span data-stu-id="2169c-182">d.</span></span> <span data-ttu-id="2169c-183">**Точка входа.** Вставьте **URL-адрес службы единого входа SAML**, скопированный ранней на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2169c-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="2169c-184">д.</span><span class="sxs-lookup"><span data-stu-id="2169c-184">e.</span></span> <span data-ttu-id="2169c-185">Установите переключатель в положение **Вкл.** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2169c-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2169c-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2169c-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="2169c-187">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2169c-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="2169c-189">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="2169c-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2169c-190">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2169c-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2169c-192">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="2169c-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2169c-194">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="2169c-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2169c-196">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2169c-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2169c-198">а.</span><span class="sxs-lookup"><span data-stu-id="2169c-198">a.</span></span> <span data-ttu-id="2169c-199">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2169c-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2169c-200">b.</span><span class="sxs-lookup"><span data-stu-id="2169c-200">b.</span></span> <span data-ttu-id="2169c-201">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2169c-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2169c-202">c.</span><span class="sxs-lookup"><span data-stu-id="2169c-202">c.</span></span> <span data-ttu-id="2169c-203">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="2169c-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2169c-204">d.</span><span class="sxs-lookup"><span data-stu-id="2169c-204">d.</span></span> <span data-ttu-id="2169c-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2169c-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="2169c-206">Создание тестового пользователя Teamphoria</span><span class="sxs-lookup"><span data-stu-id="2169c-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="2169c-207">Чтобы пользователи Azure AD могли выполнить вход в Teamphoria, они должны быть подготовлены в Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="2169c-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="2169c-208">В случае с Teamphoria подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="2169c-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="2169c-209">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="2169c-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="2169c-210">Войдите на веб-сайт Teamphoria вашей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="2169c-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="2169c-211">Щелкните **параметры администратора** на левой панели и на вкладке **Управление** щелкните **Пользователи**, чтобы открыть страницу администрирования для пользователей.</span><span class="sxs-lookup"><span data-stu-id="2169c-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="2169c-213">Щелкните **MANUAL INVITE** (Пригласить вручную).</span><span class="sxs-lookup"><span data-stu-id="2169c-213">Click on the **MANUAL INVITE** option.</span></span>

    ![Приглашение пользователей](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="2169c-215">На этой странице сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="2169c-215">On this page, perform following action.</span></span> 
    
    ![Приглашение пользователей](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="2169c-217">а.</span><span class="sxs-lookup"><span data-stu-id="2169c-217">a.</span></span> <span data-ttu-id="2169c-218">В текстовом поле **Адрес электронной почты** находится **электронный адрес** пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2169c-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2169c-219">b.</span><span class="sxs-lookup"><span data-stu-id="2169c-219">b.</span></span> <span data-ttu-id="2169c-220">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2169c-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="2169c-221">c.</span><span class="sxs-lookup"><span data-stu-id="2169c-221">c.</span></span> <span data-ttu-id="2169c-222">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2169c-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="2169c-223">d.</span><span class="sxs-lookup"><span data-stu-id="2169c-223">d.</span></span> <span data-ttu-id="2169c-224">Нажмите кнопку **INVITE 1 USER** (Пригласить одного пользователя).</span><span class="sxs-lookup"><span data-stu-id="2169c-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="2169c-225">Пользователь должен принять приглашение, чтобы его создали в системе.</span><span class="sxs-lookup"><span data-stu-id="2169c-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2169c-226">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2169c-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2169c-227">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Teamphoria, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="2169c-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="2169c-229">**Чтобы назначить пользователя Britta Simon в Teamphoria, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2169c-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="2169c-230">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2169c-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2169c-232">Из списка приложений выберите **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="2169c-232">In the applications list, select **Teamphoria**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="2169c-234">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2169c-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="2169c-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2169c-236">Click **Add** button.</span></span> <span data-ttu-id="2169c-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2169c-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="2169c-239">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2169c-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2169c-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2169c-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2169c-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="2169c-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2169c-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2169c-242">Testing single sign-on</span></span>

<span data-ttu-id="2169c-243">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="2169c-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2169c-244">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="2169c-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="2169c-245">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="2169c-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2169c-246">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2169c-246">Additional resources</span></span>

* [<span data-ttu-id="2169c-247">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2169c-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2169c-248">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2169c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

