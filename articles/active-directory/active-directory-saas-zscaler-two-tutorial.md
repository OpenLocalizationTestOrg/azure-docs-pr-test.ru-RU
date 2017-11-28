---
title: "Руководство по интеграции Azure Active Directory с Zscaler Two | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zscaler Two."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1fd8a940-7320-47e0-a176-2dd4eeca6db2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: dcd13d399f093f24a945f234401cd5b7e527ed34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-two"></a><span data-ttu-id="73e03-103">Руководство по интеграции Azure Active Directory с Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="73e03-103">Tutorial: Azure Active Directory integration with Zscaler Two</span></span>

<span data-ttu-id="73e03-104">В этом учебнике вы узнаете, как toointegrate Zscaler Two с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="73e03-104">In this tutorial, you learn how toointegrate Zscaler Two with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="73e03-105">Интеграция Zscaler Two с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="73e03-105">Integrating Zscaler Two with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="73e03-106">Можно управлять в Azure AD, имеющего доступ tooZscaler два</span><span class="sxs-lookup"><span data-stu-id="73e03-106">You can control in Azure AD who has access tooZscaler Two</span></span>
- <span data-ttu-id="73e03-107">Можно включить вашей пользователей tooautomatically get вошедшего tooZscaler двух (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="73e03-107">You can enable your users tooautomatically get signed-on tooZscaler Two (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="73e03-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="73e03-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="73e03-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="73e03-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73e03-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="73e03-110">Prerequisites</span></span>

<span data-ttu-id="73e03-111">tooconfigure интеграция Azure AD с Zscaler Two, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="73e03-111">tooconfigure Azure AD integration with Zscaler Two, you need hello following items:</span></span>

- <span data-ttu-id="73e03-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="73e03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="73e03-113">подписка Zscaler Two с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="73e03-113">A Zscaler Two single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="73e03-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="73e03-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="73e03-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="73e03-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="73e03-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="73e03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="73e03-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73e03-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="73e03-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="73e03-118">Scenario description</span></span>
<span data-ttu-id="73e03-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="73e03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="73e03-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="73e03-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="73e03-121">Добавление Zscaler Two из галереи hello</span><span class="sxs-lookup"><span data-stu-id="73e03-121">Adding Zscaler Two from hello gallery</span></span>
2. <span data-ttu-id="73e03-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73e03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-two-from-hello-gallery"></a><span data-ttu-id="73e03-123">Добавление Zscaler Two из галереи hello</span><span class="sxs-lookup"><span data-stu-id="73e03-123">Adding Zscaler Two from hello gallery</span></span>
<span data-ttu-id="73e03-124">tooconfigure hello интеграции Zscaler Two в Azure AD, вы должны tooadd Zscaler Two из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="73e03-124">tooconfigure hello integration of Zscaler Two into Azure AD, you need tooadd Zscaler Two from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="73e03-125">**tooadd Zscaler Two из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73e03-125">**tooadd Zscaler Two from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="73e03-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="73e03-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="73e03-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="73e03-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="73e03-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="73e03-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="73e03-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="73e03-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="73e03-133">Введите в поле поиска hello **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="73e03-133">In hello search box, type **Zscaler Two**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_search.png)

5. <span data-ttu-id="73e03-135">В панели результатов hello выберите **Zscaler Two**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="73e03-135">In hello results panel, select **Zscaler Two**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="73e03-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73e03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="73e03-138">В этом разделе описана настройка и проверка единого входа Azure AD в Zscaler Two с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="73e03-138">In this section, you configure and test Azure AD single sign-on with Zscaler Two based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="73e03-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Zscaler Two является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73e03-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Two is tooa user in Azure AD.</span></span> <span data-ttu-id="73e03-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Zscaler Two должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="73e03-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Two needs toobe established.</span></span>

<span data-ttu-id="73e03-141">В Zscaler Two, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="73e03-141">In Zscaler Two, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="73e03-142">tooconfigure и теста Azure AD единого входа с Zscaler Two, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="73e03-142">tooconfigure and test Azure AD single sign-on with Zscaler Two, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="73e03-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="73e03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="73e03-144">**[Настройка параметров прокси-сервера](#configuring-proxy-settings)**  -tooconfigure hello параметров прокси-сервера обозревателя Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="73e03-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="73e03-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="73e03-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="73e03-146">**[Создание тестового пользователя Zscaler Two](#creating-a-zscaler-two-test-user)**  -toohave аналог Саймон Britta в Zscaler Two, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="73e03-146">**[Creating a Zscaler Two test user](#creating-a-zscaler-two-test-user)** - toohave a counterpart of Britta Simon in Zscaler Two that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="73e03-147">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="73e03-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="73e03-148">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="73e03-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="73e03-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="73e03-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="73e03-150">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="73e03-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler Two application.</span></span>

<span data-ttu-id="73e03-151">**tooconfigure Azure AD единого входа с Zscaler Two, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73e03-151">**tooconfigure Azure AD single sign-on with Zscaler Two, perform hello following steps:**</span></span>

1. <span data-ttu-id="73e03-152">В hello в hello портала Azure **Zscaler Two** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="73e03-152">In hello Azure portal, on hello **Zscaler Two** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="73e03-154">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="73e03-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_samlbase.png)

3. <span data-ttu-id="73e03-156">На hello **Zscaler двух доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="73e03-156">On hello **Zscaler Two Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_url.png)

   <span data-ttu-id="73e03-158">В текстовом поле URL-адрес входа hello введите URL-адрес hello, используемых вашей пользователей на toosign tooyour ZScaler Two приложения.</span><span class="sxs-lookup"><span data-stu-id="73e03-158">In hello Sign-on URL textbox, type hello URL used by your users toosign-on tooyour ZScaler Two application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="73e03-159">Имеется tooupdate это значение с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="73e03-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="73e03-160">Обратитесь к [группы поддержки Zscaler два клиента](https://www.zscaler.com/company/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="73e03-160">Contact [Zscaler Two Client support team](https://www.zscaler.com/company/contact) tooget these values.</span></span>

4. <span data-ttu-id="73e03-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="73e03-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_certificate.png) 

5. <span data-ttu-id="73e03-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="73e03-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="73e03-165">На hello **две конфигурации Zscaler** щелкните **Настройка Zscaler Two** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="73e03-165">On hello **Zscaler Two Configuration** section, click **Configure Zscaler Two** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="73e03-166">Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="73e03-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_configure.png) 

7. <span data-ttu-id="73e03-168">В другом окне браузера войдите в сайт ZScaler Two компании tooyour в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="73e03-168">In a different web browser window, log in tooyour ZScaler Two company site as an administrator.</span></span>

8. <span data-ttu-id="73e03-169">В меню в верхней части hello hello выберите **администрирования**.</span><span class="sxs-lookup"><span data-stu-id="73e03-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="73e03-170">![Администрирование](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="73e03-170">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="73e03-171">В разделе **Manage Administrators & Roles** (Управление администраторами и ролями) щелкните **Manage Users & Authentication** (Управление пользователями и проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="73e03-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="73e03-172">![Управление пользователями и проверкой подлинности](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Управление пользователями и проверкой подлинности")</span><span class="sxs-lookup"><span data-stu-id="73e03-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="73e03-173">В hello **Выбор параметров проверки подлинности для вашей организации** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="73e03-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="73e03-174">![Аутентификация](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="73e03-174">![Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="73e03-175">а.</span><span class="sxs-lookup"><span data-stu-id="73e03-175">a.</span></span> <span data-ttu-id="73e03-176">Выберите параметр **Проверка подлинности с помощью единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="73e03-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="73e03-177">b.</span><span class="sxs-lookup"><span data-stu-id="73e03-177">b.</span></span> <span data-ttu-id="73e03-178">Щелкните **Настроить параметры единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="73e03-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="73e03-179">На hello **SAML единого входа параметры настройки** странице диалогового окна, выполните следующие шаги hello и нажмите кнопку **сделать**</span><span class="sxs-lookup"><span data-stu-id="73e03-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="73e03-180">![Единый вход](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="73e03-180">![Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="73e03-181">а.</span><span class="sxs-lookup"><span data-stu-id="73e03-181">a.</span></span> <span data-ttu-id="73e03-182">Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес hello портала SAML toowhich пользователей будет отправлено для проверки подлинности** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="73e03-182">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="73e03-183">b.</span><span class="sxs-lookup"><span data-stu-id="73e03-183">b.</span></span> <span data-ttu-id="73e03-184">В hello **атрибут, содержащий имя входа** введите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="73e03-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="73e03-185">c.</span><span class="sxs-lookup"><span data-stu-id="73e03-185">c.</span></span> <span data-ttu-id="73e03-186">tooupload загруженный сертификат, нажмите кнопку **PEM-файл Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="73e03-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="73e03-187">d.</span><span class="sxs-lookup"><span data-stu-id="73e03-187">d.</span></span> <span data-ttu-id="73e03-188">Выберите параметр **Включить автоматическую подготовку SAML**.</span><span class="sxs-lookup"><span data-stu-id="73e03-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="73e03-189">На hello **Настройка проверки подлинности пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="73e03-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="73e03-190">![Администрирование](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="73e03-190">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="73e03-191">а.</span><span class="sxs-lookup"><span data-stu-id="73e03-191">a.</span></span> <span data-ttu-id="73e03-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="73e03-192">Click **Save**.</span></span>

    <span data-ttu-id="73e03-193">b.</span><span class="sxs-lookup"><span data-stu-id="73e03-193">b.</span></span> <span data-ttu-id="73e03-194">Щелкните **Активировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="73e03-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="73e03-195">Настройка параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="73e03-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="73e03-196">параметры прокси-сервера tooconfigure hello в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="73e03-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="73e03-197">Запустите **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="73e03-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="73e03-198">Выберите **обозревателя** из hello **средства** меню откройте hello **обозревателя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="73e03-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="73e03-199">![Свойства браузера](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Свойства браузера")</span><span class="sxs-lookup"><span data-stu-id="73e03-199">![Internet Options](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="73e03-200">Нажмите кнопку hello **подключений** вкладки.</span><span class="sxs-lookup"><span data-stu-id="73e03-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="73e03-201">![Подключения](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Подключения")</span><span class="sxs-lookup"><span data-stu-id="73e03-201">![Connections](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="73e03-202">Нажмите кнопку **параметры локальной сети** tooopen hello **параметры локальной сети** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="73e03-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="73e03-203">В hello раздела прокси-сервера выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="73e03-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="73e03-204">![Прокси-сервер](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Прокси-сервер")</span><span class="sxs-lookup"><span data-stu-id="73e03-204">![Proxy server](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="73e03-205">а.</span><span class="sxs-lookup"><span data-stu-id="73e03-205">a.</span></span> <span data-ttu-id="73e03-206">Установите флажок **Использовать прокси-сервер для локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="73e03-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="73e03-207">b.</span><span class="sxs-lookup"><span data-stu-id="73e03-207">b.</span></span> <span data-ttu-id="73e03-208">Введите в текстовое поле адрес hello **gateway.zscalertwo.net**.</span><span class="sxs-lookup"><span data-stu-id="73e03-208">In hello Address textbox, type **gateway.zscalertwo.net**.</span></span>

    <span data-ttu-id="73e03-209">c.</span><span class="sxs-lookup"><span data-stu-id="73e03-209">c.</span></span> <span data-ttu-id="73e03-210">Введите в текстовое поле hello порт **80**.</span><span class="sxs-lookup"><span data-stu-id="73e03-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="73e03-211">d.</span><span class="sxs-lookup"><span data-stu-id="73e03-211">d.</span></span> <span data-ttu-id="73e03-212">Установите флаг **Не использовать прокси-сервер для локальных адресов**.</span><span class="sxs-lookup"><span data-stu-id="73e03-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="73e03-213">д.</span><span class="sxs-lookup"><span data-stu-id="73e03-213">e.</span></span> <span data-ttu-id="73e03-214">Нажмите кнопку **ОК** tooclose hello **параметры локальной сети (LAN)** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="73e03-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="73e03-215">Нажмите кнопку **ОК** tooclose hello **обозревателя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="73e03-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="73e03-216">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="73e03-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="73e03-217">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="73e03-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="73e03-218">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="73e03-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="73e03-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="73e03-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="73e03-220">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="73e03-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="73e03-222">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="73e03-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="73e03-223">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="73e03-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="73e03-225">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="73e03-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="73e03-227">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="73e03-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="73e03-229">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="73e03-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="73e03-231">а.</span><span class="sxs-lookup"><span data-stu-id="73e03-231">a.</span></span> <span data-ttu-id="73e03-232">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="73e03-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="73e03-233">b.</span><span class="sxs-lookup"><span data-stu-id="73e03-233">b.</span></span> <span data-ttu-id="73e03-234">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="73e03-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="73e03-235">c.</span><span class="sxs-lookup"><span data-stu-id="73e03-235">c.</span></span> <span data-ttu-id="73e03-236">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="73e03-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="73e03-237">d.</span><span class="sxs-lookup"><span data-stu-id="73e03-237">d.</span></span> <span data-ttu-id="73e03-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="73e03-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-two-test-user"></a><span data-ttu-id="73e03-239">Создание тестового пользователя Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="73e03-239">Creating a Zscaler Two test user</span></span>

<span data-ttu-id="73e03-240">Пользователи toolog tooenable Azure AD в tooZScaler два, они должны быть подготовленных tooZScaler двух.</span><span class="sxs-lookup"><span data-stu-id="73e03-240">tooenable Azure AD users toolog in tooZScaler Two, they must be provisioned tooZScaler Two.</span></span> <span data-ttu-id="73e03-241">В случае hello объекта ZScaler Two Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="73e03-241">In hello case of ZScaler Two, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="73e03-242">tooconfigure подготовки пользователей, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="73e03-242">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="73e03-243">Войдите в tooyour **Zscaler Two** клиента.</span><span class="sxs-lookup"><span data-stu-id="73e03-243">Log in tooyour **Zscaler Two** tenant.</span></span>

2. <span data-ttu-id="73e03-244">Щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="73e03-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="73e03-245">![Администрирование](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="73e03-245">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="73e03-246">Щелкните **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="73e03-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="73e03-247">![Добавление](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="73e03-247">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="73e03-248">В hello **пользователей** щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="73e03-248">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="73e03-249">![Добавление](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="73e03-249">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="73e03-250">В hello раздел добавить пользователя выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="73e03-250">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="73e03-251">![Добавление пользователя](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="73e03-251">![Add User](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="73e03-252">а.</span><span class="sxs-lookup"><span data-stu-id="73e03-252">a.</span></span> <span data-ttu-id="73e03-253">Hello тип **UserID**, **отображаемое имя пользователя**, **пароль**, **подтверждение пароля**, а затем выберите **группы**и hello **отдел** из допустимых Azure AD счета, tooprovision.</span><span class="sxs-lookup"><span data-stu-id="73e03-253">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="73e03-254">b.</span><span class="sxs-lookup"><span data-stu-id="73e03-254">b.</span></span> <span data-ttu-id="73e03-255">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="73e03-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="73e03-256">Можно использовать любые другие ZScaler Two пользователя средства создания учетных записей или интерфейсы API, предоставляемые ZScaler Two tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73e03-256">You can use any other ZScaler Two user account creation tools or APIs provided by ZScaler Two tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="73e03-257">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="73e03-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="73e03-258">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooZscaler двух.</span><span class="sxs-lookup"><span data-stu-id="73e03-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler Two.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="73e03-260">**tooassign tooZscaler Britta Simon Two, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="73e03-260">**tooassign Britta Simon tooZscaler Two, perform hello following steps:**</span></span>

1. <span data-ttu-id="73e03-261">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="73e03-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="73e03-263">В списке приложений hello выберите **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="73e03-263">In hello applications list, select **Zscaler Two**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_app.png) 

3. <span data-ttu-id="73e03-265">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="73e03-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="73e03-267">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="73e03-267">Click **Add** button.</span></span> <span data-ttu-id="73e03-268">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="73e03-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="73e03-270">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="73e03-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="73e03-271">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="73e03-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="73e03-272">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="73e03-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="73e03-273">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="73e03-273">Testing single sign-on</span></span>

<span data-ttu-id="73e03-274">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="73e03-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="73e03-275">При нажатии кнопки Zscaler Two плитки в панели доступа hello приветствия, вы должны получить tooyour автоматически подписан в приложение Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="73e03-275">When you click hello Zscaler Two tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Two application.</span></span>
<span data-ttu-id="73e03-276">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="73e03-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73e03-277">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="73e03-277">Additional resources</span></span>

* [<span data-ttu-id="73e03-278">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73e03-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="73e03-279">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="73e03-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_203.png

