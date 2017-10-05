---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и Workplace by Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="e80ac-103">Руководство по интеграции Azure Active Directory с Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="e80ac-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="e80ac-104">В этом руководстве описано, как интегрировать Workplace by Facebook с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e80ac-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e80ac-105">Интеграция Workplace by Facebook с Azure AD дает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e80ac-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e80ac-106">С помощью Azure AD вы можете контролировать доступ к Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e80ac-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="e80ac-107">Вы можете включить автоматический вход пользователей в Workplace by Facebook (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e80ac-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e80ac-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ac-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="e80ac-109">Дополнительные сведения об интеграции приложения SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="e80ac-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e80ac-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e80ac-110">Prerequisites</span></span>

<span data-ttu-id="e80ac-111">Чтобы настроить интеграцию Azure AD с Workplace by Facebook, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e80ac-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="e80ac-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e80ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e80ac-113">подписка Workplace by Facebook с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e80ac-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="e80ac-114">При проверке действий в этом руководстве соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e80ac-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="e80ac-115">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e80ac-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e80ac-116">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e80ac-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e80ac-117">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e80ac-117">Scenario description</span></span>
<span data-ttu-id="e80ac-118">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e80ac-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="e80ac-119">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e80ac-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e80ac-120">Добавление Workplace by Facebook из коллекции.</span><span class="sxs-lookup"><span data-stu-id="e80ac-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="e80ac-121">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e80ac-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="e80ac-122">Добавление Workplace by Facebook из коллекции</span><span class="sxs-lookup"><span data-stu-id="e80ac-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="e80ac-123">Чтобы настроить интеграцию Workplace by Facebook с Azure AD, необходимо добавить Workplace by Facebook из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e80ac-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="e80ac-124">На [портале Azure](https://portal.azure.com) в области слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="e80ac-126">Выберите **Корпоративные приложения** > **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="e80ac-128">Чтобы добавить новое приложение, в верхней части диалогового окна щелкните **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="e80ac-130">В поле поиска введите **Workplace by Facebook** и выберите **Workplace by Facebook** среди результатов.</span><span class="sxs-lookup"><span data-stu-id="e80ac-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="e80ac-131">Щелкните **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e80ac-131">Then select **Add**, to add the application.</span></span>

    ![Workplace by Facebook в списке результатов](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e80ac-133">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e80ac-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e80ac-134">В этом разделе описана настройка и проверка единого входа Azure AD в Workplace by Facebook с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e80ac-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e80ac-135">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Workplace by Facebook соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e80ac-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="e80ac-136">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e80ac-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="e80ac-137">Чтобы установить эту связь, укажите **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e80ac-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e80ac-138">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="e80ac-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e80ac-139">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e80ac-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="e80ac-140">На портале Azure на странице интеграции с приложением **Workplace by Facebook** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="e80ac-142">В диалоговом окне **Единый вход** из списка **Режим** выберите значение **Вход на основе SAML**, чтобы включить единый вход.</span><span class="sxs-lookup"><span data-stu-id="e80ac-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="e80ac-144">В разделе **Домены и URL-адреса приложения Workplace by Facebook** выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="e80ac-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="e80ac-145">а.</span><span class="sxs-lookup"><span data-stu-id="e80ac-145">a.</span></span> <span data-ttu-id="e80ac-146">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company subdomain>.facebook.com`.</span><span class="sxs-lookup"><span data-stu-id="e80ac-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="e80ac-147">b.</span><span class="sxs-lookup"><span data-stu-id="e80ac-147">b.</span></span> <span data-ttu-id="e80ac-148">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://www.facebook.com/company/<scim company id>`.</span><span class="sxs-lookup"><span data-stu-id="e80ac-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="e80ac-149">Эти значения приведены только для примера.</span><span class="sxs-lookup"><span data-stu-id="e80ac-149">These values are an example only.</span></span> <span data-ttu-id="e80ac-150">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="e80ac-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="e80ac-151">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="e80ac-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="e80ac-152">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e80ac-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="e80ac-154">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-154">Select **Save**.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e80ac-156">В разделе **Конфигурация Workplace by Facebook** щелкните **Настроить Workplace by Facebook**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="e80ac-157">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Конфигурация Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="e80ac-159">В другом окне веб-браузера войдите на свой корпоративный сайт Workplace by Facebook в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e80ac-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="e80ac-160">В рамках процесса аутентификации SAML приложение Workplace может использовать строки запросов размером до 2,5 КБ для передачи параметров в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e80ac-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="e80ac-161">На **панели мониторинга компании** перейдите на вкладку **Authentication** (Аутентификация).</span><span class="sxs-lookup"><span data-stu-id="e80ac-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="e80ac-162">Из раскрывающегося списка **SAML Authentication** (Аутентификация SAML) выберите **SSO Only** (Только единый вход).</span><span class="sxs-lookup"><span data-stu-id="e80ac-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="e80ac-163">Введите значения, скопированные из раздела **Конфигурация Workplace by Facebook** на портале Azure, в соответствующие поля.</span><span class="sxs-lookup"><span data-stu-id="e80ac-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="e80ac-164">В текстовое поле **SAML URL** (URL-адрес SAML) вставьте значение **URL-адрес службы единого входа**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ac-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="e80ac-165">В текстовое поле **SAML Issuer URL** (URL-адрес издателя SAML) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ac-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="e80ac-166">В текстовое поле **SAML Logout Redirect (optional)** (Перенаправление для выхода SAML (необязательно)) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ac-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="e80ac-167">Откройте в Блокноте **сертификат в кодировке Base-64**, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="e80ac-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="e80ac-168">Скопируйте его содержимое в буфер обмена и вставьте в текстовое поле **SAML Certificate** (Сертификат SAML).</span><span class="sxs-lookup"><span data-stu-id="e80ac-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="e80ac-169">Может потребоваться ввести URL-адрес аудитории, URL-адрес получателя и URL-адрес службы обработчика утверждений (ACS), указанные в разделе **Конфигурация SAML**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="e80ac-170">Прокрутите страницу до конца раздела и щелкните **Test SSO** (Проверить единый вход).</span><span class="sxs-lookup"><span data-stu-id="e80ac-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="e80ac-171">Появится всплывающее окно со страницей входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e80ac-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="e80ac-172">Введите учетные данные, как при обычной аутентификации.</span><span class="sxs-lookup"><span data-stu-id="e80ac-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="e80ac-173">Убедитесь в том, что адрес электронной почты, возвращаемый из Azure AD, совпадает с учетной записью Workplace, которая использовалась для входа.</span><span class="sxs-lookup"><span data-stu-id="e80ac-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="e80ac-174">Если тест выполнен успешно, прокрутите страницу до конца и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="e80ac-175">Теперь для аутентификации всех пользователей Workplace будет отображаться страница входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e80ac-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="e80ac-176">Можно настроить URL-адрес выхода SAML, с помощью которого можно указать страницу выхода из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e80ac-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="e80ac-177">После активации и настройки этого параметра пользователи больше не будут направляться на страницу выхода из Workplace.</span><span class="sxs-lookup"><span data-stu-id="e80ac-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="e80ac-178">Вместо этого они будут переходить по URL-адресу, указанному в параметре перенаправления для выхода SAML.</span><span class="sxs-lookup"><span data-stu-id="e80ac-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="e80ac-179">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e80ac-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="e80ac-180">После добавления этого приложения из раздела **Active Directory** > **Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка в нижней части страницы**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e80ac-181">Дополнительные сведения о встроенной документации см. в статье [Управление параметрами единого входа для корпоративных приложений]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e80ac-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="e80ac-182">Настройка частоты повторной аутентификации</span><span class="sxs-lookup"><span data-stu-id="e80ac-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="e80ac-183">Вы можете настроить в Workplace запрос на проверку SAML каждый день, каждые 3 дня, каждую неделю, каждые 2 недели, каждый месяц или никогда.</span><span class="sxs-lookup"><span data-stu-id="e80ac-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="e80ac-184">Минимальная частота проверки SAML в мобильных приложениях равна одной неделе.</span><span class="sxs-lookup"><span data-stu-id="e80ac-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="e80ac-185">Можно также принудительно применить SAML для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="e80ac-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="e80ac-186">Для этого нажмите кнопку **Require SAML authentication for all users now** (Применить аутентификацию SAML для всех пользователей).</span><span class="sxs-lookup"><span data-stu-id="e80ac-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e80ac-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e80ac-187">Create an Azure AD test user</span></span>
<span data-ttu-id="e80ac-188">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e80ac-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

1. <span data-ttu-id="e80ac-190">На **портале Azure** в области слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e80ac-192">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и выберите **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e80ac-194">Щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e80ac-196">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="e80ac-196">In the **User** dialog box, do the following:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e80ac-198">а.</span><span class="sxs-lookup"><span data-stu-id="e80ac-198">a.</span></span> <span data-ttu-id="e80ac-199">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e80ac-200">b.</span><span class="sxs-lookup"><span data-stu-id="e80ac-200">b.</span></span> <span data-ttu-id="e80ac-201">В текстовом поле **Имя пользователя** введите **адрес электронной почты** пользователя BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e80ac-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e80ac-202">c.</span><span class="sxs-lookup"><span data-stu-id="e80ac-202">c.</span></span> <span data-ttu-id="e80ac-203">Щелкните **Показать пароль** и запишите пароль.</span><span class="sxs-lookup"><span data-stu-id="e80ac-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="e80ac-204">d.</span><span class="sxs-lookup"><span data-stu-id="e80ac-204">d.</span></span> <span data-ttu-id="e80ac-205">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="e80ac-206">Создание тестового пользователя Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="e80ac-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="e80ac-207">В этом разделе вы создадите в Workplace by Facebook пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e80ac-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="e80ac-208">Workplace by Facebook поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e80ac-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="e80ac-209">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="e80ac-209">There is no action for you in this section.</span></span> <span data-ttu-id="e80ac-210">Если пользователь не существует в Workplace by Facebook, он создается при попытке доступа к Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e80ac-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="e80ac-211">Если вам нужно создать пользователя вручную, обратитесь к [группе поддержки клиентов Workplace by Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="e80ac-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e80ac-212">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e80ac-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="e80ac-213">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="e80ac-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![Назначение пользователя][200] 

1. <span data-ttu-id="e80ac-215">На портале Azure откройте представление "Приложения".</span><span class="sxs-lookup"><span data-stu-id="e80ac-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="e80ac-216">Перейдите к представлению "Каталог", перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e80ac-218">Из списка приложений выберите **Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Ссылка на Workplace by Facebook в списке "Приложения"](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="e80ac-220">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-220">In the menu on the left, select **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="e80ac-222">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-222">Select **Add**.</span></span> <span data-ttu-id="e80ac-223">Затем в области **Добавление назначения** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="e80ac-225">В диалоговом окне **Пользователи и группы** из списка "Пользователи" выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="e80ac-226">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="e80ac-227">В диалоговом окне **Добавление назначения** выберите **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e80ac-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e80ac-228">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e80ac-228">Test single sign-on</span></span>

<span data-ttu-id="e80ac-229">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="e80ac-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="e80ac-230">Дополнительные сведения см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e80ac-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e80ac-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e80ac-231">Next steps</span></span>

* <span data-ttu-id="e80ac-232">Ознакомьтесь со [списком учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="e80ac-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="e80ac-233">Прочитайте статью [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="e80ac-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="e80ac-234">Узнайте больше о том, как [настроить подготовку пользователей](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e80ac-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

