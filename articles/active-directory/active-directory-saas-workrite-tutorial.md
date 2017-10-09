---
title: "Руководство по интеграции Azure Active Directory с Workrite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a663374ae3c8b102b53d8cf05a9cb083b80dbb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="ac6ed-103">Руководство. Интеграция Azure Active Directory с Workrite</span><span class="sxs-lookup"><span data-stu-id="ac6ed-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="ac6ed-104">В этом учебнике вы узнаете, как toointegrate Workrite с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ac6ed-104">In this tutorial, you learn how toointegrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac6ed-105">Интеграция с Azure AD Workrite предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ac6ed-105">Integrating Workrite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ac6ed-106">Можно управлять в Azure AD, имеющего доступ tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-106">You can control in Azure AD who has access tooWorkrite.</span></span>
- <span data-ttu-id="ac6ed-107">Можно включить на пользователей tooautomatically get вошедшего tooWorkrite (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-107">You can enable your users tooautomatically get signed-on tooWorkrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ac6ed-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="ac6ed-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac6ed-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac6ed-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ac6ed-110">Prerequisites</span></span>

<span data-ttu-id="ac6ed-111">tooconfigure интеграция Azure AD с Workrite требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ac6ed-111">tooconfigure Azure AD integration with Workrite, you need hello following items:</span></span>

- <span data-ttu-id="ac6ed-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ac6ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac6ed-113">подписка Workrite с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac6ed-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac6ed-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ac6ed-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac6ed-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac6ed-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac6ed-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac6ed-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ac6ed-118">Scenario description</span></span>
<span data-ttu-id="ac6ed-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac6ed-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ac6ed-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac6ed-121">Добавление Workrite из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ac6ed-121">Adding Workrite from hello gallery</span></span>
2. <span data-ttu-id="ac6ed-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac6ed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-hello-gallery"></a><span data-ttu-id="ac6ed-123">Добавление Workrite из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ac6ed-123">Adding Workrite from hello gallery</span></span>
<span data-ttu-id="ac6ed-124">tooconfigure hello интеграции Workrite в Azure AD, вы должны tooadd Workrite из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-124">tooconfigure hello integration of Workrite into Azure AD, you need tooadd Workrite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ac6ed-125">**tooadd Workrite из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac6ed-125">**tooadd Workrite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac6ed-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="ac6ed-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ac6ed-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="ac6ed-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="ac6ed-133">Введите в поле поиска hello **Workrite**выберите **Workrite** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-133">In hello search box, type **Workrite**, select **Workrite** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workrite в списке результатов hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ac6ed-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac6ed-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ac6ed-136">В этом разделе описана настройка и проверка единого входа Azure AD в Workrite с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ac6ed-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Workrite является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workrite is tooa user in Azure AD.</span></span> <span data-ttu-id="ac6ed-138">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Workrite должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-138">In other words, a link relationship between an Azure AD user and hello related user in Workrite needs toobe established.</span></span>

<span data-ttu-id="ac6ed-139">В Workrite, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-139">In Workrite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ac6ed-140">tooconfigure и теста Azure AD единого входа с Workrite, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ac6ed-140">tooconfigure and test Azure AD single sign-on with Workrite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ac6ed-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ac6ed-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac6ed-143">**[Создание тестового пользователя Workrite](#create-a-workrite-test-user)**  -toohave аналог Саймон Britta в Workrite, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - toohave a counterpart of Britta Simon in Workrite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac6ed-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac6ed-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ac6ed-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac6ed-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ac6ed-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Workrite.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="ac6ed-148">**tooconfigure Azure AD единого входа с Workrite, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac6ed-148">**tooconfigure Azure AD single sign-on with Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac6ed-149">В hello в hello портала Azure **Workrite** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-149">In hello Azure portal, on hello **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="ac6ed-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="ac6ed-153">На hello **URL-адреса и домена Workrite** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ac6ed-153">On hello **Workrite Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="ac6ed-155">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="ac6ed-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ac6ed-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-156">This value is not real.</span></span> <span data-ttu-id="ac6ed-157">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ac6ed-158">Обратитесь к [группа поддержки клиента Workrite](mailto:support@workrite.co.uk) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) tooget this value.</span></span>

4. <span data-ttu-id="ac6ed-159">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="ac6ed-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ac6ed-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ac6ed-163">На hello **конфигурации Workrite** щелкните **Настройка Workrite** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-163">On hello **Workrite Configuration** section, click **Configure Workrite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ac6ed-164">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="ac6ed-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Конфигурация Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="ac6ed-166">tooconfigure единого входа на **Workrite** стороны, необходимо загрузить hello toosend **Certificate(Base64), URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Workrite поддержки](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="ac6ed-166">tooconfigure single sign-on on **Workrite** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="ac6ed-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ac6ed-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ac6ed-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ac6ed-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac6ed-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ac6ed-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac6ed-170">Create an Azure AD test user</span></span>

<span data-ttu-id="ac6ed-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="ac6ed-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac6ed-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac6ed-174">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ac6ed-176">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ac6ed-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ac6ed-180">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ac6ed-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ac6ed-182">а.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-182">a.</span></span> <span data-ttu-id="ac6ed-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac6ed-184">b.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-184">b.</span></span> <span data-ttu-id="ac6ed-185">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ac6ed-186">c.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-186">c.</span></span> <span data-ttu-id="ac6ed-187">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ac6ed-188">d.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-188">d.</span></span> <span data-ttu-id="ac6ed-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="ac6ed-190">Создание тестового пользователя Workrite</span><span class="sxs-lookup"><span data-stu-id="ac6ed-190">Create a Workrite test user</span></span>

<span data-ttu-id="ac6ed-191">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Workrite.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-191">hello objective of this section is toocreate a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="ac6ed-192">**toocreate пользователя с именем Саймон Britta в Workrite, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac6ed-192">**toocreate a user called Britta Simon in Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac6ed-193">Войдите на сайт компании workrite tooyour от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-193">Sign on tooyour workrite company site as administrator.</span></span>

2. <span data-ttu-id="ac6ed-194">В области навигации hello, щелкните **администратора**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-194">In hello navigation pane, click **Admin**.</span></span>
   
    ![Элемент управления "Admin" (Администратор)][400]

3. <span data-ttu-id="ac6ed-196">Go tooQuick ссылки и нажмите кнопку **создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-196">Go tooQuick Links, and then click **Create a User**.</span></span>
   
    ![Раздел "Create a User" (Создание пользователя)][401]

4. <span data-ttu-id="ac6ed-198">На hello **Create User** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ac6ed-198">On hello **Create User** dialog, perform hello following steps:</span></span>
   
    ![Диалоговое окно"Create a User" (Создание пользователя)][402]
    
    <span data-ttu-id="ac6ed-200">а.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-200">a.</span></span> <span data-ttu-id="ac6ed-201">В hello **электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-201">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="ac6ed-202">b.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-202">b.</span></span> <span data-ttu-id="ac6ed-203">В hello **имя** текстового поля, типа hello firstname пользователя как Britta.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-203">In hello **First Name** textbox, type hello firstname of user like Britta.</span></span>

    <span data-ttu-id="ac6ed-204">c.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-204">c.</span></span> <span data-ttu-id="ac6ed-205">В hello **Фамилия** текстовое поле, Фамилия пользователя как Саймон типа hello.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-205">In hello **Surname** textbox, type hello surname of user like Simon.</span></span>
    
    <span data-ttu-id="ac6ed-206">d.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-206">d.</span></span> <span data-ttu-id="ac6ed-207">Выберите значение **Client Administrator** (Администратор клиента) в поле **Choose Role** (Выберите роль).</span><span class="sxs-lookup"><span data-stu-id="ac6ed-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="ac6ed-208">д.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-208">e.</span></span> <span data-ttu-id="ac6ed-209">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-209">Click **Save**.</span></span>   

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ac6ed-210">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ac6ed-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ac6ed-211">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWorkrite доступа.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkrite.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="ac6ed-213">**tooassign tooWorkrite Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ac6ed-213">**tooassign Britta Simon tooWorkrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac6ed-214">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ac6ed-216">В списке приложений hello выберите **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-216">In hello applications list, select **Workrite**.</span></span>

    ![ссылка Workrite Hello в списке приложений hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="ac6ed-218">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="ac6ed-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-220">Click **Add** button.</span></span> <span data-ttu-id="ac6ed-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="ac6ed-223">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ac6ed-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac6ed-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ac6ed-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ac6ed-226">Test single sign-on</span></span>

<span data-ttu-id="ac6ed-227">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="ac6ed-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="ac6ed-228">При нажатии кнопки hello Workrite плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Workrite приложения.</span><span class="sxs-lookup"><span data-stu-id="ac6ed-228">When you click hello Workrite tile in hello Access Panel, you should get automatically signed-on tooyour Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac6ed-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ac6ed-229">Additional resources</span></span>

* [<span data-ttu-id="ac6ed-230">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac6ed-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac6ed-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac6ed-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

