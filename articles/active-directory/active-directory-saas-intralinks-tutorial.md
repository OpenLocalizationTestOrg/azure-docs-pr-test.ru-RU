---
title: "Учебник. Интеграция Azure Active Directory с Intralinks | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="8b4a6-103">Руководство. Интеграция Azure Active Directory с Intralinks</span><span class="sxs-lookup"><span data-stu-id="8b4a6-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="8b4a6-104">В этом учебнике вы узнаете, как toointegrate Intralinks с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b4a6-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b4a6-105">Интеграция с Azure AD Intralinks предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8b4a6-106">Можно управлять в Azure AD, имеющего доступ tooIntralinks</span><span class="sxs-lookup"><span data-stu-id="8b4a6-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="8b4a6-107">Можно включить на пользователей tooautomatically get вошедшего tooIntralinks (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4a6-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b4a6-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8b4a6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8b4a6-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b4a6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b4a6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8b4a6-110">Prerequisites</span></span>

<span data-ttu-id="8b4a6-111">tooconfigure интеграция Azure AD с Intralinks требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="8b4a6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8b4a6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b4a6-113">подписка Intralinks с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b4a6-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b4a6-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b4a6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b4a6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b4a6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b4a6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8b4a6-118">Scenario description</span></span>
<span data-ttu-id="8b4a6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b4a6-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b4a6-121">Добавление Intralinks из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8b4a6-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="8b4a6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4a6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="8b4a6-123">Добавление Intralinks из галереи hello</span><span class="sxs-lookup"><span data-stu-id="8b4a6-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="8b4a6-124">tooconfigure hello интеграции Intralinks в Azure AD, вы должны tooadd Intralinks из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b4a6-125">**tooadd Intralinks из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8b4a6-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b4a6-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8b4a6-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8b4a6-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8b4a6-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8b4a6-133">Введите в поле поиска hello **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-133">In hello search box, type **Intralinks**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="8b4a6-135">В панели результатов hello выберите **Intralinks**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b4a6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4a6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b4a6-138">В этом разделе описана настройка и проверка единого входа Azure AD в Intralinks с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b4a6-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Intralinks является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="8b4a6-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Intralinks должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="8b4a6-141">В Intralinks, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8b4a6-142">tooconfigure и теста Azure AD единого входа с Intralinks, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8b4a6-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8b4a6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b4a6-145">**[Создание тестового пользователя, прошедшего Intralinks](#creating-an-intralinks-test-user)**  -toohave аналог Саймон Britta в Intralinks, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b4a6-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b4a6-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b4a6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4a6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b4a6-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Intralinks.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="8b4a6-150">**tooconfigure Azure AD единого входа с Intralinks, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8b4a6-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b4a6-151">В hello в hello портала Azure **Intralinks** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8b4a6-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="8b4a6-155">На hello **URL-адреса и домена Intralinks** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="8b4a6-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="8b4a6-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b4a6-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-158">This value is not real.</span></span> <span data-ttu-id="8b4a6-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8b4a6-160">Обратитесь к [группа поддержки клиента Intralinks](https://www.intralinks.com/contact-1) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="8b4a6-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="8b4a6-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8b4a6-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b4a6-165">tooconfigure единого входа на **Intralinks** стороны, необходимо загрузить hello toosend **метаданные в формате XML** [Intralinks поддержки](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="8b4a6-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="8b4a6-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8b4a6-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="8b4a6-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8b4a6-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8b4a6-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b4a6-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b4a6-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4a6-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b4a6-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8b4a6-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8b4a6-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b4a6-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b4a6-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b4a6-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="8b4a6-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b4a6-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b4a6-182">а.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-182">a.</span></span> <span data-ttu-id="8b4a6-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b4a6-184">b.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-184">b.</span></span> <span data-ttu-id="8b4a6-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b4a6-186">c.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-186">c.</span></span> <span data-ttu-id="8b4a6-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8b4a6-188">d.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-188">d.</span></span> <span data-ttu-id="8b4a6-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="8b4a6-190">Создание тестового пользователя Intralinks</span><span class="sxs-lookup"><span data-stu-id="8b4a6-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="8b4a6-191">В этом разделе описано, как создать пользователя Britta Simon в приложении Intralinks.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="8b4a6-192">Можно работать с [Intralinks поддержки](https://www.intralinks.com/contact-1) tooadd hello пользователей на платформе Intralinks hello.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8b4a6-193">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="8b4a6-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8b4a6-194">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooIntralinks доступа.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8b4a6-196">**tooassign tooIntralinks Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8b4a6-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b4a6-197">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8b4a6-199">В списке приложений hello выберите **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-199">In hello applications list, select **Intralinks**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="8b4a6-201">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8b4a6-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-203">Click **Add** button.</span></span> <span data-ttu-id="8b4a6-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8b4a6-206">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8b4a6-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b4a6-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="8b4a6-209">Добавление приложения Intralinks VIA или Elite</span><span class="sxs-lookup"><span data-stu-id="8b4a6-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="8b4a6-210">Использует Intralinks hello же платформой удостоверений единого входа для всех других приложений Intralinks, за исключением возможности хранилища приложения.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="8b4a6-211">Поэтому если планируется toouse любого другого приложения Intralinks сначала вы имеете tooconfigure единого входа для одного приложения основной Intralinks, используя описанную выше процедуру hello.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="8b4a6-212">После этого можно выполнить hello ниже процедуры tooadd другое приложение Intralinks в клиенте, который можно использовать этот основного приложения для единого входа.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="8b4a6-213">Этот компонент является доступны только клиентам SKU Premium tooAzure AD и недоступно для клиентов Free или Basic SKU.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="8b4a6-214">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="8b4a6-216">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8b4a6-217">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-217">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8b4a6-219">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8b4a6-221">Введите в поле поиска hello **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-221">In hello search box, type **Intralinks**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="8b4a6-223">На **Intralinks добавить приложение** выполнения hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![Добавление приложения Intralinks VIA или Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="8b4a6-225">а.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-225">a.</span></span> <span data-ttu-id="8b4a6-226">В **имя** текстового поля, введите соответствующее имя приложения hello, например **элиту Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="8b4a6-227">b.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-227">b.</span></span> <span data-ttu-id="8b4a6-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="8b4a6-229">В hello в hello портала Azure **Intralinks** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

7. <span data-ttu-id="8b4a6-231">На hello **единого входа** диалогового окна выберите **режим** как **входа на связанный**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="8b4a6-233">Получить hello hello SP инициировано SSO URL-адрес [команды Intralinks](https://www.intralinks.com/contact-1) для hello другого Intralinks приложения и введите его в **Настройка URL-адрес входа** как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="8b4a6-235">В текстовом поле на URL-адрес входа hello введите URL-адрес hello, используемого приложением Intralinks tooyour toosign на пользователей, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="8b4a6-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="8b4a6-236">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8b4a6-236">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="8b4a6-238">Назначение toouser приложения hello или групп, как показано в разделе "hello"  **[назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="8b4a6-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8b4a6-239">Testing single sign-on</span></span>

<span data-ttu-id="8b4a6-240">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8b4a6-241">При нажатии кнопки Intralinks плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Intralinks приложения.</span><span class="sxs-lookup"><span data-stu-id="8b4a6-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="8b4a6-242">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8b4a6-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b4a6-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8b4a6-243">Additional resources</span></span>

* [<span data-ttu-id="8b4a6-244">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b4a6-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b4a6-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b4a6-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

