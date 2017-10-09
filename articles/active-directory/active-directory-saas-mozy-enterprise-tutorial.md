---
title: "Руководство по интеграции Azure Active Directory с Mozy Enterprise | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="e7d74-103">Учебник. Интеграция Azure Active Directory с Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="e7d74-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="e7d74-104">В этом учебнике вы узнаете, как toointegrate Mozy Enterprise с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e7d74-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e7d74-105">Интеграция Mozy Enterprise с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e7d74-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e7d74-106">Можно управлять в Azure AD, имеющего доступ tooMozy предприятия</span><span class="sxs-lookup"><span data-stu-id="e7d74-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="e7d74-107">Можно включить на пользователей tooautomatically get вошедшего tooMozy предприятия (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7d74-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e7d74-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e7d74-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e7d74-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e7d74-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7d74-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e7d74-110">Prerequisites</span></span>

<span data-ttu-id="e7d74-111">tooconfigure интеграция Azure AD с Mozy Enterprise, нужно hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="e7d74-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="e7d74-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e7d74-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e7d74-113">подписка с поддержкой единого входа Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7d74-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e7d74-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e7d74-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e7d74-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="e7d74-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e7d74-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e7d74-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e7d74-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e7d74-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e7d74-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e7d74-118">Scenario description</span></span>
<span data-ttu-id="e7d74-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e7d74-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e7d74-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="e7d74-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e7d74-121">Добавление Mozy Enterprise из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="e7d74-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="e7d74-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7d74-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="e7d74-123">Добавление Mozy Enterprise из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="e7d74-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="e7d74-124">tooconfigure hello интеграции Mozy Enterprise в Azure AD, вы должны tooadd Mozy Enterprise из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e7d74-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e7d74-125">**tooadd Mozy Enterprise из коллекции hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e7d74-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7d74-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e7d74-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e7d74-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e7d74-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e7d74-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="e7d74-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e7d74-133">Введите в поле поиска hello **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="e7d74-135">В панели результатов hello выберите **Mozy Enterprise**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e7d74-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e7d74-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7d74-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e7d74-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Mozy Enterprise с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e7d74-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e7d74-139">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в Mozy Enterprise — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7d74-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="e7d74-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Mozy Enterprise должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="e7d74-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="e7d74-141">В Mozy Enterprise, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="e7d74-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e7d74-142">tooconfigure и теста Azure AD единого входа с Mozy Enterprise, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e7d74-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e7d74-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="e7d74-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e7d74-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="e7d74-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e7d74-145">**[Создание тестового пользователя Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave аналог Саймон Britta в Mozy Enterprise, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e7d74-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e7d74-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="e7d74-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e7d74-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e7d74-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e7d74-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7d74-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e7d74-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7d74-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="e7d74-150">**tooconfigure Azure AD единого входа с Mozy Enterprise, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e7d74-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7d74-151">В hello в hello портала Azure **Mozy Enterprise** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e7d74-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="e7d74-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="e7d74-155">На hello **Mozy Enterprise доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e7d74-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="e7d74-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="e7d74-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7d74-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="e7d74-158">This value is not real.</span></span> <span data-ttu-id="e7d74-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="e7d74-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e7d74-160">Обратитесь к [группа поддержки клиент Mozy Enterprise](http://support.mozy.com/) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="e7d74-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="e7d74-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="e7d74-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="e7d74-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e7d74-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e7d74-165">На hello **Mozy Enterprise конфигурации** щелкните **Настройка Mozy Enterprise** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="e7d74-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e7d74-166">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="e7d74-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="e7d74-168">В другом окне веб-браузера войдите на сайт Mozy Enterprise компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e7d74-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="e7d74-169">В hello **конфигурации** щелкните **политика проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="e7d74-170">![Политика аутентификации](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Политика аутентификации")</span><span class="sxs-lookup"><span data-stu-id="e7d74-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="e7d74-171">На hello **политика проверки подлинности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e7d74-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e7d74-172">![Политика аутентификации](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Политика аутентификации")</span><span class="sxs-lookup"><span data-stu-id="e7d74-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="e7d74-173">а.</span><span class="sxs-lookup"><span data-stu-id="e7d74-173">a.</span></span> <span data-ttu-id="e7d74-174">Для параметра **Поставщик** выберите значение **Служба каталогов**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="e7d74-175">b.</span><span class="sxs-lookup"><span data-stu-id="e7d74-175">b.</span></span> <span data-ttu-id="e7d74-176">Выберите **Использовать LDAP для отправки**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="e7d74-177">c.</span><span class="sxs-lookup"><span data-stu-id="e7d74-177">c.</span></span> <span data-ttu-id="e7d74-178">Нажмите кнопку hello **проверку подлинности SAML** вкладки.</span><span class="sxs-lookup"><span data-stu-id="e7d74-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="e7d74-179">d.</span><span class="sxs-lookup"><span data-stu-id="e7d74-179">d.</span></span> <span data-ttu-id="e7d74-180">Вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure hello в hello **URL-адрес проверки подлинности** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="e7d74-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="e7d74-181">д.</span><span class="sxs-lookup"><span data-stu-id="e7d74-181">e.</span></span> <span data-ttu-id="e7d74-182">Вставить **идентификатор сущности SAML**, которой копируются hello портал Azure в hello **конечная точка SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="e7d74-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="e7d74-183">f.</span><span class="sxs-lookup"><span data-stu-id="e7d74-183">f.</span></span> <span data-ttu-id="e7d74-184">Откройте загруженный сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте весь сертификат в hello **сертификат SAML** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="e7d74-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="e7d74-185">ж.</span><span class="sxs-lookup"><span data-stu-id="e7d74-185">g.</span></span> <span data-ttu-id="e7d74-186">Выберите **Включить единый вход для администраторов toolog вход с помощью своих сетевых учетных данных**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="e7d74-187">h.</span><span class="sxs-lookup"><span data-stu-id="e7d74-187">h.</span></span> <span data-ttu-id="e7d74-188">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e7d74-189">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="e7d74-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e7d74-190">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="e7d74-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e7d74-191">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e7d74-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e7d74-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e7d74-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="e7d74-193">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e7d74-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e7d74-195">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e7d74-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7d74-196">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="e7d74-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e7d74-198">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e7d74-200">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="e7d74-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e7d74-202">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="e7d74-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e7d74-204">а.</span><span class="sxs-lookup"><span data-stu-id="e7d74-204">a.</span></span> <span data-ttu-id="e7d74-205">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e7d74-206">b.</span><span class="sxs-lookup"><span data-stu-id="e7d74-206">b.</span></span> <span data-ttu-id="e7d74-207">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e7d74-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e7d74-208">c.</span><span class="sxs-lookup"><span data-stu-id="e7d74-208">c.</span></span> <span data-ttu-id="e7d74-209">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e7d74-210">d.</span><span class="sxs-lookup"><span data-stu-id="e7d74-210">d.</span></span> <span data-ttu-id="e7d74-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="e7d74-212">Создание тестового пользователя Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="e7d74-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="e7d74-213">В порядке tooenable toolog пользователей Azure AD в Mozy Enterprise их необходимо подготовить в Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7d74-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="e7d74-214">В случае hello Mozy Enterprise Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="e7d74-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e7d74-215">Можно использовать любые другие Mozy Enterprise пользователя средства создания учетных записей или интерфейсы API, предоставляемые Mozy Enterprise tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="e7d74-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="e7d74-216">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="e7d74-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7d74-217">Войдите в tooyour **Mozy Enterprise** клиента.</span><span class="sxs-lookup"><span data-stu-id="e7d74-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="e7d74-218">Щелкните **Users** (Пользователи), а затем — **Add New User** (Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="e7d74-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="e7d74-219">![Пользователи](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="e7d74-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="e7d74-220">Hello **добавить пользователя** параметр отображается только в том случае, если **Mozy** выбран в качестве поставщика hello под **политика проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="e7d74-221">Если настроена проверка подлинности SAML, затем hello пользователи добавляются автоматически при их первом входе с использованием единого входа на.</span><span class="sxs-lookup"><span data-stu-id="e7d74-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="e7d74-222">На hello пользователя диалоговое окно создания выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="e7d74-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="e7d74-223">![Добавление пользователей](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "добавление пользователей")</span><span class="sxs-lookup"><span data-stu-id="e7d74-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="e7d74-224">а.</span><span class="sxs-lookup"><span data-stu-id="e7d74-224">a.</span></span> <span data-ttu-id="e7d74-225">Из hello **выберите группу** выберите группу.</span><span class="sxs-lookup"><span data-stu-id="e7d74-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="e7d74-226">b.</span><span class="sxs-lookup"><span data-stu-id="e7d74-226">b.</span></span> <span data-ttu-id="e7d74-227">Из hello **выборе типа создаваемого пользователя** выберите тип.</span><span class="sxs-lookup"><span data-stu-id="e7d74-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="e7d74-228">c.</span><span class="sxs-lookup"><span data-stu-id="e7d74-228">c.</span></span> <span data-ttu-id="e7d74-229">В hello **Username** текстовое поле, имя типа hello hello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e7d74-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="e7d74-230">d.</span><span class="sxs-lookup"><span data-stu-id="e7d74-230">d.</span></span> <span data-ttu-id="e7d74-231">В hello **электронной почты** в текстовое поле адрес электронной почты типа hello hello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="e7d74-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="e7d74-232">д.</span><span class="sxs-lookup"><span data-stu-id="e7d74-232">e.</span></span> <span data-ttu-id="e7d74-233">Выберите **Отправить пользователю электронное сообщение с указаниями**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="e7d74-234">f.</span><span class="sxs-lookup"><span data-stu-id="e7d74-234">f.</span></span> <span data-ttu-id="e7d74-235">Щелкните **Добавить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="e7d74-236">После создания пользователя hello, сообщение электронной почты будет отправлено toohello пользователя Azure AD, который включает учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="e7d74-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e7d74-237">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="e7d74-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e7d74-238">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooMozy предприятия.</span><span class="sxs-lookup"><span data-stu-id="e7d74-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e7d74-240">**tooassign Britta Simon tooMozy Enterprise, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="e7d74-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="e7d74-241">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e7d74-243">В списке приложений hello выберите **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="e7d74-245">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e7d74-247">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-247">Click **Add** button.</span></span> <span data-ttu-id="e7d74-248">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e7d74-250">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="e7d74-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e7d74-251">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e7d74-252">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e7d74-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e7d74-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e7d74-253">Testing single sign-on</span></span>

<span data-ttu-id="e7d74-254">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="e7d74-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e7d74-255">При нажатии кнопки Mozy Enterprise плитки в панели доступа hello hello, должно появиться страница входа приложения Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e7d74-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="e7d74-256">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e7d74-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7d74-257">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e7d74-257">Additional resources</span></span>

* [<span data-ttu-id="e7d74-258">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7d74-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e7d74-259">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e7d74-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

