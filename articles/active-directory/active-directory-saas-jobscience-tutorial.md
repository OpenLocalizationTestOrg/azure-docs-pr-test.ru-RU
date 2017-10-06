---
title: "Учебник. Интеграция Azure Active Directory с Jobscience | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="acf59-103">Руководство. Интеграция Azure Active Directory с Jobscience</span><span class="sxs-lookup"><span data-stu-id="acf59-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="acf59-104">В этом учебнике вы узнаете, как toointegrate Jobscience с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="acf59-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acf59-105">Интеграция Jobscience с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="acf59-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="acf59-106">Можно управлять в Azure AD, имеющего доступ tooJobscience</span><span class="sxs-lookup"><span data-stu-id="acf59-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="acf59-107">Можно включить на пользователей tooautomatically get вошедшего tooJobscience (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf59-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="acf59-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="acf59-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="acf59-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="acf59-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acf59-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="acf59-110">Prerequisites</span></span>

<span data-ttu-id="acf59-111">tooconfigure интеграция Azure AD с Jobscience требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="acf59-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="acf59-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="acf59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="acf59-113">подписка Jobscience с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="acf59-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="acf59-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="acf59-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="acf59-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="acf59-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acf59-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="acf59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="acf59-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acf59-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="acf59-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="acf59-118">Scenario description</span></span>
<span data-ttu-id="acf59-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="acf59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acf59-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="acf59-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acf59-121">Добавление Jobscience из галереи hello</span><span class="sxs-lookup"><span data-stu-id="acf59-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="acf59-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf59-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="acf59-123">Добавление Jobscience из галереи hello</span><span class="sxs-lookup"><span data-stu-id="acf59-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="acf59-124">tooconfigure hello интеграции Jobscience в Azure AD, вы должны tooadd Jobscience из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="acf59-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="acf59-125">**tooadd Jobscience из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="acf59-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="acf59-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="acf59-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="acf59-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="acf59-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="acf59-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="acf59-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="acf59-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="acf59-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="acf59-133">Введите в поле поиска hello **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="acf59-133">In hello search box, type **Jobscience**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="acf59-135">В панели результатов hello выберите **Jobscience**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="acf59-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="acf59-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf59-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="acf59-138">В этом разделе описана настройка и проверка единого входа Azure AD в Jobscience с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acf59-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="acf59-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Jobscience является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acf59-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="acf59-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Jobscience должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="acf59-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="acf59-141">В Jobscience, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="acf59-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="acf59-142">tooconfigure и теста Azure AD единого входа с Jobscience, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="acf59-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="acf59-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="acf59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="acf59-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="acf59-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="acf59-145">**[Создание тестового пользователя Jobscience](#creating-a-jobscience-test-user)**  -toohave аналог Саймон Britta в Jobscience, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="acf59-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="acf59-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="acf59-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="acf59-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="acf59-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="acf59-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf59-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="acf59-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Jobscience приложения.</span><span class="sxs-lookup"><span data-stu-id="acf59-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="acf59-150">**tooconfigure Azure AD единого входа с Jobscience, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="acf59-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="acf59-151">В hello в hello портала Azure **Jobscience** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="acf59-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="acf59-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="acf59-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="acf59-155">На hello **URL-адреса и домена Jobscience** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="acf59-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="acf59-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="acf59-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="acf59-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="acf59-158">This value is not real.</span></span> <span data-ttu-id="acf59-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="acf59-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="acf59-160">Это значение можно получить [группа поддержки клиента Jobscience](https://www.jobscience.com/support) или из hello профиль единого входа будет создана, который описан далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="acf59-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="acf59-161">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="acf59-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="acf59-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="acf59-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="acf59-165">На hello **конфигурации Jobscience** щелкните **Настройка Jobscience** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="acf59-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="acf59-166">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="acf59-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="acf59-168">Войдите в систему tooyour сайте Jobscience для компании как администратор.</span><span class="sxs-lookup"><span data-stu-id="acf59-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="acf59-169">Go слишком**установки**.</span><span class="sxs-lookup"><span data-stu-id="acf59-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="acf59-170">![Настройка](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="acf59-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="acf59-171">На панели навигации слева hello в hello **Администрирование** щелкните **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен** tooopen hello  **Мой домен** страницы.</span><span class="sxs-lookup"><span data-stu-id="acf59-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="acf59-172">![Мой домен](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="acf59-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="acf59-173">tooverify, домен настроен неправильно, убедитесь, что он находится в "**шаг 4 развернут tooUsers**» и просмотрите вашей»**мои параметры домена**».</span><span class="sxs-lookup"><span data-stu-id="acf59-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="acf59-174">![Домен развернутые tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser домена развертывания")</span><span class="sxs-lookup"><span data-stu-id="acf59-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="acf59-175">Щелкните hello сайте Jobscience для компании **управления безопасностью**и нажмите кнопку **параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="acf59-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="acf59-176">![Средства управления безопасностью](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Средства управления безопасностью")</span><span class="sxs-lookup"><span data-stu-id="acf59-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="acf59-177">В hello **параметры единого входа** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="acf59-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="acf59-178">![Параметры единого входа](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="acf59-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="acf59-179">а.</span><span class="sxs-lookup"><span data-stu-id="acf59-179">a.</span></span> <span data-ttu-id="acf59-180">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="acf59-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="acf59-181">b.</span><span class="sxs-lookup"><span data-stu-id="acf59-181">b.</span></span> <span data-ttu-id="acf59-182">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="acf59-182">Click **New**.</span></span>

13. <span data-ttu-id="acf59-183">На hello **SAML единого входа для изменения настроек** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="acf59-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="acf59-184">![Параметры единого входа SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="acf59-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="acf59-185">а.</span><span class="sxs-lookup"><span data-stu-id="acf59-185">a.</span></span> <span data-ttu-id="acf59-186">В hello **имя** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="acf59-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="acf59-187">b.</span><span class="sxs-lookup"><span data-stu-id="acf59-187">b.</span></span> <span data-ttu-id="acf59-188">В **издателя** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="acf59-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="acf59-189">c.</span><span class="sxs-lookup"><span data-stu-id="acf59-189">c.</span></span> <span data-ttu-id="acf59-190">В hello **идентификатор сущности** текстовое поле, тип`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="acf59-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="acf59-191">d.</span><span class="sxs-lookup"><span data-stu-id="acf59-191">d.</span></span> <span data-ttu-id="acf59-192">Нажмите кнопку **Обзор** tooupload сертификат Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acf59-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="acf59-193">д.</span><span class="sxs-lookup"><span data-stu-id="acf59-193">e.</span></span> <span data-ttu-id="acf59-194">Как **типа удостоверения SAML**выберите **утверждение, содержащее hello идентификатор федерации из объекта пользователя hello**.</span><span class="sxs-lookup"><span data-stu-id="acf59-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="acf59-195">f.</span><span class="sxs-lookup"><span data-stu-id="acf59-195">f.</span></span> <span data-ttu-id="acf59-196">Как **расположения удостоверения SAML**выберите **удостоверение находится в hello элемент NameIdentfier оператора Subject hello**.</span><span class="sxs-lookup"><span data-stu-id="acf59-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="acf59-197">ж.</span><span class="sxs-lookup"><span data-stu-id="acf59-197">g.</span></span> <span data-ttu-id="acf59-198">В **URL-адрес входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="acf59-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="acf59-199">h.</span><span class="sxs-lookup"><span data-stu-id="acf59-199">h.</span></span> <span data-ttu-id="acf59-200">В **URL-адрес выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="acf59-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="acf59-201">i.</span><span class="sxs-lookup"><span data-stu-id="acf59-201">i.</span></span> <span data-ttu-id="acf59-202">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="acf59-202">Click **Save**.</span></span>

14. <span data-ttu-id="acf59-203">На панели навигации слева hello в hello **Администрирование** щелкните **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен** tooopen hello  **Мой домен** страницы.</span><span class="sxs-lookup"><span data-stu-id="acf59-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="acf59-204">![Мой домен](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="acf59-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="acf59-205">На hello **Мой домен** страницы в hello **фирменная символика страницы входа** щелкните **изменить**.</span><span class="sxs-lookup"><span data-stu-id="acf59-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="acf59-206">![Фирменная символика страницы входа](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Фирменная символика страницы входа")</span><span class="sxs-lookup"><span data-stu-id="acf59-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="acf59-207">На hello **фирменная символика страницы входа** страницы в hello **службы проверки подлинности** раздела, название hello вашей **настройки единого входа SAML** отображается.</span><span class="sxs-lookup"><span data-stu-id="acf59-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="acf59-208">Выберите его, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="acf59-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="acf59-209">![Фирменная символика страницы входа](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Фирменная символика страницы входа")</span><span class="sxs-lookup"><span data-stu-id="acf59-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="acf59-210">tooget hello SP инициировал единый вход по URL-адрес входа щелкните hello **параметры единого входа** в hello **управления безопасностью** раздела меню.</span><span class="sxs-lookup"><span data-stu-id="acf59-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="acf59-211">![Средства управления безопасностью](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Средства управления безопасностью")</span><span class="sxs-lookup"><span data-stu-id="acf59-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="acf59-212">Выберите профиль единого входа hello, созданном в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="acf59-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="acf59-213">На этой странице отображаются hello единым входом на URL-адрес для вашей компании (например, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="acf59-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="acf59-214">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="acf59-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="acf59-215">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="acf59-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="acf59-216">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="acf59-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="acf59-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="acf59-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="acf59-218">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="acf59-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="acf59-220">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="acf59-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="acf59-221">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="acf59-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="acf59-223">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="acf59-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="acf59-225">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="acf59-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="acf59-227">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="acf59-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="acf59-229">а.</span><span class="sxs-lookup"><span data-stu-id="acf59-229">a.</span></span> <span data-ttu-id="acf59-230">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="acf59-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acf59-231">b.</span><span class="sxs-lookup"><span data-stu-id="acf59-231">b.</span></span> <span data-ttu-id="acf59-232">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="acf59-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="acf59-233">c.</span><span class="sxs-lookup"><span data-stu-id="acf59-233">c.</span></span> <span data-ttu-id="acf59-234">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="acf59-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="acf59-235">d.</span><span class="sxs-lookup"><span data-stu-id="acf59-235">d.</span></span> <span data-ttu-id="acf59-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="acf59-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="acf59-237">Создание тестового пользователя Jobscience</span><span class="sxs-lookup"><span data-stu-id="acf59-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="acf59-238">В порядке tooenable toolog пользователей Azure AD в tooJobscience их необходимо подготовить в Jobscience.</span><span class="sxs-lookup"><span data-stu-id="acf59-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="acf59-239">В случае hello объекта Jobscience Подготовка осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="acf59-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="acf59-240">Можно использовать любые другие Jobscience пользователя средства создания учетных записей или интерфейсы API, предоставляемые Jobscience tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="acf59-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="acf59-241">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="acf59-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="acf59-242">Войдите в tooyour **Jobscience** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="acf59-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="acf59-243">Go tooSetup.</span><span class="sxs-lookup"><span data-stu-id="acf59-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="acf59-244">![Настройка](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="acf59-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="acf59-245">Go слишком**Управление пользователями \> пользователей**.</span><span class="sxs-lookup"><span data-stu-id="acf59-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="acf59-246">![Пользователи](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="acf59-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="acf59-247">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="acf59-247">Click **New User**.</span></span>
   
   <span data-ttu-id="acf59-248">![Все пользователи](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Все пользователи")</span><span class="sxs-lookup"><span data-stu-id="acf59-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="acf59-249">На hello **изменение пользователя** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="acf59-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="acf59-250">![Изменение пользователя](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Изменение пользователя")</span><span class="sxs-lookup"><span data-stu-id="acf59-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="acf59-251">а.</span><span class="sxs-lookup"><span data-stu-id="acf59-251">a.</span></span> <span data-ttu-id="acf59-252">В hello **имя** текстовом поле введите имя пользователя hello как Britta.</span><span class="sxs-lookup"><span data-stu-id="acf59-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="acf59-253">b.</span><span class="sxs-lookup"><span data-stu-id="acf59-253">b.</span></span> <span data-ttu-id="acf59-254">В hello **Фамилия** текстовом поле введите фамилию пользователя hello как Simon.</span><span class="sxs-lookup"><span data-stu-id="acf59-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="acf59-255">c.</span><span class="sxs-lookup"><span data-stu-id="acf59-255">c.</span></span> <span data-ttu-id="acf59-256">В hello **псевдоним** текстовом поле введите имя псевдонима пользователя hello как brittas.</span><span class="sxs-lookup"><span data-stu-id="acf59-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="acf59-257">d.</span><span class="sxs-lookup"><span data-stu-id="acf59-257">d.</span></span> <span data-ttu-id="acf59-258">В hello **электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="acf59-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="acf59-259">д.</span><span class="sxs-lookup"><span data-stu-id="acf59-259">e.</span></span> <span data-ttu-id="acf59-260">В hello **имя пользователя** текстовое поле, введите имя пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="acf59-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="acf59-261">f.</span><span class="sxs-lookup"><span data-stu-id="acf59-261">f.</span></span> <span data-ttu-id="acf59-262">В hello **псевдоним** текстовом поле введите имя пользователя, например Simon ник.</span><span class="sxs-lookup"><span data-stu-id="acf59-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="acf59-263">ж.</span><span class="sxs-lookup"><span data-stu-id="acf59-263">g.</span></span> <span data-ttu-id="acf59-264">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="acf59-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="acf59-265">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="acf59-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="acf59-266">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="acf59-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="acf59-267">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooJobscience доступа.</span><span class="sxs-lookup"><span data-stu-id="acf59-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="acf59-269">**tooassign tooJobscience Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="acf59-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="acf59-270">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="acf59-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="acf59-272">В списке приложений hello выберите **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="acf59-272">In hello applications list, select **Jobscience**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="acf59-274">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="acf59-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="acf59-276">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="acf59-276">Click **Add** button.</span></span> <span data-ttu-id="acf59-277">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="acf59-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="acf59-279">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="acf59-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="acf59-280">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="acf59-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="acf59-281">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="acf59-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="acf59-282">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="acf59-282">Testing single sign-on</span></span>

<span data-ttu-id="acf59-283">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="acf59-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="acf59-284">При нажатии кнопки hello Jobscience плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на Jobscience приложения.</span><span class="sxs-lookup"><span data-stu-id="acf59-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="acf59-285">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="acf59-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="acf59-286">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="acf59-286">Additional resources</span></span>

* [<span data-ttu-id="acf59-287">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acf59-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="acf59-288">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="acf59-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

