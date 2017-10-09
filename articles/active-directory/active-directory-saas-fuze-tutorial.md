---
title: "Руководство по интеграции Azure Active Directory с Fuze | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: d0ea8c6456824e348301ed8bf1f5e00f4bfa8121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="b1bc1-103">Руководство по интеграции Azure Active Directory с Fuze</span><span class="sxs-lookup"><span data-stu-id="b1bc1-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="b1bc1-104">В этом учебнике вы узнаете, как toointegrate Fuze с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1bc1-104">In this tutorial, you learn how toointegrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1bc1-105">Интеграция с Azure AD Fuze предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b1bc1-105">Integrating Fuze with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b1bc1-106">Можно управлять в Azure AD, имеющего доступ tooFuze</span><span class="sxs-lookup"><span data-stu-id="b1bc1-106">You can control in Azure AD who has access tooFuze</span></span>
- <span data-ttu-id="b1bc1-107">Можно включить на пользователей tooautomatically get вошедшего tooFuze (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bc1-107">You can enable your users tooautomatically get signed-on tooFuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1bc1-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="b1bc1-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="b1bc1-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1bc1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1bc1-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b1bc1-110">Prerequisites</span></span>

<span data-ttu-id="b1bc1-111">tooconfigure интеграция Azure AD с Fuze требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b1bc1-111">tooconfigure Azure AD integration with Fuze, you need hello following items:</span></span>

- <span data-ttu-id="b1bc1-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b1bc1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1bc1-113">подписка Fuze с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="b1bc1-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="b1bc1-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b1bc1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1bc1-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b1bc1-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1bc1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b1bc1-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b1bc1-118">Scenario description</span></span>
<span data-ttu-id="b1bc1-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1bc1-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b1bc1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1bc1-121">Добавление Fuze из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b1bc1-121">Adding Fuze from hello gallery</span></span>
2. <span data-ttu-id="b1bc1-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bc1-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-hello-gallery"></a><span data-ttu-id="b1bc1-123">Добавление Fuze из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b1bc1-123">Adding Fuze from hello gallery</span></span>
<span data-ttu-id="b1bc1-124">tooconfigure hello интеграции Fuze в Azure AD, вы должны tooadd Fuze из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-124">tooconfigure hello integration of Fuze into Azure AD, you need tooadd Fuze from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b1bc1-125">**tooadd Fuze из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b1bc1-125">**tooadd Fuze from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1bc1-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1bc1-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b1bc1-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b1bc1-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b1bc1-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b1bc1-133">Введите в поле поиска hello **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-133">In hello search box, type **Fuze**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="b1bc1-135">В панели результатов hello выберите **Fuze**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-135">In hello results panel, select **Fuze**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1bc1-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bc1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1bc1-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Fuze с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1bc1-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Fuze является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuze is tooa user in Azure AD.</span></span> <span data-ttu-id="b1bc1-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Fuze должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-140">In other words, a link relationship between an Azure AD user and hello related user in Fuze needs toobe established.</span></span>

<span data-ttu-id="b1bc1-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Fuze.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Fuze.</span></span>

<span data-ttu-id="b1bc1-142">tooconfigure и теста Azure AD единого входа с Fuze, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b1bc1-142">tooconfigure and test Azure AD single sign-on with Fuze, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b1bc1-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b1bc1-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1bc1-145">**[Создание тестового пользователя Fuze](#creating-a-fuze-test-user)**  -toohave аналог Саймон Britta в Fuze, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - toohave a counterpart of Britta Simon in Fuze that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b1bc1-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1bc1-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1bc1-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bc1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1bc1-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Fuze.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="b1bc1-150">**tooconfigure Azure AD единого входа с Fuze, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b1bc1-150">**tooconfigure Azure AD single sign-on with Fuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1bc1-151">На портале управления Azure hello на hello **Fuze** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-151">In hello Azure Management portal, on hello **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b1bc1-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="b1bc1-155">На hello **URL-адреса и домена Fuze** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b1bc1-155">On hello **Fuze Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="b1bc1-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес hello вход как:`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="b1bc1-157">In hello **Sign on URL** textbox, type hello Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="b1bc1-158">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b1bc1-158">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="b1bc1-160">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello xml file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="b1bc1-162">tooconfigure единого входа на **Fuze** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Fuze поддержки](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="b1bc1-162">tooconfigure single sign-on on **Fuze** side, you need toosend hello downloaded **Metadata XML** too[Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="b1bc1-163">Они будут устанавливается в порядке toohave hello правильно настроенной на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-163">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1bc1-164">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bc1-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1bc1-165">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-165">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b1bc1-167">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b1bc1-167">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1bc1-168">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-168">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1bc1-170">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-170">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1bc1-172">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-172">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1bc1-174">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b1bc1-174">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1bc1-176">а.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-176">a.</span></span> <span data-ttu-id="b1bc1-177">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-177">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1bc1-178">b.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-178">b.</span></span> <span data-ttu-id="b1bc1-179">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-179">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1bc1-180">c.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-180">c.</span></span> <span data-ttu-id="b1bc1-181">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-181">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b1bc1-182">d.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-182">d.</span></span> <span data-ttu-id="b1bc1-183">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="b1bc1-184">Создание тестового пользователя Fuze</span><span class="sxs-lookup"><span data-stu-id="b1bc1-184">Creating a Fuze test user</span></span>

<span data-ttu-id="b1bc1-185">Приложение Fuze поддерживает JIT-подготовку пользователей, поэтому при входе пользователи будут создаваться автоматически.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="b1bc1-186">Для получения дополнительных пояснений, обратитесь в [службу поддержки](https://www.fuze.com/support) Fuze.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b1bc1-187">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b1bc1-187">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b1bc1-188">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooFuze доступа.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-188">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFuze.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b1bc1-190">**tooassign tooFuze Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b1bc1-190">**tooassign Britta Simon tooFuze, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1bc1-191">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-191">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b1bc1-193">В списке приложений hello выберите **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-193">In hello applications list, select **Fuze**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="b1bc1-195">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-195">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b1bc1-197">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-197">Click **Add** button.</span></span> <span data-ttu-id="b1bc1-198">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b1bc1-200">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-200">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b1bc1-201">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1bc1-202">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="b1bc1-203">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b1bc1-203">Testing single sign-on</span></span>

<span data-ttu-id="b1bc1-204">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-204">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b1bc1-205">При нажатии кнопки hello Fuze плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Fuze приложения.</span><span class="sxs-lookup"><span data-stu-id="b1bc1-205">When you click hello Fuze tile in hello Access Panel, you should get automatically signed-on tooyour Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b1bc1-206">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b1bc1-206">Additional resources</span></span>

* [<span data-ttu-id="b1bc1-207">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1bc1-207">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1bc1-208">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b1bc1-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png