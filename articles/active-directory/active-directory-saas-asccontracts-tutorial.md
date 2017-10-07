---
title: "Руководство по интеграции Azure Active Directory с ASC Contracts | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и контракты ASC."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 8320af8acfda3e3d37e589c9887cd697d5ab651c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="867d6-103">Руководство по интеграции Azure Active Directory с ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="867d6-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="867d6-104">В этом учебнике вы узнаете, как toointegrate ASC контракты с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="867d6-104">In this tutorial, you learn how toointegrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="867d6-105">Интеграция ASC контракты с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="867d6-105">Integrating ASC Contracts with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="867d6-106">Можно управлять в Azure AD, который имеет доступ tooASC контрактов</span><span class="sxs-lookup"><span data-stu-id="867d6-106">You can control in Azure AD who has access tooASC Contracts</span></span>
- <span data-ttu-id="867d6-107">Можно включить вашей tooautomatically пользователи получить tooASC вошедшего контрактов (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="867d6-107">You can enable your users tooautomatically get signed-on tooASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="867d6-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="867d6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="867d6-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="867d6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="867d6-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="867d6-110">Prerequisites</span></span>

<span data-ttu-id="867d6-111">tooconfigure интеграция Azure AD с контрактами ASC требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="867d6-111">tooconfigure Azure AD integration with ASC Contracts, you need hello following items:</span></span>

- <span data-ttu-id="867d6-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="867d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="867d6-113">подписка ASC Contracts с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="867d6-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="867d6-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="867d6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="867d6-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="867d6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="867d6-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="867d6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="867d6-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="867d6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="867d6-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="867d6-118">Scenario description</span></span>
<span data-ttu-id="867d6-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="867d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="867d6-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="867d6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="867d6-121">Добавление ASC контракты из галереи hello</span><span class="sxs-lookup"><span data-stu-id="867d6-121">Adding ASC Contracts from hello gallery</span></span>
2. <span data-ttu-id="867d6-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="867d6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-hello-gallery"></a><span data-ttu-id="867d6-123">Добавление ASC контракты из галереи hello</span><span class="sxs-lookup"><span data-stu-id="867d6-123">Adding ASC Contracts from hello gallery</span></span>
<span data-ttu-id="867d6-124">tooconfigure hello интеграция ASC контрактов в Azure AD, вы должны tooadd ASC контракты из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="867d6-124">tooconfigure hello integration of ASC Contracts into Azure AD, you need tooadd ASC Contracts from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="867d6-125">**tooadd ASC контракты из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="867d6-125">**tooadd ASC Contracts from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="867d6-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="867d6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="867d6-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="867d6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="867d6-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="867d6-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="867d6-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="867d6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="867d6-133">Введите в поле поиска hello **контракты ASC**.</span><span class="sxs-lookup"><span data-stu-id="867d6-133">In hello search box, type **ASC Contracts**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="867d6-135">В панели результатов hello выберите **контракты ASC**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="867d6-135">In hello results panel, select **ASC Contracts**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="867d6-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="867d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="867d6-138">В этом разделе описана настройка и проверка единого входа Azure AD в ASC Contracts с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="867d6-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="867d6-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в контрактах ASC является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="867d6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ASC Contracts is tooa user in Azure AD.</span></span> <span data-ttu-id="867d6-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в контрактах ASC должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="867d6-140">In other words, a link relationship between an Azure AD user and hello related user in ASC Contracts needs toobe established.</span></span>

<span data-ttu-id="867d6-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в контрактах ASC.</span><span class="sxs-lookup"><span data-stu-id="867d6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ASC Contracts.</span></span>

<span data-ttu-id="867d6-142">tooconfigure и тестирования Azure AD единого входа с контрактами ASC, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="867d6-142">tooconfigure and test Azure AD single sign-on with ASC Contracts, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="867d6-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="867d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="867d6-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="867d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="867d6-145">**[Создание тестового пользователя, прошедшего контракты ASC](#creating-an-asc-contracts-test-user)**  -toohave аналог Саймон Britta в контрактах ASC, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="867d6-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - toohave a counterpart of Britta Simon in ASC Contracts that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="867d6-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="867d6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="867d6-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="867d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="867d6-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="867d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="867d6-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ASC контракты.</span><span class="sxs-lookup"><span data-stu-id="867d6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="867d6-150">**tooconfigure Azure AD единого входа с контрактами ASC, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="867d6-150">**tooconfigure Azure AD single sign-on with ASC Contracts, perform hello following steps:**</span></span>

1. <span data-ttu-id="867d6-151">В hello в hello портала Azure **контракты ASC** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="867d6-151">In hello Azure portal, on hello **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="867d6-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="867d6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="867d6-155">На hello **URL-адреса и домена контракты ASC** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="867d6-155">On hello **ASC Contracts Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="867d6-157">а.</span><span class="sxs-lookup"><span data-stu-id="867d6-157">a.</span></span> <span data-ttu-id="867d6-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="867d6-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="867d6-159">b.</span><span class="sxs-lookup"><span data-stu-id="867d6-159">b.</span></span> <span data-ttu-id="867d6-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="867d6-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="867d6-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="867d6-161">These values are not real.</span></span> <span data-ttu-id="867d6-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="867d6-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="867d6-163">Обратитесь в службу Inc. сетей ASC (ASC) в **613.599.6178** tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="867d6-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** tooget these values.</span></span>

4. <span data-ttu-id="867d6-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="867d6-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="867d6-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="867d6-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="867d6-168">tooconfigure единого входа на **контракты ASC** стороны, обратитесь в службу поддержки Inc. сетей ASC (ASC) в **613.599.6178** и предоставить им загружаются hello **метаданные в формате XML**.</span><span class="sxs-lookup"><span data-stu-id="867d6-168">tooconfigure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with hello downloaded **Metadata XML**.</span></span> <span data-ttu-id="867d6-169">Они устанавливаются это приложение hello toohave правильно настроенной на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="867d6-169">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="867d6-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="867d6-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="867d6-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="867d6-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="867d6-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="867d6-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="867d6-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="867d6-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="867d6-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="867d6-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="867d6-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="867d6-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="867d6-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="867d6-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="867d6-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="867d6-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="867d6-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="867d6-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="867d6-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="867d6-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="867d6-185">а.</span><span class="sxs-lookup"><span data-stu-id="867d6-185">a.</span></span> <span data-ttu-id="867d6-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="867d6-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="867d6-187">b.</span><span class="sxs-lookup"><span data-stu-id="867d6-187">b.</span></span> <span data-ttu-id="867d6-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="867d6-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="867d6-189">c.</span><span class="sxs-lookup"><span data-stu-id="867d6-189">c.</span></span> <span data-ttu-id="867d6-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="867d6-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="867d6-191">d.</span><span class="sxs-lookup"><span data-stu-id="867d6-191">d.</span></span> <span data-ttu-id="867d6-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="867d6-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="867d6-193">Создание тестового пользователя ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="867d6-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="867d6-194">Работать с группой поддержки Inc. сетей ASC (ASC) в **613.599.6178** tooget пользователей hello, добавленные в hello ASC контракты платформы.</span><span class="sxs-lookup"><span data-stu-id="867d6-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** tooget hello users added in hello ASC Contracts platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="867d6-195">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="867d6-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="867d6-196">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooASC контракты.</span><span class="sxs-lookup"><span data-stu-id="867d6-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooASC Contracts.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="867d6-198">**tooassign Britta Simon tooASC контрактов, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="867d6-198">**tooassign Britta Simon tooASC Contracts, perform hello following steps:**</span></span>

1. <span data-ttu-id="867d6-199">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="867d6-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="867d6-201">В списке приложений hello выберите **контракты ASC**.</span><span class="sxs-lookup"><span data-stu-id="867d6-201">In hello applications list, select **ASC Contracts**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="867d6-203">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="867d6-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="867d6-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="867d6-205">Click **Add** button.</span></span> <span data-ttu-id="867d6-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="867d6-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="867d6-208">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="867d6-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="867d6-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="867d6-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="867d6-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="867d6-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="867d6-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="867d6-211">Testing single sign-on</span></span>

<span data-ttu-id="867d6-212">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="867d6-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="867d6-213">При нажатии кнопки приветствия контракты ASC плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour контракты ASC приложения.</span><span class="sxs-lookup"><span data-stu-id="867d6-213">When you click hello ASC Contracts tile in hello Access Panel, you should get automatically signed-on tooyour ASC Contracts application.</span></span> <span data-ttu-id="867d6-214">Дополнительные сведения о панели доступа см. в статье</span><span class="sxs-lookup"><span data-stu-id="867d6-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="867d6-215">[Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="867d6-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="867d6-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="867d6-216">Additional resources</span></span>

* [<span data-ttu-id="867d6-217">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="867d6-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="867d6-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="867d6-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

