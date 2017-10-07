---
title: "Учебник. Интеграция Azure Active Directory с Fuse | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и предохранитель."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 720ed8af0b5de1e3bee5a40353ca0ee661766864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="c4422-103">Руководство. Интеграция Azure Active Directory с Fuse</span><span class="sxs-lookup"><span data-stu-id="c4422-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="c4422-104">В этом учебнике вы узнаете, как объединять toointegrate с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4422-104">In this tutorial, you learn how toointegrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4422-105">Интеграция предохранитель с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c4422-105">Integrating Fuse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4422-106">Можно управлять в Azure AD, имеющего доступ tooFuse.</span><span class="sxs-lookup"><span data-stu-id="c4422-106">You can control in Azure AD who has access tooFuse.</span></span>
- <span data-ttu-id="c4422-107">Можно включить на пользователей tooautomatically get вошедшего tooFuse (Single Sign-On) с помощью своих учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4422-107">You can enable your users tooautomatically get signed-on tooFuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c4422-108">Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c4422-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c4422-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4422-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4422-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c4422-110">Prerequisites</span></span>

<span data-ttu-id="c4422-111">Интеграция Azure AD tooconfigure с предохранитель, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="c4422-111">tooconfigure Azure AD integration with Fuse, you need hello following items:</span></span>

- <span data-ttu-id="c4422-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c4422-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4422-113">Подписка на Fuse с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c4422-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4422-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c4422-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4422-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="c4422-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4422-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c4422-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4422-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4422-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4422-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c4422-118">Scenario description</span></span>
<span data-ttu-id="c4422-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c4422-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4422-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c4422-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4422-121">Добавление предохранителя из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="c4422-121">Add Fuse from hello gallery</span></span>
2. <span data-ttu-id="c4422-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4422-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-hello-gallery"></a><span data-ttu-id="c4422-123">Добавление предохранителя из коллекции hello</span><span class="sxs-lookup"><span data-stu-id="c4422-123">Add Fuse from hello gallery</span></span>
<span data-ttu-id="c4422-124">tooconfigure hello интеграции предохранитель в Azure AD, вы должны tooadd предохранитель из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c4422-124">tooconfigure hello integration of Fuse into Azure AD, you need tooadd Fuse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4422-125">**tooadd предохранитель из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4422-125">**tooadd Fuse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4422-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="c4422-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка Hello Azure Active Directory][1]

2. <span data-ttu-id="c4422-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="c4422-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4422-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c4422-129">Then go too**All applications**.</span></span>

    ![Hello корпоративных приложений колонку][2]
    
3. <span data-ttu-id="c4422-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c4422-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Кнопка нового приложения Hello][3]

4. <span data-ttu-id="c4422-133">Введите в поле поиска hello **предохранителя**выберите **предохранителя** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c4422-133">In hello search box, type **Fuse**, select **Fuse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![В списке результатов hello предохранителя](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c4422-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4422-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c4422-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Fuse с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4422-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4422-137">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в предохранитель является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4422-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuse is tooa user in Azure AD.</span></span> <span data-ttu-id="c4422-138">Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в toobe потребностей предохранитель установлено.</span><span class="sxs-lookup"><span data-stu-id="c4422-138">In other words, a link relationship between an Azure AD user and hello related user in Fuse needs toobe established.</span></span>

