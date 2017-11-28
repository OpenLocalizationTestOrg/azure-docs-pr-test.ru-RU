---
title: "Учебник. Интеграция Azure Active Directory с Lifesize Cloud | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Lifesize Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="4c892-103">Учебник. Интеграция Azure Active Directory с Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="4c892-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="4c892-104">В этом учебнике описано, как интегрировать приложение Lifesize Cloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c892-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c892-105">Интеграция Azure AD с приложением Lifesize Cloud обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4c892-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c892-106">С помощью Azure AD вы можете контролировать доступ к Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c892-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="4c892-107">Вы можете включить автоматический вход пользователей в Lifesize Cloud (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c892-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c892-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4c892-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4c892-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c892-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c892-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4c892-110">Prerequisites</span></span>

<span data-ttu-id="4c892-111">Чтобы настроить интеграцию Azure AD с приложением Lifesize Cloud, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="4c892-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="4c892-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4c892-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c892-113">подписка Lifesize Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4c892-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c892-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="4c892-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c892-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="4c892-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c892-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4c892-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c892-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c892-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c892-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4c892-118">Scenario description</span></span>
<span data-ttu-id="4c892-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4c892-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c892-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="4c892-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c892-121">Добавление Lifesize Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="4c892-121">Adding Lifesize Cloud from the gallery</span></span>
2. <span data-ttu-id="4c892-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c892-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="4c892-123">Добавление Lifesize Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="4c892-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="4c892-124">Чтобы настроить интеграцию Lifesize Cloud с Azure AD, необходимо добавить Lifesize Cloud из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4c892-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c892-125">**Чтобы добавить Lifesize Cloud из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4c892-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c892-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c892-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c892-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4c892-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c892-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4c892-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4c892-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="4c892-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4c892-133">В поле поиска введите **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c892-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="4c892-135">На панели результатов выберите **Lifesize Cloud** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="4c892-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c892-137">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c892-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c892-138">В этом разделе описана настройка и проверка единого входа Azure AD в Lifesize Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c892-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c892-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Lifesize Cloud соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c892-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="4c892-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c892-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="4c892-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c892-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4c892-142">Чтобы настроить и проверить единый вход Azure AD в Lifesize Cloud, выполните действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="4c892-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c892-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="4c892-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c892-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c892-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c892-145">**[Создание тестового пользователя Lifesize Cloud](#creating-a-lifesize-cloud-test-user)** требуется для создания в Lifesize Cloud пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c892-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c892-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c892-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c892-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4c892-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c892-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c892-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c892-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c892-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="4c892-150">**Чтобы настроить единый вход Azure AD в Lifesize Cloud, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4c892-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4c892-151">На портале Azure на странице интеграции с приложением **Lifesize Cloud** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="4c892-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4c892-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="4c892-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="4c892-155">В разделе **Домены и URL-адреса приложения Lifesize Cloud** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4c892-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="4c892-157">а.</span><span class="sxs-lookup"><span data-stu-id="4c892-157">a.</span></span> <span data-ttu-id="4c892-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="4c892-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="4c892-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c892-159">b.</span></span> <span data-ttu-id="4c892-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4c892-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="4c892-161">Установите флажок **Показывать дополнительные параметры URL-адреса** и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4c892-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="4c892-163">В текстовое поле **Состояние ретранслятора** введите URL-адрес в следующем формате: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="4c892-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="4c892-164">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="4c892-164">Please note that these are not the real values.</span></span> <span data-ttu-id="4c892-165">Необходимо заменить эти значения фактическим URL-адресом для входа и идентификатором, значением состояния ретранслятора и идентификатора.</span><span class="sxs-lookup"><span data-stu-id="4c892-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="4c892-166">Обратитесь в [службу поддержки клиентов Lifesize Cloud](https://www.lifesize.com/support) для получения URL-адреса входа и значений идентификаторов, а также значения состояния ретрансляции из конфигурации единого входа, которое описывается далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="4c892-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

4. <span data-ttu-id="4c892-167">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="4c892-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="4c892-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4c892-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c892-171">В разделе **Конфигурация Lifesize Cloud** щелкните **Настроить Lifesize Cloud**, чтобы открыть окно **Настройка входа**.</span><span class="sxs-lookup"><span data-stu-id="4c892-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4c892-172">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="4c892-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="4c892-174">Для настройки единого входа в вашем приложении необходимо войти в приложение Lifesize Cloud с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="4c892-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="4c892-175">В правом верхнем углу страницы щелкните свое имя и выберите **Advance Settings** (Дополнительные параметры).</span><span class="sxs-lookup"><span data-stu-id="4c892-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="4c892-177">В меню Advance Settings (Дополнительные параметры) щелкните ссылку **SSO Configuration** (Конфигурация единого входа).</span><span class="sxs-lookup"><span data-stu-id="4c892-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="4c892-178">Откроется страница "SSO Configuration" (Конфигурация единого входа) для вашего экземпляра.</span><span class="sxs-lookup"><span data-stu-id="4c892-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="4c892-180">Теперь настройте следующие значения в пользовательском интерфейсе единого входа.</span><span class="sxs-lookup"><span data-stu-id="4c892-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="4c892-182">а.</span><span class="sxs-lookup"><span data-stu-id="4c892-182">a.</span></span> <span data-ttu-id="4c892-183">В текстовое поле **Издатель поставщика удостоверений** вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4c892-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4c892-184">b.</span><span class="sxs-lookup"><span data-stu-id="4c892-184">b.</span></span>  <span data-ttu-id="4c892-185">В текстовое поле **URL-адрес входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4c892-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4c892-186">c.</span><span class="sxs-lookup"><span data-stu-id="4c892-186">c.</span></span> <span data-ttu-id="4c892-187">Откройте в блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Сертификат X.509**.</span><span class="sxs-lookup"><span data-stu-id="4c892-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="4c892-188">г)</span><span class="sxs-lookup"><span data-stu-id="4c892-188">d.</span></span> <span data-ttu-id="4c892-189">В разделе "SAML Attribute Mappings" (Сопоставления атрибутов SAML) в текстовом поле "First Name" (Имя) введите значение **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="4c892-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="4c892-190">д.</span><span class="sxs-lookup"><span data-stu-id="4c892-190">e.</span></span> <span data-ttu-id="4c892-191">В разделе "SAML Attribute Mappings" (Сопоставления атрибутов SAML) в текстовом поле **Last Name** (Фамилия) введите значение **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="4c892-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="4c892-192">Е.</span><span class="sxs-lookup"><span data-stu-id="4c892-192">f.</span></span> <span data-ttu-id="4c892-193">В разделе "SAML Attribute Mappings" (Сопоставления атрибутов SAML) в текстовом поле **Email** (Электронный адрес) введите значение **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="4c892-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="4c892-194">Чтобы проверить конфигурацию, можно нажать кнопку **Test** (Проверить).</span><span class="sxs-lookup"><span data-stu-id="4c892-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="4c892-195">Чтобы проверка прошла успешно, необходимо завершить работу мастера настройки в Azure AD, а также предоставить доступ пользователям или группам, которые будут выполнять эту проверку.</span><span class="sxs-lookup"><span data-stu-id="4c892-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

12. <span data-ttu-id="4c892-196">Чтобы включить единый вход, установите флажок **Enable SSO** (Включить единый вход).</span><span class="sxs-lookup"><span data-stu-id="4c892-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

13. <span data-ttu-id="4c892-197">Затем нажмите кнопку **Update** (Обновить), чтобы сохранить все параметры.</span><span class="sxs-lookup"><span data-stu-id="4c892-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="4c892-198">При этом будет создано значение RelayState.</span><span class="sxs-lookup"><span data-stu-id="4c892-198">This will generate the RelayState value.</span></span> <span data-ttu-id="4c892-199">Скопируйте значение RelayState, созданное в текстовом поле, и вставьте его в поле **Состояние ретранслятора** в разделе **URL-адреса и домены Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c892-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="4c892-200">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="4c892-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4c892-201">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="4c892-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4c892-202">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="4c892-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c892-203">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c892-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="4c892-204">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c892-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4c892-206">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4c892-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c892-207">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c892-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c892-209">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="4c892-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c892-211">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4c892-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c892-213">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4c892-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c892-215">а.</span><span class="sxs-lookup"><span data-stu-id="4c892-215">a.</span></span> <span data-ttu-id="4c892-216">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c892-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c892-217">b.</span><span class="sxs-lookup"><span data-stu-id="4c892-217">b.</span></span> <span data-ttu-id="4c892-218">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c892-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c892-219">c.</span><span class="sxs-lookup"><span data-stu-id="4c892-219">c.</span></span> <span data-ttu-id="4c892-220">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="4c892-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4c892-221">d.</span><span class="sxs-lookup"><span data-stu-id="4c892-221">d.</span></span> <span data-ttu-id="4c892-222">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4c892-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="4c892-223">Создание тестового пользователя Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="4c892-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="4c892-224">В этом разделе описано, как создать пользователя Britta Simon в приложении Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c892-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="4c892-225">Lifesize Cloud поддерживает автоматическую подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="4c892-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="4c892-226">После успешной аутентификации в Azure AD для пользователя будет автоматически выполняться подготовка в приложении.</span><span class="sxs-lookup"><span data-stu-id="4c892-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4c892-227">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c892-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4c892-228">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c892-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4c892-230">**Чтобы назначить пользователя Britta Simon в FileCloud, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="4c892-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4c892-231">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4c892-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4c892-233">В списке приложений выберите **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4c892-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="4c892-235">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4c892-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4c892-237">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4c892-237">Click **Add** button.</span></span> <span data-ttu-id="4c892-238">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4c892-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4c892-240">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4c892-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c892-241">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4c892-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c892-242">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4c892-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c892-243">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4c892-243">Testing single sign-on</span></span>

<span data-ttu-id="4c892-244">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="4c892-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4c892-245">После щелчка элемента Lifesize Cloud на панели доступа откроется страница входа в приложение Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="4c892-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="4c892-246">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c892-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c892-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4c892-247">Additional resources</span></span>

* [<span data-ttu-id="4c892-248">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c892-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c892-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c892-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

