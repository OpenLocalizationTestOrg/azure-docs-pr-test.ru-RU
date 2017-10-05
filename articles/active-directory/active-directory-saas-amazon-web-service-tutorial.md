---
title: "Руководство по интеграции Azure Active Directory с Amazon Web Services (AWS) | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="88e3a-103">Руководство по интеграции Azure Active Directory с Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="88e3a-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="88e3a-104">В этом руководстве описано, как интегрировать приложение Amazon Web Services (AWS) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88e3a-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88e3a-105">Интеграция Azure AD с приложением Amazon Web Services обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="88e3a-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88e3a-106">С помощью Azure AD вы можете контролировать доступ к Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="88e3a-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="88e3a-107">Вы можете включить автоматический вход пользователей в Amazon Web Services (AWS) (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e3a-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88e3a-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="88e3a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="88e3a-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88e3a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="88e3a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="88e3a-110">Prerequisites</span></span>

<span data-ttu-id="88e3a-111">Чтобы настроить интеграцию Azure AD с Amazon Web Services, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="88e3a-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="88e3a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="88e3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88e3a-113">Подписка с поддержкой единого входа в Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="88e3a-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88e3a-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="88e3a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88e3a-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="88e3a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88e3a-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="88e3a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="88e3a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88e3a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88e3a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="88e3a-118">Scenario description</span></span>
<span data-ttu-id="88e3a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="88e3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88e3a-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="88e3a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88e3a-121">Добавление Amazon Web Services из коллекции.</span><span class="sxs-lookup"><span data-stu-id="88e3a-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="88e3a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="88e3a-123">Добавление Amazon Web Services из коллекции</span><span class="sxs-lookup"><span data-stu-id="88e3a-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="88e3a-124">Чтобы настроить интеграцию Amazon Web Services с Azure AD, вам потребуется добавить Amazon Web Services из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="88e3a-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88e3a-125">**Чтобы добавить Amazon Web Services (AWS) из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="88e3a-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88e3a-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88e3a-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88e3a-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="88e3a-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="88e3a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="88e3a-133">В поле поиска введите **Amazon Web Services (AWS)**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="88e3a-135">На панели результатов выберите **Amazon Web Services (AWS)** и щелкните **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="88e3a-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88e3a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e3a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88e3a-138">В этом разделе описана настройка и проверка единого входа Azure AD в Amazon Web Services (AWS) с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88e3a-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88e3a-139">Чтобы единый вход работал, в Azure AD необходимо указать, какой пользователь в Amazon Web Services соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e3a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="88e3a-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="88e3a-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="88e3a-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="88e3a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="88e3a-142">Чтобы настроить и проверить единый вход Azure AD в Amazon Web Services, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="88e3a-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88e3a-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="88e3a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88e3a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88e3a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88e3a-145">**[Создание тестового пользователя Amazon Web Services](#creating-an-amazon-web-services-test-user)** требуется для создания соответствующего пользователя Britta Simon в Amazon Web Services, связанного с ее представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e3a-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="88e3a-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e3a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88e3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="88e3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88e3a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e3a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88e3a-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Amazon Web Services (AWS).</span><span class="sxs-lookup"><span data-stu-id="88e3a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="88e3a-150">**Чтобы настроить единый вход Azure AD в Amazon Web Services, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="88e3a-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="88e3a-151">На портале Azure на странице интеграции с приложением **Amazon Web Services (AWS)** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="88e3a-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="88e3a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="88e3a-155">В разделе **Домены и URL-адреса приложения Amazon Web Services (AWS)** не нужно выполнять никаких действий, так как приложение уже предварительно интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="88e3a-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="88e3a-157">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="88e3a-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="88e3a-159">Приложение Amazon Web Services (AWS) ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="88e3a-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="88e3a-160">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="88e3a-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="88e3a-161">Управлять значениями этих атрибутов можно в разделе **Атрибуты пользователя** на странице интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="88e3a-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="88e3a-162">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="88e3a-162">The following screenshot shows an example for this.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="88e3a-164">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке выше, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="88e3a-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="88e3a-165">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="88e3a-165">Attribute Name</span></span>  | <span data-ttu-id="88e3a-166">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="88e3a-166">Attribute Value</span></span> | <span data-ttu-id="88e3a-167">Пространство имен</span><span class="sxs-lookup"><span data-stu-id="88e3a-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="88e3a-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="88e3a-168">RoleSessionName</span></span> | <span data-ttu-id="88e3a-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="88e3a-169">user.userprincipalname</span></span> | <span data-ttu-id="88e3a-170">https://aws.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="88e3a-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="88e3a-171">Роль</span><span class="sxs-lookup"><span data-stu-id="88e3a-171">Role</span></span>            | <span data-ttu-id="88e3a-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="88e3a-172">user.assignedroles</span></span> |  <span data-ttu-id="88e3a-173">https://aws.Amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="88e3a-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="88e3a-174">Необходимо настроить подготовку пользователя в Azure AD для получения всех ролей из консоли AWS.</span><span class="sxs-lookup"><span data-stu-id="88e3a-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="88e3a-175">Этапы подготовки см. ниже.</span><span class="sxs-lookup"><span data-stu-id="88e3a-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="88e3a-176">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-176">a.</span></span> <span data-ttu-id="88e3a-177">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="88e3a-179">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-179">b.</span></span> <span data-ttu-id="88e3a-180">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="88e3a-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="88e3a-182">c.</span><span class="sxs-lookup"><span data-stu-id="88e3a-182">c.</span></span> <span data-ttu-id="88e3a-183">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="88e3a-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="88e3a-184">Добавьте значение пространства имен, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="88e3a-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="88e3a-185">г)</span><span class="sxs-lookup"><span data-stu-id="88e3a-185">d.</span></span> <span data-ttu-id="88e3a-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-186">Click **Ok**.</span></span>

7. <span data-ttu-id="88e3a-187">Нажмите кнопку **Сохранить**, чтобы сохранить параметры в Azure.</span><span class="sxs-lookup"><span data-stu-id="88e3a-187">Click **Save** button to save the settings on Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="88e3a-189">В другом окне браузера войдите на сайт Amazon Web Services компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="88e3a-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="88e3a-190">Щелкните **Console Home**(Домашняя страница консоли).</span><span class="sxs-lookup"><span data-stu-id="88e3a-190">Click **Console Home**.</span></span>
   
    ![Настройка единого входа][11]

10. <span data-ttu-id="88e3a-192">Щелкните **IAM** в службе **Security, Identity & Compliance** (Безопасность, удостоверения и соответствие требованиям).</span><span class="sxs-lookup"><span data-stu-id="88e3a-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![Настройка единого входа][12]

11. <span data-ttu-id="88e3a-194">Щелкните **Identity Providers** (Поставщики удостоверений), затем щелкните **Create Provider** (Создать поставщик).</span><span class="sxs-lookup"><span data-stu-id="88e3a-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![Настройка единого входа][13]

12. <span data-ttu-id="88e3a-196">На странице диалогового окна **Configure Provider** (Настройка поставщика) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88e3a-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![Настройка единого входа][14]
 
    <span data-ttu-id="88e3a-198">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-198">a.</span></span> <span data-ttu-id="88e3a-199">Выберите для параметра **Тип поставщика** значение **SAML**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="88e3a-200">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-200">b.</span></span> <span data-ttu-id="88e3a-201">В текстовом поле **Имя поставщика** введите имя поставщика (например, *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="88e3a-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="88e3a-202">В.</span><span class="sxs-lookup"><span data-stu-id="88e3a-202">c.</span></span> <span data-ttu-id="88e3a-203">Чтобы отправить загруженный файл метаданных, нажмите кнопку **Выбрать файл**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="88e3a-204">d.</span><span class="sxs-lookup"><span data-stu-id="88e3a-204">d.</span></span> <span data-ttu-id="88e3a-205">Щелкните **Следующий шаг**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="88e3a-206">На странице диалогового окна **Verify Provider Information** (Проверка сведений о поставщике) щелкните **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="88e3a-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![Настройка единого входа][15]

14. <span data-ttu-id="88e3a-208">Щелкните **Roles** (Роли), а затем нажмите кнопку **Create New Role** (Создать новую роль).</span><span class="sxs-lookup"><span data-stu-id="88e3a-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![Настройка единого входа][16]

15. <span data-ttu-id="88e3a-210">В диалоговом окне **Set Role Name** (Настройка имени роли) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88e3a-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![Настройка единого входа][17] 

    <span data-ttu-id="88e3a-212">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-212">a.</span></span> <span data-ttu-id="88e3a-213">В текстовом поле **Имя роли** введите имя роли (например, *TestUser*).</span><span class="sxs-lookup"><span data-stu-id="88e3a-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="88e3a-214">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-214">b.</span></span> <span data-ttu-id="88e3a-215">Щелкните **Следующий шаг**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="88e3a-216">В диалоговом окне **Select Role Type** (Выбор типа роли) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88e3a-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![Настройка единого входа][18] 

    <span data-ttu-id="88e3a-218">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-218">a.</span></span> <span data-ttu-id="88e3a-219">Выберите **Роль для доступа поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="88e3a-220">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-220">b.</span></span> <span data-ttu-id="88e3a-221">В разделе **Grant Web Single Sign-On (WebSSO) access to SAML providers** (Предоставление единого входа через Интернет (WebSSO) для доступа к поставщикам SAML) щелкните **Select** (Выбрать).</span><span class="sxs-lookup"><span data-stu-id="88e3a-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="88e3a-222">В диалоговом окне **Establish Trust** (Установка доверия) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88e3a-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![Настройка единого входа][19] 

    <span data-ttu-id="88e3a-224">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-224">a.</span></span> <span data-ttu-id="88e3a-225">В качестве поставщика SAML выберите поставщик SAML, созданный ранее (например, *WAAD*).</span><span class="sxs-lookup"><span data-stu-id="88e3a-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="88e3a-226">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-226">b.</span></span> <span data-ttu-id="88e3a-227">Щелкните **Следующий шаг**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="88e3a-228">В диалоговом окне **Verify Role Trust** (Проверка доверия роли) нажмите кнопку **Next Step** (Следующий шаг).</span><span class="sxs-lookup"><span data-stu-id="88e3a-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![Настройка единого входа][32]

19. <span data-ttu-id="88e3a-230">В диалоговом окне **Attach Policy** (Присоединение политики) нажмите кнопку **Next Step** (Следующий шаг).</span><span class="sxs-lookup"><span data-stu-id="88e3a-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![Настройка единого входа][33]

20. <span data-ttu-id="88e3a-232">В диалоговом окне **Review** (Обзор) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88e3a-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![Настройка единого входа][34]
 
    <span data-ttu-id="88e3a-234">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-234">a.</span></span> <span data-ttu-id="88e3a-235">Щелкните **Создать роль**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-235">Click **Create Role**.</span></span>

    <span data-ttu-id="88e3a-236">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-236">b.</span></span> <span data-ttu-id="88e3a-237">Создайте необходимое количество ролей и сопоставьте их с поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="88e3a-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="88e3a-238">Теперь настройте подготовку пользователя для получения всех ролей из AWS.</span><span class="sxs-lookup"><span data-stu-id="88e3a-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="88e3a-239">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-239">a.</span></span> <span data-ttu-id="88e3a-240">В консоли AWS войдите в систему с использованием учетной записи root.</span><span class="sxs-lookup"><span data-stu-id="88e3a-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="88e3a-241">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-241">b.</span></span> <span data-ttu-id="88e3a-242">В правом верхнем углу щелкните свое имя и выберите параметр **My Security Credentials** (Мои учетные данные для безопасного доступа).</span><span class="sxs-lookup"><span data-stu-id="88e3a-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="88e3a-243">Откроется экран с предупреждением.</span><span class="sxs-lookup"><span data-stu-id="88e3a-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="88e3a-244">Нажмите кнопку **Security Credentials** (Учетные данные для безопасного доступа), чтобы закрыть предупреждение.</span><span class="sxs-lookup"><span data-stu-id="88e3a-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![Настройка единого входа][36]

       ![Настройка единого входа][37]

    <span data-ttu-id="88e3a-247">c.</span><span class="sxs-lookup"><span data-stu-id="88e3a-247">c.</span></span> <span data-ttu-id="88e3a-248">В разделе "Ключи доступа" щелкните **Create New Access Key** (Создать ключ доступа).</span><span class="sxs-lookup"><span data-stu-id="88e3a-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="88e3a-249">При этом будет создан идентификатор ключа доступа и значение токена.</span><span class="sxs-lookup"><span data-stu-id="88e3a-249">This generates the Access Key ID and a token value.</span></span>
    
       ![Настройка единого входа][38]

    <span data-ttu-id="88e3a-251">d.</span><span class="sxs-lookup"><span data-stu-id="88e3a-251">d.</span></span> <span data-ttu-id="88e3a-252">Скопируйте оба эти значения, а также скачайте их, чтобы не потерять.</span><span class="sxs-lookup"><span data-stu-id="88e3a-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="88e3a-253">д.</span><span class="sxs-lookup"><span data-stu-id="88e3a-253">e.</span></span> <span data-ttu-id="88e3a-254">На портале Azure на странице интеграции с приложением Amazon Web Services (AWS) щелкните **Подготовка**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![Настройка единого входа][35]

    <span data-ttu-id="88e3a-256">f.</span><span class="sxs-lookup"><span data-stu-id="88e3a-256">f.</span></span> <span data-ttu-id="88e3a-257">Для параметра "Режим подготовки к работе" выберите значение **Автоматически**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![Настройка единого входа][39]

    <span data-ttu-id="88e3a-259">g.</span><span class="sxs-lookup"><span data-stu-id="88e3a-259">g.</span></span> <span data-ttu-id="88e3a-260">Теперь в поле **Секрет клиента** и **Секретный токен** вставьте соответствующие значения, скопированные из консоли AWS ранее.</span><span class="sxs-lookup"><span data-stu-id="88e3a-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="88e3a-261">h.</span><span class="sxs-lookup"><span data-stu-id="88e3a-261">h.</span></span> <span data-ttu-id="88e3a-262">Вы можете нажать кнопку **Проверить подключение**, чтобы проверить возможность подключения.</span><span class="sxs-lookup"><span data-stu-id="88e3a-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="88e3a-263">Если все подключено, можно запустить соединитель подготовки.</span><span class="sxs-lookup"><span data-stu-id="88e3a-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![Настройка единого входа][40]

    <span data-ttu-id="88e3a-265">i.</span><span class="sxs-lookup"><span data-stu-id="88e3a-265">i.</span></span> <span data-ttu-id="88e3a-266">Теперь в разделе "Состояние подготовки" нажмите кнопку **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="88e3a-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="88e3a-267">При этом запустится выборка ролей из приложения.</span><span class="sxs-lookup"><span data-stu-id="88e3a-267">This starts fetching the roles from the application.</span></span>

       ![Настройка единого входа][41]

    > [!NOTE]
    > <span data-ttu-id="88e3a-269">Через некоторое время запустится служба подготовки Azure AD для синхронизации ролей из AWS.</span><span class="sxs-lookup"><span data-stu-id="88e3a-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="88e3a-270">В Azure AD должны отображаться все роли AWS, подключенные к поставщику удостоверений. Их можно использовать при назначении приложения пользователям или группам.</span><span class="sxs-lookup"><span data-stu-id="88e3a-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88e3a-271">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e3a-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="88e3a-272">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88e3a-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="88e3a-274">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="88e3a-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88e3a-275">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88e3a-277">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="88e3a-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88e3a-279">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88e3a-281">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88e3a-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88e3a-283">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-283">a.</span></span> <span data-ttu-id="88e3a-284">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88e3a-285">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-285">b.</span></span> <span data-ttu-id="88e3a-286">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88e3a-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88e3a-287">c.</span><span class="sxs-lookup"><span data-stu-id="88e3a-287">c.</span></span> <span data-ttu-id="88e3a-288">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88e3a-289">d.</span><span class="sxs-lookup"><span data-stu-id="88e3a-289">d.</span></span> <span data-ttu-id="88e3a-290">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="88e3a-291">Создание тестового пользователя Amazon Web Services</span><span class="sxs-lookup"><span data-stu-id="88e3a-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="88e3a-292">Чтобы пользователи Azure AD могли войти в службу Amazon Web Services (AWS), их необходимо подготовить в ней.</span><span class="sxs-lookup"><span data-stu-id="88e3a-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="88e3a-293">В случае с Amazon Web Services (AWS) подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="88e3a-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="88e3a-294">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="88e3a-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="88e3a-295">Войдите на сайт компании **Amazon Web Services** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="88e3a-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="88e3a-296">Щелкните значок **домашней страницы консоли** .</span><span class="sxs-lookup"><span data-stu-id="88e3a-296">Click the **Console Home** icon.</span></span> 
   
    ![Настройка единого входа][11]

3. <span data-ttu-id="88e3a-298">Щелкните Identity and Access Management (Управление удостоверениями и доступом).</span><span class="sxs-lookup"><span data-stu-id="88e3a-298">Click Identity and Access Management.</span></span> 
   
    ![Настройка единого входа][28]

4. <span data-ttu-id="88e3a-300">На панели мониторинга щелкните **Пользователи**, а затем — **Create New Users** (Создать пользователей).</span><span class="sxs-lookup"><span data-stu-id="88e3a-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![Настройка единого входа][29]

5. <span data-ttu-id="88e3a-302">В диалоговом окне Create User (Создание пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="88e3a-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![Настройка единого входа][30]   
    
    <span data-ttu-id="88e3a-304">а.</span><span class="sxs-lookup"><span data-stu-id="88e3a-304">a.</span></span> <span data-ttu-id="88e3a-305">В текстовых полях **Введите имена пользователей** введите имя пользователя (userprincipalname) в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e3a-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="88e3a-306">b.</span><span class="sxs-lookup"><span data-stu-id="88e3a-306">b.</span></span> <span data-ttu-id="88e3a-307">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88e3a-308">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e3a-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88e3a-309">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Amazon Web Services (AWS), чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="88e3a-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="88e3a-311">**Чтобы назначить пользователя Britta Simon в Amazon Web Services (AWS), сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="88e3a-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="88e3a-312">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="88e3a-314">В списке приложений выберите **Amazon Web Services**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="88e3a-316">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-316">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="88e3a-318">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-318">Click **Add** button.</span></span> <span data-ttu-id="88e3a-319">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="88e3a-321">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88e3a-322">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88e3a-323">На вкладке **Выбор роли** выберите соответствующую роль для пользователя.</span><span class="sxs-lookup"><span data-stu-id="88e3a-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="88e3a-324">Все эти роли показаны со своими именами и именами поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="88e3a-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="88e3a-325">Таким образом, можно легко определить роли из AWS.</span><span class="sxs-lookup"><span data-stu-id="88e3a-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="88e3a-326">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="88e3a-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88e3a-327">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="88e3a-327">Testing single sign-on</span></span>

<span data-ttu-id="88e3a-328">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="88e3a-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="88e3a-329">Щелкнув плитку Amazon Web Services на панели доступа, вы автоматически войдете в приложение Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="88e3a-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="88e3a-330">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="88e3a-330">Additional resources</span></span>

* [<span data-ttu-id="88e3a-331">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88e3a-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88e3a-332">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88e3a-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
