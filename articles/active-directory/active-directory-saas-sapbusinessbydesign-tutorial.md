---
title: "Руководство по интеграции Azure Active Directory с SAP Business ByDesign | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="acdbf-103">Руководство по интеграции Azure Active Directory с SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="acdbf-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="acdbf-104">В этом руководстве описано, как интегрировать SAP Business ByDesign с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="acdbf-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acdbf-105">Интеграция SAP Business ByDesign с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="acdbf-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="acdbf-106">С помощью Azure AD вы можете контролировать доступ к приложению SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="acdbf-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="acdbf-107">Вы можете включить автоматический вход пользователей в SAP Business ByDesign (единый вход) с использованием их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acdbf-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="acdbf-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="acdbf-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="acdbf-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="acdbf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acdbf-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="acdbf-110">Prerequisites</span></span>

<span data-ttu-id="acdbf-111">Чтобы настроить интеграцию Azure AD с SAP Business ByDesign, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="acdbf-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="acdbf-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="acdbf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="acdbf-113">подписка SAP Business ByDesign с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="acdbf-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="acdbf-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="acdbf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="acdbf-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="acdbf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acdbf-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="acdbf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="acdbf-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acdbf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="acdbf-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="acdbf-118">Scenario description</span></span>
<span data-ttu-id="acdbf-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="acdbf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acdbf-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="acdbf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acdbf-121">Добавление SAP Business ByDesign из коллекции</span><span class="sxs-lookup"><span data-stu-id="acdbf-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="acdbf-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="acdbf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="acdbf-123">Добавление SAP Business ByDesign из коллекции</span><span class="sxs-lookup"><span data-stu-id="acdbf-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="acdbf-124">Чтобы настроить интеграцию SAP Business ByDesign с Azure AD, необходимо добавить SAP Business ByDesign из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="acdbf-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="acdbf-125">**Чтобы добавить SAP Business ByDesign из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="acdbf-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="acdbf-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="acdbf-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="acdbf-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="acdbf-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="acdbf-133">В поле поиска введите **SAP Business ByDesign**, выберите **SAP Business ByDesign** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="acdbf-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign в списке результатов](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="acdbf-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="acdbf-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="acdbf-136">В этом разделе описана настройка и проверка единого входа Azure AD в SAP Business ByDesign с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acdbf-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="acdbf-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в SAP Business ByDesign соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acdbf-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="acdbf-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="acdbf-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="acdbf-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="acdbf-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="acdbf-140">Чтобы настроить и проверить единый вход Azure AD в SAP Business ByDesign, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="acdbf-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="acdbf-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="acdbf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="acdbf-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acdbf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="acdbf-143">**[Создание тестового пользователя SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)** требуется для того, чтобы в SAP Business ByDesign существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acdbf-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="acdbf-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acdbf-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="acdbf-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="acdbf-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="acdbf-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="acdbf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="acdbf-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="acdbf-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="acdbf-148">**Чтобы настроить единый вход Azure AD в SAP Business ByDesign, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="acdbf-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="acdbf-149">На портале Azure на странице интеграции с приложением **SAP Business ByDesign** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="acdbf-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="acdbf-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="acdbf-153">В разделе **Домены и URL-адреса приложения SAP Business ByDesign** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="acdbf-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="acdbf-155">а.</span><span class="sxs-lookup"><span data-stu-id="acdbf-155">a.</span></span> <span data-ttu-id="acdbf-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="acdbf-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="acdbf-157">b.</span><span class="sxs-lookup"><span data-stu-id="acdbf-157">b.</span></span> <span data-ttu-id="acdbf-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="acdbf-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="acdbf-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="acdbf-159">These values are not real.</span></span> <span data-ttu-id="acdbf-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="acdbf-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="acdbf-161">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="acdbf-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="acdbf-162">В разделе **Атрибуты пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="acdbf-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![Раздел атрибутов SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="acdbf-164">а.</span><span class="sxs-lookup"><span data-stu-id="acdbf-164">a.</span></span> <span data-ttu-id="acdbf-165">Из списка **Идентификатор пользователя** выберите функцию **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="acdbf-166">b.</span><span class="sxs-lookup"><span data-stu-id="acdbf-166">b.</span></span> <span data-ttu-id="acdbf-167">В списке **Почта** выберите атрибут пользователя, который вы хотите использовать в своей реализации.</span><span class="sxs-lookup"><span data-stu-id="acdbf-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="acdbf-168">Например, если в качестве уникального идентификатора пользователя вы хотите использовать EmployeeID и сохранили значение атрибута в ExtensionAttribute2, выберите user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="acdbf-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="acdbf-169">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="acdbf-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="acdbf-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="acdbf-171">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="acdbf-173">В разделе **Настройка SAP Business ByDesign** щелкните **Настроить SAP Business ByDesign**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="acdbf-174">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="acdbf-176">Чтобы настроить единый вход для приложения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="acdbf-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="acdbf-177">а.</span><span class="sxs-lookup"><span data-stu-id="acdbf-177">a.</span></span> <span data-ttu-id="acdbf-178">Войдите на портал SAP Business ByDesign с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="acdbf-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="acdbf-179">b.</span><span class="sxs-lookup"><span data-stu-id="acdbf-179">b.</span></span> <span data-ttu-id="acdbf-180">Перейдите к элементу **Application and User Management Common Task** (Общие задачи управления приложением и пользователем) и откройте вкладку **Identity Provider** (Поставщик удостоверений).</span><span class="sxs-lookup"><span data-stu-id="acdbf-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="acdbf-181">c.</span><span class="sxs-lookup"><span data-stu-id="acdbf-181">c.</span></span> <span data-ttu-id="acdbf-182">Щелкните **New Identity Provider** (Новый поставщик удостоверений) и выберите XML-файл метаданных, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="acdbf-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="acdbf-183">Импортируя метаданные, система автоматически отправляет требуемые сертификаты подписи и шифрования.</span><span class="sxs-lookup"><span data-stu-id="acdbf-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="acdbf-185">d.</span><span class="sxs-lookup"><span data-stu-id="acdbf-185">d.</span></span> <span data-ttu-id="acdbf-186">Чтобы включить **URL-адрес службы обработчика утверждений** в запрос SAML, выберите **Include Assertion Consumer Service URL** (Включить URL-адрес службы обработчика утверждений).</span><span class="sxs-lookup"><span data-stu-id="acdbf-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="acdbf-187">д.</span><span class="sxs-lookup"><span data-stu-id="acdbf-187">e.</span></span> <span data-ttu-id="acdbf-188">Щелкните **Activate Single Sign-On**(Активировать единый вход).</span><span class="sxs-lookup"><span data-stu-id="acdbf-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="acdbf-189">Е.</span><span class="sxs-lookup"><span data-stu-id="acdbf-189">f.</span></span> <span data-ttu-id="acdbf-190">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="acdbf-190">Save your changes.</span></span>
   
    <span data-ttu-id="acdbf-191">g.</span><span class="sxs-lookup"><span data-stu-id="acdbf-191">g.</span></span> <span data-ttu-id="acdbf-192">Перейдите на вкладку **My System** (Моя система).</span><span class="sxs-lookup"><span data-stu-id="acdbf-192">Click the **My System** tab.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="acdbf-194">h.</span><span class="sxs-lookup"><span data-stu-id="acdbf-194">h.</span></span> <span data-ttu-id="acdbf-195">В текстовое поле **Azure AD Sign On URL** (URL-адрес входа в Azure AD) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="acdbf-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="acdbf-197">i.</span><span class="sxs-lookup"><span data-stu-id="acdbf-197">i.</span></span> <span data-ttu-id="acdbf-198">Укажите, сможет ли сотрудник вручную переключаться между входом с помощью учетных данных (идентификатора пользователя и пароля) и единым входом, выбрав **Manual Identity Provider Selection**(Выбор поставщика удостоверений вручную).</span><span class="sxs-lookup"><span data-stu-id="acdbf-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="acdbf-199">j.</span><span class="sxs-lookup"><span data-stu-id="acdbf-199">j.</span></span> <span data-ttu-id="acdbf-200">В разделе **SSO URL** (URL-адрес единого входа) укажите URL-адрес, который будет использоваться вашими сотрудниками для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="acdbf-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="acdbf-201">В раскрывающемся списке URL Sent to Employee (URL-адрес для отправки сотруднику) можно выбрать следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="acdbf-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="acdbf-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="acdbf-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="acdbf-203">Система отправит сотруднику обычный URL-адрес системы.</span><span class="sxs-lookup"><span data-stu-id="acdbf-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="acdbf-204">Сотрудник не сможет входить в систему с помощью единого входа. Вместо этого ему необходимо использовать пароль или сертификат.</span><span class="sxs-lookup"><span data-stu-id="acdbf-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="acdbf-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="acdbf-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="acdbf-206">Система отправит сотруднику URL-адрес единого входа.</span><span class="sxs-lookup"><span data-stu-id="acdbf-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="acdbf-207">Сотрудник сможет входить в систему с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="acdbf-207">The employee can log on using SSO.</span></span> <span data-ttu-id="acdbf-208">Запрос на проверку подлинности перенаправляется через поставщик удостоверений.</span><span class="sxs-lookup"><span data-stu-id="acdbf-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="acdbf-209">**Automatic Selection**</span><span class="sxs-lookup"><span data-stu-id="acdbf-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="acdbf-210">Если функция единого входа неактивна, система отправит сотруднику обычный URL-адрес системы.</span><span class="sxs-lookup"><span data-stu-id="acdbf-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="acdbf-211">Если функция единого входа активна, система проверит, есть ли у сотрудника пароль.</span><span class="sxs-lookup"><span data-stu-id="acdbf-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="acdbf-212">При наличии пароля сотруднику будет отправлен URL-адрес единого входа и URL-адрес другого метода входа.</span><span class="sxs-lookup"><span data-stu-id="acdbf-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="acdbf-213">Если пароля нет, сотруднику будет отправлен только URL-адрес единого входа.</span><span class="sxs-lookup"><span data-stu-id="acdbf-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="acdbf-214">k.</span><span class="sxs-lookup"><span data-stu-id="acdbf-214">k.</span></span> <span data-ttu-id="acdbf-215">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="acdbf-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="acdbf-216">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="acdbf-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="acdbf-217">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="acdbf-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="acdbf-218">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="acdbf-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="acdbf-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="acdbf-219">Create an Azure AD test user</span></span>

<span data-ttu-id="acdbf-220">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acdbf-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="acdbf-222">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="acdbf-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="acdbf-223">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="acdbf-225">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="acdbf-227">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="acdbf-229">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="acdbf-229">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="acdbf-231">а.</span><span class="sxs-lookup"><span data-stu-id="acdbf-231">a.</span></span> <span data-ttu-id="acdbf-232">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acdbf-233">b.</span><span class="sxs-lookup"><span data-stu-id="acdbf-233">b.</span></span> <span data-ttu-id="acdbf-234">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acdbf-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="acdbf-235">c.</span><span class="sxs-lookup"><span data-stu-id="acdbf-235">c.</span></span> <span data-ttu-id="acdbf-236">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="acdbf-237">г)</span><span class="sxs-lookup"><span data-stu-id="acdbf-237">d.</span></span> <span data-ttu-id="acdbf-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="acdbf-239">Создание тестового пользователя SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="acdbf-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="acdbf-240">В этом разделе мы создадим пользователя Britta Simon в приложении SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="acdbf-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="acdbf-241">Чтобы добавить пользователей в SAP Business ByDesign обратитесь в [службу поддержки клиентов SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="acdbf-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="acdbf-242">Значение идентификатора имени должно совпадать с полем имени пользователя на платформе SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="acdbf-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="acdbf-243">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="acdbf-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="acdbf-244">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к приложению SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="acdbf-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="acdbf-246">**Чтобы назначить пользователя Britta Simon приложению SAP Business ByDesign, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="acdbf-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="acdbf-247">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="acdbf-249">В списке приложений выберите **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![Ссылка на SAP Business ByDesign в списке приложений](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="acdbf-251">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="acdbf-253">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-253">Click **Add** button.</span></span> <span data-ttu-id="acdbf-254">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="acdbf-256">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="acdbf-257">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="acdbf-258">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="acdbf-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="acdbf-259">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="acdbf-259">Test single sign-on</span></span>

<span data-ttu-id="acdbf-260">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="acdbf-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="acdbf-261">Щелкнув плитку SAP Business ByDesign на панели доступа, вы автоматически войдете в приложение SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="acdbf-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="acdbf-262">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="acdbf-262">Additional resources</span></span>

* [<span data-ttu-id="acdbf-263">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acdbf-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="acdbf-264">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="acdbf-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

