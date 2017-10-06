---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и рабочей области с Facebook."
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
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="613e2-103">Руководство по интеграции Azure Active Directory с Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="613e2-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="613e2-104">В этом учебнике вы узнаете, как toointegrate рабочему месту с Facebook с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="613e2-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="613e2-105">Интеграция рабочему месту с Facebook с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="613e2-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="613e2-106">Можно управлять в Azure AD, имеющего доступ tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="613e2-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="613e2-107">Можно включить пользователей tooautomatically получить вход tooWorkplace с Facebook (единый вход) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="613e2-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="613e2-108">Можно управлять учетными записями в одном централизованном месте: hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="613e2-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="613e2-109">Дополнительные сведения об интеграции приложения SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="613e2-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="613e2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="613e2-110">Prerequisites</span></span>

<span data-ttu-id="613e2-111">tooconfigure интеграция Azure AD в рабочей области с Facebook, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="613e2-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="613e2-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="613e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="613e2-113">подписка Workplace by Facebook с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="613e2-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="613e2-114">tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="613e2-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="613e2-115">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="613e2-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="613e2-116">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="613e2-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="613e2-117">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="613e2-117">Scenario description</span></span>
<span data-ttu-id="613e2-118">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="613e2-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="613e2-119">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="613e2-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="613e2-120">Добавление рабочей области с Facebook из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="613e2-121">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="613e2-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="613e2-122">Добавление рабочей области с Facebook из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="613e2-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="613e2-123">tooconfigure интеграция рабочему месту с Facebook hello в Azure AD, добавить рабочему месту с Facebook из hello коллекции tooyour список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="613e2-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="613e2-124">В hello [портал Azure](https://portal.azure.com)в левой области hello, выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="613e2-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="613e2-126">Обзор слишком**корпоративных приложений** > **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="613e2-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="613e2-128">tooadd hello новые приложения, выберите **новое приложение** в верхней части hello диалогового окна «hello».</span><span class="sxs-lookup"><span data-stu-id="613e2-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="613e2-130">Введите в поле поиска hello **рабочему месту с Facebook**и выберите **рабочему месту с Facebook** из результатов.</span><span class="sxs-lookup"><span data-stu-id="613e2-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="613e2-131">Выберите **добавить**, tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-131">Then select **Add**, tooadd hello application.</span></span>

    ![Рабочая область с Facebook в списке результатов hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="613e2-133">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="613e2-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="613e2-134">В этом разделе описана настройка и проверка единого входа Azure AD в Workplace by Facebook с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="613e2-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="613e2-135">Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в рабочей области с Facebook является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="613e2-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="613e2-136">Другими словами следует установить ссылочного отношения между пользователя Azure AD и связанных пользователей hello в рабочей области с Facebook.</span><span class="sxs-lookup"><span data-stu-id="613e2-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="613e2-137">Установить это отношение, назначив значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в рабочей области с Facebook.</span><span class="sxs-lookup"><span data-stu-id="613e2-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="613e2-138">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="613e2-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="613e2-139">В этом разделе Включить единый вход Azure AD в hello портал Azure и настроить единый вход в рабочую область с помощью приложения Facebook.</span><span class="sxs-lookup"><span data-stu-id="613e2-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="613e2-140">В hello в hello портала Azure **рабочему месту с Facebook** странице интеграции приложений выберите **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="613e2-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="613e2-142">В hello **единого входа** выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="613e2-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="613e2-144">В hello **рабочему месту с URL-адреса и домена Facebook** статьи, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="613e2-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="613e2-145">а.</span><span class="sxs-lookup"><span data-stu-id="613e2-145">a.</span></span> <span data-ttu-id="613e2-146">В hello **URL-адрес входа** текстовом поле введите URL-адрес, использующий hello следующий шаблон:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="613e2-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="613e2-147">b.</span><span class="sxs-lookup"><span data-stu-id="613e2-147">b.</span></span> <span data-ttu-id="613e2-148">В hello **идентификатор** текстовом поле введите URL-адрес, использующий hello следующий шаблон:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="613e2-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="613e2-149">Эти значения приведены только для примера.</span><span class="sxs-lookup"><span data-stu-id="613e2-149">These values are an example only.</span></span> <span data-ttu-id="613e2-150">Обновите эти значения с hello фактический URL-адрес входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="613e2-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="613e2-151">Обратитесь в службу hello [рабочей группой поддержки клиент Facebook](https://workplace.fb.com/faq/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="613e2-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="613e2-152">В hello **сертификат подписи SAML** выберите **сертификата (Base64)**, а затем сохраните файл сертификата hello на компьютере.</span><span class="sxs-lookup"><span data-stu-id="613e2-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="613e2-154">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="613e2-154">Select **Save**.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="613e2-156">В hello **рабочему месту конфигурацией Facebook** выберите **Настройка рабочей области с Facebook** tooopen hello **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="613e2-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="613e2-157">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник** раздела.</span><span class="sxs-lookup"><span data-stu-id="613e2-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Конфигурация Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="613e2-159">В другом окне браузера войдите в рабочей области с Facebook корпоративный сайт tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="613e2-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="613e2-160">Как часть процесса проверки подлинности SAML hello рабочей области можно использовать строки запроса из копии too2.5 килобайт размер в порядке toopass параметры tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="613e2-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="613e2-161">В hello **панели мониторинга компании**, go toohello **проверки подлинности** вкладки.</span><span class="sxs-lookup"><span data-stu-id="613e2-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="613e2-162">В разделе **проверку подлинности SAML**выберите **SSO только** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="613e2-163">Введите hello значения, скопированные из hello **рабочему месту конфигурацией Facebook** раздел hello портал Azure в соответствующие поля hello:</span><span class="sxs-lookup"><span data-stu-id="613e2-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="613e2-164">В **URL-адрес SAML** текстовое поле, вставить значение hello **единого входа URL-адрес службы**, который вы скопировали из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="613e2-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="613e2-165">В **URL-адрес издателя SAML** текстовое поле, вставить значение hello **идентификатор сущности SAML**, который вы скопировали из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="613e2-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="613e2-166">В **SAML выхода перенаправления (необязательно)**, вставьте значение hello **URL-адрес выхода**, который вы скопировали из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="613e2-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="613e2-167">Откройте ваш **сертификат в кодировке base-64** в блокноте, загружаются из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="613e2-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="613e2-168">Скопируйте содержимое hello в буфер обмена и вставьте его в toothe **сертификат SAML** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="613e2-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="613e2-169">Может потребоваться аудитории hello tooenter URL-адрес, URL-адрес получателя и ACS (службы обработчика утверждений) URL-адрес, перечисленных в разделе hello **конфигурация SAML** раздела.</span><span class="sxs-lookup"><span data-stu-id="613e2-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="613e2-170">Прокрутите toohello нижней части раздела hello и выберите **тестирования единого входа**.</span><span class="sxs-lookup"><span data-stu-id="613e2-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="613e2-171">Появится всплывающее окно с hello Azure AD на странице входа.</span><span class="sxs-lookup"><span data-stu-id="613e2-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="613e2-172">tooauthenticate, введите свои учетные данные в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="613e2-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="613e2-173">Убедитесь, Здравствуйте hello адрес электронной почты, возвращенный Azure AD, так же, как hello рабочей учетной записи, которой вы вошли в систему.</span><span class="sxs-lookup"><span data-stu-id="613e2-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="613e2-174">Если hello тестирования успешно завершено, прокрутите toohello нижней части страницы hello и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="613e2-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="613e2-175">Теперь для аутентификации всех пользователей Workplace будет отображаться страница входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="613e2-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="613e2-176">Вы можете tooconfigure выхода SAML в URL-адрес, который можно использовать toopoint на страницы выхода hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="613e2-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="613e2-177">Если этот параметр включен и настроен, hello пользователь больше не страницы выхода направленной toohello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="613e2-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="613e2-178">Вместо этого пользователь hello является перенаправленный toohello URL-адрес, которое было добавлено в параметр перенаправления выхода SAML hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="613e2-179">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="613e2-180">После добавления этого приложения из hello **Active Directory** > **корпоративных приложений** просто выберите hello **Single Sign-On** вкладку и hello доступа внедренные документации с помощью hello **конфигурации** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="613e2-181">Вы можете прочитать больше о документации embedded hello в hello [Azure AD внедренных документации]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="613e2-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="613e2-182">Настройка частоты повторной аутентификации</span><span class="sxs-lookup"><span data-stu-id="613e2-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="613e2-183">Можно настроить tooprompt рабочему месту для проверки SAML каждый день, в течение трех дней, одна неделя, две недели, один месяц или никогда.</span><span class="sxs-lookup"><span data-stu-id="613e2-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="613e2-184">Hello минимальное значение для проверки SAML hello мобильных приложений имеет значение tooone недели.</span><span class="sxs-lookup"><span data-stu-id="613e2-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="613e2-185">Можно также принудительно применить SAML для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="613e2-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="613e2-186">toodo это, используйте hello **требуется проверка подлинности SAML для всех пользователей теперь** кнопки.</span><span class="sxs-lookup"><span data-stu-id="613e2-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="613e2-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="613e2-187">Create an Azure AD test user</span></span>
<span data-ttu-id="613e2-188">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="613e2-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

1. <span data-ttu-id="613e2-190">В hello **портал Azure**в левой области hello, выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="613e2-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="613e2-192">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп**и выберите **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="613e2-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="613e2-194">tooopen hello **пользователя** выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="613e2-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="613e2-196">В hello **пользователя** диалогового окна поле, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="613e2-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="613e2-198">а.</span><span class="sxs-lookup"><span data-stu-id="613e2-198">a.</span></span> <span data-ttu-id="613e2-199">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="613e2-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="613e2-200">b.</span><span class="sxs-lookup"><span data-stu-id="613e2-200">b.</span></span> <span data-ttu-id="613e2-201">В hello **имя пользователя** текстовое поле, тип hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="613e2-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="613e2-202">c.</span><span class="sxs-lookup"><span data-stu-id="613e2-202">c.</span></span> <span data-ttu-id="613e2-203">Щелкните **Показать пароль** и запишите пароль.</span><span class="sxs-lookup"><span data-stu-id="613e2-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="613e2-204">d.</span><span class="sxs-lookup"><span data-stu-id="613e2-204">d.</span></span> <span data-ttu-id="613e2-205">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="613e2-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="613e2-206">Создание тестового пользователя Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="613e2-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="613e2-207">В этом разделе вы создадите в Workplace by Facebook пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="613e2-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="613e2-208">Workplace by Facebook поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="613e2-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="613e2-209">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="613e2-209">There is no action for you in this section.</span></span> <span data-ttu-id="613e2-210">Если пользователь не существует в рабочей области с Facebook, новый созданный при попытке tooaccess рабочему месту Facebook.</span><span class="sxs-lookup"><span data-stu-id="613e2-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="613e2-211">Если вам требуется toocreate пользователя вручную, обратитесь в службу hello [рабочей группой поддержки клиент Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="613e2-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="613e2-212">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="613e2-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="613e2-213">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooWorkplace с Facebook.</span><span class="sxs-lookup"><span data-stu-id="613e2-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![Назначение пользователя][200] 

1. <span data-ttu-id="613e2-215">В hello Azure просмотрите приложений портала, откройте hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="613e2-216">Перейдите в представление каталога toohello, перейдите в слишком**корпоративных приложений**, а затем выберите **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="613e2-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="613e2-218">В списке приложений hello выберите **рабочему месту с Facebook**.</span><span class="sxs-lookup"><span data-stu-id="613e2-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Hello рабочему месту с Facebook ссылку в списке приложений hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="613e2-220">Выберите в меню hello слева hello, **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="613e2-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="613e2-222">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="613e2-222">Select **Add**.</span></span> <span data-ttu-id="613e2-223">Затем в hello **добавить назначение** выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="613e2-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="613e2-225">В hello **пользователей и групп** выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="613e2-226">В hello **пользователей и групп** выберите **выберите**.</span><span class="sxs-lookup"><span data-stu-id="613e2-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="613e2-227">В hello **добавить назначение** выберите **назначить**.</span><span class="sxs-lookup"><span data-stu-id="613e2-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="613e2-228">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="613e2-228">Test single sign-on</span></span>

<span data-ttu-id="613e2-229">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="613e2-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="613e2-230">Дополнительные сведения см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="613e2-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="613e2-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="613e2-231">Next steps</span></span>

* <span data-ttu-id="613e2-232">В разделе hello [список учебников по toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="613e2-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="613e2-233">Прочитайте статью [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="613e2-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="613e2-234">Дополнительные сведения о том, как слишком[Настройка подготовки пользователя](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="613e2-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



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

