---
title: "Руководство. Интеграция Azure Active Directory с Aha! | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="dede1-104">Руководство. Интеграция Azure Active Directory с Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="dede1-105">В этом учебнике вы узнаете, как toointegrate Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="dede1-106">с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dede1-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dede1-107">Интеграция Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-107">Integrating Aha!</span></span> <span data-ttu-id="dede1-108">с помощью Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="dede1-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dede1-109">Можно управлять в Azure AD, имеющего доступ tooAha!</span><span class="sxs-lookup"><span data-stu-id="dede1-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="dede1-110">Можно включить на пользователей tooautomatically get вошедшего tooAha!</span><span class="sxs-lookup"><span data-stu-id="dede1-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="dede1-111">с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dede1-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dede1-112">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="dede1-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dede1-113">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dede1-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dede1-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dede1-114">Prerequisites</span></span>

<span data-ttu-id="dede1-115">tooconfigure интеграция Azure AD с Aha!, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="dede1-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="dede1-116">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dede1-116">An Azure AD subscription</span></span>
- <span data-ttu-id="dede1-117">Подписка</span><span class="sxs-lookup"><span data-stu-id="dede1-117">An Aha!</span></span> <span data-ttu-id="dede1-118">Aha! с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dede1-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dede1-119">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="dede1-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dede1-120">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="dede1-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dede1-121">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dede1-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dede1-122">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dede1-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dede1-123">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dede1-123">Scenario description</span></span>
<span data-ttu-id="dede1-124">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dede1-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dede1-125">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="dede1-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dede1-126">Добавление Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-126">Adding Aha!</span></span> <span data-ttu-id="dede1-127">из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dede1-127">from hello gallery</span></span>
2. <span data-ttu-id="dede1-128">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dede1-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="dede1-129">Добавление Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-129">Adding Aha!</span></span> <span data-ttu-id="dede1-130">из галереи hello</span><span class="sxs-lookup"><span data-stu-id="dede1-130">from hello gallery</span></span>
<span data-ttu-id="dede1-131">Интеграция hello tooconfigure Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="dede1-132">в Azure AD необходимо tooadd Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="dede1-133">из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dede1-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dede1-134">**tooadd Aha! из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dede1-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dede1-135">В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dede1-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dede1-137">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="dede1-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dede1-138">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dede1-138">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dede1-140">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="dede1-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dede1-142">Введите в поле поиска hello **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="dede1-142">In hello search box, type **Aha!**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="dede1-144">В панели результатов hello выберите **Aha!**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="dede1-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dede1-146">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dede1-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dede1-147">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="dede1-148">с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dede1-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dede1-149">Для единого входа toowork Azure AD необходима tooknow, какой пользователь hello аналога в Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="dede1-150">— пользователь tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dede1-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="dede1-151">Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="dede1-152">необходимо установить toobe.</span><span class="sxs-lookup"><span data-stu-id="dede1-152">needs toobe established.</span></span>

