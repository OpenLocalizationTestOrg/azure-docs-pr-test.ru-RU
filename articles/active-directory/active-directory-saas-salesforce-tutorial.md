---
title: "Руководство по интеграции Azure Active Directory с Salesforce | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="f66c5-103">Руководство по интеграции Azure Active Directory с Salesforce</span><span class="sxs-lookup"><span data-stu-id="f66c5-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="f66c5-104">В этом учебнике вы узнаете, как toointegrate Salesforce с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f66c5-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f66c5-105">Интеграция Salesforce с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f66c5-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f66c5-106">Можно управлять в Azure AD, имеющего доступ tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="f66c5-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="f66c5-107">Можно включить на пользователей tooautomatically get вошедшего tooSalesforce (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="f66c5-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f66c5-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f66c5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f66c5-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f66c5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f66c5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f66c5-110">Prerequisites</span></span>

<span data-ttu-id="f66c5-111">tooconfigure интеграция Azure AD с Salesforce требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f66c5-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="f66c5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f66c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f66c5-113">подписка Salesforce с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f66c5-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f66c5-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="f66c5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f66c5-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="f66c5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f66c5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f66c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f66c5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f66c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f66c5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f66c5-118">Scenario description</span></span>
<span data-ttu-id="f66c5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f66c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f66c5-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="f66c5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f66c5-121">Добавление Salesforce из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f66c5-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="f66c5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f66c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="f66c5-123">Добавление Salesforce из галереи hello</span><span class="sxs-lookup"><span data-stu-id="f66c5-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="f66c5-124">tooconfigure hello интеграция Salesforce в Azure AD, вы должны tooadd Salesforce из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f66c5-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f66c5-125">**tooadd Salesforce из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f66c5-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f66c5-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f66c5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f66c5-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f66c5-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f66c5-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="f66c5-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f66c5-133">Введите в поле поиска hello **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-133">In hello search box, type **Salesforce**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="f66c5-135">В панели результатов hello выберите **Salesforce**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f66c5-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f66c5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f66c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f66c5-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Salesforce с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f66c5-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f66c5-139">Для единого входа toowork Azure AD необходима tooknow hello аналог пользователя в Salesforce — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f66c5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="f66c5-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Salesforce должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="f66c5-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="f66c5-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f66c5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="f66c5-142">tooconfigure и теста Azure AD единого входа с Salesforce, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f66c5-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f66c5-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="f66c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f66c5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="f66c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f66c5-145">**[Создание тестового пользователя Salesforce](#creating-a-salesforce-test-user)**  -toohave аналог Саймон Britta в Salesforce, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="f66c5-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f66c5-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="f66c5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f66c5-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f66c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f66c5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f66c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f66c5-149">В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в приложение Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f66c5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="f66c5-150">**tooconfigure Azure AD единого входа с Salesforce, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f66c5-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="f66c5-151">В hello в hello портала Azure **Salesforce** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f66c5-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="f66c5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="f66c5-155">На hello **URL-адреса и домена Salesforce** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f66c5-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="f66c5-157">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="f66c5-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="f66c5-158">Учетная запись предприятия: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f66c5-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="f66c5-159">Учетная запись разработчика: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f66c5-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f66c5-160">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="f66c5-160">These values are not hello real.</span></span> <span data-ttu-id="f66c5-161">Обновите эти значения с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="f66c5-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="f66c5-162">Обратитесь к [группа поддержки клиента Salesforce](https://help.salesforce.com/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="f66c5-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="f66c5-163">На hello **сертификат подписи SAML** щелкните **сертификат** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="f66c5-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="f66c5-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f66c5-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f66c5-167">На hello **конфигурации Salesforce** щелкните **Настройка Salesforce** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="f66c5-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f66c5-168">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="f66c5-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="f66c5-169">![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="f66c5-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="f66c5-170">Откройте новую вкладку в браузере и войдите в учетную запись администратора Salesforce tooyour.</span><span class="sxs-lookup"><span data-stu-id="f66c5-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="f66c5-171">Под hello **администратора** панели навигации щелкните **управления безопасностью** tooexpand hello связанных разделов.</span><span class="sxs-lookup"><span data-stu-id="f66c5-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="f66c5-172">Затем щелкните **Параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-172">Then click **Single Sign-On Settings**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="f66c5-174">На hello **параметры единого входа** щелкните hello **изменить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f66c5-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="f66c5-175">![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="f66c5-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="f66c5-176">Если не удается tooenable параметры единого входа для учетной записи Salesforce, может потребоваться toocontact [группа поддержки клиента Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="f66c5-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="f66c5-177">Выберите **SAML Enabled** (SAML включен), а затем щелкните **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="f66c5-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="f66c5-179">tooconfigure единого входа параметры SAML, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="f66c5-181">На hello **SAML единого входа для изменения настроек** задайте hello конфигурации:</span><span class="sxs-lookup"><span data-stu-id="f66c5-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="f66c5-183">а.</span><span class="sxs-lookup"><span data-stu-id="f66c5-183">a.</span></span> <span data-ttu-id="f66c5-184">Для hello **имя** введите понятное имя для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f66c5-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="f66c5-185">Предоставить значение для **имя** автоматически заполнять hello **имя API** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="f66c5-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="f66c5-186">b.</span><span class="sxs-lookup"><span data-stu-id="f66c5-186">b.</span></span> <span data-ttu-id="f66c5-187">Вставить **идентификатор сущности SMAL** значение в hello **издателя** в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f66c5-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="f66c5-188">c.</span><span class="sxs-lookup"><span data-stu-id="f66c5-188">c.</span></span> <span data-ttu-id="f66c5-189">В hello **идентификатор сущности textbox**, введите доменное имя Salesforce с помощью hello следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="f66c5-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="f66c5-190">Учетная запись предприятия: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f66c5-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="f66c5-191">Учетная запись разработчика: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f66c5-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="f66c5-192">d.</span><span class="sxs-lookup"><span data-stu-id="f66c5-192">d.</span></span> <span data-ttu-id="f66c5-193">Нажмите кнопку **Обзор** или **выбрать файл** tooopen hello **tooUpload выбрать файл** диалоговое окно, выберите сертификат Salesforce и нажмите кнопку **откройте**tooupload hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="f66c5-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="f66c5-194">д.</span><span class="sxs-lookup"><span data-stu-id="f66c5-194">e.</span></span> <span data-ttu-id="f66c5-195">В поле **SAML Identity Type** (Тип удостоверения SAML) выберите значение **Assertion contains User's salesforce.com username** (Утверждение содержит имя пользователя salesforce.com).</span><span class="sxs-lookup"><span data-stu-id="f66c5-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="f66c5-196">f.</span><span class="sxs-lookup"><span data-stu-id="f66c5-196">f.</span></span> <span data-ttu-id="f66c5-197">Для **расположения удостоверения SAML**выберите **удостоверение находится в элемент hello NameIdentifier оператора Subject hello**</span><span class="sxs-lookup"><span data-stu-id="f66c5-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="f66c5-198">ж.</span><span class="sxs-lookup"><span data-stu-id="f66c5-198">g.</span></span> <span data-ttu-id="f66c5-199">Вставить **единого входа URL-адрес службы** в hello **URL-адрес входа поставщика удостоверений** в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f66c5-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="f66c5-200">h.</span><span class="sxs-lookup"><span data-stu-id="f66c5-200">h.</span></span> <span data-ttu-id="f66c5-201">В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициируемых поставщиком услуг) выберите значение **HTTP Redirect** (Перенаправление HTTP).</span><span class="sxs-lookup"><span data-stu-id="f66c5-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="f66c5-202">i.</span><span class="sxs-lookup"><span data-stu-id="f66c5-202">i.</span></span> <span data-ttu-id="f66c5-203">Наконец, нажмите кнопку **Сохранить** tooapply единого входа параметры SAML.</span><span class="sxs-lookup"><span data-stu-id="f66c5-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="f66c5-204">На панели навигации слева hello в Salesforce щелкните **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="f66c5-206">Прокрутите вниз toohello **настройки проверки подлинности** и нажмите кнопку hello **изменить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f66c5-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="f66c5-208">В hello **службы проверки подлинности** статьи hello понятное имя конфигурации единого входа SAML и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="f66c5-210">Если выбрано более одной службы проверки подлинности, пользователи не запрошенные tooselect, какие службы проверки подлинности угодно toosign в систему при запуске среда tooyour Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f66c5-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="f66c5-211">Если вы не хотите toohappen, то следует **все остальные службы проверки подлинности не устанавливайте флажок**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="f66c5-212">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="f66c5-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f66c5-213">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="f66c5-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f66c5-214">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f66c5-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f66c5-215">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f66c5-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="f66c5-216">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f66c5-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f66c5-218">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f66c5-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f66c5-219">На панели навигации слева hello в hello **портал Azure**, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="f66c5-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f66c5-221">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f66c5-223">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="f66c5-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f66c5-225">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f66c5-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f66c5-227">а.</span><span class="sxs-lookup"><span data-stu-id="f66c5-227">a.</span></span> <span data-ttu-id="f66c5-228">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f66c5-229">b.</span><span class="sxs-lookup"><span data-stu-id="f66c5-229">b.</span></span> <span data-ttu-id="f66c5-230">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f66c5-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f66c5-231">c.</span><span class="sxs-lookup"><span data-stu-id="f66c5-231">c.</span></span> <span data-ttu-id="f66c5-232">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f66c5-233">d.</span><span class="sxs-lookup"><span data-stu-id="f66c5-233">d.</span></span> <span data-ttu-id="f66c5-234">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="f66c5-235">Создание тестового пользователя Salesforce</span><span class="sxs-lookup"><span data-stu-id="f66c5-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="f66c5-236">В этом разделе вы создадите в Salesforce пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f66c5-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="f66c5-237">Приложение Salesforce поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f66c5-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="f66c5-238">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="f66c5-238">There is no action item for you in this section.</span></span> <span data-ttu-id="f66c5-239">Если пользователь еще не существует в Salesforce, создается новый, при попытке tooaccess Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f66c5-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f66c5-240">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="f66c5-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f66c5-241">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSalesforce доступа.</span><span class="sxs-lookup"><span data-stu-id="f66c5-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f66c5-243">**tooassign tooSalesforce Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="f66c5-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="f66c5-244">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f66c5-246">В списке приложений hello выберите **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-246">In hello applications list, select **Salesforce**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="f66c5-248">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f66c5-250">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-250">Click **Add** button.</span></span> <span data-ttu-id="f66c5-251">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f66c5-253">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="f66c5-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f66c5-254">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f66c5-255">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f66c5-256">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f66c5-256">Testing single sign-on</span></span>

<span data-ttu-id="f66c5-257">tootest входа параметры единого, откройте hello панель доступа по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com/), затем войдите в hello тестовую учетную запись и нажмите кнопку **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="f66c5-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f66c5-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f66c5-258">Additional resources</span></span>

* [<span data-ttu-id="f66c5-259">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f66c5-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f66c5-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f66c5-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f66c5-261">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="f66c5-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

