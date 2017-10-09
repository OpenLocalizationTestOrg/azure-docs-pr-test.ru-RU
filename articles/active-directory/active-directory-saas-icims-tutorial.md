---
title: "Учебник. Интеграция Azure Active Directory с ICIMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="75af7-103">Руководство. Интеграция Azure Active Directory с ICIMS</span><span class="sxs-lookup"><span data-stu-id="75af7-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="75af7-104">В этом учебнике вы узнаете, как toointegrate ICIMS с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75af7-104">In this tutorial, you learn how toointegrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75af7-105">Интеграция с Azure AD ICIMS предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="75af7-105">Integrating ICIMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="75af7-106">Можно управлять в Azure AD, имеющего доступ tooICIMS</span><span class="sxs-lookup"><span data-stu-id="75af7-106">You can control in Azure AD who has access tooICIMS</span></span>
- <span data-ttu-id="75af7-107">Можно включить на пользователей tooautomatically get вошедшего tooICIMS (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="75af7-107">You can enable your users tooautomatically get signed-on tooICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75af7-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="75af7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="75af7-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75af7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75af7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="75af7-110">Prerequisites</span></span>

<span data-ttu-id="75af7-111">tooconfigure интеграция Azure AD с ICIMS требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="75af7-111">tooconfigure Azure AD integration with ICIMS, you need hello following items:</span></span>

- <span data-ttu-id="75af7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="75af7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75af7-113">подписка ICIMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="75af7-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75af7-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="75af7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75af7-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="75af7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75af7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="75af7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75af7-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75af7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75af7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="75af7-118">Scenario description</span></span>
<span data-ttu-id="75af7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="75af7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75af7-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="75af7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75af7-121">Добавление ICIMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="75af7-121">Adding ICIMS from hello gallery</span></span>
2. <span data-ttu-id="75af7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="75af7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-hello-gallery"></a><span data-ttu-id="75af7-123">Добавление ICIMS из галереи hello</span><span class="sxs-lookup"><span data-stu-id="75af7-123">Adding ICIMS from hello gallery</span></span>
<span data-ttu-id="75af7-124">tooconfigure hello интеграции ICIMS в Azure AD, вы должны tooadd ICIMS из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="75af7-124">tooconfigure hello integration of ICIMS into Azure AD, you need tooadd ICIMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="75af7-125">**tooadd ICIMS из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="75af7-125">**tooadd ICIMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="75af7-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="75af7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="75af7-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="75af7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="75af7-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="75af7-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="75af7-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="75af7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="75af7-133">Введите в поле поиска hello **ICIMS**выберите **ICIMS** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="75af7-133">In hello search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ICIMS в списке результатов hello](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="75af7-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="75af7-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="75af7-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение ICIMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75af7-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75af7-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ICIMS является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75af7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ICIMS is tooa user in Azure AD.</span></span> <span data-ttu-id="75af7-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в ICIMS должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="75af7-138">In other words, a link relationship between an Azure AD user and hello related user in ICIMS needs toobe established.</span></span>

<span data-ttu-id="75af7-139">В ICIMS, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="75af7-139">In ICIMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="75af7-140">tooconfigure и теста Azure AD единого входа с ICIMS, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="75af7-140">tooconfigure and test Azure AD single sign-on with ICIMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="75af7-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="75af7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="75af7-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="75af7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75af7-143">**[Создание тестового пользователя, прошедшего ICIMS](#create-an-icims-test-user)**  -toohave аналог Саймон Britta в ICIMS, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="75af7-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - toohave a counterpart of Britta Simon in ICIMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="75af7-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="75af7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75af7-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="75af7-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="75af7-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="75af7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="75af7-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ICIMS.</span><span class="sxs-lookup"><span data-stu-id="75af7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="75af7-148">**tooconfigure Azure AD единого входа с ICIMS, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="75af7-148">**tooconfigure Azure AD single sign-on with ICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="75af7-149">В hello в hello портала Azure **ICIMS** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="75af7-149">In hello Azure portal, on hello **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="75af7-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="75af7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="75af7-153">На hello **URL-адреса и домена ICIMS** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="75af7-153">On hello **ICIMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="75af7-155">а.</span><span class="sxs-lookup"><span data-stu-id="75af7-155">a.</span></span> <span data-ttu-id="75af7-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="75af7-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="75af7-157">b.</span><span class="sxs-lookup"><span data-stu-id="75af7-157">b.</span></span> <span data-ttu-id="75af7-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="75af7-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75af7-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="75af7-159">These values are not real.</span></span> <span data-ttu-id="75af7-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="75af7-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="75af7-161">Обратитесь к [группа поддержки клиента ICIMS](https://www.icims.com/contact-us) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="75af7-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="75af7-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="75af7-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="75af7-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="75af7-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="75af7-166">На hello **конфигурации ICIMS** щелкните **Настройка ICIMS** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="75af7-166">On hello **ICIMS Configuration** section, click **Configure ICIMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="75af7-167">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="75af7-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="75af7-169">tooconfigure единого входа на **ICIMS** стороны, необходимо загрузить hello toosend **метаданные в формате XML**, **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком [ICIMS поддержки](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="75af7-169">tooconfigure single sign-on on **ICIMS** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="75af7-170">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="75af7-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="75af7-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="75af7-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="75af7-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="75af7-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="75af7-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75af7-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="75af7-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="75af7-174">Create an Azure AD test user</span></span>
<span data-ttu-id="75af7-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="75af7-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="75af7-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="75af7-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="75af7-178">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="75af7-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75af7-180">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="75af7-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75af7-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="75af7-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75af7-184">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="75af7-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75af7-186">а.</span><span class="sxs-lookup"><span data-stu-id="75af7-186">a.</span></span> <span data-ttu-id="75af7-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75af7-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75af7-188">b.</span><span class="sxs-lookup"><span data-stu-id="75af7-188">b.</span></span> <span data-ttu-id="75af7-189">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="75af7-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="75af7-190">c.</span><span class="sxs-lookup"><span data-stu-id="75af7-190">c.</span></span> <span data-ttu-id="75af7-191">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="75af7-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="75af7-192">d.</span><span class="sxs-lookup"><span data-stu-id="75af7-192">d.</span></span> <span data-ttu-id="75af7-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="75af7-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="75af7-194">Создание тестового пользователя ICIMS</span><span class="sxs-lookup"><span data-stu-id="75af7-194">Create an ICIMS test user</span></span>

<span data-ttu-id="75af7-195">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в ICIMS.</span><span class="sxs-lookup"><span data-stu-id="75af7-195">hello objective of this section is toocreate a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="75af7-196">Работать с [ICIMS поддержки](https://www.icims.com/contact-us) tooadd пользователей hello в hello ICIMS учетной записи.</span><span class="sxs-lookup"><span data-stu-id="75af7-196">Work with [ICIMS support team](https://www.icims.com/contact-us) tooadd hello users in hello ICIMS account.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="75af7-197">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="75af7-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="75af7-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooICIMS доступа.</span><span class="sxs-lookup"><span data-stu-id="75af7-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooICIMS.</span></span>

![Назначение пользователям ролей hello][200]

<span data-ttu-id="75af7-200">**tooassign tooICIMS Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="75af7-200">**tooassign Britta Simon tooICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="75af7-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="75af7-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="75af7-203">В списке приложений hello выберите **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="75af7-203">In hello applications list, select **ICIMS**.</span></span>

    ![ссылка ICIMS Hello в списке приложений hello](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="75af7-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="75af7-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202] 

4. <span data-ttu-id="75af7-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="75af7-207">Click **Add** button.</span></span> <span data-ttu-id="75af7-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="75af7-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="75af7-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="75af7-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="75af7-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="75af7-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75af7-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="75af7-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="75af7-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="75af7-213">Test single sign-on</span></span>

<span data-ttu-id="75af7-214">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="75af7-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="75af7-215">При нажатии кнопки ICIMS плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour ICIMS приложения.</span><span class="sxs-lookup"><span data-stu-id="75af7-215">When you click hello ICIMS tile in hello Access Panel, you should get automatically signed-on tooyour ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75af7-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="75af7-216">Additional resources</span></span>

* [<span data-ttu-id="75af7-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75af7-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75af7-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="75af7-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

