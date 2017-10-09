---
title: "Учебник. Интеграция Azure Active Directory с HireVue | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и HireVue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f890633ee4f13919c32a43d7b6cf30f2270ef6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="5cc4b-103">Руководство. Интеграция Azure Active Directory с HireVue</span><span class="sxs-lookup"><span data-stu-id="5cc4b-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="5cc4b-104">В этом учебнике вы узнаете, как toointegrate HireVue с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5cc4b-104">In this tutorial, you learn how toointegrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5cc4b-105">Интеграция с Azure AD HireVue предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-105">Integrating HireVue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5cc4b-106">Можно управлять в Azure AD, имеющего доступ tooHireVue</span><span class="sxs-lookup"><span data-stu-id="5cc4b-106">You can control in Azure AD who has access tooHireVue</span></span>
- <span data-ttu-id="5cc4b-107">Можно включить на пользователей tooautomatically get вошедшего tooHireVue (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cc4b-107">You can enable your users tooautomatically get signed-on tooHireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5cc4b-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5cc4b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5cc4b-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5cc4b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cc4b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5cc4b-110">Prerequisites</span></span>

<span data-ttu-id="5cc4b-111">tooconfigure интеграция Azure AD с HireVue требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-111">tooconfigure Azure AD integration with HireVue, you need hello following items:</span></span>

- <span data-ttu-id="5cc4b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5cc4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5cc4b-113">подписка на HireVue с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5cc4b-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5cc4b-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5cc4b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5cc4b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5cc4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5cc4b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5cc4b-118">Scenario description</span></span>
<span data-ttu-id="5cc4b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5cc4b-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5cc4b-121">Добавление HireVue из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5cc4b-121">Adding HireVue from hello gallery</span></span>
2. <span data-ttu-id="5cc4b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cc4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-hello-gallery"></a><span data-ttu-id="5cc4b-123">Добавление HireVue из галереи hello</span><span class="sxs-lookup"><span data-stu-id="5cc4b-123">Adding HireVue from hello gallery</span></span>
<span data-ttu-id="5cc4b-124">tooconfigure hello интеграции HireVue в Azure AD, вы должны tooadd HireVue из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-124">tooconfigure hello integration of HireVue into Azure AD, you need tooadd HireVue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5cc4b-125">**tooadd HireVue из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5cc4b-125">**tooadd HireVue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5cc4b-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5cc4b-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5cc4b-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5cc4b-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5cc4b-133">Введите в поле поиска hello **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-133">In hello search box, type **HireVue**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="5cc4b-135">В панели результатов hello выберите **HireVue**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-135">In hello results panel, select **HireVue**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5cc4b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cc4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5cc4b-138">В этом разделе описана настройка и проверка единого входа Azure AD в HireVue с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5cc4b-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в HireVue является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HireVue is tooa user in Azure AD.</span></span> <span data-ttu-id="5cc4b-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в HireVue должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-140">In other words, a link relationship between an Azure AD user and hello related user in HireVue needs toobe established.</span></span>

<span data-ttu-id="5cc4b-141">В HireVue, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-141">In HireVue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5cc4b-142">tooconfigure и теста Azure AD единого входа с HireVue, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-142">tooconfigure and test Azure AD single sign-on with HireVue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5cc4b-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5cc4b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5cc4b-145">**[Создание тестового пользователя HireVue](#creating-a-hirevue-test-user)**  -toohave аналог Саймон Britta в HireVue, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - toohave a counterpart of Britta Simon in HireVue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5cc4b-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5cc4b-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5cc4b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cc4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5cc4b-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении HireVue.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="5cc4b-150">**tooconfigure Azure AD единого входа с HireVue, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5cc4b-150">**tooconfigure Azure AD single sign-on with HireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="5cc4b-151">В hello в hello портала Azure **HireVue** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-151">In hello Azure portal, on hello **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5cc4b-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="5cc4b-155">На hello **URL-адреса и домена HireVue** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-155">On hello **HireVue Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="5cc4b-157">а.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-157">a.</span></span> <span data-ttu-id="5cc4b-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>

    | <span data-ttu-id="5cc4b-159">Среда</span><span class="sxs-lookup"><span data-stu-id="5cc4b-159">Environment</span></span> | <span data-ttu-id="5cc4b-160">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="5cc4b-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="5cc4b-161">Производство</span><span class="sxs-lookup"><span data-stu-id="5cc4b-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="5cc4b-162">Промежуточная</span><span class="sxs-lookup"><span data-stu-id="5cc4b-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="5cc4b-163">b.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-163">b.</span></span> <span data-ttu-id="5cc4b-164">В hello **идентификатор** текстовом поле введите URL-адрес как:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-164">In hello **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="5cc4b-165">Среда</span><span class="sxs-lookup"><span data-stu-id="5cc4b-165">Environment</span></span> | <span data-ttu-id="5cc4b-166">URN</span><span class="sxs-lookup"><span data-stu-id="5cc4b-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="5cc4b-167">Производство</span><span class="sxs-lookup"><span data-stu-id="5cc4b-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="5cc4b-168">Промежуточная</span><span class="sxs-lookup"><span data-stu-id="5cc4b-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="5cc4b-169">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-169">These values are not real.</span></span> <span data-ttu-id="5cc4b-170">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-170">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5cc4b-171">Обратитесь к [группа поддержки клиента HireVue](mailto:samlsupport@hirevue.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="5cc4b-172">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-172">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="5cc4b-174">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5cc4b-174">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5cc4b-176">На hello **конфигурации HireVue** щелкните **Настройка HireVue** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-176">On hello **HireVue Configuration** section, click **Configure HireVue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5cc4b-177">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="5cc4b-177">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="5cc4b-179">tooconfigure единого входа на **HireVue** стороны, необходимо загрузить hello toosend **Certificate(Base64)** и **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[HireVue поддержки](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="5cc4b-179">tooconfigure single sign-on on **HireVue** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="5cc4b-180">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-180">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5cc4b-181">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="5cc4b-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5cc4b-182">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5cc4b-183">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5cc4b-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5cc4b-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cc4b-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="5cc4b-185">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5cc4b-187">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5cc4b-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5cc4b-188">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5cc4b-190">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5cc4b-192">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="5cc4b-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5cc4b-194">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="5cc4b-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5cc4b-196">а.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-196">a.</span></span> <span data-ttu-id="5cc4b-197">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5cc4b-198">b.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-198">b.</span></span> <span data-ttu-id="5cc4b-199">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5cc4b-200">c.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-200">c.</span></span> <span data-ttu-id="5cc4b-201">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5cc4b-202">d.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-202">d.</span></span> <span data-ttu-id="5cc4b-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="5cc4b-204">Создание тестового пользователя HireVue</span><span class="sxs-lookup"><span data-stu-id="5cc4b-204">Creating a HireVue test user</span></span>

<span data-ttu-id="5cc4b-205">В этом разделе описано, как создать пользователя Britta Simon в приложении HireVue.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="5cc4b-206">Можно работать с [HireVue поддержки](mailto:samlsupport@hirevue.com) tooadd hello пользователей на платформе HireVue hello.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) tooadd hello users in hello HireVue platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5cc4b-207">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="5cc4b-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5cc4b-208">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHireVue доступа.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHireVue.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5cc4b-210">**tooassign tooHireVue Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="5cc4b-210">**tooassign Britta Simon tooHireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="5cc4b-211">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5cc4b-213">В списке приложений hello выберите **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-213">In hello applications list, select **HireVue**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="5cc4b-215">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5cc4b-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-217">Click **Add** button.</span></span> <span data-ttu-id="5cc4b-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5cc4b-220">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5cc4b-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5cc4b-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5cc4b-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5cc4b-223">Testing single sign-on</span></span>

<span data-ttu-id="5cc4b-224">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5cc4b-225">При нажатии кнопки hello HireVue плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour HireVue приложения.</span><span class="sxs-lookup"><span data-stu-id="5cc4b-225">When you click hello HireVue tile in hello Access Panel, you should get automatically signed-on tooyour HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5cc4b-226">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5cc4b-226">Additional resources</span></span>

* [<span data-ttu-id="5cc4b-227">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5cc4b-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5cc4b-228">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5cc4b-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