<span data-ttu-id="dede1-153">В Aha!, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="dede1-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dede1-154">tooconfigure и Azure AD тестирования единого входа с Aha!, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="dede1-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dede1-155">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="dede1-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dede1-156">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="dede1-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dede1-157">**[Создание Aha! Тестовый пользователь](#creating-an-aha-test-user) ** -toohave аналог Саймон Britta в Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="dede1-158">Это связанный toohello представление пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dede1-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dede1-159">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="dede1-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dede1-160">**[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dede1-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dede1-161">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dede1-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dede1-162">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="dede1-163">приложении Aha!.</span><span class="sxs-lookup"><span data-stu-id="dede1-163">application.</span></span>

<span data-ttu-id="dede1-164">**tooconfigure Azure AD единого входа с Aha!, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="dede1-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="dede1-165">В hello в hello портала Azure **Aha!**</span><span class="sxs-lookup"><span data-stu-id="dede1-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="dede1-166">щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="dede1-166">application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dede1-168">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="dede1-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="dede1-170">На hello **Aha! URL-адреса и домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dede1-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="dede1-172">а.</span><span class="sxs-lookup"><span data-stu-id="dede1-172">a.</span></span> <span data-ttu-id="dede1-173">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="dede1-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="dede1-174">b.</span><span class="sxs-lookup"><span data-stu-id="dede1-174">b.</span></span> <span data-ttu-id="dede1-175">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="dede1-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dede1-176">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="dede1-176">These values are not real.</span></span> <span data-ttu-id="dede1-177">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="dede1-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dede1-178">Обратитесь к [группе Группа поддержки клиента](https://www.aha.io/company/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="dede1-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="dede1-179">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="dede1-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="dede1-181">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dede1-181">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dede1-183">В другом окне браузера войдите в tooyour Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="dede1-184">в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="dede1-184">company site as an administrator.</span></span>

7. <span data-ttu-id="dede1-185">В меню в верхней части hello hello выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="dede1-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="dede1-186">![Параметры](./media/active-directory-saas-aha-tutorial/IC798950.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="dede1-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="dede1-187">Выберите раздел **Учетная запись**.</span><span class="sxs-lookup"><span data-stu-id="dede1-187">Click **Account**.</span></span>
   
    <span data-ttu-id="dede1-188">![Профиль](./media/active-directory-saas-aha-tutorial/IC798951.png "Профиль")</span><span class="sxs-lookup"><span data-stu-id="dede1-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="dede1-189">Нажмите **Безопасность и единый вход**.</span><span class="sxs-lookup"><span data-stu-id="dede1-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="dede1-190">![Безопасность и единый вход](./media/active-directory-saas-aha-tutorial/IC798952.png "Безопасность и единый вход")</span><span class="sxs-lookup"><span data-stu-id="dede1-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="dede1-191">В разделе **Единый вход** в качестве **поставщика удостоверений** выберите **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="dede1-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="dede1-192">![Безопасность и единый вход](./media/active-directory-saas-aha-tutorial/IC798953.png "Безопасность и единый вход")</span><span class="sxs-lookup"><span data-stu-id="dede1-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="dede1-193">На hello **Single Sign-On** конфигурации выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dede1-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="dede1-194">![Единый вход](./media/active-directory-saas-aha-tutorial/IC798954.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="dede1-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="dede1-195">а.</span><span class="sxs-lookup"><span data-stu-id="dede1-195">a.</span></span> <span data-ttu-id="dede1-196">В hello **имя** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dede1-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="dede1-197">b.</span><span class="sxs-lookup"><span data-stu-id="dede1-197">b.</span></span> <span data-ttu-id="dede1-198">Для параметра **Configure using** (Использовать при настройке) выберите значение **Файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="dede1-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="dede1-199">c.</span><span class="sxs-lookup"><span data-stu-id="dede1-199">c.</span></span> <span data-ttu-id="dede1-200">tooupload скачанный файл метаданных, щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="dede1-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="dede1-201">d.</span><span class="sxs-lookup"><span data-stu-id="dede1-201">d.</span></span> <span data-ttu-id="dede1-202">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="dede1-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="dede1-203">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="dede1-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dede1-204">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="dede1-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dede1-205">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dede1-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dede1-206">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dede1-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="dede1-207">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dede1-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dede1-209">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="dede1-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dede1-210">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="dede1-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dede1-212">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="dede1-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dede1-214">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="dede1-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dede1-216">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="dede1-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dede1-218">а.</span><span class="sxs-lookup"><span data-stu-id="dede1-218">a.</span></span> <span data-ttu-id="dede1-219">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dede1-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dede1-220">b.</span><span class="sxs-lookup"><span data-stu-id="dede1-220">b.</span></span> <span data-ttu-id="dede1-221">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dede1-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dede1-222">c.</span><span class="sxs-lookup"><span data-stu-id="dede1-222">c.</span></span> <span data-ttu-id="dede1-223">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="dede1-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dede1-224">d.</span><span class="sxs-lookup"><span data-stu-id="dede1-224">d.</span></span> <span data-ttu-id="dede1-225">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dede1-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="dede1-226">Создание тестового</span><span class="sxs-lookup"><span data-stu-id="dede1-226">Creating an Aha!</span></span> <span data-ttu-id="dede1-227">пользователя Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-227">test user</span></span>

<span data-ttu-id="dede1-228">toolog tooenable Azure AD пользователи в tooAha!, их необходимо подготовить в Aha!.</span><span class="sxs-lookup"><span data-stu-id="dede1-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="dede1-229">В случае, когда hello Aha!, Подготовка — это автоматизированная задача.</span><span class="sxs-lookup"><span data-stu-id="dede1-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="dede1-230">С вашей стороны никакие действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="dede1-230">There is no action item for you.</span></span>

<span data-ttu-id="dede1-231">Пользователи создаются автоматически при необходимости hello первой единого входа попытки.</span><span class="sxs-lookup"><span data-stu-id="dede1-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="dede1-232">Вы можете использовать любые другие средства создания учетной записи пользователя Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-232">You can use any other Aha!</span></span> <span data-ttu-id="dede1-233">или API, предоставляемые Aha!</span><span class="sxs-lookup"><span data-stu-id="dede1-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="dede1-234">tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="dede1-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dede1-235">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="dede1-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dede1-236">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAha!.</span><span class="sxs-lookup"><span data-stu-id="dede1-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dede1-238">**tooassign tooAha Britta Simon!, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="dede1-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="dede1-239">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dede1-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dede1-241">В списке приложений hello выберите **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="dede1-241">In hello applications list, select **Aha!**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="dede1-243">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="dede1-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dede1-245">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dede1-245">Click **Add** button.</span></span> <span data-ttu-id="dede1-246">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dede1-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dede1-248">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="dede1-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dede1-249">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dede1-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dede1-250">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dede1-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dede1-251">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dede1-251">Testing single sign-on</span></span>

<span data-ttu-id="dede1-252">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="dede1-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="dede1-253">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dede1-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dede1-254">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dede1-254">Additional resources</span></span>

* [<span data-ttu-id="dede1-255">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dede1-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dede1-256">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dede1-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

