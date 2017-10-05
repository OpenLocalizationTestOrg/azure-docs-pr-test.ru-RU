---
title: "Руководство по интеграции Azure Active Directory с Adobe Creative Cloud | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Adobe Creative Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="9803a-103">Руководство по интеграции Azure Active Directory с Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="9803a-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="9803a-104">В этом учебнике описано, как интегрировать приложение Adobe Creative Cloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9803a-104">In this tutorial, you learn how to integrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9803a-105">Интеграция Azure AD с приложением Adobe Creative Cloud обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9803a-105">Integrating Adobe Creative Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9803a-106">С помощью Azure AD вы можете контролировать доступ к Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="9803a-106">You can control in Azure AD who has access to Adobe Creative Cloud</span></span>
- <span data-ttu-id="9803a-107">Вы можете включить автоматический вход пользователей в Adobe Creative Cloud (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9803a-107">You can enable your users to automatically get signed-on to Adobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9803a-108">Вы можете управлять учетными записями централизованно — через портал управления Azure.</span><span class="sxs-lookup"><span data-stu-id="9803a-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="9803a-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9803a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9803a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9803a-110">Prerequisites</span></span>

<span data-ttu-id="9803a-111">Чтобы настроить интеграцию Azure AD с приложением Adobe Creative Cloud, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="9803a-111">To configure Azure AD integration with Adobe Creative Cloud, you need the following items:</span></span>

- <span data-ttu-id="9803a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9803a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9803a-113">подписка Adobe Creative Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="9803a-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9803a-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9803a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9803a-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9803a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9803a-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="9803a-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9803a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9803a-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9803a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9803a-118">Scenario description</span></span>
<span data-ttu-id="9803a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9803a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9803a-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9803a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9803a-121">Добавление Adobe Creative Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="9803a-121">Adding Adobe Creative Cloud from the gallery</span></span>
2. <span data-ttu-id="9803a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9803a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a><span data-ttu-id="9803a-123">Добавление Adobe Creative Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="9803a-123">Adding Adobe Creative Cloud from the gallery</span></span>
<span data-ttu-id="9803a-124">Чтобы настроить интеграцию Adobe Creative Cloud с Azure AD, необходимо добавить Adobe Creative Cloud из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9803a-124">To configure the integration of Adobe Creative Cloud into Azure AD, you need to add Adobe Creative Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9803a-125">**Чтобы добавить Adobe Creative Cloud из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9803a-125">**To add Adobe Creative Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9803a-126">На **[портале управления Azure](https://portal.azure.com)** в левой области навигации нажмите значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9803a-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9803a-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9803a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9803a-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9803a-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9803a-131">Нажмите кнопку **Добавить** в верхней части диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9803a-131">Click **Add** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9803a-133">В поле поиска введите **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="9803a-133">In the search box, type **Adobe Creative Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="9803a-135">На панели результатов выберите **Adobe Creative Cloud** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="9803a-135">In the results panel, select **Adobe Creative Cloud**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9803a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9803a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9803a-138">В этом разделе описана настройка и проверка единого входа Azure AD в Adobe Creative Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9803a-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9803a-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Adobe Creative Cloud соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9803a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Creative Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="9803a-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="9803a-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Creative Cloud needs to be established.</span></span>

<span data-ttu-id="9803a-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="9803a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="9803a-142">Чтобы настроить и проверить единый вход Azure AD в Adobe Creative Cloud, выполните действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="9803a-142">To configure and test Azure AD single sign-on with Adobe Creative Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9803a-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9803a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9803a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9803a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9803a-145">**[Создание тестового пользователя Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)** требуется для создания в Adobe Creative Cloud пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9803a-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - to have a counterpart of Britta Simon in Adobe Creative Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9803a-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9803a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9803a-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9803a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9803a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9803a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9803a-149">В данном разделе описано, как включить единый вход в Azure AD на портале управления Azure и настроить его в приложении Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="9803a-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="9803a-150">**Чтобы настроить единый вход Azure AD в Adobe Creative Cloud, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9803a-150">**To configure Azure AD single sign-on with Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="9803a-151">На портале управления Azure на странице интеграции с приложением **Adobe Creative Cloud** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9803a-151">In the Azure Management portal, on the **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9803a-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9803a-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="9803a-155">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Adobe Creative Cloud** выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="9803a-155">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="9803a-157">а.</span><span class="sxs-lookup"><span data-stu-id="9803a-157">a.</span></span> <span data-ttu-id="9803a-158">В текстовом поле **Идентификатор** введите значение `https://www.okta.com/saml2/service-provider/<token>`.</span><span class="sxs-lookup"><span data-stu-id="9803a-158">In the **Identifier** textbox, type the value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="9803a-159">b.</span><span class="sxs-lookup"><span data-stu-id="9803a-159">b.</span></span> <span data-ttu-id="9803a-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<company name>.okta.com/auth/saml20/accauthlinktest`.</span><span class="sxs-lookup"><span data-stu-id="9803a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9803a-161">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="9803a-161">Please note that these are not the real values.</span></span> <span data-ttu-id="9803a-162">Необходимо указать фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="9803a-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9803a-163">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9803a-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="9803a-164">Чтобы создать пользователя вручную, необходимо обратиться к группе поддержки Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="9803a-164">If you need to create an user manually, you need to contact the Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="9803a-165">Если вы хотите настроить приложение в **режиме, инициированном провайдером службы**, то в разделе **Домены и URL-адреса приложения Adobe Creative Cloud** выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="9803a-165">On the **Adobe Creative Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="9803a-167">а.</span><span class="sxs-lookup"><span data-stu-id="9803a-167">a.</span></span> <span data-ttu-id="9803a-168">Щелкните параметр **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="9803a-168">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="9803a-169">b.</span><span class="sxs-lookup"><span data-stu-id="9803a-169">b.</span></span> <span data-ttu-id="9803a-170">В текстовом поле **URL-адрес для входа** введите значение `https://adobe.com`.</span><span class="sxs-lookup"><span data-stu-id="9803a-170">In the **Sign-on URL** textbox, type the value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="9803a-171">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9803a-171">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="9803a-173">В разделе **Конфигурация Adobe Creative Cloud** щелкните **Настройка Adobe Creative Cloud**, чтобы открыть окно **настройки входа**.</span><span class="sxs-lookup"><span data-stu-id="9803a-173">On the **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9803a-174">Скопируйте **Идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** из раздела "Краткий справочник".</span><span class="sxs-lookup"><span data-stu-id="9803a-174">Please copy the **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="9803a-176">В другом окне веб-браузера войдите в свой клиент Adobe Creative Cloud с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="9803a-176">In a different web browser window, sign-on to your Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="9803a-177">Выберите пункты **Identity** (Идентификация) на панели навигации слева и щелкните свой домен.</span><span class="sxs-lookup"><span data-stu-id="9803a-177">Go to **Identity** on the left navigation pane and click your domain.</span></span> <span data-ttu-id="9803a-178">В разделе **Single Sign On Configuration Required** (Обязательная конфигурация единого входа) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9803a-178">Then perform the following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="9803a-179">![Параметры](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="9803a-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="9803a-180">Щелкните **Browse** (Просмотр), чтобы найти и передать сертификат, загруженный из Azure AD, в качестве **сертификата поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="9803a-180">Click **Browse** to upload the downloaded certificate from Azure AD to **IDP Certificate**.</span></span>

10. <span data-ttu-id="9803a-181">В текстовое поле **IDP issuer** (Издатель удостоверений) поместите значение **Идентификатор сущности SAML**, который вы скопировали из раздела **Настройка входа** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9803a-181">In the **IDP issuer** textbox, put the value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="9803a-182">В текстовое поле **IDP Login URL** (URL-адрес входа поставщика удостоверений) поместите значение **URL-адрес службы единого входа SAML**, который вы скопировали из раздела **Настройка входа** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9803a-182">In the **IDP Login URL** textbox, put the value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="9803a-183">Для параметра **HTTP — Redirect** (Перенаправление HTTP) выберите вариант **IDP Binding** (Привязка к поставщику удостоверений).</span><span class="sxs-lookup"><span data-stu-id="9803a-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="9803a-184">Для параметра **Email Address** (Адрес электронной почты) выберите вариант **User Login Setting** (Настройки входа пользователя).</span><span class="sxs-lookup"><span data-stu-id="9803a-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="9803a-185">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9803a-185">Click **Save** button.</span></span>

15. <span data-ttu-id="9803a-186">Теперь на панели мониторинга отобразится XML-файл **Download Metadata** (Загрузить метаданные).</span><span class="sxs-lookup"><span data-stu-id="9803a-186">The dashboard will now present the XML **"Download Metadata"** file.</span></span> <span data-ttu-id="9803a-187">Он содержит URL-адреса компании Adobe для описания сущности (EntityDescriptor) и URL-адреса службы утверждений (AssertionConsumerService).</span><span class="sxs-lookup"><span data-stu-id="9803a-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="9803a-188">Откройте этот файл и перенесите настройки в приложение Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9803a-188">Please open the file and configure them in the Azure AD application.</span></span>

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="9803a-191">а.</span><span class="sxs-lookup"><span data-stu-id="9803a-191">a.</span></span> <span data-ttu-id="9803a-192">Используйте значение EntityDescriptor, предоставленное компанией Adobe, в качестве значения для параметра **Identifier** (Идентификатор) в диалоговом окне **Configure App Settings** (Настройка параметров приложения).</span><span class="sxs-lookup"><span data-stu-id="9803a-192">Use the EntityDescriptor value Adobe provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="9803a-193">b.</span><span class="sxs-lookup"><span data-stu-id="9803a-193">b.</span></span> <span data-ttu-id="9803a-194">Используйте значение AssertionConsumerService, предоставленное компанией Adobe, в качестве значения для параметра **Reply URL** (URL-адрес ответа) в диалоговом окне **Configure App Settings** (Настройка параметров приложения).</span><span class="sxs-lookup"><span data-stu-id="9803a-194">Use the AssertionConsumerService value Adobe provided you for **Reply URL** on the **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9803a-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9803a-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="9803a-196">Цель этого раздела — создать на портале управления Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9803a-196">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9803a-198">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9803a-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9803a-199">На **портале управления Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9803a-199">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9803a-201">Перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**, чтобы отобразить список пользователей.</span><span class="sxs-lookup"><span data-stu-id="9803a-201">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9803a-203">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="9803a-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9803a-205">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9803a-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9803a-207">а.</span><span class="sxs-lookup"><span data-stu-id="9803a-207">a.</span></span> <span data-ttu-id="9803a-208">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9803a-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9803a-209">b.</span><span class="sxs-lookup"><span data-stu-id="9803a-209">b.</span></span> <span data-ttu-id="9803a-210">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9803a-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9803a-211">c.</span><span class="sxs-lookup"><span data-stu-id="9803a-211">c.</span></span> <span data-ttu-id="9803a-212">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9803a-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9803a-213">d.</span><span class="sxs-lookup"><span data-stu-id="9803a-213">d.</span></span> <span data-ttu-id="9803a-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9803a-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="9803a-215">Создание тестового пользователя Adobe Creative Cloud</span><span class="sxs-lookup"><span data-stu-id="9803a-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="9803a-216">Чтобы пользователи Azure AD могли входить в Adobe Creative Cloud, они должны быть подготовлены для Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="9803a-216">In order to enable Azure AD users to log into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="9803a-217">В случае Adobe Creative Cloud подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9803a-217">In the case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="9803a-218">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9803a-218">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="9803a-219">Выполните вход на корпоративный сайт Adobe Creative Cloud с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="9803a-219">Log in to your Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="9803a-220">Выберите параметр **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="9803a-220">Click **People**.</span></span>

    <span data-ttu-id="9803a-221">![Люди](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="9803a-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="9803a-222">Нажмите кнопку **Пригласить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="9803a-222">Click **Invite User**.</span></span>

    <span data-ttu-id="9803a-223">![Приглашение пользователей](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "приглашение пользователей")</span><span class="sxs-lookup"><span data-stu-id="9803a-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="9803a-224">На странице диалогового окна **Приглашение пользователей** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9803a-224">On the **Invite People** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="9803a-225">![Приглашение участников](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="9803a-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="9803a-226">а.</span><span class="sxs-lookup"><span data-stu-id="9803a-226">a.</span></span> <span data-ttu-id="9803a-227">В текстовом поле **Электронная почта** введите адрес электронной почты учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9803a-227">In the **Email** textbox, type the email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="9803a-228">b.</span><span class="sxs-lookup"><span data-stu-id="9803a-228">b.</span></span> <span data-ttu-id="9803a-229">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="9803a-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9803a-230">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9803a-230">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9803a-231">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9803a-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9803a-232">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="9803a-232">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Adobe Creative Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9803a-234">**Чтобы назначить пользователя Britta Simon в Adobe Creative Cloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="9803a-234">**To assign Britta Simon to Adobe Creative Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="9803a-235">На портале управления Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9803a-235">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9803a-237">В списке приложений выберите **Adobe Creative Cloud**.</span><span class="sxs-lookup"><span data-stu-id="9803a-237">In the applications list, select **Adobe Creative Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="9803a-239">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9803a-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9803a-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9803a-241">Click **Add** button.</span></span> <span data-ttu-id="9803a-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9803a-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9803a-244">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9803a-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9803a-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9803a-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9803a-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9803a-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9803a-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9803a-247">Testing single sign-on</span></span>

<span data-ttu-id="9803a-248">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9803a-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9803a-249">Щелкнув элемент Adobe Creative Cloud на панели доступа, вы автоматически войдете в приложение Adobe Creative Cloud.</span><span class="sxs-lookup"><span data-stu-id="9803a-249">When you click the Adobe Creative Cloud tile in the Access Panel, you should get automatically signed-on to your Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9803a-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9803a-250">Additional resources</span></span>

* [<span data-ttu-id="9803a-251">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9803a-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9803a-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9803a-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png