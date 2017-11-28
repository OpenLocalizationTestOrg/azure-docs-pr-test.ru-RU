---
title: "Учебник. Интеграция Azure Active Directory с FileCloud | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ad03516f684acc59912ffc57f6e0712828bd03f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="8e35c-103">Учебник. Интеграция Azure Active Directory с FileCloud</span><span class="sxs-lookup"><span data-stu-id="8e35c-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="8e35c-104">В этом руководстве описано, как интегрировать FileCloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e35c-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e35c-105">Интеграция FileCloud с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="8e35c-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e35c-106">С помощью Azure AD вы можете контролировать доступ к FileCloud.</span><span class="sxs-lookup"><span data-stu-id="8e35c-106">You can control in Azure AD who has access to FileCloud.</span></span>
- <span data-ttu-id="8e35c-107">Вы можете включить автоматический вход пользователей в FileCloud (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e35c-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8e35c-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8e35c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8e35c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e35c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e35c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8e35c-110">Prerequisites</span></span>

<span data-ttu-id="8e35c-111">Чтобы настроить интеграцию Azure AD с FileCloud, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8e35c-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

- <span data-ttu-id="8e35c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8e35c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e35c-113">подписка FileCloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8e35c-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e35c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8e35c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e35c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8e35c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e35c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8e35c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e35c-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e35c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e35c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8e35c-118">Scenario description</span></span>
<span data-ttu-id="8e35c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8e35c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e35c-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8e35c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e35c-121">Добавление FileCloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="8e35c-121">Adding FileCloud from the gallery</span></span>
2. <span data-ttu-id="8e35c-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e35c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-the-gallery"></a><span data-ttu-id="8e35c-123">Добавление FileCloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="8e35c-123">Adding FileCloud from the gallery</span></span>
<span data-ttu-id="8e35c-124">Чтобы настроить интеграцию FileCloud с Azure AD, необходимо добавить FileCloud из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8e35c-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e35c-125">**Чтобы добавить FileCloud из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8e35c-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e35c-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="8e35c-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e35c-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="8e35c-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="8e35c-133">В поле поиска введите **FileCloud**, выберите **FileCloud** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8e35c-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span></span>

    ![FileCloud в списке результатов](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8e35c-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e35c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8e35c-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение FileCloud с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e35c-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e35c-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в FileCloud соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e35c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span></span> <span data-ttu-id="8e35c-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в FileCloud.</span><span class="sxs-lookup"><span data-stu-id="8e35c-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="8e35c-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в FileCloud.</span><span class="sxs-lookup"><span data-stu-id="8e35c-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8e35c-140">Чтобы настроить и проверить единый вход Azure AD в FileCloud, выполните следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="8e35c-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e35c-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8e35c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8e35c-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e35c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e35c-143">**[Создание тестового пользователя FileCloud](#create-a-filecloud-test-user)** нужно для того, чтобы в FileCloud также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e35c-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e35c-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e35c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e35c-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8e35c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8e35c-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e35c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8e35c-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении FileCloud.</span><span class="sxs-lookup"><span data-stu-id="8e35c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="8e35c-148">**Чтобы настроить единый вход Azure AD в FileCloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8e35c-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="8e35c-149">На портале Azure на странице интеграции с приложением **FileCloud** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="8e35c-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8e35c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="8e35c-153">В разделе **Домены и URL-адреса приложения FileCloud** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="8e35c-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="8e35c-155">а.</span><span class="sxs-lookup"><span data-stu-id="8e35c-155">a.</span></span> <span data-ttu-id="8e35c-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="8e35c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="8e35c-157">b.</span><span class="sxs-lookup"><span data-stu-id="8e35c-157">b.</span></span> <span data-ttu-id="8e35c-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="8e35c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e35c-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="8e35c-159">These values are not real.</span></span> <span data-ttu-id="8e35c-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="8e35c-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8e35c-161">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="8e35c-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span></span>

4. <span data-ttu-id="8e35c-162">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8e35c-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="8e35c-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8e35c-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e35c-166">В разделе **Настройка FileCloud** щелкните **Настроить FileCloud**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8e35c-167">Скопируйте значение **SAML Entity ID** (Идентификатор сущности SAML) из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Настройка FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="8e35c-169">В другом окне веб-браузера войдите в свой клиент FileCloud с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8e35c-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="8e35c-170">В левой панели навигации щелкните **Settings**(Параметры).</span><span class="sxs-lookup"><span data-stu-id="8e35c-170">On the left navigation pane, click **Settings**.</span></span> 
   
    ![Раздел "Settings" (Параметры) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="8e35c-172">Щелкните вкладку **SSO** (Единый вход) в разделе "Settings" (Параметры).</span><span class="sxs-lookup"><span data-stu-id="8e35c-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Вкладка "Single Sign-On" (Единый вход) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="8e35c-174">На панели **Single Sign On (SSO) Settings** (Параметры единого входа) для параметра **Default SSO Type** (Тип единого входа по умолчанию) выберите значение **SAML**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Панель "Single Sign-On Settings" (Параметры единого входа) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="8e35c-176">Вставьте значение **Идентификатор сущности SAML**, скопированное на портале Azure, в поле **IdP End Point URL** (URL-адрес конечной точки IdP).</span><span class="sxs-lookup"><span data-stu-id="8e35c-176">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP End Point URL** textbox.</span></span>

    ![Текстовое поле "IDP End Point URL" (URL-адрес конечной точки IDP)](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="8e35c-178">Откройте скачанный файл метаданных в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте в текстовое поле **IdP Meta Data** (Метаданные IdP) на панели **SAML Settings** (Параметры SAML).</span><span class="sxs-lookup"><span data-stu-id="8e35c-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Раздел "IDP Meta Data" (Метаданные IDP) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="8e35c-180">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8e35c-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="8e35c-181">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8e35c-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e35c-182">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8e35c-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e35c-183">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8e35c-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8e35c-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e35c-184">Create an Azure AD test user</span></span>

<span data-ttu-id="8e35c-185">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e35c-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="8e35c-187">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8e35c-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e35c-188">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8e35c-190">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8e35c-192">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8e35c-194">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="8e35c-194">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8e35c-196">а.</span><span class="sxs-lookup"><span data-stu-id="8e35c-196">a.</span></span> <span data-ttu-id="8e35c-197">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e35c-198">b.</span><span class="sxs-lookup"><span data-stu-id="8e35c-198">b.</span></span> <span data-ttu-id="8e35c-199">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e35c-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8e35c-200">c.</span><span class="sxs-lookup"><span data-stu-id="8e35c-200">c.</span></span> <span data-ttu-id="8e35c-201">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8e35c-202">г)</span><span class="sxs-lookup"><span data-stu-id="8e35c-202">d.</span></span> <span data-ttu-id="8e35c-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="8e35c-204">Создание тестового пользователя FileCloud</span><span class="sxs-lookup"><span data-stu-id="8e35c-204">Create a FileCloud test user</span></span>

<span data-ttu-id="8e35c-205">Цель этого раздела — создать пользователя с именем Britta Simon в FileCloud.</span><span class="sxs-lookup"><span data-stu-id="8e35c-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="8e35c-206">FileCloud поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e35c-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="8e35c-207">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="8e35c-207">There is no action item for you in this section.</span></span> <span data-ttu-id="8e35c-208">Пользователь создается при попытке получить доступ к приложению FileCloud (если он еще не существует).</span><span class="sxs-lookup"><span data-stu-id="8e35c-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="8e35c-209">Если вам нужно вручную создать пользователя, обратитесь в [службу поддержки клиентов FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="8e35c-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8e35c-210">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e35c-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="8e35c-211">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к FileCloud.</span><span class="sxs-lookup"><span data-stu-id="8e35c-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="8e35c-213">**Чтобы назначить пользователя Britta Simon в FileCloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8e35c-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="8e35c-214">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8e35c-216">Из списка приложений выберите **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-216">In the applications list, select **FileCloud**.</span></span>

    ![Ссылка на FileCloud в списке "Приложения"](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="8e35c-218">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="8e35c-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-220">Click **Add** button.</span></span> <span data-ttu-id="8e35c-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="8e35c-223">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e35c-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e35c-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8e35c-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8e35c-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8e35c-226">Test single sign-on</span></span>

<span data-ttu-id="8e35c-227">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8e35c-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8e35c-228">Щелкнув элемент "FileCloud" на панели доступа, вы автоматически войдете в приложение FileCloud.</span><span class="sxs-lookup"><span data-stu-id="8e35c-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e35c-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8e35c-229">Additional resources</span></span>

* [<span data-ttu-id="8e35c-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e35c-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e35c-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e35c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

