---
title: "Учебник. Интеграция Azure Active Directory с Chromeriver | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Chromeriver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 445c5600-e340-4724-a9cb-3cfaf5770b70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 7cf0e36fb6407bf3915e26717a2a997ac13110e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-chromeriver"></a><span data-ttu-id="4404f-103">Руководство. Интеграция Azure Active Directory с Chromeriver</span><span class="sxs-lookup"><span data-stu-id="4404f-103">Tutorial: Azure Active Directory integration with Chromeriver</span></span>

<span data-ttu-id="4404f-104">В этом учебнике вы узнаете, как toointegrate Chromeriver с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4404f-104">In this tutorial, you learn how toointegrate Chromeriver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4404f-105">Интеграция Chromeriver с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4404f-105">Integrating Chromeriver with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4404f-106">Можно управлять в Azure AD, имеющего доступ tooChromeriver</span><span class="sxs-lookup"><span data-stu-id="4404f-106">You can control in Azure AD who has access tooChromeriver</span></span>
- <span data-ttu-id="4404f-107">Можно включить на пользователей tooautomatically get вошедшего tooChromeriver (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="4404f-107">You can enable your users tooautomatically get signed-on tooChromeriver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4404f-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4404f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4404f-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4404f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4404f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4404f-110">Prerequisites</span></span>

<span data-ttu-id="4404f-111">tooconfigure интеграция Azure AD с Chromeriver требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4404f-111">tooconfigure Azure AD integration with Chromeriver, you need hello following items:</span></span>

- <span data-ttu-id="4404f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="4404f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4404f-113">подписка Chromeriver с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="4404f-113">A Chromeriver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4404f-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4404f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4404f-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="4404f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4404f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="4404f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4404f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4404f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4404f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="4404f-118">Scenario description</span></span>
<span data-ttu-id="4404f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="4404f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4404f-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="4404f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4404f-121">Добавление Chromeriver из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4404f-121">Adding Chromeriver from hello gallery</span></span>
2. <span data-ttu-id="4404f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4404f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-chromeriver-from-hello-gallery"></a><span data-ttu-id="4404f-123">Добавление Chromeriver из галереи hello</span><span class="sxs-lookup"><span data-stu-id="4404f-123">Adding Chromeriver from hello gallery</span></span>
<span data-ttu-id="4404f-124">tooconfigure hello интеграции Chromeriver в Azure AD, вы должны tooadd Chromeriver из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="4404f-124">tooconfigure hello integration of Chromeriver into Azure AD, you need tooadd Chromeriver from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4404f-125">**tooadd Chromeriver из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4404f-125">**tooadd Chromeriver from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4404f-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4404f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4404f-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="4404f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4404f-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4404f-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="4404f-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="4404f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="4404f-133">Введите в поле поиска hello **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="4404f-133">In hello search box, type **Chromeriver**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_search.png)

5. <span data-ttu-id="4404f-135">В панели результатов hello выберите **Chromeriver**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4404f-135">In hello results panel, select **Chromeriver**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4404f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4404f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4404f-138">В этом разделе описана настройка и проверка единого входа Azure AD в Chromeriver с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4404f-138">In this section, you configure and test Azure AD single sign-on with Chromeriver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4404f-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Chromeriver является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4404f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Chromeriver is tooa user in Azure AD.</span></span> <span data-ttu-id="4404f-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Chromeriver должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="4404f-140">In other words, a link relationship between an Azure AD user and hello related user in Chromeriver needs toobe established.</span></span>

<span data-ttu-id="4404f-141">В Chromeriver, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="4404f-141">In Chromeriver, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4404f-142">tooconfigure и теста Azure AD единого входа с Chromeriver, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4404f-142">tooconfigure and test Azure AD single sign-on with Chromeriver, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4404f-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="4404f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4404f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="4404f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4404f-145">**[Создание тестового пользователя Chromeriver](#creating-a-chromeriver-test-user)**  -toohave аналог Саймон Britta в Chromeriver, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="4404f-145">**[Creating a Chromeriver test user](#creating-a-chromeriver-test-user)** - toohave a counterpart of Britta Simon in Chromeriver that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4404f-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="4404f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4404f-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4404f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4404f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="4404f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4404f-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="4404f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Chromeriver application.</span></span>

<span data-ttu-id="4404f-150">**Azure AD tooconfigure единого входа с Chromeriver, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4404f-150">**tooconfigure Azure AD single sign-on with Chromeriver, perform hello following steps:**</span></span>

1. <span data-ttu-id="4404f-151">В hello в hello портала Azure **Chromeriver** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="4404f-151">In hello Azure portal, on hello **Chromeriver** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="4404f-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="4404f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_samlbase.png)

