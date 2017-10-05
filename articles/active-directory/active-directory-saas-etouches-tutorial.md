---
title: "Руководство по интеграции Azure Active Directory с etouches | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3cd9e9d6aae924369065ca492b1f6380c0ddc5fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="37f72-103">Руководство. Интеграция Azure Active Directory с etouches</span><span class="sxs-lookup"><span data-stu-id="37f72-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="37f72-104">В этом руководстве описано, как интегрировать приложение etouches с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37f72-104">In this tutorial, you learn how to integrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37f72-105">Интеграция Azure AD с приложением etouches обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="37f72-105">Integrating etouches with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37f72-106">С помощью Azure AD вы можете контролировать доступ к etouches.</span><span class="sxs-lookup"><span data-stu-id="37f72-106">You can control in Azure AD who has access to etouches</span></span>
- <span data-ttu-id="37f72-107">Вы можете включить автоматический вход пользователей в etouches (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37f72-107">You can enable your users to automatically get signed-on to etouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37f72-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="37f72-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37f72-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37f72-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37f72-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="37f72-110">Prerequisites</span></span>

<span data-ttu-id="37f72-111">Чтобы настроить интеграцию Azure AD с etouches, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="37f72-111">To configure Azure AD integration with etouches, you need the following items:</span></span>

- <span data-ttu-id="37f72-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="37f72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37f72-113">подписка etouches с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="37f72-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37f72-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="37f72-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37f72-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="37f72-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37f72-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="37f72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37f72-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37f72-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37f72-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="37f72-118">Scenario description</span></span>
<span data-ttu-id="37f72-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="37f72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37f72-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="37f72-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37f72-121">Добавление etouches из коллекции.</span><span class="sxs-lookup"><span data-stu-id="37f72-121">Adding etouches from the gallery</span></span>
2. <span data-ttu-id="37f72-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-the-gallery"></a><span data-ttu-id="37f72-123">Добавление etouches из коллекции</span><span class="sxs-lookup"><span data-stu-id="37f72-123">Adding etouches from the gallery</span></span>
<span data-ttu-id="37f72-124">Чтобы настроить интеграцию etouches с Azure AD, необходимо добавить etouches из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="37f72-124">To configure the integration of etouches into Azure AD, you need to add etouches from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37f72-125">**Чтобы добавить etouches из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="37f72-125">**To add etouches from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37f72-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37f72-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="37f72-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="37f72-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37f72-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="37f72-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="37f72-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="37f72-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="37f72-133">В поле поиска введите **etouches**, выберите **etouches** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="37f72-133">In the search box, type **etouches**, select **etouches** from result panel then click **Add** button to add the application.</span></span>

    ![etouches в списке результатов](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="37f72-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f72-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="37f72-136">В этом разделе описана настройка и проверка единого входа Azure AD в etouches с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37f72-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37f72-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в etouches соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37f72-137">For single sign-on to work, Azure AD needs to know what the counterpart user in etouches is to a user in Azure AD.</span></span> <span data-ttu-id="37f72-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в etouches.</span><span class="sxs-lookup"><span data-stu-id="37f72-138">In other words, a link relationship between an Azure AD user and the related user in etouches needs to be established.</span></span>

<span data-ttu-id="37f72-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в etouches.</span><span class="sxs-lookup"><span data-stu-id="37f72-139">In etouches, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37f72-140">Чтобы настроить и проверить единый вход Azure AD в etouches, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="37f72-140">To configure and test Azure AD single sign-on with etouches, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37f72-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="37f72-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="37f72-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37f72-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37f72-143">**[Создание тестового пользователя etouches](#create-an-etouches-test-user)** требуется для создания в etouches пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37f72-143">**[Create an etouches test user](#create-an-etouches-test-user)** - to have a counterpart of Britta Simon in etouches that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="37f72-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37f72-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37f72-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="37f72-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="37f72-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f72-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="37f72-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении etouches.</span><span class="sxs-lookup"><span data-stu-id="37f72-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="37f72-148">**Чтобы настроить единый вход Azure AD в etouches, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="37f72-148">**To configure Azure AD single sign-on with etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="37f72-149">На портале Azure на странице интеграции с приложением **etouches** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="37f72-149">In the Azure portal, on the **etouches** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="37f72-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="37f72-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="37f72-153">В разделе **Домены и URL-адреса приложения etouches** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37f72-153">On the **etouches Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="37f72-155">а.</span><span class="sxs-lookup"><span data-stu-id="37f72-155">a.</span></span> <span data-ttu-id="37f72-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="37f72-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="37f72-157">b.</span><span class="sxs-lookup"><span data-stu-id="37f72-157">b.</span></span> <span data-ttu-id="37f72-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="37f72-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37f72-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="37f72-159">These values are not real.</span></span> <span data-ttu-id="37f72-160">Их необходимо заменить на фактический URL-адрес входа и идентификатор, как описано далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="37f72-160">You update the value with the actual Sign on URL and Identifier, which is explained later in the tutorial.</span></span>
    > 

4. <span data-ttu-id="37f72-161">Приложение etouches ожидает утверждения SAML в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="37f72-161">etouches application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="37f72-162">Настройте следующие утверждения для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="37f72-162">Configure the following claims for this application.</span></span> <span data-ttu-id="37f72-163">Управлять значениями этих атрибутов можно на вкладке **Атрибут пользователя** приложения.</span><span class="sxs-lookup"><span data-stu-id="37f72-163">You can manage the values of these attributes from the **User Attribute** of the application.</span></span> <span data-ttu-id="37f72-164">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="37f72-164">The following screenshot shows an example for this.</span></span> 

    ![Атрибут пользователя](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="37f72-166">В разделе **Атрибуты пользователя** диалогового окна **Единый вход** настройте атрибут токена SAML, как показано на рисунке, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37f72-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="37f72-167">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="37f72-167">Attribute Name</span></span> | <span data-ttu-id="37f72-168">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="37f72-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="37f72-169">Email</span><span class="sxs-lookup"><span data-stu-id="37f72-169">Email</span></span> | <span data-ttu-id="37f72-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="37f72-170">user.mail</span></span> |    
    
    <span data-ttu-id="37f72-171">а.</span><span class="sxs-lookup"><span data-stu-id="37f72-171">a.</span></span> <span data-ttu-id="37f72-172">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="37f72-172">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Добавление атрибута](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Диалоговое окно добавления атрибута](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="37f72-175">b.</span><span class="sxs-lookup"><span data-stu-id="37f72-175">b.</span></span> <span data-ttu-id="37f72-176">В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="37f72-176">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="37f72-177">c.</span><span class="sxs-lookup"><span data-stu-id="37f72-177">c.</span></span> <span data-ttu-id="37f72-178">В списке **Значение** выберите значение атрибута, отображаемое для этой строки.</span><span class="sxs-lookup"><span data-stu-id="37f72-178">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="37f72-179">г)</span><span class="sxs-lookup"><span data-stu-id="37f72-179">d.</span></span> <span data-ttu-id="37f72-180">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="37f72-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="37f72-181">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="37f72-181">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="37f72-183">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="37f72-183">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="37f72-185">Чтобы настроить единый вход для приложения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37f72-185">To get SSO configured for your application, perform the following steps in the etouches application:</span></span> 

    ![Настройка etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="37f72-187">а.</span><span class="sxs-lookup"><span data-stu-id="37f72-187">a.</span></span> <span data-ttu-id="37f72-188">Войдите в приложение **etouches** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="37f72-188">Login to **etouches** application using the Admin rights.</span></span>
   
    <span data-ttu-id="37f72-189">b.</span><span class="sxs-lookup"><span data-stu-id="37f72-189">b.</span></span> <span data-ttu-id="37f72-190">Перейдите к настройке **SAML**.</span><span class="sxs-lookup"><span data-stu-id="37f72-190">Go to the **SAML** Configuration.</span></span>

    <span data-ttu-id="37f72-191">c.</span><span class="sxs-lookup"><span data-stu-id="37f72-191">c.</span></span> <span data-ttu-id="37f72-192">Перейдите в раздел **General Settings** (Общие параметры), откройте в Блокноте скачанный с портала Azure сертификат, скопируйте его содержимое и вставьте в текстовое поле IDP metadata (Метаданные поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="37f72-192">In the **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy the content, and then paste it into the IDP metadata textbox.</span></span> 

    <span data-ttu-id="37f72-193">d.</span><span class="sxs-lookup"><span data-stu-id="37f72-193">d.</span></span> <span data-ttu-id="37f72-194">Нажмите кнопку **Save & Stay** (Сохранить и остаться).</span><span class="sxs-lookup"><span data-stu-id="37f72-194">Click on the **Save & Stay** button.</span></span>
  
    <span data-ttu-id="37f72-195">д.</span><span class="sxs-lookup"><span data-stu-id="37f72-195">e.</span></span> <span data-ttu-id="37f72-196">В разделе метаданных SAML нажмите кнопку **Update Metadata** (Обновить метаданные).</span><span class="sxs-lookup"><span data-stu-id="37f72-196">Click on the **Update Metadata** button in the SAML Metadata section.</span></span> 

    <span data-ttu-id="37f72-197">f.</span><span class="sxs-lookup"><span data-stu-id="37f72-197">f.</span></span> <span data-ttu-id="37f72-198">Это действие открывает страницу единого входа.</span><span class="sxs-lookup"><span data-stu-id="37f72-198">This opens the page and perform SSO.</span></span> <span data-ttu-id="37f72-199">Если единый вход работает, можно настроить имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="37f72-199">Once the SSO is working then you can set up the username.</span></span>

    <span data-ttu-id="37f72-200">g.</span><span class="sxs-lookup"><span data-stu-id="37f72-200">g.</span></span> <span data-ttu-id="37f72-201">В поле Username (Имя пользователя) выберите значение **emailaddress**, как показано на изображении ниже.</span><span class="sxs-lookup"><span data-stu-id="37f72-201">In the Username field, select the **emailaddress** as shown in the image below.</span></span> 

    <span data-ttu-id="37f72-202">h.</span><span class="sxs-lookup"><span data-stu-id="37f72-202">h.</span></span> <span data-ttu-id="37f72-203">Скопируйте значение **SP entity ID** (Идентификатор сущности SP) и вставьте его в текстовое поле **Идентификатор** в разделе **Домены и URL-адреса приложения etouches** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="37f72-203">Copy the **SP entity ID** value and paste it into the **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="37f72-204">i.</span><span class="sxs-lookup"><span data-stu-id="37f72-204">i.</span></span> <span data-ttu-id="37f72-205">Скопируйте значение **SSO URL / ACS** (URL-адрес и ASC для единого входа) и вставьте его в текстовое поле **URL-адрес для входа** в разделе **Домены и URL-адреса приложения etouches** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="37f72-205">Copy the **SSO URL / ACS** value and paste it into the **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="37f72-206">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="37f72-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37f72-207">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="37f72-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37f72-208">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="37f72-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="37f72-209">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f72-209">Create an Azure AD test user</span></span>
<span data-ttu-id="37f72-210">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37f72-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="37f72-212">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="37f72-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37f72-213">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37f72-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37f72-215">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="37f72-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37f72-217">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="37f72-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37f72-219">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="37f72-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37f72-221">а.</span><span class="sxs-lookup"><span data-stu-id="37f72-221">a.</span></span> <span data-ttu-id="37f72-222">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37f72-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37f72-223">b.</span><span class="sxs-lookup"><span data-stu-id="37f72-223">b.</span></span> <span data-ttu-id="37f72-224">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37f72-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37f72-225">c.</span><span class="sxs-lookup"><span data-stu-id="37f72-225">c.</span></span> <span data-ttu-id="37f72-226">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="37f72-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37f72-227">d.</span><span class="sxs-lookup"><span data-stu-id="37f72-227">d.</span></span> <span data-ttu-id="37f72-228">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="37f72-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="37f72-229">Создание тестового пользователя etouches</span><span class="sxs-lookup"><span data-stu-id="37f72-229">Create an etouches test user</span></span>

<span data-ttu-id="37f72-230">В этом разделе описано, как создать пользователя Britta Simon в приложении etouches.</span><span class="sxs-lookup"><span data-stu-id="37f72-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="37f72-231">Обратитесь в [службу поддержки etouches](https://www.etouches.com/event-software/support/customer-support/), чтобы добавить пользователей на платформу etouches.</span><span class="sxs-lookup"><span data-stu-id="37f72-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) to add the users in the etouches platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="37f72-232">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="37f72-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="37f72-233">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к etouches.</span><span class="sxs-lookup"><span data-stu-id="37f72-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to etouches.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="37f72-235">**Чтобы назначить пользователя Britta Simon в etouches, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="37f72-235">**To assign Britta Simon to etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="37f72-236">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="37f72-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="37f72-238">В списке приложений выберите **etouches**.</span><span class="sxs-lookup"><span data-stu-id="37f72-238">In the applications list, select **etouches**.</span></span>

    ![Ссылка на etouches в списке приложений](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="37f72-240">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="37f72-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="37f72-242">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="37f72-242">Click **Add** button.</span></span> <span data-ttu-id="37f72-243">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="37f72-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="37f72-245">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="37f72-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="37f72-246">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="37f72-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37f72-247">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="37f72-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="37f72-248">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="37f72-248">Test single sign-on</span></span>


<span data-ttu-id="37f72-249">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="37f72-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="37f72-250">Щелкнув плитку etouches на панели доступа, вы автоматически войдете в приложение etouches.</span><span class="sxs-lookup"><span data-stu-id="37f72-250">When you click the etouches tile in the Access Panel, you should get automatically signed-on to your etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37f72-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="37f72-251">Additional resources</span></span>

* [<span data-ttu-id="37f72-252">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37f72-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37f72-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37f72-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

