---
title: "Руководство. Интеграция Azure Active Directory с Procore SSO | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Procore SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="02c0a-103">Руководство. Интеграция Azure Active Directory с Procore SSO</span><span class="sxs-lookup"><span data-stu-id="02c0a-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="02c0a-104">В этом руководстве описано, как интегрировать Procore SSO с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="02c0a-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="02c0a-105">Интеграция Azure AD с приложением Procore SSO обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="02c0a-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="02c0a-106">С помощью Azure AD вы можете контролировать доступ к Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="02c0a-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="02c0a-107">Вы можете включить автоматический вход пользователей в Procore SSO (единый вход) с помощью учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c0a-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="02c0a-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="02c0a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="02c0a-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="02c0a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="02c0a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="02c0a-110">Prerequisites</span></span>

<span data-ttu-id="02c0a-111">Чтобы настроить интеграцию Azure AD с Procore SSO, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="02c0a-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="02c0a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="02c0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="02c0a-113">подписка на Procore SSO с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="02c0a-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="02c0a-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="02c0a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="02c0a-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="02c0a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="02c0a-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="02c0a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="02c0a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02c0a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="02c0a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="02c0a-118">Scenario description</span></span>
<span data-ttu-id="02c0a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="02c0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="02c0a-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="02c0a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="02c0a-121">Добавление Procore SSO из коллекции</span><span class="sxs-lookup"><span data-stu-id="02c0a-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="02c0a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="02c0a-123">Добавление Procore SSO из коллекции</span><span class="sxs-lookup"><span data-stu-id="02c0a-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="02c0a-124">Чтобы настроить интеграцию Procore SSO с Azure AD, необходимо добавить Procore SSO из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="02c0a-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="02c0a-125">**Чтобы добавить приложение Procore SSO из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="02c0a-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="02c0a-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="02c0a-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="02c0a-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="02c0a-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="02c0a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="02c0a-133">В поле поиска введите **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-133">In the search box, type **Procore SSO**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="02c0a-135">На панели результатов выберите **Procore SSO** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="02c0a-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="02c0a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c0a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="02c0a-138">В этом разделе описана настройка и проверка единого входа Azure AD в Procore SSO с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02c0a-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="02c0a-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Procore SSO соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c0a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="02c0a-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="02c0a-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="02c0a-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="02c0a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="02c0a-142">Чтобы настроить и проверить единый вход Azure AD в Procore SSO, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="02c0a-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="02c0a-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="02c0a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="02c0a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02c0a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="02c0a-145">**[Создание тестового пользователя Procore SSO](#creating-a-procore-sso-test-user)** требуется для создания пользователя Britta Simon в Procore SSO, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c0a-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="02c0a-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="02c0a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="02c0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="02c0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="02c0a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c0a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="02c0a-149">В данном разделе описано, как включить единый вход в Azure AD на портале управления Azure и настроить его в приложении Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="02c0a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="02c0a-150">**Чтобы настроить единый вход Azure AD в Procore SSO, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="02c0a-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="02c0a-151">На портале управления Azure на странице интеграции с приложением **Procore SSO** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="02c0a-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="02c0a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="02c0a-155">В разделе **Домен и URL-адреса единого входа в Procore SSO** не нужно выполнять никаких действий, поскольку приложение уже предварительно интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="02c0a-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="02c0a-157">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="02c0a-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="02c0a-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="02c0a-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="02c0a-161">В разделе **Конфигурация Procore SSO** щелкните **Настроить Procore SSO**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="02c0a-162">Скопируйте **Идентификатор сущности SAML, URL-адрес службы единого входа SAML и URL-адрес единого входа** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="02c0a-164">Чтобы настроить единый вход на стороне **Procore SSO**, выполните вход на корпоративный сайт Procore с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="02c0a-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="02c0a-165">В раскрывающемся списке инструментов щелкните **Admin** (Администрирование), чтобы открыть страницу для настройки единого входа.</span><span class="sxs-lookup"><span data-stu-id="02c0a-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="02c0a-167">Вставьте в поля нужные значения, как описано ниже</span><span class="sxs-lookup"><span data-stu-id="02c0a-167">Paste the values in the boxes as described below-</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="02c0a-169">а.</span><span class="sxs-lookup"><span data-stu-id="02c0a-169">a.</span></span> <span data-ttu-id="02c0a-170">В поле **Single Sign On Issuer URL** (URL-адрес издателя единого входа), вставьте идентификатор сущности SAML, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="02c0a-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="02c0a-171">b.</span><span class="sxs-lookup"><span data-stu-id="02c0a-171">b.</span></span> <span data-ttu-id="02c0a-172">В поле **Single Sign On Target URL)** (Целевой URL-адрес единого входа), вставьте URL-адрес службы единого входа SAML, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="02c0a-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="02c0a-173">c.</span><span class="sxs-lookup"><span data-stu-id="02c0a-173">c.</span></span> <span data-ttu-id="02c0a-174">Теперь откройте **XML-файл метаданных**, который вы ранее скачали с портала Azure, и скопируйте из него сертификат, расположенный в теге с именем **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="02c0a-175">Вставьте это значение в поле **Single Sign On x509 Certificate** (Сертификат x509 для единого входа).</span><span class="sxs-lookup"><span data-stu-id="02c0a-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="02c0a-176">Щелкните **Save Changes** (Сохранить изменения).</span><span class="sxs-lookup"><span data-stu-id="02c0a-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="02c0a-177">Когда вы завершите эту настройку, передайте **имя домена** (например, **contoso.com**), для которого осуществляется вход в Procore, в [службу поддержки Procore](https://support.procore.com/) для активации федеративного единого входа для этого домена.</span><span class="sxs-lookup"><span data-stu-id="02c0a-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="02c0a-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c0a-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="02c0a-179">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="02c0a-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="02c0a-181">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="02c0a-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="02c0a-182">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="02c0a-184">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="02c0a-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="02c0a-186">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="02c0a-188">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="02c0a-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="02c0a-190">а.</span><span class="sxs-lookup"><span data-stu-id="02c0a-190">a.</span></span> <span data-ttu-id="02c0a-191">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="02c0a-192">b.</span><span class="sxs-lookup"><span data-stu-id="02c0a-192">b.</span></span> <span data-ttu-id="02c0a-193">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="02c0a-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="02c0a-194">c.</span><span class="sxs-lookup"><span data-stu-id="02c0a-194">c.</span></span> <span data-ttu-id="02c0a-195">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="02c0a-196">d.</span><span class="sxs-lookup"><span data-stu-id="02c0a-196">d.</span></span> <span data-ttu-id="02c0a-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="02c0a-198">Создание тестового пользователя Procore SSO</span><span class="sxs-lookup"><span data-stu-id="02c0a-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="02c0a-199">Выполните следующие действия, чтобы создать тестового пользователя на стороне Procore.</span><span class="sxs-lookup"><span data-stu-id="02c0a-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="02c0a-200">Войдите на корпоративный сайт Procore с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="02c0a-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="02c0a-201">В раскрывающемся списке инструментов щелкните **Directory** (Каталог), чтобы открыть страницу корпоративного каталога.</span><span class="sxs-lookup"><span data-stu-id="02c0a-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="02c0a-203">Щелкните **Add a Person** (Добавить сотрудника), чтобы открыть форму регистрации, и введите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="02c0a-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="02c0a-205">а.</span><span class="sxs-lookup"><span data-stu-id="02c0a-205">a.</span></span> <span data-ttu-id="02c0a-206">В текстовое поле **First Name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="02c0a-207">b.</span><span class="sxs-lookup"><span data-stu-id="02c0a-207">b.</span></span> <span data-ttu-id="02c0a-208">В текстовое поле **Last Name** (Фамилия) введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="02c0a-209">c.</span><span class="sxs-lookup"><span data-stu-id="02c0a-209">c.</span></span> <span data-ttu-id="02c0a-210">В текстовое поле **Email Address** (Адрес электронной почты) введите адрес электронной почты пользователя, например **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="02c0a-211">d.</span><span class="sxs-lookup"><span data-stu-id="02c0a-211">d.</span></span> <span data-ttu-id="02c0a-212">Для параметра **Permission Template** (Шаблон разрешений) выберите значение **Apply Permission Template Later** (Применить шаблон разрешений позже).</span><span class="sxs-lookup"><span data-stu-id="02c0a-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="02c0a-213">д.</span><span class="sxs-lookup"><span data-stu-id="02c0a-213">e.</span></span> <span data-ttu-id="02c0a-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-214">Click **Create**.</span></span>

4. <span data-ttu-id="02c0a-215">Проверьте и измените при необходимости сведения о добавляемом сотруднике.</span><span class="sxs-lookup"><span data-stu-id="02c0a-215">Check and update the details for the newly added contact.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="02c0a-217">Щелкните действие **Save and Send Invitiation** (Сохранить и отправить приглашение), если требуется приглашение, или просто **Save** (Сохранить), чтобы завершить регистрацию пользователя.</span><span class="sxs-lookup"><span data-stu-id="02c0a-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="02c0a-219">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="02c0a-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="02c0a-220">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="02c0a-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="02c0a-222">**Чтобы назначить пользователя Britta Simon в приложение Procore SSO, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="02c0a-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="02c0a-223">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="02c0a-225">В списке приложений выберите **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-225">In the applications list, select **Procore SSO**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="02c0a-227">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="02c0a-229">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-229">Click **Add** button.</span></span> <span data-ttu-id="02c0a-230">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="02c0a-232">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="02c0a-233">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="02c0a-234">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="02c0a-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="02c0a-235">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="02c0a-235">Testing single sign-on</span></span>

<span data-ttu-id="02c0a-236">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="02c0a-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="02c0a-237">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="02c0a-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="02c0a-238">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="02c0a-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="02c0a-239">Щелкнув плитку Procore SSO на панели доступа, вы автоматически войдете в приложение Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="02c0a-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="02c0a-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="02c0a-240">Additional resources</span></span>

* [<span data-ttu-id="02c0a-241">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="02c0a-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="02c0a-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="02c0a-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

