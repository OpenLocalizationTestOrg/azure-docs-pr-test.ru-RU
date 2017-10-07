---
title: "Руководство по интеграции Azure Active Directory с Synergi | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Synergi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5d4a9a596db2a60dda5bcac2c86b88b460a2e2cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="6101d-103">Руководство. Интеграция Azure Active Directory с Synergi</span><span class="sxs-lookup"><span data-stu-id="6101d-103">Tutorial: Azure Active Directory integration with Synergi</span></span>

<span data-ttu-id="6101d-104">В этом учебнике вы узнаете, как toointegrate Synergi с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6101d-104">In this tutorial, you learn how toointegrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6101d-105">Интеграция с Azure AD Synergi предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="6101d-105">Integrating Synergi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6101d-106">Можно управлять в Azure AD, имеющего доступ tooSynergi.</span><span class="sxs-lookup"><span data-stu-id="6101d-106">You can control in Azure AD who has access tooSynergi.</span></span>
- <span data-ttu-id="6101d-107">Можно включить на пользователей tooautomatically get вошедшего tooSynergi (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6101d-107">You can enable your users tooautomatically get signed-on tooSynergi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6101d-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6101d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6101d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6101d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6101d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6101d-110">Prerequisites</span></span>

<span data-ttu-id="6101d-111">tooconfigure интеграция Azure AD с Synergi требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="6101d-111">tooconfigure Azure AD integration with Synergi, you need hello following items:</span></span>

- <span data-ttu-id="6101d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6101d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6101d-113">подписка на Synergi с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="6101d-113">A Synergi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6101d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6101d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6101d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="6101d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6101d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6101d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6101d-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6101d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6101d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6101d-118">Scenario description</span></span>
<span data-ttu-id="6101d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6101d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6101d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="6101d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6101d-121">Добавление Synergi из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6101d-121">Adding Synergi from hello gallery</span></span>
2. <span data-ttu-id="6101d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6101d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-synergi-from-hello-gallery"></a><span data-ttu-id="6101d-123">Добавление Synergi из галереи hello</span><span class="sxs-lookup"><span data-stu-id="6101d-123">Adding Synergi from hello gallery</span></span>
<span data-ttu-id="6101d-124">tooconfigure hello интеграции Synergi в Azure AD, вы должны tooadd Synergi из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6101d-124">tooconfigure hello integration of Synergi into Azure AD, you need tooadd Synergi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6101d-125">**tooadd Synergi из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6101d-125">**tooadd Synergi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6101d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="6101d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="6101d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="6101d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6101d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6101d-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="6101d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6101d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="6101d-133">Введите в поле поиска hello **Synergi**выберите **Synergi** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6101d-133">In hello search box, type **Synergi**, select **Synergi** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Synergi в списке результатов hello](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6101d-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6101d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6101d-136">В этом разделе описана настройка и проверка единого входа Azure AD в Synergi с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6101d-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6101d-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Synergi является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6101d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Synergi is tooa user in Azure AD.</span></span> <span data-ttu-id="6101d-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Synergi должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="6101d-138">In other words, a link relationship between an Azure AD user and hello related user in Synergi needs toobe established.</span></span>

<span data-ttu-id="6101d-139">В Synergi, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="6101d-139">In Synergi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6101d-140">tooconfigure и теста Azure AD единого входа с Synergi, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6101d-140">tooconfigure and test Azure AD single sign-on with Synergi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6101d-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="6101d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6101d-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="6101d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6101d-143">**[Создание тестового пользователя Synergi](#create-a-synergi-test-user)**  -toohave аналог Саймон Britta в Synergi, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="6101d-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - toohave a counterpart of Britta Simon in Synergi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6101d-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="6101d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6101d-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6101d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6101d-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="6101d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6101d-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Synergi.</span><span class="sxs-lookup"><span data-stu-id="6101d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Synergi application.</span></span>

<span data-ttu-id="6101d-148">**tooconfigure Azure AD единого входа с Synergi, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6101d-148">**tooconfigure Azure AD single sign-on with Synergi, perform hello following steps:**</span></span>

1. <span data-ttu-id="6101d-149">В hello в hello портала Azure **Synergi** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="6101d-149">In hello Azure portal, on hello **Synergi** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="6101d-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="6101d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_samlbase.png)

