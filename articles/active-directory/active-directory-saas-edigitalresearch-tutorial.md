---
title: "Учебник. Интеграция Azure Active Directory с eDigitalResearch | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="76045-103">Руководство. Интеграция Azure Active Directory с eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="76045-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="76045-104">В этом учебнике вы узнаете, как eDigitalResearch toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76045-104">In this tutorial, you learn how toointegrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76045-105">Интеграция с Azure AD eDigitalResearch предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="76045-105">Integrating eDigitalResearch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="76045-106">Можно управлять в Azure AD, имеющего доступ tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="76045-106">You can control in Azure AD who has access tooeDigitalResearch.</span></span>
- <span data-ttu-id="76045-107">Можно включить на пользователей tooautomatically get вошедшего tooeDigitalResearch (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76045-107">You can enable your users tooautomatically get signed-on tooeDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="76045-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="76045-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="76045-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76045-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76045-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="76045-110">Prerequisites</span></span>

<span data-ttu-id="76045-111">tooconfigure интеграция Azure AD с eDigitalResearch требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="76045-111">tooconfigure Azure AD integration with eDigitalResearch, you need hello following items:</span></span>

- <span data-ttu-id="76045-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="76045-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76045-113">подписка на eDigitalResearch с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="76045-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76045-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="76045-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76045-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="76045-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76045-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="76045-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76045-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76045-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76045-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="76045-118">Scenario description</span></span>
<span data-ttu-id="76045-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="76045-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76045-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="76045-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76045-121">Добавление eDigitalResearch из галереи hello</span><span class="sxs-lookup"><span data-stu-id="76045-121">Adding eDigitalResearch from hello gallery</span></span>
2. <span data-ttu-id="76045-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="76045-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-hello-gallery"></a><span data-ttu-id="76045-123">Добавление eDigitalResearch из галереи hello</span><span class="sxs-lookup"><span data-stu-id="76045-123">Adding eDigitalResearch from hello gallery</span></span>
<span data-ttu-id="76045-124">tooconfigure hello интеграции eDigitalResearch в Azure AD, вы должны eDigitalResearch tooadd из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="76045-124">tooconfigure hello integration of eDigitalResearch into Azure AD, you need tooadd eDigitalResearch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="76045-125">**eDigitalResearch tooadd из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="76045-125">**tooadd eDigitalResearch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="76045-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="76045-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="76045-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="76045-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="76045-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="76045-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="76045-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="76045-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="76045-133">Введите в поле поиска hello **eDigitalResearch**выберите **eDigitalResearch** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="76045-133">In hello search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button tooadd hello application.</span></span>

    ![eDigitalResearch в списке результатов hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="76045-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="76045-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="76045-136">В этом разделе описана настройка и проверка единого входа Azure AD в eDigitalResearch с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76045-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76045-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в eDigitalResearch является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76045-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eDigitalResearch is tooa user in Azure AD.</span></span> <span data-ttu-id="76045-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в eDigitalResearch должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="76045-138">In other words, a link relationship between an Azure AD user and hello related user in eDigitalResearch needs toobe established.</span></span>

<span data-ttu-id="76045-139">В eDigitalResearch, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="76045-139">In eDigitalResearch, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="76045-140">tooconfigure и теста Azure AD единого входа с eDigitalResearch, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="76045-140">tooconfigure and test Azure AD single sign-on with eDigitalResearch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="76045-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="76045-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="76045-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="76045-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76045-143">**[Создание тестового пользователя eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave аналог Саймон Britta в eDigitalResearch, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="76045-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - toohave a counterpart of Britta Simon in eDigitalResearch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="76045-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="76045-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76045-145">**[Тестирование единого входа](#test-single-sign-on)**  tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76045-145">**[Test single sign-on](#test-single-sign-on)**  tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="76045-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="76045-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="76045-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="76045-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="76045-148">**tooconfigure Azure AD единого входа с eDigitalResearch, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="76045-148">**tooconfigure Azure AD single sign-on with eDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="76045-149">В hello в hello портала Azure **eDigitalResearch** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="76045-149">In hello Azure portal, on hello **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="76045-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="76045-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="76045-153">На hello **eDigitalResearch URL-адреса и домена** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="76045-153">On hello **eDigitalResearch Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="76045-155">а.</span><span class="sxs-lookup"><span data-stu-id="76045-155">a.</span></span> <span data-ttu-id="76045-156">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="76045-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="76045-157">b.</span><span class="sxs-lookup"><span data-stu-id="76045-157">b.</span></span> <span data-ttu-id="76045-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="76045-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="76045-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="76045-159">These values are not real.</span></span> <span data-ttu-id="76045-160">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="76045-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="76045-161">Обратитесь к [eDigitalResearch поддержки](http://www.maruedr.com/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="76045-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) tooget these values.</span></span>
 


4. <span data-ttu-id="76045-162">На hello **сертификат подписи SAML** щелкните **Base(64) сертификат** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="76045-162">On hello **SAML Signing Certificate** section, click **Certificate Base(64)** and then save hello certificate file on your computer.</span></span>

    <span data-ttu-id="76045-163">!</span><span class="sxs-lookup"><span data-stu-id="76045-163">!</span></span>![ссылку для скачивания сертификата Hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="76045-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="76045-165">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="76045-167">На hello **eDigitalResearch конфигурации** щелкните **Настройка eDigitalResearch** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="76045-167">On hello **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="76045-168">Копировать hello **URL-адрес выхода, идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="76045-168">Copy hello **Sign-Out URL, SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="76045-170">tooconfigure единого входа на **eDigitalResearch** стороны, необходимо загрузить hello toosend **файл сертификата (Base64)**, **идентификатор сущности SAML**, и  **URL-адрес выхода** слишком[eDigitalResearch поддержки](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="76045-170">tooconfigure single sign-on on **eDigitalResearch** side, you need toosend hello downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** too[eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="76045-171">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="76045-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="76045-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="76045-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="76045-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="76045-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="76045-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76045-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="76045-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="76045-175">Create an Azure AD test user</span></span>

<span data-ttu-id="76045-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="76045-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="76045-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="76045-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="76045-179">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="76045-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="76045-181">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="76045-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="76045-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="76045-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="76045-185">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="76045-185">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="76045-187">а.</span><span class="sxs-lookup"><span data-stu-id="76045-187">a.</span></span> <span data-ttu-id="76045-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76045-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76045-189">b.</span><span class="sxs-lookup"><span data-stu-id="76045-189">b.</span></span> <span data-ttu-id="76045-190">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="76045-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="76045-191">c.</span><span class="sxs-lookup"><span data-stu-id="76045-191">c.</span></span> <span data-ttu-id="76045-192">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="76045-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="76045-193">d.</span><span class="sxs-lookup"><span data-stu-id="76045-193">d.</span></span> <span data-ttu-id="76045-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="76045-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="76045-195">Создание тестового пользователя eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="76045-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="76045-196">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="76045-196">hello objective of this section is toocreate a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="76045-197">Работать с hello [eDigitalResearch поддержки](http://www.maruedr.com/contact) tooget пользователей, созданных.</span><span class="sxs-lookup"><span data-stu-id="76045-197">Work with hello [eDigitalResearch support team](http://www.maruedr.com/contact) tooget users created.</span></span>       
    
 > [!NOTE]
 > <span data-ttu-id="76045-198">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="76045-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="76045-199">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="76045-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="76045-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooeDigitalResearch доступа.</span><span class="sxs-lookup"><span data-stu-id="76045-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeDigitalResearch.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="76045-202">**tooassign tooeDigitalResearch Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="76045-202">**tooassign Britta Simon tooeDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="76045-203">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="76045-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="76045-205">В списке приложений hello выберите **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="76045-205">In hello applications list, select **eDigitalResearch**.</span></span>

    ![ссылка eDigitalResearch Hello в списке приложений hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="76045-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="76045-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="76045-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="76045-209">Click **Add** button.</span></span> <span data-ttu-id="76045-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="76045-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="76045-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="76045-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="76045-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="76045-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="76045-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="76045-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="76045-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="76045-215">Test single sign-on</span></span>

<span data-ttu-id="76045-216">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="76045-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="76045-217">При нажатии кнопки hello eDigitalResearch плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour eDigitalResearch приложения.</span><span class="sxs-lookup"><span data-stu-id="76045-217">When you click hello eDigitalResearch tile in hello Access Panel, you should get automatically signed-on tooyour eDigitalResearch application.</span></span>
<span data-ttu-id="76045-218">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76045-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="76045-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="76045-219">Additional resources</span></span>

* [<span data-ttu-id="76045-220">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76045-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76045-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="76045-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