<span data-ttu-id="c4422-139">В предохранитель, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="c4422-139">In Fuse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c4422-140">tooconfigure и теста Azure AD единого входа с предохранитель, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c4422-140">tooconfigure and test Azure AD single sign-on with Fuse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4422-141">**[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="c4422-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4422-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c4422-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4422-143">**[Создание тестового пользователя предохранитель](#create-a-fuse-test-user)**  -toohave аналог Саймон Britta в предохранитель, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="c4422-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - toohave a counterpart of Britta Simon in Fuse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4422-144">**[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="c4422-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4422-145">**[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c4422-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c4422-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4422-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c4422-147">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении предохранитель.</span><span class="sxs-lookup"><span data-stu-id="c4422-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="c4422-148">**tooconfigure Azure AD единого входа с предохранитель, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4422-148">**tooconfigure Azure AD single sign-on with Fuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4422-149">В hello в hello портала Azure **предохранителя** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c4422-149">In hello Azure portal, on hello **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="c4422-151">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="c4422-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="c4422-153">На hello **URL-адреса и домена предохранителя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c4422-153">On hello **Fuse Domain and URLs** section, perform hello following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="c4422-155">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="c4422-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4422-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="c4422-156">This value is not real.</span></span> <span data-ttu-id="c4422-157">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="c4422-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c4422-158">Обратитесь к [группа поддержки предохранителя клиента](mailto:support@fusion-universal.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="c4422-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="c4422-159">На hello **сертификат подписи SAML** щелкните **сертификата (Raw)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c4422-159">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="c4422-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c4422-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4422-163">На hello **предохранителя конфигурации** щелкните **настройки предохранителя** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="c4422-163">On hello **Fuse Configuration** section, click **Configure Fuse** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c4422-164">Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="c4422-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Настройка Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="c4422-166">tooget SSO настроен для вашего приложения, обратитесь в службу [группа поддержки предохранитель](mailto:support@fusion-universal.com) и предоставить им hello следующее:</span><span class="sxs-lookup"><span data-stu-id="c4422-166">tooget SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with hello following:</span></span>

    * <span data-ttu-id="c4422-167">загружаются Hello **файл сертификата (Raw)**</span><span class="sxs-lookup"><span data-stu-id="c4422-167">hello downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="c4422-168">Hello **SAML единого входа URL-адрес службы**</span><span class="sxs-lookup"><span data-stu-id="c4422-168">hello **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="c4422-169">Hello **SAML идентификатор сущности**</span><span class="sxs-lookup"><span data-stu-id="c4422-169">hello **SAML Entity ID**</span></span>
    * <span data-ttu-id="c4422-170">Hello **URL-адрес выхода**</span><span class="sxs-lookup"><span data-stu-id="c4422-170">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="c4422-171">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="c4422-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4422-172">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="c4422-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4422-173">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4422-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c4422-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4422-174">Create an Azure AD test user</span></span>

<span data-ttu-id="c4422-175">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c4422-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="c4422-177">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4422-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4422-178">В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c4422-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c4422-180">слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c4422-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c4422-182">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c4422-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c4422-184">В hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="c4422-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c4422-186">а.</span><span class="sxs-lookup"><span data-stu-id="c4422-186">a.</span></span> <span data-ttu-id="c4422-187">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4422-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4422-188">b.</span><span class="sxs-lookup"><span data-stu-id="c4422-188">b.</span></span> <span data-ttu-id="c4422-189">В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="c4422-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c4422-190">c.</span><span class="sxs-lookup"><span data-stu-id="c4422-190">c.</span></span> <span data-ttu-id="c4422-191">Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.</span><span class="sxs-lookup"><span data-stu-id="c4422-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c4422-192">d.</span><span class="sxs-lookup"><span data-stu-id="c4422-192">d.</span></span> <span data-ttu-id="c4422-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c4422-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="c4422-194">Создание тестового пользователя в Fuse</span><span class="sxs-lookup"><span data-stu-id="c4422-194">Create a Fuse test user</span></span>

<span data-ttu-id="c4422-195">В этом разделе описано, как создать пользователя Britta Simon в приложении Fuse.</span><span class="sxs-lookup"><span data-stu-id="c4422-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="c4422-196">Можно работать с [группа поддержки предохранитель](mailto:support@fusion-universal.com) tooadd hello пользователей на платформе предохранитель hello.</span><span class="sxs-lookup"><span data-stu-id="c4422-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) tooadd hello users in hello Fuse platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c4422-197">Назначить hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="c4422-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c4422-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooFuse доступа.</span><span class="sxs-lookup"><span data-stu-id="c4422-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFuse.</span></span>

![Назначение пользователям ролей hello][200] 

<span data-ttu-id="c4422-200">**tooassign tooFuse Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="c4422-200">**tooassign Britta Simon tooFuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4422-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c4422-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c4422-203">В списке приложений hello выберите **предохранителя**.</span><span class="sxs-lookup"><span data-stu-id="c4422-203">In hello applications list, select **Fuse**.</span></span>

    ![ссылка предохранитель Hello в списке приложений hello](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="c4422-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="c4422-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Hello ссылку «Пользователи и группы»][202]

4. <span data-ttu-id="c4422-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c4422-207">Click **Add** button.</span></span> <span data-ttu-id="c4422-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c4422-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![область назначения, добавьте Hello][203]

5. <span data-ttu-id="c4422-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="c4422-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4422-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c4422-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4422-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c4422-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c4422-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c4422-213">Test single sign-on</span></span>

<span data-ttu-id="c4422-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="c4422-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c4422-215">При выборе плитки предохранитель hello в hello панели доступа, следует получать автоматически вошедшего tooyour предохранитель приложения.</span><span class="sxs-lookup"><span data-stu-id="c4422-215">When you click hello Fuse tile in hello Access Panel, you should get automatically signed-on tooyour Fuse application.</span></span>
<span data-ttu-id="c4422-216">Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4422-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c4422-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c4422-217">Additional resources</span></span>

* [<span data-ttu-id="c4422-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4422-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4422-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4422-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