3. <span data-ttu-id="6101d-153">На hello **URL-адреса и домена Synergi** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6101d-153">On hello **Synergi Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_url.png)

    <span data-ttu-id="6101d-155">а.</span><span class="sxs-lookup"><span data-stu-id="6101d-155">a.</span></span> <span data-ttu-id="6101d-156">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.irmsecurity.com`</span><span class="sxs-lookup"><span data-stu-id="6101d-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.irmsecurity.com`</span></span>

    <span data-ttu-id="6101d-157">b.</span><span class="sxs-lookup"><span data-stu-id="6101d-157">b.</span></span> <span data-ttu-id="6101d-158">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.irmsecurity.com/sso/<organization id>`</span><span class="sxs-lookup"><span data-stu-id="6101d-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6101d-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="6101d-159">These values are not real.</span></span> <span data-ttu-id="6101d-160">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6101d-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6101d-161">Обратитесь к [Synergi поддержки](https://www.irmsecurity.com/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="6101d-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) tooget these values.</span></span>

4. <span data-ttu-id="6101d-162">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="6101d-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_certificate.png) 

5. <span data-ttu-id="6101d-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6101d-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-synergi-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6101d-166">На hello **конфигурации Synergi** щелкните **Настройка Synergi** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="6101d-166">On hello **Synergi Configuration** section, click **Configure Synergi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6101d-167">Копировать hello **URL-адрес выхода и идентификатор сущности SAML** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="6101d-167">Copy hello **Sign-Out URL and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Настройка Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_configure.png) 

7. <span data-ttu-id="6101d-169">tooconfigure единого входа на **Synergi** стороны, необходимо загрузить hello toosend **Certificate(Base64), URL-адрес выхода и идентификатор сущности SAML** слишком[Synergi поддержки](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="6101d-169">tooconfigure single sign-on on **Synergi** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** too[Synergi support team](https://www.irmsecurity.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="6101d-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="6101d-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6101d-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="6101d-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6101d-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6101d-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6101d-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6101d-173">Create an Azure AD test user</span></span>

<span data-ttu-id="6101d-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6101d-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="6101d-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6101d-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6101d-177">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6101d-177">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-synergi-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6101d-179">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6101d-179">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-synergi-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6101d-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6101d-181">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-synergi-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6101d-183">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="6101d-183">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-synergi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6101d-185">а.</span><span class="sxs-lookup"><span data-stu-id="6101d-185">a.</span></span> <span data-ttu-id="6101d-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6101d-186">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6101d-187">b.</span><span class="sxs-lookup"><span data-stu-id="6101d-187">b.</span></span> <span data-ttu-id="6101d-188">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="6101d-188">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6101d-189">c.</span><span class="sxs-lookup"><span data-stu-id="6101d-189">c.</span></span> <span data-ttu-id="6101d-190">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="6101d-190">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6101d-191">d.</span><span class="sxs-lookup"><span data-stu-id="6101d-191">d.</span></span> <span data-ttu-id="6101d-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6101d-192">Click **Create**.</span></span>
  
### <a name="create-a-synergi-test-user"></a><span data-ttu-id="6101d-193">Создание тестового пользователя Synergi</span><span class="sxs-lookup"><span data-stu-id="6101d-193">Create a Synergi test user</span></span>

<span data-ttu-id="6101d-194">В этом разделе описано, как создать пользователя Britta Simon в приложении Synergi.</span><span class="sxs-lookup"><span data-stu-id="6101d-194">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="6101d-195">Работать с [Synergi поддержки](https://www.irmsecurity.com/contact/) для добавления пользователей hello в платформе Synergi hello.</span><span class="sxs-lookup"><span data-stu-id="6101d-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add hello users in hello Synergi platform.</span></span> <span data-ttu-id="6101d-196">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="6101d-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6101d-197">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="6101d-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6101d-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSynergi доступа.</span><span class="sxs-lookup"><span data-stu-id="6101d-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSynergi.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="6101d-200">**tooassign tooSynergi Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="6101d-200">**tooassign Britta Simon tooSynergi, perform hello following steps:**</span></span>

1. <span data-ttu-id="6101d-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6101d-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="6101d-203">В списке приложений hello выберите **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="6101d-203">In hello applications list, select **Synergi**.</span></span>

    ![ссылка Synergi Hello в списке приложений hello](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_app.png)  

3. <span data-ttu-id="6101d-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="6101d-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="6101d-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6101d-207">Click **Add** button.</span></span> <span data-ttu-id="6101d-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6101d-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="6101d-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="6101d-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6101d-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6101d-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6101d-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="6101d-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6101d-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6101d-213">Test single sign-on</span></span>

<span data-ttu-id="6101d-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="6101d-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6101d-215">При нажатии кнопки hello Synergi плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Synergi приложения.</span><span class="sxs-lookup"><span data-stu-id="6101d-215">When you click hello Synergi tile in hello Access Panel, you should get automatically signed-on tooyour Synergi application.</span></span>
<span data-ttu-id="6101d-216">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6101d-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6101d-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6101d-217">Additional resources</span></span>

* [<span data-ttu-id="6101d-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6101d-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6101d-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6101d-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_203.png

