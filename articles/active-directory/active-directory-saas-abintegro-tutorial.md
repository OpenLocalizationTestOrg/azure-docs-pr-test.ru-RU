---
title: "Руководство по интеграции Azure Active Directory с Abintegro | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Abintegro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 54e2865860940cab0c0ef31a496f42dd55b0e907
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="7a959-103">Руководство. Интеграция Azure Active Directory с Abintegro</span><span class="sxs-lookup"><span data-stu-id="7a959-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="7a959-104">В этом учебнике вы узнаете, как toointegrate Abintegro с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a959-104">In this tutorial, you learn how toointegrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a959-105">Интеграция Abintegro с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7a959-105">Integrating Abintegro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7a959-106">Можно управлять в Azure AD, имеющего доступ tooAbintegro</span><span class="sxs-lookup"><span data-stu-id="7a959-106">You can control in Azure AD who has access tooAbintegro</span></span>
- <span data-ttu-id="7a959-107">Можно включить на пользователей tooautomatically get вошедшего tooAbintegro (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a959-107">You can enable your users tooautomatically get signed-on tooAbintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a959-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7a959-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7a959-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7a959-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a959-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a959-110">Prerequisites</span></span>

<span data-ttu-id="7a959-111">tooconfigure интеграция Azure AD с Abintegro требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="7a959-111">tooconfigure Azure AD integration with Abintegro, you need hello following items:</span></span>

- <span data-ttu-id="7a959-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7a959-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a959-113">подписка Abintegro с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7a959-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a959-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7a959-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a959-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="7a959-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a959-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7a959-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a959-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a959-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a959-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7a959-118">Scenario description</span></span>
<span data-ttu-id="7a959-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7a959-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a959-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="7a959-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a959-121">Добавление Abintegro из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7a959-121">Adding Abintegro from hello gallery</span></span>
2. <span data-ttu-id="7a959-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a959-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-hello-gallery"></a><span data-ttu-id="7a959-123">Добавление Abintegro из галереи hello</span><span class="sxs-lookup"><span data-stu-id="7a959-123">Adding Abintegro from hello gallery</span></span>
<span data-ttu-id="7a959-124">tooconfigure hello интеграции Abintegro в Azure AD, вы должны tooadd Abintegro из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7a959-124">tooconfigure hello integration of Abintegro into Azure AD, you need tooadd Abintegro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7a959-125">**tooadd Abintegro из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7a959-125">**tooadd Abintegro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a959-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7a959-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7a959-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="7a959-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7a959-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7a959-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7a959-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="7a959-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7a959-133">Введите в поле поиска hello **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="7a959-133">In hello search box, type **Abintegro**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="7a959-135">В панели результатов hello выберите **Abintegro**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7a959-135">In hello results panel, select **Abintegro**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a959-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a959-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a959-138">В этом разделе мы настроим и проверим единый вход Azure AD в Abintegro с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a959-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7a959-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Abintegro является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a959-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Abintegro is tooa user in Azure AD.</span></span> <span data-ttu-id="7a959-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в Abintegro должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="7a959-140">In other words, a link relationship between an Azure AD user and hello related user in Abintegro needs toobe established.</span></span>

<span data-ttu-id="7a959-141">В Abintegro, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="7a959-141">In Abintegro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7a959-142">tooconfigure и теста Azure AD единого входа с Abintegro, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7a959-142">tooconfigure and test Azure AD single sign-on with Abintegro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7a959-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="7a959-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7a959-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="7a959-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7a959-145">**[Создание тестового пользователя, прошедшего Abintegro](#creating-an-abintegro-test-user)**  -toohave аналог Саймон Britta в Abintegro, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a959-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - toohave a counterpart of Britta Simon in Abintegro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7a959-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="7a959-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7a959-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7a959-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a959-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a959-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a959-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Abintegro приложения.</span><span class="sxs-lookup"><span data-stu-id="7a959-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="7a959-150">**Azure AD tooconfigure единого входа с Abintegro, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7a959-150">**tooconfigure Azure AD single sign-on with Abintegro, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a959-151">В hello в hello портала Azure **Abintegro** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7a959-151">In hello Azure portal, on hello **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7a959-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="7a959-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="7a959-155">На hello **URL-адреса и домена Abintegro** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7a959-155">On hello **Abintegro Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="7a959-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="7a959-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a959-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="7a959-158">This value is not real.</span></span> <span data-ttu-id="7a959-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="7a959-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7a959-160">Обратитесь к [группа поддержки Abintegro клиента](mailto:support@abintegro.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="7a959-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="7a959-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="7a959-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="7a959-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7a959-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7a959-165">tooconfigure единого входа на **Abintegro** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки abintegro](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="7a959-165">tooconfigure single sign-on on **Abintegro** side, you need toosend hello downloaded **Metadata XML** too[Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="7a959-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="7a959-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7a959-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="7a959-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7a959-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="7a959-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7a959-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a959-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a959-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7a959-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a959-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7a959-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7a959-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7a959-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a959-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="7a959-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7a959-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="7a959-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7a959-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="7a959-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7a959-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7a959-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a959-182">а.</span><span class="sxs-lookup"><span data-stu-id="7a959-182">a.</span></span> <span data-ttu-id="7a959-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a959-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a959-184">b.</span><span class="sxs-lookup"><span data-stu-id="7a959-184">b.</span></span> <span data-ttu-id="7a959-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a959-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a959-186">c.</span><span class="sxs-lookup"><span data-stu-id="7a959-186">c.</span></span> <span data-ttu-id="7a959-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="7a959-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7a959-188">d.</span><span class="sxs-lookup"><span data-stu-id="7a959-188">d.</span></span> <span data-ttu-id="7a959-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7a959-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="7a959-190">Создание тестового пользователя Abintegro</span><span class="sxs-lookup"><span data-stu-id="7a959-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="7a959-191">Нет элемента действия для вас tooconfigure подготовки пользователей tooAbintegro.</span><span class="sxs-lookup"><span data-stu-id="7a959-191">There is no action item for you tooconfigure user provisioning tooAbintegro.</span></span> <span data-ttu-id="7a959-192">Когда назначенный пользователь пытается toolog в Abintegro с помощью панели доступа hello, Abintegro проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="7a959-192">When an assigned user tries toolog into Abintegro using hello access panel, Abintegro checks whether hello user exists.</span></span>
  
<span data-ttu-id="7a959-193">Если учетная запись пользователя отсутствует, Abintegro автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="7a959-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7a959-194">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="7a959-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7a959-195">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAbintegro доступа.</span><span class="sxs-lookup"><span data-stu-id="7a959-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbintegro.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7a959-197">**tooassign tooAbintegro Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="7a959-197">**tooassign Britta Simon tooAbintegro, perform hello following steps:**</span></span>

1. <span data-ttu-id="7a959-198">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7a959-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7a959-200">В списке приложений hello выберите **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="7a959-200">In hello applications list, select **Abintegro**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="7a959-202">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="7a959-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7a959-204">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7a959-204">Click **Add** button.</span></span> <span data-ttu-id="7a959-205">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7a959-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7a959-207">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="7a959-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7a959-208">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7a959-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7a959-209">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7a959-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a959-210">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7a959-210">Testing single sign-on</span></span>

<span data-ttu-id="7a959-211">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="7a959-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7a959-212">При выборе плитки Abintegro hello в hello панели доступа, должно появиться страница входа Abintegro приложения.</span><span class="sxs-lookup"><span data-stu-id="7a959-212">When you click hello Abintegro tile in hello Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="7a959-213">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7a959-213">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7a959-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7a959-214">Additional resources</span></span>

* [<span data-ttu-id="7a959-215">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a959-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7a959-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a959-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