3. <span data-ttu-id="4404f-155">На hello **URL-адреса и домена Chromeriver** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4404f-155">On hello **Chromeriver Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_url.png)

    <span data-ttu-id="4404f-157">а.</span><span class="sxs-lookup"><span data-stu-id="4404f-157">a.</span></span> <span data-ttu-id="4404f-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.chromeriver.com`</span><span class="sxs-lookup"><span data-stu-id="4404f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.chromeriver.com`</span></span>

    <span data-ttu-id="4404f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4404f-159">b.</span></span> <span data-ttu-id="4404f-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="4404f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4404f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="4404f-161">These values are not real.</span></span> <span data-ttu-id="4404f-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="4404f-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="4404f-163">Обратитесь к [поддержки chromeriver](https://www.chromeriver.com/services/support) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="4404f-163">Contact [Chromeriver support team](https://www.chromeriver.com/services/support) tooget these values.</span></span>
 


4. <span data-ttu-id="4404f-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="4404f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_certificate.png) 

5. <span data-ttu-id="4404f-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="4404f-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4404f-168">tooconfigure единого входа на **Chromeriver** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="4404f-168">tooconfigure single sign-on on **Chromeriver** side, you need toosend hello downloaded **Metadata XML** too[Chromeriver support team](https://www.chromeriver.com/services/support).</span></span> <span data-ttu-id="4404f-169">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="4404f-169">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="4404f-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="4404f-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4404f-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="4404f-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4404f-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4404f-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4404f-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="4404f-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="4404f-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4404f-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="4404f-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4404f-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4404f-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="4404f-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4404f-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4404f-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4404f-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="4404f-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4404f-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4404f-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4404f-185">а.</span><span class="sxs-lookup"><span data-stu-id="4404f-185">a.</span></span> <span data-ttu-id="4404f-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4404f-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4404f-187">b.</span><span class="sxs-lookup"><span data-stu-id="4404f-187">b.</span></span> <span data-ttu-id="4404f-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4404f-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4404f-189">c.</span><span class="sxs-lookup"><span data-stu-id="4404f-189">c.</span></span> <span data-ttu-id="4404f-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="4404f-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4404f-191">d.</span><span class="sxs-lookup"><span data-stu-id="4404f-191">d.</span></span> <span data-ttu-id="4404f-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4404f-192">Click **Create**.</span></span>
 
### <a name="creating-a-chromeriver-test-user"></a><span data-ttu-id="4404f-193">Создание тестового пользователя Chromeriver</span><span class="sxs-lookup"><span data-stu-id="4404f-193">Creating a Chromeriver test user</span></span>

<span data-ttu-id="4404f-194">Пользователи toolog tooenable Azure AD в tooChromeriver, их необходимо подготовить в Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="4404f-194">tooenable Azure AD users toolog in tooChromeriver, they must be provisioned into Chromeriver.</span></span>  

<span data-ttu-id="4404f-195">В случае hello Chromeriver, учетные записи пользователей hello должны toobe, созданные вашей [поддержки chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="4404f-195">In hello case of Chromeriver, hello user accounts need toobe created by your [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span>

>[!NOTE]
><span data-ttu-id="4404f-196">Можно использовать любые другие Chromeriver пользователя средства создания учетных записей или API, предоставленные Chromeriver tooprovision Azure Active Directory учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="4404f-196">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4404f-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="4404f-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4404f-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooChromeriver доступа.</span><span class="sxs-lookup"><span data-stu-id="4404f-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooChromeriver.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="4404f-200">**tooassign tooChromeriver Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="4404f-200">**tooassign Britta Simon tooChromeriver, perform hello following steps:**</span></span>

1. <span data-ttu-id="4404f-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="4404f-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="4404f-203">В списке приложений hello выберите **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="4404f-203">In hello applications list, select **Chromeriver**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_app.png) 

3. <span data-ttu-id="4404f-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="4404f-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="4404f-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4404f-207">Click **Add** button.</span></span> <span data-ttu-id="4404f-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="4404f-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="4404f-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="4404f-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4404f-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4404f-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4404f-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="4404f-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4404f-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="4404f-213">Testing single sign-on</span></span>

<span data-ttu-id="4404f-214">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="4404f-214">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4404f-215">При нажатии кнопки hello Chromeriver плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="4404f-215">When you click hello Chromeriver tile in hello Access Panel, you should get automatically signed-on tooyour Chromeriver application.</span></span> <span data-ttu-id="4404f-216">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4404f-216">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4404f-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4404f-217">Additional resources</span></span>

* [<span data-ttu-id="4404f-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4404f-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4404f-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4404f-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_203.png

