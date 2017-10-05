---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и Workplace by Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1590a66f215f0c093d24ff602c0ad951ba1e1eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="c92a9-103">Руководство по интеграции Azure Active Directory с Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="c92a9-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="c92a9-104">В этом руководстве описано, как интегрировать Workplace by Facebook с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c92a9-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c92a9-105">Интеграция Workplace by Facebook с Azure AD дает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="c92a9-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c92a9-106">С помощью Azure AD вы можете контролировать доступ к Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="c92a9-106">You can control in Azure AD who has access to Workplace by Facebook</span></span>
- <span data-ttu-id="c92a9-107">Вы можете включить автоматический вход пользователей в Workplace by Facebook (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c92a9-107">You can enable your users to automatically get signed-on to Workplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c92a9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c92a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c92a9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c92a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c92a9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c92a9-110">Prerequisites</span></span>

<span data-ttu-id="c92a9-111">Чтобы настроить интеграцию Azure AD с Workplace by Facebook, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c92a9-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="c92a9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c92a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c92a9-113">подписка Workplace by Facebook с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c92a9-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c92a9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c92a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c92a9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c92a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c92a9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c92a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c92a9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c92a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c92a9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c92a9-118">Scenario description</span></span>
<span data-ttu-id="c92a9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c92a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c92a9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c92a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c92a9-121">Добавление Workplace by Facebook из коллекции</span><span class="sxs-lookup"><span data-stu-id="c92a9-121">Adding Workplace by Facebook from the gallery</span></span>
2. <span data-ttu-id="c92a9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c92a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="c92a9-123">Добавление Workplace by Facebook из коллекции</span><span class="sxs-lookup"><span data-stu-id="c92a9-123">Adding Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="c92a9-124">Чтобы настроить интеграцию Workplace by Facebook с Azure AD, необходимо добавить Workplace by Facebook из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c92a9-124">To configure the integration of Workplace by Facebook into Azure AD, you need to add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c92a9-125">**Чтобы добавить Workplace by Facebook из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c92a9-125">**To add Workplace by Facebook from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c92a9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c92a9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c92a9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c92a9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c92a9-133">В поле поиска введите **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-133">In the search box, type **Workplace by Facebook**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="c92a9-135">На панели результатов выберите **Workplace by Facebook** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="c92a9-135">In the results panel, select **Workplace by Facebook**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c92a9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c92a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c92a9-138">В этом разделе описана настройка и проверка единого входа Azure AD в Workplace by Facebook с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c92a9-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c92a9-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Workplace by Facebook соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c92a9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="c92a9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="c92a9-140">In other words, a link relationship between an Azure AD user and the related user in Workplace by Facebook needs to be established.</span></span>

<span data-ttu-id="c92a9-141">Чтобы установить эту связь, следует указать **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="c92a9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="c92a9-142">Чтобы настроить и проверить единый вход Azure AD в Workplace by Facebook, вам потребуется выполнить действия в указанных ниже стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="c92a9-142">To configure and test Azure AD single sign-on with Workplace by Facebook, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c92a9-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c92a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c92a9-144">**[Настройка частоты повторной проверки подлинности](#configuring-reauthentication-frequency)** необходима для настройки запроса на проверку SAML в Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="c92a9-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - to configure Workplace to prompt for a SAML check.</span></span>
3. <span data-ttu-id="c92a9-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c92a9-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="c92a9-146">**[Создание тестового пользователя Workplace by Facebook](#creating-a-workplace-by-facebook-test-user)** требуется для того, чтобы в Workplace by Facebook существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c92a9-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - to have a counterpart of Britta Simon in Workplace by Facebook that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="c92a9-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c92a9-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="c92a9-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c92a9-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c92a9-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c92a9-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c92a9-150">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="c92a9-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="c92a9-151">**Чтобы настроить единый вход Azure AD в Workplace by Facebook, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c92a9-151">**To configure Azure AD single sign-on with Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="c92a9-152">На портале Azure на странице интеграции с приложением **Workplace by Facebook** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-152">In the Azure portal, on the **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c92a9-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c92a9-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="c92a9-156">В разделе **Домены и URL-адреса приложения Workplace by Facebook** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="c92a9-156">On the **Workplace by Facebook Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="c92a9-158">а.</span><span class="sxs-lookup"><span data-stu-id="c92a9-158">a.</span></span> <span data-ttu-id="c92a9-159">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="c92a9-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="c92a9-160">b.</span><span class="sxs-lookup"><span data-stu-id="c92a9-160">b.</span></span> <span data-ttu-id="c92a9-161">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c92a9-161">In the **Identifier** textbox, type a URL using the following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c92a9-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c92a9-162">These values are not the real.</span></span> <span data-ttu-id="c92a9-163">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="c92a9-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c92a9-164">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="c92a9-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="c92a9-165">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c92a9-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="c92a9-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c92a9-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c92a9-169">В разделе **Конфигурация Workplace by Facebook** щелкните **Настроить Workplace by Facebook**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-169">On the **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c92a9-170">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="c92a9-172">В другом окне веб-браузера войдите на свой корпоративный сайт Workplace by Facebook в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c92a9-172">In a different web browser window, login to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="c92a9-173">В рамках процесса проверки подлинности SAML приложение Workplace может использовать строки запросов размером до 2,5 КБ для передачи параметров в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c92a9-173">As part of the SAML authentication process, Workplace may utilize query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="c92a9-174">На **панели мониторинга компании** перейдите на вкладку **Authentication** (Аутентификация).</span><span class="sxs-lookup"><span data-stu-id="c92a9-174">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="c92a9-175">Из раскрывающегося списка **SAML Authentication** (Аутентификация SAML) выберите **SSO Only** (Только единый вход).</span><span class="sxs-lookup"><span data-stu-id="c92a9-175">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="c92a9-176">Введите значения, скопированные из раздела **Конфигурация Workplace by Facebook** на портале Azure, в соответствующие поля.</span><span class="sxs-lookup"><span data-stu-id="c92a9-176">Input the values copied from **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="c92a9-177">В текстовое поле **SAML URL** (URL-адрес SAML) вставьте значение **URL-адрес службы единого входа**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c92a9-177">In **SAML URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="c92a9-178">В текстовое поле **SAML Issuer URL** (URL-адрес издателя SAML) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c92a9-178">In **SAML Issuer URL textbox**, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="c92a9-179">В текстовое поле **SAML Logout Redirect** (Перенаправление для выхода SAML) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c92a9-179">In **SAML Logout Redirect** (Optional), paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="c92a9-180">Откройте в Блокноте **сертификат в кодировке Base64**, скачанный с портала Azure, скопируйте его содержимое в буфер обмена и вставьте в текстовое поле **SAML Certificate** (Сертификат SAML).</span><span class="sxs-lookup"><span data-stu-id="c92a9-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="c92a9-181">Может потребоваться ввести URL-адрес аудитории, URL-адрес получателя и URL-адрес службы обработчика утверждений (ACS), указанные в разделе **Конфигурация SAML**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-181">You may need to enter the Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="c92a9-182">Прокрутите страницу до конца раздела и нажмите кнопку **Test SSO** (Проверить единый вход).</span><span class="sxs-lookup"><span data-stu-id="c92a9-182">Scroll to the bottom of the section and click the **Test SSO** button.</span></span> <span data-ttu-id="c92a9-183">Появится всплывающее окно со страницей входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c92a9-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="c92a9-184">Введите учетные данные, как при обычной аутентификации.</span><span class="sxs-lookup"><span data-stu-id="c92a9-184">Enter your credentials in as normal to authenticate.</span></span> 

    <span data-ttu-id="c92a9-185">**Устранение неполадок**. Убедитесь в том, что адрес электронной почты, возвращаемый из Azure AD, совпадает с учетной записью Workplace, которая использовалась для входа.</span><span class="sxs-lookup"><span data-stu-id="c92a9-185">**Troubleshooting:** Ensure the email address being returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="c92a9-186">После успешного прохождения проверки прокрутите страницу до конца и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="c92a9-186">Once the test has been completed successfully, scroll to the bottom of the page and click the **Save** button.</span></span>

14. <span data-ttu-id="c92a9-187">Теперь для аутентификации всех пользователей Workplace будет отображаться страница входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c92a9-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="c92a9-188">**Перенаправление для выхода SAML (необязательно)** -</span><span class="sxs-lookup"><span data-stu-id="c92a9-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="c92a9-189">При необходимости можно настроить URL-адрес выхода SAML, с помощью которого можно указать страницу выхода из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c92a9-189">You can choose to optionally configure a SAML Logout Url, which can be used to point at Azure AD's logout page.</span></span> <span data-ttu-id="c92a9-190">После активации и настройки этого параметра пользователи больше не будут направляться на страницу выхода из Workplace.</span><span class="sxs-lookup"><span data-stu-id="c92a9-190">When this setting is enabled and configured, the user will no longer be directed to the Workplace logout page.</span></span> <span data-ttu-id="c92a9-191">Вместо этого они будут переходить по URL-адресу, указанному в параметре перенаправления для выхода SAML.</span><span class="sxs-lookup"><span data-stu-id="c92a9-191">Instead, the user will be redirected to the url that was added in the SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="c92a9-192">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c92a9-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c92a9-193">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c92a9-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c92a9-194">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c92a9-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="c92a9-195">Настройка частоты повторной аутентификации</span><span class="sxs-lookup"><span data-stu-id="c92a9-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="c92a9-196">Вы можете настроить в Workplace запрос на проверку SAML каждый день, каждые 3 дня, каждую неделю, каждые 2 недели, каждый месяц или никогда.</span><span class="sxs-lookup"><span data-stu-id="c92a9-196">You can configure Workplace to prompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="c92a9-197">Минимальная частота проверки SAML в мобильных приложениях составляет одну неделю.</span><span class="sxs-lookup"><span data-stu-id="c92a9-197">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="c92a9-198">Вы также можете принудительно сбросить SAML для всех пользователей, нажав кнопку "Require SAML authentication for all users now" (Потребовать проверку подлинности SAML для всех пользователей).</span><span class="sxs-lookup"><span data-stu-id="c92a9-198">You can also force a SAML reset for all users using the button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c92a9-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c92a9-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="c92a9-200">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c92a9-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c92a9-202">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c92a9-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c92a9-203">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c92a9-205">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c92a9-207">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c92a9-209">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c92a9-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c92a9-211">а.</span><span class="sxs-lookup"><span data-stu-id="c92a9-211">a.</span></span> <span data-ttu-id="c92a9-212">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c92a9-213">b.</span><span class="sxs-lookup"><span data-stu-id="c92a9-213">b.</span></span> <span data-ttu-id="c92a9-214">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c92a9-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c92a9-215">c.</span><span class="sxs-lookup"><span data-stu-id="c92a9-215">c.</span></span> <span data-ttu-id="c92a9-216">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c92a9-217">d.</span><span class="sxs-lookup"><span data-stu-id="c92a9-217">d.</span></span> <span data-ttu-id="c92a9-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="c92a9-219">Создание тестового пользователя Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="c92a9-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="c92a9-220">В этом разделе вы создадите в Workplace by Facebook пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c92a9-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="c92a9-221">Workplace by Facebook поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c92a9-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="c92a9-222">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="c92a9-222">There is no action for you in this section.</span></span> <span data-ttu-id="c92a9-223">Если пользователь не существует в Workplace by Facebook, он создается при попытке доступа к Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="c92a9-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="c92a9-224">Если вам нужно создать пользователя вручную, обратитесь к [группе поддержки клиентов Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="c92a9-224">If you need to create a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c92a9-225">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c92a9-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c92a9-226">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="c92a9-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workplace by Facebook.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c92a9-228">**Чтобы назначить пользователя Britta Simon в Workplace by Facebook, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c92a9-228">**To assign Britta Simon to Workplace by Facebook, perform the following steps:**</span></span>

1. <span data-ttu-id="c92a9-229">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c92a9-231">Из списка приложений выберите **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-231">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="c92a9-233">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c92a9-235">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-235">Click **Add** button.</span></span> <span data-ttu-id="c92a9-236">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c92a9-238">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c92a9-239">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c92a9-240">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c92a9-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c92a9-241">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c92a9-241">Testing single sign-on</span></span>

<span data-ttu-id="c92a9-242">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="c92a9-242">If you want to test your single sign-on settings, open the Access Panel.</span></span>
<span data-ttu-id="c92a9-243">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c92a9-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c92a9-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c92a9-244">Additional resources</span></span>

* [<span data-ttu-id="c92a9-245">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c92a9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c92a9-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c92a9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c92a9-247">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="c92a9-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

