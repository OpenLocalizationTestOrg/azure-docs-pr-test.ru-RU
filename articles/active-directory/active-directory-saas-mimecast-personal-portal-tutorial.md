---
title: "Руководство по интеграции Azure Active Directory с Mimecast Personal Portal | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и личного портала Mimecast."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="0962a-103">Руководство по интеграции Azure Active Directory с Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="0962a-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="0962a-104">В этом учебнике вы узнаете, как toointegrate личного портала Mimecast с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0962a-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0962a-105">Интеграция личного портала Mimecast с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0962a-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0962a-106">Можно управлять в Azure AD, имеющего доступ tooMimecast личного портала</span><span class="sxs-lookup"><span data-stu-id="0962a-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="0962a-107">Ваш пользователей tooautomatically get вошедшего tooMimecast личного портала (Single Sign-On) можно включить с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0962a-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0962a-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0962a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0962a-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0962a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0962a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0962a-110">Prerequisites</span></span>

<span data-ttu-id="0962a-111">tooconfigure интеграция Azure AD с личного портала Mimecast требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0962a-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="0962a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0962a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0962a-113">Подписка на личный портал Mimecast с поддержкой единого входа</span><span class="sxs-lookup"><span data-stu-id="0962a-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0962a-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0962a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0962a-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0962a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0962a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0962a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0962a-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0962a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0962a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0962a-118">Scenario description</span></span>
<span data-ttu-id="0962a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0962a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0962a-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0962a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0962a-121">Добавление личного портала Mimecast из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0962a-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="0962a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0962a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="0962a-123">Добавление личного портала Mimecast из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0962a-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="0962a-124">tooconfigure hello интеграции личного портала Mimecast в Azure AD, вы должны tooadd личного портала Mimecast из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0962a-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0962a-125">**tooadd личного портала Mimecast из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0962a-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0962a-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0962a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0962a-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0962a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0962a-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0962a-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0962a-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0962a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0962a-133">Введите в поле поиска hello **личного портала Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="0962a-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="0962a-135">В панели результатов hello выберите **личного портала Mimecast**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0962a-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0962a-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0962a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0962a-138">В этом разделе описана настройка и проверка единого входа Azure AD в Mimecast Personal Portal с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0962a-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0962a-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в личный портал Mimecast является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0962a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="0962a-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в личный портал Mimecast должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0962a-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="0962a-141">В личный портал Mimecast, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="0962a-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0962a-142">tooconfigure и теста Azure AD единого входа с личного портала Mimecast, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0962a-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0962a-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0962a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0962a-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0962a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0962a-145">**[Создание тестового пользователя личного портала Mimecast](#creating-a-mimecast-personal-portal-test-user)**  -toohave аналог Саймон Britta в личный портал Mimecast, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="0962a-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0962a-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0962a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0962a-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0962a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0962a-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0962a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0962a-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение личного портала Mimecast.</span><span class="sxs-lookup"><span data-stu-id="0962a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="0962a-150">**tooconfigure Azure AD единого входа с помощью личного портала Mimecast, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0962a-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="0962a-151">В hello в hello портала Azure **личного портала Mimecast** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0962a-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0962a-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0962a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="0962a-155">На hello **URL-адреса и личного домена портала Mimecast** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0962a-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="0962a-157">а.</span><span class="sxs-lookup"><span data-stu-id="0962a-157">a.</span></span> <span data-ttu-id="0962a-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="0962a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="0962a-159">b.</span><span class="sxs-lookup"><span data-stu-id="0962a-159">b.</span></span> <span data-ttu-id="0962a-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="0962a-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="0962a-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0962a-161">These values are not real.</span></span> <span data-ttu-id="0962a-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="0962a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0962a-163">Обратитесь к [группа поддержки личных клиентского портала Mimecast](https://www.mimecast.com/customer-success/technical-support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="0962a-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="0962a-164">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0962a-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="0962a-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0962a-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0962a-168">На hello **конфигурации личного портала Mimecast** щелкните **настройки личного портала Mimecast** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="0962a-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0962a-169">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="0962a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="0962a-171">В другом окне веб-браузера войдите в личный портал Mimecast в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="0962a-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="0962a-172">Go слишком**службы \> приложений**.</span><span class="sxs-lookup"><span data-stu-id="0962a-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="0962a-173">![Приложения](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="0962a-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="0962a-174">Щелкните **Профили проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="0962a-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="0962a-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles") (Профили аутентификации)</span><span class="sxs-lookup"><span data-stu-id="0962a-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="0962a-176">Щелкните **Новый профиль проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="0962a-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="0962a-177">![Создание профиля аутентификации](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span><span class="sxs-lookup"><span data-stu-id="0962a-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="0962a-178">В hello **профиль проверки подлинности** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0962a-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0962a-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile") (Профиль аутентификации)</span><span class="sxs-lookup"><span data-stu-id="0962a-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="0962a-180">а.</span><span class="sxs-lookup"><span data-stu-id="0962a-180">a.</span></span> <span data-ttu-id="0962a-181">В hello **описание** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0962a-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="0962a-182">b.</span><span class="sxs-lookup"><span data-stu-id="0962a-182">b.</span></span> <span data-ttu-id="0962a-183">Выберите **Обязательное использование проверки подлинности SAML для личного портала Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="0962a-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="0962a-184">c.</span><span class="sxs-lookup"><span data-stu-id="0962a-184">c.</span></span> <span data-ttu-id="0962a-185">В поле **Provider** (Поставщик) выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0962a-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="0962a-186">d.</span><span class="sxs-lookup"><span data-stu-id="0962a-186">d.</span></span> <span data-ttu-id="0962a-187">В **URL-адрес издателя** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0962a-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="0962a-188">д.</span><span class="sxs-lookup"><span data-stu-id="0962a-188">e.</span></span> <span data-ttu-id="0962a-189">В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0962a-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="0962a-190">f.</span><span class="sxs-lookup"><span data-stu-id="0962a-190">f.</span></span> <span data-ttu-id="0962a-191">В **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0962a-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0962a-192">ж.</span><span class="sxs-lookup"><span data-stu-id="0962a-192">g.</span></span> <span data-ttu-id="0962a-193">Откройте ваш **base-64** закодированный сертификат в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений (метаданные)** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="0962a-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="0962a-194">h.</span><span class="sxs-lookup"><span data-stu-id="0962a-194">h.</span></span> <span data-ttu-id="0962a-195">Установите флажок **Разрешить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0962a-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="0962a-196">i.</span><span class="sxs-lookup"><span data-stu-id="0962a-196">i.</span></span> <span data-ttu-id="0962a-197">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0962a-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0962a-198">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="0962a-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0962a-199">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0962a-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0962a-200">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0962a-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0962a-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0962a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="0962a-202">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0962a-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0962a-204">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0962a-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0962a-205">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0962a-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0962a-207">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0962a-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0962a-209">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="0962a-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0962a-211">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0962a-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0962a-213">а.</span><span class="sxs-lookup"><span data-stu-id="0962a-213">a.</span></span> <span data-ttu-id="0962a-214">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0962a-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0962a-215">b.</span><span class="sxs-lookup"><span data-stu-id="0962a-215">b.</span></span> <span data-ttu-id="0962a-216">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0962a-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0962a-217">c.</span><span class="sxs-lookup"><span data-stu-id="0962a-217">c.</span></span> <span data-ttu-id="0962a-218">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0962a-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0962a-219">d.</span><span class="sxs-lookup"><span data-stu-id="0962a-219">d.</span></span> <span data-ttu-id="0962a-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0962a-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="0962a-221">Создание тестового пользователя Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="0962a-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="0962a-222">В порядке tooenable toolog пользователей Azure AD на личный портал Mimecast их необходимо подготовить в личный портал Mimecast.</span><span class="sxs-lookup"><span data-stu-id="0962a-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="0962a-223">В случае hello личного портала Mimecast Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="0962a-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="0962a-224">Перед созданием пользователей необходимо tooregister домена.</span><span class="sxs-lookup"><span data-stu-id="0962a-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="0962a-225">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0962a-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="0962a-226">Войдите на tooyour **личного портала Mimecast** от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="0962a-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="0962a-227">Go слишком**каталогов \> внутренний**.</span><span class="sxs-lookup"><span data-stu-id="0962a-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="0962a-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories") (Каталоги)</span><span class="sxs-lookup"><span data-stu-id="0962a-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="0962a-229">Щелкните **Зарегистрировать новый домен**.</span><span class="sxs-lookup"><span data-stu-id="0962a-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="0962a-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain") (Зарегистрировать новый домен)</span><span class="sxs-lookup"><span data-stu-id="0962a-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="0962a-231">После создания нового домена щелкните **Новый адрес**.</span><span class="sxs-lookup"><span data-stu-id="0962a-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="0962a-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address") (Новый адрес)</span><span class="sxs-lookup"><span data-stu-id="0962a-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="0962a-233">В новый диалог адрес hello, выполнять hello инструкциям допустимым Azure AD счета, tooprovision:</span><span class="sxs-lookup"><span data-stu-id="0962a-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="0962a-234">![Сохранить](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Сохранить")</span><span class="sxs-lookup"><span data-stu-id="0962a-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="0962a-235">а.</span><span class="sxs-lookup"><span data-stu-id="0962a-235">a.</span></span> <span data-ttu-id="0962a-236">В hello **адрес электронной почты** введите **адрес электронной почты** hello пользователя как  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="0962a-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="0962a-237">b.</span><span class="sxs-lookup"><span data-stu-id="0962a-237">b.</span></span> <span data-ttu-id="0962a-238">В hello **глобальное имя** в текстовое поле типа hello **username** как **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0962a-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="0962a-239">c.</span><span class="sxs-lookup"><span data-stu-id="0962a-239">c.</span></span> <span data-ttu-id="0962a-240">В hello **пароль**, и **подтверждение пароля** текстовые поля, типа hello **пароль** hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="0962a-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="0962a-241">b.</span><span class="sxs-lookup"><span data-stu-id="0962a-241">b.</span></span> <span data-ttu-id="0962a-242">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0962a-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="0962a-243">Можно использовать другие инструменты создания учетных записей личного портала Mimecast или интерфейсы API, предоставляемые учетных записей пользователей Azure AD tooprovision личного портала Mimecast.</span><span class="sxs-lookup"><span data-stu-id="0962a-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0962a-244">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0962a-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0962a-245">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooMimecast личного портала.</span><span class="sxs-lookup"><span data-stu-id="0962a-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0962a-247">**tooassign tooMimecast Britta Simon личного портала выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="0962a-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="0962a-248">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0962a-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0962a-250">В списке приложений hello выберите **личного портала Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="0962a-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="0962a-252">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0962a-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0962a-254">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0962a-254">Click **Add** button.</span></span> <span data-ttu-id="0962a-255">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0962a-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0962a-257">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0962a-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0962a-258">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0962a-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0962a-259">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0962a-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0962a-260">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0962a-260">Testing single sign-on</span></span>
<span data-ttu-id="0962a-261">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0962a-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0962a-262">При нажатии кнопки hello личного портала Mimecast плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на личный портал Mimecast приложения.</span><span class="sxs-lookup"><span data-stu-id="0962a-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="0962a-263">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0962a-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0962a-264">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0962a-264">Additional resources</span></span>

* [<span data-ttu-id="0962a-265">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0962a-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0962a-266">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0962a-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

