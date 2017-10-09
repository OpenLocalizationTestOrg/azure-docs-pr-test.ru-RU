---
title: "Руководство по интеграции Azure Active Directory с SimpleNexus | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SimpleNexus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 89f455d8c551045ddfcbe7234e86b13dad1140a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="ab5ea-103">Учебник. Интеграция Azure Active Directory с SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="ab5ea-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="ab5ea-104">В этом учебнике вы узнаете, как toointegrate SimpleNexus с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ab5ea-104">In this tutorial, you learn how toointegrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ab5ea-105">Интеграция SimpleNexus с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ab5ea-105">Integrating SimpleNexus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ab5ea-106">Можно управлять в Azure AD, имеющего доступ tooSimpleNexus</span><span class="sxs-lookup"><span data-stu-id="ab5ea-106">You can control in Azure AD who has access tooSimpleNexus</span></span>
- <span data-ttu-id="ab5ea-107">Можно включить на пользователей tooautomatically get вошедшего tooSimpleNexus (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab5ea-107">You can enable your users tooautomatically get signed-on tooSimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ab5ea-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ab5ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ab5ea-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ab5ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab5ea-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ab5ea-110">Prerequisites</span></span>

<span data-ttu-id="ab5ea-111">tooconfigure интеграция Azure AD с SimpleNexus требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ab5ea-111">tooconfigure Azure AD integration with SimpleNexus, you need hello following items:</span></span>

- <span data-ttu-id="ab5ea-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ab5ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ab5ea-113">подписка SimpleNexus с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ab5ea-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ab5ea-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ab5ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ab5ea-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ab5ea-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab5ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ab5ea-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ab5ea-118">Scenario description</span></span>
<span data-ttu-id="ab5ea-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ab5ea-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ab5ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ab5ea-121">Добавление SimpleNexus из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ab5ea-121">Adding SimpleNexus from hello gallery</span></span>
2. <span data-ttu-id="ab5ea-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab5ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-hello-gallery"></a><span data-ttu-id="ab5ea-123">Добавление SimpleNexus из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ab5ea-123">Adding SimpleNexus from hello gallery</span></span>
<span data-ttu-id="ab5ea-124">tooconfigure hello интеграции SimpleNexus в Azure AD, вы должны tooadd SimpleNexus из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-124">tooconfigure hello integration of SimpleNexus into Azure AD, you need tooadd SimpleNexus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ab5ea-125">**tooadd SimpleNexus из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ab5ea-125">**tooadd SimpleNexus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab5ea-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ab5ea-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ab5ea-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ab5ea-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ab5ea-133">Введите в поле поиска hello **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-133">In hello search box, type **SimpleNexus**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_search.png)

5. <span data-ttu-id="ab5ea-135">В панели результатов hello выберите **SimpleNexus**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-135">In hello results panel, select **SimpleNexus**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ab5ea-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab5ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ab5ea-138">В этом разделе описана настройка и проверка единого входа Azure AD в SimpleNexus с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ab5ea-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SimpleNexus является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SimpleNexus is tooa user in Azure AD.</span></span> <span data-ttu-id="ab5ea-140">Другими словами связи между пользователя Azure AD и hello связанных пользователей в SimpleNexus должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-140">In other words, a link relationship between an Azure AD user and hello related user in SimpleNexus needs toobe established.</span></span>

<span data-ttu-id="ab5ea-141">В SimpleNexus, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-141">In SimpleNexus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ab5ea-142">tooconfigure и теста Azure AD единого входа с SimpleNexus, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ab5ea-142">tooconfigure and test Azure AD single sign-on with SimpleNexus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ab5ea-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ab5ea-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ab5ea-145">**[Создание тестового пользователя SimpleNexus](#creating-a-simplenexus-test-user)**  -toohave аналог Саймон Britta в SimpleNexus, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - toohave a counterpart of Britta Simon in SimpleNexus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ab5ea-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ab5ea-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ab5ea-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab5ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ab5ea-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="ab5ea-150">**tooconfigure Azure AD единого входа с SimpleNexus, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ab5ea-150">**tooconfigure Azure AD single sign-on with SimpleNexus, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab5ea-151">В hello в hello портала Azure **SimpleNexus** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-151">In hello Azure portal, on hello **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ab5ea-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

3. <span data-ttu-id="ab5ea-155">На hello **URL-адреса и домена SimpleNexus** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ab5ea-155">On hello **SimpleNexus Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="ab5ea-157">а.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-157">a.</span></span> <span data-ttu-id="ab5ea-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://simplenexus.com/<companyname>_login`</span><span class="sxs-lookup"><span data-stu-id="ab5ea-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="ab5ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-159">b.</span></span> <span data-ttu-id="ab5ea-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="ab5ea-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ab5ea-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-161">These values are not real.</span></span> <span data-ttu-id="ab5ea-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ab5ea-163">Обратитесь к [группе поддержки SimpleNexus клиента](https://simplenexus.com/site/contact) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-163">Contact [SimpleNexus Client support team](https://simplenexus.com/site/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="ab5ea-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

5. <span data-ttu-id="ab5ea-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ab5ea-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ab5ea-168">tooconfigure единого входа на **SimpleNexus** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группой поддержки SimpleNexus](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="ab5ea-168">tooconfigure single sign-on on **SimpleNexus** side, you need toosend hello downloaded **Metadata XML** too[SimpleNexus support team](https://simplenexus.com/site/contact).</span></span> <span data-ttu-id="ab5ea-169">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ab5ea-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ab5ea-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ab5ea-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ab5ea-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ab5ea-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ab5ea-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab5ea-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ab5ea-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ab5ea-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ab5ea-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab5ea-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ab5ea-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ab5ea-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ab5ea-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ab5ea-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ab5ea-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ab5ea-185">а.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-185">a.</span></span> <span data-ttu-id="ab5ea-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ab5ea-187">b.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-187">b.</span></span> <span data-ttu-id="ab5ea-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ab5ea-189">c.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-189">c.</span></span> <span data-ttu-id="ab5ea-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ab5ea-191">d.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-191">d.</span></span> <span data-ttu-id="ab5ea-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="ab5ea-193">Создание тестового пользователя SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="ab5ea-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="ab5ea-194">В порядке tooenable toolog пользователей Azure AD в tooSimpleNexus их необходимо подготовить в SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-194">In order tooenable Azure AD users toolog in tooSimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="ab5ea-195">В hello случае SimpleNexus Подготовка выполняется вручную выполняется администратором клиента hello.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-195">In hello case of SimpleNexus, provisioning is a manual task performed by hello tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="ab5ea-196">Можно использовать любые другие SimpleNexus пользователя средства создания учетных записей или интерфейсы API, предоставляемые SimpleNexus tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ab5ea-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ab5ea-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ab5ea-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSimpleNexus доступа.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSimpleNexus.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ab5ea-200">**tooassign tooSimpleNexus Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ab5ea-200">**tooassign Britta Simon tooSimpleNexus, perform hello following steps:**</span></span>

1. <span data-ttu-id="ab5ea-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ab5ea-203">В списке приложений hello выберите **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-203">In hello applications list, select **SimpleNexus**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_app.png) 

3. <span data-ttu-id="ab5ea-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ab5ea-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-207">Click **Add** button.</span></span> <span data-ttu-id="ab5ea-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ab5ea-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ab5ea-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ab5ea-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ab5ea-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ab5ea-213">Testing single sign-on</span></span>

<span data-ttu-id="ab5ea-214">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="ab5ea-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ab5ea-215">При нажатии кнопки SimpleNexus плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour SimpleNexus приложения.</span><span class="sxs-lookup"><span data-stu-id="ab5ea-215">When you click hello SimpleNexus tile in hello Access Panel, you should get automatically signed-on tooyour SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab5ea-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ab5ea-216">Additional resources</span></span>

* [<span data-ttu-id="ab5ea-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab5ea-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ab5ea-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ab5ea-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_203.png

