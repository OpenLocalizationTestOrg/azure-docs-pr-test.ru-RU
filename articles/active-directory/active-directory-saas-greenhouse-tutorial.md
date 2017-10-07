---
title: "Учебник. Интеграция Azure Active Directory с Greenhouse | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Greenhouse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 1a7cdd00c4f2b15a1afc89522d79af22f4c5d866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="c2512-103">Руководство. Интеграция Azure Active Directory с Greenhouse</span><span class="sxs-lookup"><span data-stu-id="c2512-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="c2512-104">В этом учебнике вы узнаете, как toointegrate Greenhouse с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c2512-104">In this tutorial, you learn how toointegrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c2512-105">Интеграция Greenhouse с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c2512-105">Integrating Greenhouse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c2512-106">Можно управлять в Azure AD, имеющего доступ tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="c2512-106">You can control in Azure AD who has access tooGreenhouse.</span></span>
- <span data-ttu-id="c2512-107">Можно включить на пользователей tooautomatically get вошедшего tooGreenhouse (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2512-107">You can enable your users tooautomatically get signed-on tooGreenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c2512-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c2512-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c2512-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c2512-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2512-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2512-110">Prerequisites</span></span>

<span data-ttu-id="c2512-111">tooconfigure интеграция Azure AD с Greenhouse требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c2512-111">tooconfigure Azure AD integration with Greenhouse, you need hello following items:</span></span>

- <span data-ttu-id="c2512-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c2512-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c2512-113">подписка с поддержкой единого входа Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="c2512-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2512-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c2512-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c2512-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c2512-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c2512-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c2512-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c2512-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2512-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c2512-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c2512-118">Scenario description</span></span>
<span data-ttu-id="c2512-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c2512-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c2512-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c2512-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c2512-121">Добавление Greenhouse из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c2512-121">Adding Greenhouse from hello gallery</span></span>
2. <span data-ttu-id="c2512-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2512-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-hello-gallery"></a><span data-ttu-id="c2512-123">Добавление Greenhouse из галереи hello</span><span class="sxs-lookup"><span data-stu-id="c2512-123">Adding Greenhouse from hello gallery</span></span>
<span data-ttu-id="c2512-124">tooconfigure hello интеграции Greenhouse в Azure AD, вы должны tooadd Greenhouse из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c2512-124">tooconfigure hello integration of Greenhouse into Azure AD, you need tooadd Greenhouse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c2512-125">**tooadd Greenhouse из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c2512-125">**tooadd Greenhouse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2512-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c2512-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="c2512-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c2512-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c2512-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c2512-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="c2512-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c2512-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="c2512-133">Введите в поле поиска hello **Greenhouse**выберите **Greenhouse** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c2512-133">In hello search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Greenhouse в списке результатов hello](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c2512-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2512-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c2512-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Greenhouse с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2512-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c2512-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Greenhouse является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2512-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Greenhouse is tooa user in Azure AD.</span></span> <span data-ttu-id="c2512-138">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Greenhouse должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="c2512-138">In other words, a link relationship between an Azure AD user and hello related user in Greenhouse needs toobe established.</span></span>

<span data-ttu-id="c2512-139">В Greenhouse, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c2512-139">In Greenhouse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c2512-140">tooconfigure и теста Azure AD единого входа с Greenhouse, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c2512-140">tooconfigure and test Azure AD single sign-on with Greenhouse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c2512-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c2512-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c2512-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c2512-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c2512-143">**[Создание тестового пользователя Greenhouse](#create-a-greenhouse-test-user)**  -toohave аналог Саймон Britta в Greenhouse, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c2512-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - toohave a counterpart of Britta Simon in Greenhouse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c2512-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c2512-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c2512-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c2512-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c2512-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2512-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c2512-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="c2512-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="c2512-148">**tooconfigure Azure AD единого входа с Greenhouse, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c2512-148">**tooconfigure Azure AD single sign-on with Greenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2512-149">В hello в hello портала Azure **Greenhouse** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c2512-149">In hello Azure portal, on hello **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="c2512-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c2512-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="c2512-153">На hello **URL-адреса и домена Greenhouse** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c2512-153">On hello **Greenhouse Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="c2512-155">а.</span><span class="sxs-lookup"><span data-stu-id="c2512-155">a.</span></span> <span data-ttu-id="c2512-156">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="c2512-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="c2512-157">b.</span><span class="sxs-lookup"><span data-stu-id="c2512-157">b.</span></span> <span data-ttu-id="c2512-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="c2512-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c2512-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c2512-159">These values are not real.</span></span> <span data-ttu-id="c2512-160">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c2512-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c2512-161">Обратитесь к [группа поддержки Greenhouse клиента](https://www.greenhouse.io/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="c2512-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) tooget these values.</span></span> 
 


4. <span data-ttu-id="c2512-162">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c2512-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="c2512-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c2512-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c2512-166">tooconfigure единого входа на **Greenhouse** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки greenhouse](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="c2512-166">tooconfigure single sign-on on **Greenhouse** side, you need toosend hello downloaded **Metadata XML** too[Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="c2512-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c2512-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c2512-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c2512-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c2512-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c2512-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c2512-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2512-170">Create an Azure AD test user</span></span>

<span data-ttu-id="c2512-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c2512-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="c2512-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c2512-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2512-174">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c2512-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c2512-176">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c2512-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c2512-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c2512-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c2512-180">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c2512-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c2512-182">а.</span><span class="sxs-lookup"><span data-stu-id="c2512-182">a.</span></span> <span data-ttu-id="c2512-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c2512-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c2512-184">b.</span><span class="sxs-lookup"><span data-stu-id="c2512-184">b.</span></span> <span data-ttu-id="c2512-185">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c2512-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c2512-186">c.</span><span class="sxs-lookup"><span data-stu-id="c2512-186">c.</span></span> <span data-ttu-id="c2512-187">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="c2512-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c2512-188">d.</span><span class="sxs-lookup"><span data-stu-id="c2512-188">d.</span></span> <span data-ttu-id="c2512-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c2512-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="c2512-190">Создание тестового пользователя Greenhouse</span><span class="sxs-lookup"><span data-stu-id="c2512-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="c2512-191">В порядке tooenable toolog пользователей Azure AD в Greenhouse их необходимо подготовить в Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="c2512-191">In order tooenable Azure AD users toolog into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="c2512-192">В случае Greenhouse hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="c2512-192">In hello case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="c2512-193">Можно использовать любые другие Greenhouse пользователя средства создания учетных записей или интерфейсы API, предоставляемые Greenhouse tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="c2512-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="c2512-194">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="c2512-194">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2512-195">Войдите в tooyour **Greenhouse** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c2512-195">Log in tooyour **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="c2512-196">В меню в верхней части hello hello выберите **Настройка**, а затем нажмите кнопку **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c2512-196">In hello menu on hello top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="c2512-197">![Пользователи](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="c2512-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="c2512-198">Нажмите кнопку **Новые пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c2512-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="c2512-199">![Новый пользователь](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="c2512-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="c2512-200">В hello **добавить пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c2512-200">In hello **Add New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="c2512-201">![Добавление нового пользователя](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Добавление нового пользователя")</span><span class="sxs-lookup"><span data-stu-id="c2512-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="c2512-202">а.</span><span class="sxs-lookup"><span data-stu-id="c2512-202">a.</span></span> <span data-ttu-id="c2512-203">В hello **сообщений электронной почты пользователя введите** текстовом поле введите адрес электронной почты hello действительной учетной записи Azure Active Directory требуется tooprovision.</span><span class="sxs-lookup"><span data-stu-id="c2512-203">In hello **Enter user emails** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision.</span></span>

   <span data-ttu-id="c2512-204">b.</span><span class="sxs-lookup"><span data-stu-id="c2512-204">b.</span></span> <span data-ttu-id="c2512-205">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c2512-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="c2512-206">Владельцы учетных записей Hello Azure Active Directory получит сообщение электронной почты, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="c2512-206">hello Azure Active Directory account holders will receive an email including a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c2512-207">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c2512-207">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c2512-208">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooGreenhouse доступа.</span><span class="sxs-lookup"><span data-stu-id="c2512-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGreenhouse.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="c2512-210">**tooassign tooGreenhouse Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c2512-210">**tooassign Britta Simon tooGreenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2512-211">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c2512-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c2512-213">В списке приложений hello выберите **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="c2512-213">In hello applications list, select **Greenhouse**.</span></span>

    ![ссылка Greenhouse Hello в списке приложений hello](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="c2512-215">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c2512-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="c2512-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c2512-217">Click **Add** button.</span></span> <span data-ttu-id="c2512-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c2512-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="c2512-220">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c2512-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c2512-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c2512-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c2512-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c2512-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c2512-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c2512-223">Test single sign-on</span></span>

<span data-ttu-id="c2512-224">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c2512-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c2512-225">При нажатии кнопки hello Greenhouse плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="c2512-225">When you click hello Greenhouse tile in hello Access Panel, you should get automatically signed-on tooyour Greenhouse application.</span></span>
<span data-ttu-id="c2512-226">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c2512-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c2512-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c2512-227">Additional resources</span></span>

* [<span data-ttu-id="c2512-228">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2512-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c2512-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c2512-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

