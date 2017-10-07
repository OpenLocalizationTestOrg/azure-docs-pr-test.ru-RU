---
title: "Учебник. Интеграция Azure Active Directory с Jitbit Helpdesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="57283-103">Руководство. Интеграция Azure Active Directory с Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="57283-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="57283-104">В этом учебнике вы узнаете, как toointegrate Jitbit Helpdesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57283-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57283-105">Интеграция Jitbit Helpdesk с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="57283-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="57283-106">Можно управлять в Azure AD, имеющего доступ tooJitbit службы технической поддержки</span><span class="sxs-lookup"><span data-stu-id="57283-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="57283-107">Можно включить на пользователей tooautomatically get вошедшего tooJitbit службы технической поддержки (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="57283-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57283-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="57283-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="57283-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57283-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57283-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="57283-110">Prerequisites</span></span>

<span data-ttu-id="57283-111">tooconfigure интеграция Azure AD с Jitbit Helpdesk, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="57283-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="57283-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="57283-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57283-113">подписка с поддержкой единого входа Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="57283-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57283-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="57283-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57283-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="57283-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57283-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="57283-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="57283-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57283-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57283-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="57283-118">Scenario description</span></span>
<span data-ttu-id="57283-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="57283-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57283-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="57283-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57283-121">Добавление Jitbit Helpdesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="57283-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="57283-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="57283-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="57283-123">Добавление Jitbit Helpdesk из галереи hello</span><span class="sxs-lookup"><span data-stu-id="57283-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="57283-124">tooconfigure hello интеграции Jitbit Helpdesk в Azure AD, вы должны tooadd Jitbit Helpdesk из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="57283-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="57283-125">**tooadd Jitbit Helpdesk из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57283-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="57283-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="57283-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57283-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="57283-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="57283-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="57283-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="57283-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="57283-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="57283-133">Введите в поле поиска hello **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="57283-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="57283-135">В панели результатов hello выберите **Jitbit Helpdesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="57283-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57283-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="57283-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57283-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Jitbit Helpdesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57283-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57283-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Jitbit Helpdesk является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57283-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="57283-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Jitbit Helpdesk должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="57283-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="57283-141">В Jitbit Helpdesk, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="57283-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="57283-142">tooconfigure и теста Azure AD единого входа с Jitbit Helpdesk, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="57283-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="57283-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="57283-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="57283-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="57283-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57283-145">**[Создание тестового пользователя Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave аналог Саймон Britta в Jitbit Helpdesk, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="57283-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="57283-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="57283-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57283-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="57283-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57283-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="57283-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57283-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Jitbit Helpdesk приложения.</span><span class="sxs-lookup"><span data-stu-id="57283-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="57283-150">**tooconfigure Azure AD единого входа с Jitbit Helpdesk, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57283-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="57283-151">В hello в hello портала Azure **Jitbit Helpdesk** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="57283-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="57283-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="57283-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="57283-155">На hello **Jitbit Helpdesk доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="57283-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="57283-157">а.</span><span class="sxs-lookup"><span data-stu-id="57283-157">a.</span></span> <span data-ttu-id="57283-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="57283-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="57283-159">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="57283-159">This value is not real.</span></span> <span data-ttu-id="57283-160">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="57283-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="57283-161">Обратитесь к [группа поддержки Jitbit Helpdesk клиента](https://www.jitbit.com/support/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="57283-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="57283-162">b.</span><span class="sxs-lookup"><span data-stu-id="57283-162">b.</span></span>  <span data-ttu-id="57283-163">В hello **идентификатор** текстовом поле введите URL-адрес, следующим образом:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="57283-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="57283-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="57283-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="57283-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="57283-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="57283-168">На hello **Jitbit Helpdesk конфигурации** щелкните **Настройка Jitbit Helpdesk** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="57283-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="57283-169">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="57283-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="57283-171">В другом окне браузера войдите на свой корпоративный веб-сайт Jitbit Helpdesk в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="57283-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="57283-172">Щелкните hello панели инструментов в верхней части hello **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="57283-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="57283-173">![Администрирование](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="57283-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="57283-174">Щелкните **Общие параметры**.</span><span class="sxs-lookup"><span data-stu-id="57283-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="57283-175">![Пользователи, организации и разрешения](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Пользователи, организации и разрешения")</span><span class="sxs-lookup"><span data-stu-id="57283-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="57283-176">В hello **параметры проверки подлинности** конфигурации выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="57283-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="57283-177">![Параметры аутентификации](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Параметры аутентификации")</span><span class="sxs-lookup"><span data-stu-id="57283-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="57283-178">а.</span><span class="sxs-lookup"><span data-stu-id="57283-178">a.</span></span> <span data-ttu-id="57283-179">Выберите **включить SAML 2.0 единого входа в**, toosign использовать единый вход (SSO), с **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="57283-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="57283-180">b.</span><span class="sxs-lookup"><span data-stu-id="57283-180">b.</span></span> <span data-ttu-id="57283-181">В hello **URL-адрес конечной точки** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="57283-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="57283-182">c.</span><span class="sxs-lookup"><span data-stu-id="57283-182">c.</span></span> <span data-ttu-id="57283-183">Откройте ваш **base-64** закодированный сертификат в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля</span><span class="sxs-lookup"><span data-stu-id="57283-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="57283-184">d.</span><span class="sxs-lookup"><span data-stu-id="57283-184">d.</span></span> <span data-ttu-id="57283-185">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="57283-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="57283-186">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="57283-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="57283-187">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="57283-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="57283-188">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="57283-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57283-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="57283-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="57283-190">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="57283-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="57283-192">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57283-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="57283-193">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="57283-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57283-195">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="57283-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57283-197">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="57283-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57283-199">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="57283-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57283-201">а.</span><span class="sxs-lookup"><span data-stu-id="57283-201">a.</span></span> <span data-ttu-id="57283-202">В hello **имя** в текстовое поле имя типа как **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57283-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="57283-203">b.</span><span class="sxs-lookup"><span data-stu-id="57283-203">b.</span></span> <span data-ttu-id="57283-204">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57283-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57283-205">c.</span><span class="sxs-lookup"><span data-stu-id="57283-205">c.</span></span> <span data-ttu-id="57283-206">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="57283-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="57283-207">d.</span><span class="sxs-lookup"><span data-stu-id="57283-207">d.</span></span> <span data-ttu-id="57283-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="57283-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="57283-209">Создание тестового пользователя Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="57283-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="57283-210">В порядке tooenable toolog пользователей Azure AD в Jitbit Helpdesk их необходимо подготовить в Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="57283-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="57283-211">В случае Jitbit Helpdesk hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="57283-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="57283-212">**tooprovision учетной записи пользователя, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="57283-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="57283-213">Войдите в tooyour **Jitbit Helpdesk** клиента.</span><span class="sxs-lookup"><span data-stu-id="57283-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="57283-214">В меню в верхней части hello hello выберите **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="57283-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="57283-215">![Администрирование](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="57283-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="57283-216">Нажмите кнопку **Пользователи, компании и разрешения**.</span><span class="sxs-lookup"><span data-stu-id="57283-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="57283-217">![Пользователи, организации и разрешения](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Пользователи, организации и разрешения")</span><span class="sxs-lookup"><span data-stu-id="57283-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="57283-218">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="57283-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="57283-219">![Добавление пользователя](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="57283-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="57283-220">Hello создать раздел введите данные hello hello Azure AD от имени учетной записи требуется tooprovision следующим образом:</span><span class="sxs-lookup"><span data-stu-id="57283-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="57283-221">![Создание](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Создание")</span><span class="sxs-lookup"><span data-stu-id="57283-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="57283-222">а.</span><span class="sxs-lookup"><span data-stu-id="57283-222">a.</span></span> <span data-ttu-id="57283-223">В hello **Username** введите **BrittaSimon**, имя пользователя hello как hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="57283-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="57283-224">b.</span><span class="sxs-lookup"><span data-stu-id="57283-224">b.</span></span> <span data-ttu-id="57283-225">В hello **электронной почты** текстовое поле, такие как тип адреса электронной почты пользователя hello  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="57283-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="57283-226">c.</span><span class="sxs-lookup"><span data-stu-id="57283-226">c.</span></span> <span data-ttu-id="57283-227">В hello **имя** в текстовое поле имя первого типа hello пользователя как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="57283-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="57283-228">d.</span><span class="sxs-lookup"><span data-stu-id="57283-228">d.</span></span> <span data-ttu-id="57283-229">В hello **Фамилия** текстовое поле, тип фамилию пользователя hello как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="57283-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="57283-230">д.</span><span class="sxs-lookup"><span data-stu-id="57283-230">e.</span></span> <span data-ttu-id="57283-231">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="57283-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="57283-232">Можно использовать любые другие Jitbit Helpdesk пользователя средства создания учетных записей или интерфейсы API, предоставляемые Jitbit Helpdesk tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57283-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="57283-233">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="57283-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="57283-234">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooJitbit службы технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="57283-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="57283-236">**tooassign tooJitbit Britta Simon службы технической поддержки, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="57283-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="57283-237">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="57283-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="57283-239">В списке приложений hello выберите **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="57283-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="57283-241">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="57283-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="57283-243">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="57283-243">Click **Add** button.</span></span> <span data-ttu-id="57283-244">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="57283-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="57283-246">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="57283-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="57283-247">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="57283-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57283-248">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="57283-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57283-249">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="57283-249">Testing single sign-on</span></span>

<span data-ttu-id="57283-250">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="57283-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="57283-251">При нажатии кнопки Jitbit Helpdesk плитки в панели доступа hello hello, должно появиться страница входа приложения Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="57283-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="57283-252">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="57283-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57283-253">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="57283-253">Additional resources</span></span>

* [<span data-ttu-id="57283-254">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57283-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57283-255">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57283-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

