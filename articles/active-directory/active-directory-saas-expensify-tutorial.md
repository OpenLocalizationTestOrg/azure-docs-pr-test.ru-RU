---
title: "Учебник. Интеграция Azure Active Directory с Expensify | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: 141513ef27c90dae2d77a52ecab2f89c4e5a55ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="40459-103">Руководство. Интеграция Azure Active Directory с Expensify</span><span class="sxs-lookup"><span data-stu-id="40459-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="40459-104">В этом учебнике вы узнаете, как toointegrate Expensify с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="40459-104">In this tutorial, you learn how toointegrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="40459-105">Интеграция с Azure AD Expensify предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="40459-105">Integrating Expensify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="40459-106">Можно управлять в Azure AD, имеющего доступ tooExpensify</span><span class="sxs-lookup"><span data-stu-id="40459-106">You can control in Azure AD who has access tooExpensify</span></span>
- <span data-ttu-id="40459-107">Можно включить на пользователей tooautomatically get вошедшего tooExpensify (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="40459-107">You can enable your users tooautomatically get signed-on tooExpensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="40459-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="40459-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="40459-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="40459-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40459-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="40459-110">Prerequisites</span></span>

<span data-ttu-id="40459-111">tooconfigure интеграция Azure AD с Expensify требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="40459-111">tooconfigure Azure AD integration with Expensify, you need hello following items:</span></span>

- <span data-ttu-id="40459-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="40459-112">An Azure AD subscription</span></span>
- <span data-ttu-id="40459-113">подписка с поддержкой единого входа Expensify.</span><span class="sxs-lookup"><span data-stu-id="40459-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="40459-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="40459-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="40459-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="40459-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="40459-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="40459-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="40459-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="40459-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="40459-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="40459-118">Scenario description</span></span>
<span data-ttu-id="40459-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="40459-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="40459-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="40459-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="40459-121">Добавление Expensify из галереи hello</span><span class="sxs-lookup"><span data-stu-id="40459-121">Adding Expensify from hello gallery</span></span>
2. <span data-ttu-id="40459-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40459-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-hello-gallery"></a><span data-ttu-id="40459-123">Добавление Expensify из галереи hello</span><span class="sxs-lookup"><span data-stu-id="40459-123">Adding Expensify from hello gallery</span></span>
<span data-ttu-id="40459-124">tooconfigure hello интеграции Expensify в Azure AD, вы должны tooadd Expensify из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="40459-124">tooconfigure hello integration of Expensify into Azure AD, you need tooadd Expensify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="40459-125">**tooadd Expensify из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="40459-125">**tooadd Expensify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="40459-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="40459-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="40459-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="40459-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="40459-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40459-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="40459-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="40459-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="40459-133">Введите в поле поиска hello **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="40459-133">In hello search box, type **Expensify**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="40459-135">В панели результатов hello выберите **Expensify**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="40459-135">In hello results panel, select **Expensify**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="40459-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40459-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="40459-138">В этом разделе описана настройка и проверка единого входа Azure AD в Expensify с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="40459-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="40459-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Expensify является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="40459-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Expensify is tooa user in Azure AD.</span></span> <span data-ttu-id="40459-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Expensify должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="40459-140">In other words, a link relationship between an Azure AD user and hello related user in Expensify needs toobe established.</span></span>

<span data-ttu-id="40459-141">В Expensify, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="40459-141">In Expensify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="40459-142">tooconfigure и теста Azure AD единого входа с Expensify, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="40459-142">tooconfigure and test Azure AD single sign-on with Expensify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="40459-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="40459-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="40459-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="40459-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="40459-145">**[Создание тестового пользователя, прошедшего Expensify](#creating-an-expensify-test-user)**  -toohave аналог Саймон Britta в Expensify, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="40459-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - toohave a counterpart of Britta Simon in Expensify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="40459-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="40459-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="40459-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="40459-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="40459-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="40459-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="40459-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Expensify.</span><span class="sxs-lookup"><span data-stu-id="40459-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="40459-150">**tooconfigure Azure AD единого входа с Expensify, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="40459-150">**tooconfigure Azure AD single sign-on with Expensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="40459-151">В hello в hello портала Azure **Expensify** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="40459-151">In hello Azure portal, on hello **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="40459-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="40459-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="40459-155">На hello **Expensify доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="40459-155">On hello **Expensify Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="40459-157">а.</span><span class="sxs-lookup"><span data-stu-id="40459-157">a.</span></span> <span data-ttu-id="40459-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="40459-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="40459-159">b.</span><span class="sxs-lookup"><span data-stu-id="40459-159">b.</span></span> <span data-ttu-id="40459-160">В hello **URL-адрес идентификатора** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="40459-160">In hello **Identifier URL** textbox, type a URL using hello following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="40459-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="40459-161">These values are not real.</span></span> <span data-ttu-id="40459-162">Обновите эти значения с hello фактический URL-адрес входа и идентификатора URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="40459-162">Update these values with hello actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="40459-163">Обратитесь к [Expensify клиента поддержки](mailto:help@expensify.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="40459-163">Contact [Expensify Client support team](mailto:help@expensify.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="40459-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="40459-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="40459-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="40459-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="40459-168">tooenable единого входа в Expensify, необходимо сначала tooenable **управления домена** в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="40459-168">tooenable SSO in Expensify, you first need tooenable **Domain Control** in hello application.</span></span> <span data-ttu-id="40459-169">Управления домена можно включить в приложение hello через hello шаги, указанные [здесь](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="40459-169">You can enable Domain Control in hello application through hello steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="40459-170">Для получения дополнительной поддержки обратитесь в [службу поддержки клиентов Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="40459-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="40459-171">После включения управления доменами сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="40459-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="40459-173">а.</span><span class="sxs-lookup"><span data-stu-id="40459-173">a.</span></span> <span data-ttu-id="40459-174">Войдите на tooyour Expensify приложения.</span><span class="sxs-lookup"><span data-stu-id="40459-174">Sign on tooyour Expensify application.</span></span>
    
    <span data-ttu-id="40459-175">b.</span><span class="sxs-lookup"><span data-stu-id="40459-175">b.</span></span> <span data-ttu-id="40459-176">Щелкните hello панели инструментов в верхней части hello **администратора**.</span><span class="sxs-lookup"><span data-stu-id="40459-176">In hello toolbar on hello top, click **Admin**.</span></span>
    
    <span data-ttu-id="40459-177">c.</span><span class="sxs-lookup"><span data-stu-id="40459-177">c.</span></span> <span data-ttu-id="40459-178">Hello левой панели щелкните **домена**.</span><span class="sxs-lookup"><span data-stu-id="40459-178">In hello left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="40459-179">d.</span><span class="sxs-lookup"><span data-stu-id="40459-179">d.</span></span> <span data-ttu-id="40459-180">Щелкните имя проверенного домена.</span><span class="sxs-lookup"><span data-stu-id="40459-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="40459-181">д.</span><span class="sxs-lookup"><span data-stu-id="40459-181">e.</span></span> <span data-ttu-id="40459-182">Hello левой панели щелкните **SAML**, а затем выберите **включено**.</span><span class="sxs-lookup"><span data-stu-id="40459-182">In hello left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="40459-183">f.</span><span class="sxs-lookup"><span data-stu-id="40459-183">f.</span></span> <span data-ttu-id="40459-184">Откройте hello загруженных метаданных федерации с Azure AD в блокноте, hello копирования содержимого и вставьте его в hello **метаданные поставщика удостоверений** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="40459-184">Open hello downloaded Federation Metadata from Azure AD in notepad, copy hello content, and then paste it into hello **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="40459-185">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="40459-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="40459-186">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="40459-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="40459-187">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="40459-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="40459-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="40459-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="40459-189">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="40459-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="40459-191">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="40459-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="40459-192">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="40459-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="40459-194">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="40459-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="40459-196">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="40459-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="40459-198">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="40459-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="40459-200">а.</span><span class="sxs-lookup"><span data-stu-id="40459-200">a.</span></span> <span data-ttu-id="40459-201">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="40459-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="40459-202">b.</span><span class="sxs-lookup"><span data-stu-id="40459-202">b.</span></span> <span data-ttu-id="40459-203">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="40459-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="40459-204">c.</span><span class="sxs-lookup"><span data-stu-id="40459-204">c.</span></span> <span data-ttu-id="40459-205">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="40459-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="40459-206">d.</span><span class="sxs-lookup"><span data-stu-id="40459-206">d.</span></span> <span data-ttu-id="40459-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="40459-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="40459-208">Создание тестового пользователя Expensify</span><span class="sxs-lookup"><span data-stu-id="40459-208">Creating an Expensify test user</span></span>

<span data-ttu-id="40459-209">В этом разделе описано, как создать пользователя Britta Simon в приложении Expensify.</span><span class="sxs-lookup"><span data-stu-id="40459-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="40459-210">Работать с [Expensify клиента поддержки](mailto:help@expensify.com) tooadd hello пользователей на платформе Expensify hello.</span><span class="sxs-lookup"><span data-stu-id="40459-210">Work with [Expensify Client support team](mailto:help@expensify.com) tooadd hello users in hello Expensify platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="40459-211">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="40459-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="40459-212">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooExpensify доступа.</span><span class="sxs-lookup"><span data-stu-id="40459-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooExpensify.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="40459-214">**tooassign tooExpensify Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="40459-214">**tooassign Britta Simon tooExpensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="40459-215">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="40459-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="40459-217">В списке приложений hello выберите **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="40459-217">In hello applications list, select **Expensify**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="40459-219">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="40459-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="40459-221">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="40459-221">Click **Add** button.</span></span> <span data-ttu-id="40459-222">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="40459-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="40459-224">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="40459-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="40459-225">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="40459-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="40459-226">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="40459-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="40459-227">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="40459-227">Testing single sign-on</span></span>

<span data-ttu-id="40459-228">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="40459-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="40459-229">При нажатии кнопки hello Expensify плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Expensify приложения.</span><span class="sxs-lookup"><span data-stu-id="40459-229">When you click hello Expensify tile in hello Access Panel, you should get automatically signed-on tooyour Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="40459-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="40459-230">Additional resources</span></span>

* [<span data-ttu-id="40459-231">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40459-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="40459-232">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="40459-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

