---
title: "Руководство. Интеграция Azure Active Directory с Workday | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и рабочего дня."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="b0683-103">Руководство. Интеграция Azure Active Directory с Workday</span><span class="sxs-lookup"><span data-stu-id="b0683-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="b0683-104">В этом учебнике вы узнаете, как toointegrate дня с помощью Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0683-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0683-105">Интеграция рабочего дня с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b0683-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0683-106">Можно управлять в Azure AD, имеющего доступ tooWorkday</span><span class="sxs-lookup"><span data-stu-id="b0683-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="b0683-107">Можно включить на пользователей tooautomatically get вошедшего tooWorkday (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0683-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0683-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b0683-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b0683-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0683-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0683-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b0683-110">Prerequisites</span></span>

<span data-ttu-id="b0683-111">tooconfigure интеграция Azure AD с Workday требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b0683-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="b0683-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b0683-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0683-113">подписка Workday с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b0683-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0683-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b0683-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0683-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b0683-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0683-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b0683-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0683-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0683-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0683-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b0683-118">Scenario description</span></span>
<span data-ttu-id="b0683-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b0683-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0683-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b0683-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0683-121">Добавление рабочего дня из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b0683-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="b0683-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0683-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="b0683-123">Добавление рабочего дня из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b0683-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="b0683-124">tooconfigure hello интеграции рабочего дня в Azure AD, вы должны tooadd рабочего дня из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b0683-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0683-125">**tooadd рабочего дня из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b0683-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0683-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b0683-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0683-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b0683-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0683-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b0683-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b0683-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b0683-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b0683-133">Введите в поле поиска hello **Workday**.</span><span class="sxs-lookup"><span data-stu-id="b0683-133">In hello search box, type **Workday**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="b0683-135">В панели результатов hello, выберите **Workday**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b0683-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0683-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0683-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0683-138">В этом разделе описана настройка и проверка единого входа Azure AD в Workday с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0683-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b0683-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочий день является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0683-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="b0683-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочий день должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b0683-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="b0683-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в рабочий день.</span><span class="sxs-lookup"><span data-stu-id="b0683-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="b0683-142">tooconfigure и теста Azure AD единого входа с рабочего дня, необходимы следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b0683-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0683-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b0683-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0683-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b0683-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0683-145">**[Создание тестового пользователя Workday](#creating-a-workday-test-user)**  -toohave аналог Саймон Britta в рабочий день, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="b0683-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0683-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b0683-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0683-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b0683-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0683-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0683-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0683-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении рабочего дня.</span><span class="sxs-lookup"><span data-stu-id="b0683-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="b0683-150">**tooconfigure Azure AD единого входа с Workday, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b0683-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0683-151">В hello в hello портала Azure **Workday** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b0683-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b0683-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b0683-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="b0683-155">На hello **URL-адреса и домена рабочий день** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b0683-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="b0683-157">а.</span><span class="sxs-lookup"><span data-stu-id="b0683-157">a.</span></span> <span data-ttu-id="b0683-158">В hello **URL-адрес входа** текстовое поле, значение типа hello как:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="b0683-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="b0683-159">b.</span><span class="sxs-lookup"><span data-stu-id="b0683-159">b.</span></span> <span data-ttu-id="b0683-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="b0683-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0683-161">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="b0683-161">These values are not hello real.</span></span> <span data-ttu-id="b0683-162">Обновите эти значения с hello фактический URL-адрес входа и URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="b0683-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="b0683-163">URL-адрес ответа должен содержать поддомен (например, www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span><span class="sxs-lookup"><span data-stu-id="b0683-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="b0683-164">Можно указать адрес вида *http://www.myworkday.com*, но формат *http://myworkday.com* не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b0683-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="b0683-165">Обратитесь к [группа поддержки клиента Workday](https://www.workday.com/en-us/partners-services/services/support.html) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="b0683-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="b0683-166">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b0683-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="b0683-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b0683-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0683-170">На hello **конфигурации рабочего дня** щелкните **Настройка Workday** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="b0683-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b0683-171">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="b0683-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="b0683-172">![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="b0683-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="b0683-173">В другом окне браузера войти в корпоративный сайт Workday tooyour с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="b0683-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="b0683-174">Go слишком**меню \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="b0683-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="b0683-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="b0683-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="b0683-176">Go слишком**Администрирование учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="b0683-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="b0683-177">![Администрирование учетной записи](./media/active-directory-saas-workday-tutorial/IC782924.png "Администрирование учетной записи")</span><span class="sxs-lookup"><span data-stu-id="b0683-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="b0683-178">Go слишком**изменение настройки клиента — безопасность**.</span><span class="sxs-lookup"><span data-stu-id="b0683-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="b0683-179">![Изменение параметров безопасности клиента](./media/active-directory-saas-workday-tutorial/IC782925.png "Изменение параметров безопасности клиента")</span><span class="sxs-lookup"><span data-stu-id="b0683-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="b0683-180">В hello **URL-адреса перенаправления** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b0683-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b0683-181">![URL-адреса перенаправления](./media/active-directory-saas-workday-tutorial/IC7829581.png "URL-адреса перенаправления")</span><span class="sxs-lookup"><span data-stu-id="b0683-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="b0683-182">а.</span><span class="sxs-lookup"><span data-stu-id="b0683-182">a.</span></span> <span data-ttu-id="b0683-183">Нажмите кнопку **Добавить строку**.</span><span class="sxs-lookup"><span data-stu-id="b0683-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="b0683-184">b.</span><span class="sxs-lookup"><span data-stu-id="b0683-184">b.</span></span> <span data-ttu-id="b0683-185">В hello **URL-адрес перенаправления входа** текстового поля и hello **URL-адрес перенаправления Mobile** в текстовое поле типа hello **URL-адрес входа** , указанный на hello **домена рабочего дня и URL-адреса** раздел hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b0683-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="b0683-186">c.</span><span class="sxs-lookup"><span data-stu-id="b0683-186">c.</span></span> <span data-ttu-id="b0683-187">В hello в hello портала Azure **Настройка входа** окна, hello копирования **URL-адрес выхода**и вставьте его в hello **URL-адрес перенаправления выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b0683-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="b0683-188">d.</span><span class="sxs-lookup"><span data-stu-id="b0683-188">d.</span></span>  <span data-ttu-id="b0683-189">В **среды** в текстовое поле имя среды типа hello.</span><span class="sxs-lookup"><span data-stu-id="b0683-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="b0683-190">Hello значение hello атрибута среды привязано значение toohello URL-адреса клиента hello:</span><span class="sxs-lookup"><span data-stu-id="b0683-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="b0683-191">-Если hello доменное имя URL-адрес клиента Workday hello начинается с impl пример: *https://impl.workday.com/\<клиента\>/login-saml2.htmld*), hello **среды** атрибут должен иметь значение tooImplementation.</span><span class="sxs-lookup"><span data-stu-id="b0683-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="b0683-192">-Если hello имя домена начинается по-другому, необходимо toocontact [группа поддержки клиента Workday](https://www.workday.com/en-us/partners-services/services/support.html) сопоставления hello tooget **среды** значение.</span><span class="sxs-lookup"><span data-stu-id="b0683-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="b0683-193">В hello **Настройка SAML** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b0683-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b0683-194">![Настройка SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="b0683-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="b0683-195">а.</span><span class="sxs-lookup"><span data-stu-id="b0683-195">a.</span></span>  <span data-ttu-id="b0683-196">Установите флажок **Включить проверку подлинности SAML**.</span><span class="sxs-lookup"><span data-stu-id="b0683-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="b0683-197">b.</span><span class="sxs-lookup"><span data-stu-id="b0683-197">b.</span></span>  <span data-ttu-id="b0683-198">Нажмите кнопку **Добавить строку**.</span><span class="sxs-lookup"><span data-stu-id="b0683-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="b0683-199">В hello раздел Поставщики удостоверений SAML выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b0683-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b0683-200">![Поставщики удостоверений SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Поставщики удостоверений SAML")</span><span class="sxs-lookup"><span data-stu-id="b0683-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="b0683-201">а.</span><span class="sxs-lookup"><span data-stu-id="b0683-201">a.</span></span> <span data-ttu-id="b0683-202">В текстовом поле имя поставщика удостоверений hello, введите имя поставщика (например: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="b0683-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="b0683-203">b.</span><span class="sxs-lookup"><span data-stu-id="b0683-203">b.</span></span> <span data-ttu-id="b0683-204">В hello в hello портала Azure **Настройка входа** окна, hello копирования **идентификатор сущности SAML** значение, а затем вставьте его в hello **издателя** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="b0683-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="b0683-205">c.</span><span class="sxs-lookup"><span data-stu-id="b0683-205">c.</span></span> <span data-ttu-id="b0683-206">Установите флажок **Enable Workday Initiated Logout** (Включить выход, инициируемый Workday).</span><span class="sxs-lookup"><span data-stu-id="b0683-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="b0683-207">d.</span><span class="sxs-lookup"><span data-stu-id="b0683-207">d.</span></span> <span data-ttu-id="b0683-208">В hello в hello портала Azure **Настройка входа** окна, hello копирования **URL-адрес выхода** значение, а затем вставьте его в hello **URL-адрес запроса выхода** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b0683-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="b0683-209">д.</span><span class="sxs-lookup"><span data-stu-id="b0683-209">e.</span></span> <span data-ttu-id="b0683-210">Щелкните **Identity Provider Public Key Certificate** (Сертификат открытого ключа поставщика удостоверений), а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b0683-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="b0683-211">![Создание](./media/active-directory-saas-workday-tutorial/IC782928.png "Создание")</span><span class="sxs-lookup"><span data-stu-id="b0683-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="b0683-212">Е.</span><span class="sxs-lookup"><span data-stu-id="b0683-212">f.</span></span> <span data-ttu-id="b0683-213">Щелкните **Create x509 Public Key**(Создать открытый ключ x509).</span><span class="sxs-lookup"><span data-stu-id="b0683-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="b0683-214">![Создание](./media/active-directory-saas-workday-tutorial/IC782929.png "Создание")</span><span class="sxs-lookup"><span data-stu-id="b0683-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="b0683-215">В hello **x509 Просмотр открытого ключа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b0683-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="b0683-216">![Просмотр открытого ключа x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Просмотр открытого ключа x509")</span><span class="sxs-lookup"><span data-stu-id="b0683-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="b0683-217">а.</span><span class="sxs-lookup"><span data-stu-id="b0683-217">a.</span></span> <span data-ttu-id="b0683-218">В hello **имя** текстовом поле введите имя для сертификата (например: *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="b0683-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="b0683-219">b.</span><span class="sxs-lookup"><span data-stu-id="b0683-219">b.</span></span> <span data-ttu-id="b0683-220">В hello **Valid From** текстового поля, типа hello значение сертификата.</span><span class="sxs-lookup"><span data-stu-id="b0683-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="b0683-221">c.</span><span class="sxs-lookup"><span data-stu-id="b0683-221">c.</span></span>  <span data-ttu-id="b0683-222">В hello **Valid To** текстовое значение допустимым tooattribute hello типа сертификата.</span><span class="sxs-lookup"><span data-stu-id="b0683-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="b0683-223">Можно получить hello допустимые дату и hello допустимым toodate из сертификата загружен hello, дважды щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="b0683-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="b0683-224">Hello даты будут указаны в списке hello **сведения** вкладки.</span><span class="sxs-lookup"><span data-stu-id="b0683-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="b0683-225">d.</span><span class="sxs-lookup"><span data-stu-id="b0683-225">d.</span></span>  <span data-ttu-id="b0683-226">Откройте сертификат в кодировке base-64 в блокноте, а затем hello копирования содержимого его.</span><span class="sxs-lookup"><span data-stu-id="b0683-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="b0683-227">д.</span><span class="sxs-lookup"><span data-stu-id="b0683-227">e.</span></span>  <span data-ttu-id="b0683-228">В hello **сертификат** textbox hello вставить содержимое буфера обмена.</span><span class="sxs-lookup"><span data-stu-id="b0683-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="b0683-229">f.</span><span class="sxs-lookup"><span data-stu-id="b0683-229">f.</span></span>  <span data-ttu-id="b0683-230">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b0683-230">Click **OK**.</span></span>

15. <span data-ttu-id="b0683-231">Выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="b0683-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="b0683-232">![Настройка единого входа](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="b0683-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="b0683-233">а.</span><span class="sxs-lookup"><span data-stu-id="b0683-233">a.</span></span>  <span data-ttu-id="b0683-234">Включить hello **x509 закрытого ключа**.</span><span class="sxs-lookup"><span data-stu-id="b0683-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="b0683-235">b.</span><span class="sxs-lookup"><span data-stu-id="b0683-235">b.</span></span>  <span data-ttu-id="b0683-236">В hello **идентификатора поставщика услуг** введите **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="b0683-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="b0683-237">c.</span><span class="sxs-lookup"><span data-stu-id="b0683-237">c.</span></span>  <span data-ttu-id="b0683-238">Установите флажок **Включить проверку подлинности SAML, инициированную поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="b0683-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="b0683-239">d.</span><span class="sxs-lookup"><span data-stu-id="b0683-239">d.</span></span>  <span data-ttu-id="b0683-240">В hello в hello портала Azure **Настройка входа** окна, hello копирования **SAML единого входа URL-адрес службы** значение, а затем вставьте его в hello **URL-адрес службы единого входа поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="b0683-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="b0683-241">д.</span><span class="sxs-lookup"><span data-stu-id="b0683-241">e.</span></span> <span data-ttu-id="b0683-242">Выберите параметр **Не отклонять запрос проверки подлинности, инициированный поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="b0683-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="b0683-243">Е.</span><span class="sxs-lookup"><span data-stu-id="b0683-243">f.</span></span> <span data-ttu-id="b0683-244">Для параметра **Authentication Request Signature Method** (Метод подписи запроса аутентификации) выберите значение **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="b0683-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="b0683-245">![Метод подписи запроса аутентификации](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Метод подписи запроса аутентификации")</span><span class="sxs-lookup"><span data-stu-id="b0683-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="b0683-246">g.</span><span class="sxs-lookup"><span data-stu-id="b0683-246">g.</span></span> <span data-ttu-id="b0683-247">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b0683-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="b0683-248">![ОК](./media/active-directory-saas-workday-tutorial/IC782933.png "ОК")
<CE></span><span class="sxs-lookup"><span data-stu-id="b0683-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="b0683-249">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b0683-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b0683-250">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b0683-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b0683-251">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0683-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0683-252">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0683-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0683-253">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b0683-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b0683-255">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b0683-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0683-256">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b0683-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0683-258">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b0683-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0683-260">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b0683-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0683-262">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b0683-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0683-264">а.</span><span class="sxs-lookup"><span data-stu-id="b0683-264">a.</span></span> <span data-ttu-id="b0683-265">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0683-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0683-266">b.</span><span class="sxs-lookup"><span data-stu-id="b0683-266">b.</span></span> <span data-ttu-id="b0683-267">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0683-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0683-268">c.</span><span class="sxs-lookup"><span data-stu-id="b0683-268">c.</span></span> <span data-ttu-id="b0683-269">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b0683-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b0683-270">d.</span><span class="sxs-lookup"><span data-stu-id="b0683-270">d.</span></span> <span data-ttu-id="b0683-271">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b0683-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="b0683-272">Создание тестового пользователя Workday</span><span class="sxs-lookup"><span data-stu-id="b0683-272">Creating a Workday test user</span></span>

<span data-ttu-id="b0683-273">tooget тестового пользователя, подготовленного в Workday, необходимо toocontact hello [группа поддержки клиента Workday](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="b0683-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="b0683-274">Hello [группа поддержки клиента Workday](https://www.workday.com/en-us/partners-services/services/support.html) hello пользователя будет создан.</span><span class="sxs-lookup"><span data-stu-id="b0683-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b0683-275">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b0683-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b0683-276">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWorkday доступа.</span><span class="sxs-lookup"><span data-stu-id="b0683-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b0683-278">**tooassign tooWorkday Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b0683-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0683-279">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b0683-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b0683-281">В списке приложений hello выберите **Workday**.</span><span class="sxs-lookup"><span data-stu-id="b0683-281">In hello applications list, select **Workday**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="b0683-283">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b0683-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b0683-285">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b0683-285">Click **Add** button.</span></span> <span data-ttu-id="b0683-286">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b0683-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b0683-288">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b0683-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0683-289">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b0683-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0683-290">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b0683-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0683-291">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b0683-291">Testing single sign-on</span></span>

<span data-ttu-id="b0683-292">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b0683-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="b0683-293">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0683-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0683-294">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b0683-294">Additional resources</span></span>

* [<span data-ttu-id="b0683-295">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0683-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0683-296">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0683-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b0683-297">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="b0683-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

