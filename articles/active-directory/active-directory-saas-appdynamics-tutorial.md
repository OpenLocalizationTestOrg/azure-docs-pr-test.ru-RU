---
title: "Руководство. Интеграция Azure Active Directory с AppDynamics | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="23856-103">Руководство. Интеграция Azure Active Directory с AppDynamics</span><span class="sxs-lookup"><span data-stu-id="23856-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="23856-104">В этом учебнике вы узнаете, как toointegrate AppDynamics с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="23856-104">In this tutorial, you learn how toointegrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23856-105">Интеграция AppDynamics с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="23856-105">Integrating AppDynamics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="23856-106">Можно управлять в Azure AD, имеющего доступ tooAppDynamics</span><span class="sxs-lookup"><span data-stu-id="23856-106">You can control in Azure AD who has access tooAppDynamics</span></span>
- <span data-ttu-id="23856-107">Можно включить на пользователей tooautomatically get вошедшего tooAppDynamics (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="23856-107">You can enable your users tooautomatically get signed-on tooAppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23856-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="23856-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="23856-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="23856-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23856-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="23856-110">Prerequisites</span></span>

<span data-ttu-id="23856-111">tooconfigure интеграция Azure AD с AppDynamics требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="23856-111">tooconfigure Azure AD integration with AppDynamics, you need hello following items:</span></span>

- <span data-ttu-id="23856-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="23856-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23856-113">Подписка с поддержкой единого входа AppDynamics</span><span class="sxs-lookup"><span data-stu-id="23856-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23856-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="23856-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23856-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="23856-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23856-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="23856-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23856-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23856-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23856-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="23856-118">Scenario description</span></span>
<span data-ttu-id="23856-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="23856-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23856-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="23856-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23856-121">Добавление AppDynamics из галереи hello</span><span class="sxs-lookup"><span data-stu-id="23856-121">Adding AppDynamics from hello gallery</span></span>
2. <span data-ttu-id="23856-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="23856-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-hello-gallery"></a><span data-ttu-id="23856-123">Добавление AppDynamics из галереи hello</span><span class="sxs-lookup"><span data-stu-id="23856-123">Adding AppDynamics from hello gallery</span></span>
<span data-ttu-id="23856-124">tooconfigure hello интеграции AppDynamics в Azure AD, вы должны tooadd AppDynamics из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="23856-124">tooconfigure hello integration of AppDynamics into Azure AD, you need tooadd AppDynamics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="23856-125">**tooadd AppDynamics из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="23856-125">**tooadd AppDynamics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="23856-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="23856-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23856-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="23856-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="23856-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="23856-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="23856-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="23856-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="23856-133">Введите в поле поиска hello **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="23856-133">In hello search box, type **AppDynamics**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="23856-135">В панели результатов hello выберите **AppDynamics**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="23856-135">In hello results panel, select **AppDynamics**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23856-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="23856-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23856-138">В этом разделе описана настройка и проверка единого входа Azure AD в AppDynamics с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23856-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="23856-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в AppDynamics является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23856-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppDynamics is tooa user in Azure AD.</span></span> <span data-ttu-id="23856-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в AppDynamics должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="23856-140">In other words, a link relationship between an Azure AD user and hello related user in AppDynamics needs toobe established.</span></span>

<span data-ttu-id="23856-141">В AppDynamics, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="23856-141">In AppDynamics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="23856-142">tooconfigure и теста Azure AD единого входа с AppDynamics, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="23856-142">tooconfigure and test Azure AD single sign-on with AppDynamics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="23856-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="23856-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="23856-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="23856-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23856-145">**[Создание тестового пользователя, прошедшего AppDynamics](#creating-an-appdynamics-test-user)**  -toohave аналог Саймон Britta в AppDynamics, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="23856-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - toohave a counterpart of Britta Simon in AppDynamics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="23856-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="23856-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23856-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23856-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23856-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="23856-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23856-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в AppDynamics приложения.</span><span class="sxs-lookup"><span data-stu-id="23856-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="23856-150">**tooconfigure Azure AD единого входа с AppDynamics, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="23856-150">**tooconfigure Azure AD single sign-on with AppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="23856-151">В hello в hello портала Azure **AppDynamics** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="23856-151">In hello Azure portal, on hello **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="23856-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="23856-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="23856-155">На hello **URL-адреса и домена AppDynamics** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="23856-155">On hello **AppDynamics Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="23856-157">а.</span><span class="sxs-lookup"><span data-stu-id="23856-157">a.</span></span> <span data-ttu-id="23856-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="23856-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="23856-159">b.</span><span class="sxs-lookup"><span data-stu-id="23856-159">b.</span></span> <span data-ttu-id="23856-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="23856-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23856-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="23856-161">These values are not real.</span></span> <span data-ttu-id="23856-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="23856-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="23856-163">Обратитесь к [группа поддержки клиента AppDynamics](https://www.appdynamics.com/support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="23856-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="23856-164">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="23856-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="23856-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="23856-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="23856-168">На hello **конфигурации AppDynamics** щелкните **Настройка AppDynamics** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="23856-168">On hello **AppDynamics Configuration** section, click **Configure AppDynamics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="23856-169">Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="23856-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="23856-171">В другом окне браузера войти в корпоративный сайт AppDynamics tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="23856-171">In a different web browser window, log in tooyour AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="23856-172">Щелкните hello панели инструментов в верхней части hello **параметры**, а затем нажмите кнопку **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="23856-172">In hello toolbar on hello top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="23856-173">![Администрирование](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="23856-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="23856-174">Нажмите кнопку hello **поставщика проверки подлинности** вкладки.</span><span class="sxs-lookup"><span data-stu-id="23856-174">Click hello **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="23856-175">![Поставщик проверки подлинности](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Поставщик проверки подлинности")</span><span class="sxs-lookup"><span data-stu-id="23856-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="23856-176">В hello **поставщика проверки подлинности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="23856-176">In hello **Authentication Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="23856-177">![Настройка SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="23856-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="23856-178">а.</span><span class="sxs-lookup"><span data-stu-id="23856-178">a.</span></span> <span data-ttu-id="23856-179">Для параметра **Authentication Provider** (Поставщик проверки подлинности) выберите значение **SAML**.</span><span class="sxs-lookup"><span data-stu-id="23856-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="23856-180">b.</span><span class="sxs-lookup"><span data-stu-id="23856-180">b.</span></span> <span data-ttu-id="23856-181">В hello **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="23856-181">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="23856-182">c.</span><span class="sxs-lookup"><span data-stu-id="23856-182">c.</span></span> <span data-ttu-id="23856-183">В hello **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="23856-183">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="23856-184">d.</span><span class="sxs-lookup"><span data-stu-id="23856-184">d.</span></span> <span data-ttu-id="23856-185">Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат** текстового поля</span><span class="sxs-lookup"><span data-stu-id="23856-185">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox</span></span>

    <span data-ttu-id="23856-186">д.</span><span class="sxs-lookup"><span data-stu-id="23856-186">e.</span></span> <span data-ttu-id="23856-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="23856-187">Click **Save**.</span></span>

     <span data-ttu-id="23856-188">![Сохранить](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Сохранить")</span><span class="sxs-lookup"><span data-stu-id="23856-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="23856-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="23856-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="23856-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="23856-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="23856-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="23856-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23856-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="23856-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="23856-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="23856-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="23856-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="23856-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="23856-196">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="23856-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23856-198">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="23856-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23856-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="23856-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23856-202">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="23856-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23856-204">а.</span><span class="sxs-lookup"><span data-stu-id="23856-204">a.</span></span> <span data-ttu-id="23856-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="23856-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23856-206">b.</span><span class="sxs-lookup"><span data-stu-id="23856-206">b.</span></span> <span data-ttu-id="23856-207">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="23856-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23856-208">c.</span><span class="sxs-lookup"><span data-stu-id="23856-208">c.</span></span> <span data-ttu-id="23856-209">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="23856-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="23856-210">d.</span><span class="sxs-lookup"><span data-stu-id="23856-210">d.</span></span> <span data-ttu-id="23856-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="23856-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="23856-212">Создание тестового пользователя AppDynamics</span><span class="sxs-lookup"><span data-stu-id="23856-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="23856-213">Пользователи toolog tooenable Azure AD в tooAppDynamics, их необходимо подготовить в AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="23856-213">tooenable Azure AD users toolog in tooAppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="23856-214">В случае AppDynamics hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="23856-214">In hello case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="23856-215">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="23856-215">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="23856-216">Войдите в систему tooyour сайт AppDynamics компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="23856-216">Log in tooyour AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="23856-217">Go слишком**пользователей**и нажмите кнопку  **+**  tooopen hello **Create User** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="23856-217">Go too**Users**, and then click **+** tooopen hello **Create User** dialog.</span></span>
   
    <span data-ttu-id="23856-218">![Пользователи](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="23856-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="23856-219">В hello **Create User** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="23856-219">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="23856-220">![Создание пользователя](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="23856-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="23856-221">а.</span><span class="sxs-lookup"><span data-stu-id="23856-221">a.</span></span> <span data-ttu-id="23856-222">Тип hello **Username**, **имя**, **электронной почты**, **новый пароль**, **повторно введенный новый пароль** из допустимых AAD учетной записи, которые должны tooprovision hello связанные текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="23856-222">Type hello **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="23856-223">b.</span><span class="sxs-lookup"><span data-stu-id="23856-223">b.</span></span> <span data-ttu-id="23856-224">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="23856-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="23856-225">Можно использовать любые другие AppDynamics пользователя средства создания учетных записей или API, предоставленные AppDynamics tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23856-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="23856-226">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="23856-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="23856-227">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAppDynamics доступа.</span><span class="sxs-lookup"><span data-stu-id="23856-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppDynamics.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="23856-229">**tooassign tooAppDynamics Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="23856-229">**tooassign Britta Simon tooAppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="23856-230">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="23856-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="23856-232">В списке приложений hello выберите **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="23856-232">In hello applications list, select **AppDynamics**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="23856-234">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="23856-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="23856-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="23856-236">Click **Add** button.</span></span> <span data-ttu-id="23856-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="23856-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="23856-239">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="23856-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="23856-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="23856-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23856-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="23856-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23856-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="23856-242">Testing single sign-on</span></span>

<span data-ttu-id="23856-243">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="23856-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="23856-244">При нажатии кнопки AppDynamics плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour AppDynamics приложения.</span><span class="sxs-lookup"><span data-stu-id="23856-244">When you click hello AppDynamics tile in hello Access Panel, you should get automatically signed-on tooyour AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="23856-245">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="23856-245">Additional resources</span></span>

* [<span data-ttu-id="23856-246">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23856-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23856-247">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23856-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

