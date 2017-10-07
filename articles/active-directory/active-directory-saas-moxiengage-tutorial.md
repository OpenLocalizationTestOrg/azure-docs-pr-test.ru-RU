---
title: "Руководство. Интеграция Azure Active Directory с Moxi Engage | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и задействовать Moxi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1135a879-8f00-43b0-ac8a-831593d9586d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: ff3242a0981aff6dff9ec6e3f66f0e7c4a9b5b20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxi-engage"></a><span data-ttu-id="a2e5c-103">Руководство. Интеграция Azure Active Directory с Moxi Engage</span><span class="sxs-lookup"><span data-stu-id="a2e5c-103">Tutorial: Azure Active Directory integration with Moxi Engage</span></span>

<span data-ttu-id="a2e5c-104">В этом учебнике вы узнаете, как toointegrate Moxi общении с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2e5c-104">In this tutorial, you learn how toointegrate Moxi Engage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2e5c-105">Интеграция с Azure AD привлекать Moxi предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="a2e5c-105">Integrating Moxi Engage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2e5c-106">Можно управлять в Azure AD, имеющего доступ tooMoxi Владейте</span><span class="sxs-lookup"><span data-stu-id="a2e5c-106">You can control in Azure AD who has access tooMoxi Engage</span></span>
- <span data-ttu-id="a2e5c-107">Можно включить на пользователей tooautomatically get вошедшего tooMoxi Владейте (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e5c-107">You can enable your users tooautomatically get signed-on tooMoxi Engage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2e5c-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a2e5c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2e5c-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2e5c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2e5c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a2e5c-110">Prerequisites</span></span>

<span data-ttu-id="a2e5c-111">tooconfigure интеграция Azure AD с Moxi привлекать требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="a2e5c-111">tooconfigure Azure AD integration with Moxi Engage, you need hello following items:</span></span>

- <span data-ttu-id="a2e5c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a2e5c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2e5c-113">подписка Moxi Engage с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-113">A Moxi Engage single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2e5c-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2e5c-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="a2e5c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2e5c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2e5c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2e5c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2e5c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a2e5c-118">Scenario description</span></span>
<span data-ttu-id="a2e5c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2e5c-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="a2e5c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2e5c-121">Добавление привлекать Moxi из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a2e5c-121">Adding Moxi Engage from hello gallery</span></span>
2. <span data-ttu-id="a2e5c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e5c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxi-engage-from-hello-gallery"></a><span data-ttu-id="a2e5c-123">Добавление привлекать Moxi из галереи hello</span><span class="sxs-lookup"><span data-stu-id="a2e5c-123">Adding Moxi Engage from hello gallery</span></span>
<span data-ttu-id="a2e5c-124">tooconfigure hello интеграции Moxi задействовать в Azure AD, вы должны tooadd Moxi привлекать из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-124">tooconfigure hello integration of Moxi Engage into Azure AD, you need tooadd Moxi Engage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2e5c-125">**tooadd Moxi привлекать из галереи hello выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a2e5c-125">**tooadd Moxi Engage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2e5c-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2e5c-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2e5c-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a2e5c-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a2e5c-133">Введите в поле поиска hello **Moxi привлекать**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-133">In hello search box, type **Moxi Engage**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_search.png)

5. <span data-ttu-id="a2e5c-135">В панели результатов hello выберите **привлекать Moxi**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-135">In hello results panel, select **Moxi Engage**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2e5c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e5c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2e5c-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Moxi Engage с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-138">In this section, you configure and test Azure AD single sign-on with Moxi Engage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2e5c-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в привлекать Moxi является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxi Engage is tooa user in Azure AD.</span></span> <span data-ttu-id="a2e5c-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Moxi привлекать должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-140">In other words, a link relationship between an Azure AD user and hello related user in Moxi Engage needs toobe established.</span></span>

<span data-ttu-id="a2e5c-141">В Moxi связаться, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-141">In Moxi Engage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a2e5c-142">tooconfigure и теста Azure AD единого входа с привлекать Moxi, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a2e5c-142">tooconfigure and test Azure AD single sign-on with Moxi Engage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2e5c-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2e5c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2e5c-145">**[Создание тестового пользователя привлекать Moxi](#creating-a-moxi-engage-test-user)**  -toohave аналог Саймон Britta в Moxi привлекать, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-145">**[Creating a Moxi Engage test user](#creating-a-moxi-engage-test-user)** - toohave a counterpart of Britta Simon in Moxi Engage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2e5c-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2e5c-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2e5c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e5c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2e5c-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении привлекать Moxi.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxi Engage application.</span></span>

<span data-ttu-id="a2e5c-150">**tooconfigure Azure AD единого входа с задействовать Moxi, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2e5c-150">**tooconfigure Azure AD single sign-on with Moxi Engage, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2e5c-151">В hello в hello портала Azure **привлекать Moxi** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-151">In hello Azure portal, on hello **Moxi Engage** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a2e5c-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_samlbase.png)

3. <span data-ttu-id="a2e5c-155">На hello **URL-адреса и домена привлекать Moxi** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a2e5c-155">On hello **Moxi Engage Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_url.png)

    <span data-ttu-id="a2e5c-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span><span class="sxs-lookup"><span data-stu-id="a2e5c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2e5c-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-158">This value is not real.</span></span> <span data-ttu-id="a2e5c-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a2e5c-160">Обратитесь к [группа поддержки клиента привлекать Moxi](mailto:support@moxiworks.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-160">Contact [Moxi Engage Client support team](mailto:support@moxiworks.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="a2e5c-161">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_certificate.png) 

5. <span data-ttu-id="a2e5c-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a2e5c-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2e5c-165">tooconfigure единого входа на **привлекать Moxi** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Moxi выполнять группа поддержки](mailto:support@moxiworks.com).</span><span class="sxs-lookup"><span data-stu-id="a2e5c-165">tooconfigure single sign-on on **Moxi Engage** side, you need toosend hello downloaded **Metadata XML** too[Moxi Engage support team](mailto:support@moxiworks.com).</span></span> <span data-ttu-id="a2e5c-166">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a2e5c-167">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="a2e5c-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2e5c-168">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2e5c-169">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2e5c-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2e5c-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2e5c-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2e5c-171">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a2e5c-173">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="a2e5c-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2e5c-174">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2e5c-176">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2e5c-178">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="a2e5c-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2e5c-180">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="a2e5c-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2e5c-182">а.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-182">a.</span></span> <span data-ttu-id="a2e5c-183">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2e5c-184">b.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-184">b.</span></span> <span data-ttu-id="a2e5c-185">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2e5c-186">c.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-186">c.</span></span> <span data-ttu-id="a2e5c-187">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2e5c-188">d.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-188">d.</span></span> <span data-ttu-id="a2e5c-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-189">Click **Create**.</span></span>
 
### <a name="creating-a-moxi-engage-test-user"></a><span data-ttu-id="a2e5c-190">Создание тестового пользователя Moxi Engage</span><span class="sxs-lookup"><span data-stu-id="a2e5c-190">Creating a Moxi Engage test user</span></span>

<span data-ttu-id="a2e5c-191">В этом разделе описано, как создать пользователя Britta Simon в Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-191">In this section, you create a user called Britta Simon in Moxi Engage.</span></span> <span data-ttu-id="a2e5c-192">Работать с [Moxi выполнять группа поддержки](mailto:support@moxiworks.com) для добавления пользователей hello в платформе привлекать Moxi hello.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-192">Work with [Moxi Engage support team](mailto:support@moxiworks.com) to add hello users in hello Moxi Engage platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2e5c-193">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="a2e5c-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2e5c-194">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooMoxi Владейте.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxi Engage.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a2e5c-196">**tooassign tooMoxi Britta Simon Владейте, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="a2e5c-196">**tooassign Britta Simon tooMoxi Engage, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2e5c-197">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a2e5c-199">В списке приложений hello выберите **Moxi привлекать**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-199">In hello applications list, select **Moxi Engage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_app.png) 

3. <span data-ttu-id="a2e5c-201">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a2e5c-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-203">Click **Add** button.</span></span> <span data-ttu-id="a2e5c-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a2e5c-206">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2e5c-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2e5c-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2e5c-209">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a2e5c-209">Testing single sign-on</span></span>

<span data-ttu-id="a2e5c-210">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2e5c-211">При нажатии кнопки hello привлекать Moxi плитки в панели доступа hello, вы должны получить охват приложения tooMoxi автоматический вход.</span><span class="sxs-lookup"><span data-stu-id="a2e5c-211">When you click hello Moxi Engage tile in hello Access Panel, you should get automatic login tooMoxi Engage application.</span></span>
<span data-ttu-id="a2e5c-212">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2e5c-212">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a2e5c-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a2e5c-213">Additional resources</span></span>

* [<span data-ttu-id="a2e5c-214">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2e5c-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2e5c-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2e5c-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_203.png

