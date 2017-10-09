---
title: "Руководство по интеграции Azure Active Directory с PolicyStat | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="f6932-103">Руководство по интеграции Azure Active Directory с PolicyStat</span><span class="sxs-lookup"><span data-stu-id="f6932-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="f6932-104">В этом учебнике вы узнаете, как toointegrate PolicyStat с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6932-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6932-105">Интеграция с Azure AD PolicyStat предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f6932-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f6932-106">Можно управлять в Azure AD, имеющего доступ tooPolicyStat</span><span class="sxs-lookup"><span data-stu-id="f6932-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="f6932-107">Можно включить на пользователей tooautomatically get вошедшего tooPolicyStat (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6932-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6932-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f6932-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f6932-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6932-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6932-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f6932-110">Prerequisites</span></span>

<span data-ttu-id="f6932-111">tooconfigure интеграция Azure AD с PolicyStat требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f6932-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="f6932-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f6932-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6932-113">подписка PolicyStat с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f6932-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6932-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f6932-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6932-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f6932-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6932-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f6932-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6932-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6932-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6932-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f6932-118">Scenario description</span></span>
<span data-ttu-id="f6932-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f6932-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6932-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f6932-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6932-121">Добавление PolicyStat из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f6932-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="f6932-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6932-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="f6932-123">Добавление PolicyStat из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f6932-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="f6932-124">tooconfigure hello интеграции PolicyStat в Azure AD, вы должны tooadd PolicyStat из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f6932-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6932-125">**tooadd PolicyStat из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f6932-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6932-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f6932-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6932-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f6932-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f6932-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f6932-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f6932-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f6932-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f6932-133">Введите в поле поиска hello **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="f6932-133">In hello search box, type **PolicyStat**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="f6932-135">В панели результатов hello выберите **PolicyStat**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f6932-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6932-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6932-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6932-138">В этом разделе описана настройка и проверка единого входа Azure AD в PolicyStat с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f6932-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f6932-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PolicyStat является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6932-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="f6932-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в PolicyStat должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f6932-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="f6932-141">В PolicyStat, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="f6932-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f6932-142">tooconfigure и теста Azure AD единого входа с PolicyStat, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f6932-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f6932-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f6932-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f6932-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f6932-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6932-145">**[Создание тестового пользователя PolicyStat](#creating-a-policystat-test-user)**  -toohave аналог Саймон Britta в PolicyStat, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f6932-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6932-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f6932-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6932-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f6932-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6932-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6932-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6932-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="f6932-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="f6932-150">**tooconfigure Azure AD единого входа с PolicyStat, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f6932-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6932-151">В hello в hello портала Azure **PolicyStat** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f6932-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f6932-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f6932-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="f6932-155">На hello **URL-адреса и домена PolicyStat** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f6932-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="f6932-157">а.</span><span class="sxs-lookup"><span data-stu-id="f6932-157">a.</span></span> <span data-ttu-id="f6932-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="f6932-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="f6932-159">b.</span><span class="sxs-lookup"><span data-stu-id="f6932-159">b.</span></span> <span data-ttu-id="f6932-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="f6932-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6932-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f6932-161">These values are not real.</span></span> <span data-ttu-id="f6932-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="f6932-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f6932-163">Обратитесь к [группа поддержки клиента PolicyStat](http://www.policystat.com/support/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f6932-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="f6932-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f6932-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="f6932-166">Цель этого раздела Hello — toooutline как tooPolicyStat tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="f6932-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="f6932-167">Hello PolicyStat приложения ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена SAML** конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f6932-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="f6932-168">Следующий снимок экрана приветствия показан пример этого.</span><span class="sxs-lookup"><span data-stu-id="f6932-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="f6932-169">![Атрибуты](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="f6932-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="f6932-170">сопоставления атрибутов hello необходимые tooadd, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="f6932-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="f6932-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="f6932-171">Attribute Name</span></span>    |   <span data-ttu-id="f6932-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="f6932-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="f6932-173">uid</span><span class="sxs-lookup"><span data-stu-id="f6932-173">uid</span></span> | <span data-ttu-id="f6932-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="f6932-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="f6932-175">а.</span><span class="sxs-lookup"><span data-stu-id="f6932-175">a.</span></span> <span data-ttu-id="f6932-176">Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f6932-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="f6932-179">b.</span><span class="sxs-lookup"><span data-stu-id="f6932-179">b.</span></span> <span data-ttu-id="f6932-180">В hello **имя атрибута** введите **uid**.</span><span class="sxs-lookup"><span data-stu-id="f6932-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="f6932-181">c.</span><span class="sxs-lookup"><span data-stu-id="f6932-181">c.</span></span> <span data-ttu-id="f6932-182">В hello **значение атрибута** текстового поля, выберите **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="f6932-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="f6932-183">d.</span><span class="sxs-lookup"><span data-stu-id="f6932-183">d.</span></span> <span data-ttu-id="f6932-184">Из hello **Mail** выберите **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="f6932-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="f6932-185">д.</span><span class="sxs-lookup"><span data-stu-id="f6932-185">e.</span></span> <span data-ttu-id="f6932-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f6932-186">Click **Ok**</span></span>

7. <span data-ttu-id="f6932-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f6932-187">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f6932-189">В другом окне веб-браузера войдите на сайт PolicyStat своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="f6932-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="f6932-190">Нажмите кнопку hello **администратора** , а затем щелкните **настройки единого входа** в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="f6932-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="f6932-191">![Меню администратора](./media/active-directory-saas-policystat-tutorial/ic808633.png "Меню администратора")</span><span class="sxs-lookup"><span data-stu-id="f6932-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="f6932-192">В hello **установки** выберите **Включение единого входа интеграции**.</span><span class="sxs-lookup"><span data-stu-id="f6932-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="f6932-193">![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808634.png "Конфигурация единого входа")</span><span class="sxs-lookup"><span data-stu-id="f6932-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="f6932-194">Нажмите кнопку **Настройка атрибутов**, а затем в hello **Настройка атрибутов** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f6932-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f6932-195">![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808635.png "Конфигурация единого входа")</span><span class="sxs-lookup"><span data-stu-id="f6932-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="f6932-196">а.</span><span class="sxs-lookup"><span data-stu-id="f6932-196">a.</span></span> <span data-ttu-id="f6932-197">В hello **атрибута Username** введите **uid**.</span><span class="sxs-lookup"><span data-stu-id="f6932-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="f6932-198">b.</span><span class="sxs-lookup"><span data-stu-id="f6932-198">b.</span></span> <span data-ttu-id="f6932-199">В hello **атрибут имени** введите **firstname** пользователя **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f6932-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="f6932-200">c.</span><span class="sxs-lookup"><span data-stu-id="f6932-200">c.</span></span> <span data-ttu-id="f6932-201">В hello **атрибут фамилии** введите **lastname** пользователя **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f6932-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="f6932-202">d.</span><span class="sxs-lookup"><span data-stu-id="f6932-202">d.</span></span> <span data-ttu-id="f6932-203">В hello **атрибут адреса электронной почты** введите **emailaddress** пользователя  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f6932-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="f6932-204">д.</span><span class="sxs-lookup"><span data-stu-id="f6932-204">e.</span></span> <span data-ttu-id="f6932-205">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="f6932-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="f6932-206">Нажмите кнопку **свои метаданные поставщика Удостоверений**, а затем в hello **свои метаданные поставщика Удостоверений** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f6932-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f6932-207">![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808636.png "Конфигурация единого входа")</span><span class="sxs-lookup"><span data-stu-id="f6932-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="f6932-208">а.</span><span class="sxs-lookup"><span data-stu-id="f6932-208">a.</span></span> <span data-ttu-id="f6932-209">Откройте скачанный файл метаданных в hello копирования содержимого, а затем вставьте его в hello **свои метаданные поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="f6932-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="f6932-210">b.</span><span class="sxs-lookup"><span data-stu-id="f6932-210">b.</span></span> <span data-ttu-id="f6932-211">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="f6932-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f6932-212">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f6932-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f6932-213">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f6932-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f6932-214">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6932-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6932-215">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6932-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6932-216">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f6932-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f6932-218">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f6932-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6932-219">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f6932-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6932-221">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f6932-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6932-223">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f6932-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6932-225">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f6932-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6932-227">а.</span><span class="sxs-lookup"><span data-stu-id="f6932-227">a.</span></span> <span data-ttu-id="f6932-228">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6932-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6932-229">b.</span><span class="sxs-lookup"><span data-stu-id="f6932-229">b.</span></span> <span data-ttu-id="f6932-230">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f6932-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6932-231">c.</span><span class="sxs-lookup"><span data-stu-id="f6932-231">c.</span></span> <span data-ttu-id="f6932-232">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f6932-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f6932-233">d.</span><span class="sxs-lookup"><span data-stu-id="f6932-233">d.</span></span> <span data-ttu-id="f6932-234">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f6932-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="f6932-235">Создание тестового пользователя PolicyStat</span><span class="sxs-lookup"><span data-stu-id="f6932-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="f6932-236">В порядке tooenable toolog пользователей Azure AD в PolicyStat их необходимо подготовить в PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="f6932-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="f6932-237">PolicyStat поддерживает подготовку пользователей «на лету».</span><span class="sxs-lookup"><span data-stu-id="f6932-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="f6932-238">Это означает, что не требуется вручную пользователей hello tooadd tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="f6932-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="f6932-239">Hello пользователей будет автоматически добавляются при их первом входе с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="f6932-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="f6932-240">Можно использовать любые другие PolicyStat пользователя средства создания учетных записей или интерфейсы API, предоставляемые PolicyStat tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6932-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f6932-241">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f6932-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f6932-242">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPolicyStat доступа.</span><span class="sxs-lookup"><span data-stu-id="f6932-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f6932-244">**tooassign tooPolicyStat Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f6932-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="f6932-245">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f6932-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f6932-247">В списке приложений hello выберите **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="f6932-247">In hello applications list, select **PolicyStat**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="f6932-249">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f6932-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f6932-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f6932-251">Click **Add** button.</span></span> <span data-ttu-id="f6932-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f6932-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f6932-254">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f6932-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f6932-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f6932-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6932-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f6932-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6932-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f6932-257">Testing single sign-on</span></span>

<span data-ttu-id="f6932-258">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="f6932-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f6932-259">При нажатии кнопки hello PolicyStat плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour PolicyStat приложения.</span><span class="sxs-lookup"><span data-stu-id="f6932-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="f6932-260">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f6932-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6932-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f6932-261">Additional resources</span></span>

* [<span data-ttu-id="f6932-262">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6932-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6932-263">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6932-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

