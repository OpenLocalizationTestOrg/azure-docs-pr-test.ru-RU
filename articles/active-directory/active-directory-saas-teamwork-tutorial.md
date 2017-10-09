---
title: "Руководство по интеграции Azure Active Directory с Teamwork | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и работу в команде."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="caaf0-103">Руководство по интеграции Azure Active Directory с Teamwork</span><span class="sxs-lookup"><span data-stu-id="caaf0-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="caaf0-104">В этом учебнике вы узнаете, как toointegrate качества совместной работы с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="caaf0-104">In this tutorial, you learn how toointegrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="caaf0-105">Интеграция командной работы с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="caaf0-105">Integrating Teamwork with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="caaf0-106">Можно управлять в Azure AD, имеющего доступ tooTeamwork</span><span class="sxs-lookup"><span data-stu-id="caaf0-106">You can control in Azure AD who has access tooTeamwork</span></span>
- <span data-ttu-id="caaf0-107">Можно включить на пользователей tooautomatically get вошедшего tooTeamwork (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="caaf0-107">You can enable your users tooautomatically get signed-on tooTeamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="caaf0-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="caaf0-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="caaf0-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="caaf0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caaf0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="caaf0-110">Prerequisites</span></span>

<span data-ttu-id="caaf0-111">tooconfigure интеграция Azure AD с работу в команде необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="caaf0-111">tooconfigure Azure AD integration with Teamwork, you need hello following items:</span></span>

- <span data-ttu-id="caaf0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="caaf0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="caaf0-113">подписка на Teamwork с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="caaf0-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="caaf0-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="caaf0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="caaf0-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="caaf0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="caaf0-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="caaf0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="caaf0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="caaf0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="caaf0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="caaf0-118">Scenario description</span></span>
<span data-ttu-id="caaf0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="caaf0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="caaf0-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="caaf0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="caaf0-121">Добавление сотрудничество из галереи hello</span><span class="sxs-lookup"><span data-stu-id="caaf0-121">Adding Teamwork from hello gallery</span></span>
2. <span data-ttu-id="caaf0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="caaf0-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-hello-gallery"></a><span data-ttu-id="caaf0-123">Добавление сотрудничество из галереи hello</span><span class="sxs-lookup"><span data-stu-id="caaf0-123">Adding Teamwork from hello gallery</span></span>
<span data-ttu-id="caaf0-124">tooconfigure hello интеграции сотрудничество в Azure AD, вы должны tooadd сотрудничество из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="caaf0-124">tooconfigure hello integration of Teamwork into Azure AD, you need tooadd Teamwork from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="caaf0-125">**tooadd сотрудничество из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="caaf0-125">**tooadd Teamwork from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="caaf0-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="caaf0-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="caaf0-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="caaf0-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="caaf0-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="caaf0-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="caaf0-133">Введите в поле поиска hello **работу в команде**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-133">In hello search box, type **Teamwork**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="caaf0-135">В панели результатов hello выберите **сотрудничество**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="caaf0-135">In hello results panel, select **Teamwork**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="caaf0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="caaf0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="caaf0-138">В этом разделе описана настройка и проверка единого входа Azure AD в Teamwork с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="caaf0-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="caaf0-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в работу в команде является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caaf0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamwork is tooa user in Azure AD.</span></span> <span data-ttu-id="caaf0-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в работу в команде должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="caaf0-140">In other words, a link relationship between an Azure AD user and hello related user in Teamwork needs toobe established.</span></span>

<span data-ttu-id="caaf0-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в работу в команде.</span><span class="sxs-lookup"><span data-stu-id="caaf0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamwork.</span></span>

<span data-ttu-id="caaf0-142">tooconfigure и теста Azure AD единого входа с работу в команде, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="caaf0-142">tooconfigure and test Azure AD single sign-on with Teamwork, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="caaf0-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="caaf0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="caaf0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="caaf0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="caaf0-145">**[Создание тестового пользователя сотрудничество](#creating-a-teamwork-test-user)**  -toohave аналог Саймон Britta в работу в команде, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="caaf0-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - toohave a counterpart of Britta Simon in Teamwork that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="caaf0-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="caaf0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="caaf0-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="caaf0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="caaf0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="caaf0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="caaf0-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении командной работы.</span><span class="sxs-lookup"><span data-stu-id="caaf0-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="caaf0-150">**tooconfigure Azure AD единого входа с работы, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="caaf0-150">**tooconfigure Azure AD single sign-on with Teamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="caaf0-151">На портале управления Azure hello на hello **сотрудничество** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-151">In hello Azure Management portal, on hello **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="caaf0-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="caaf0-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="caaf0-155">На hello **работы домена и URL-адреса** раздела hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="caaf0-155">On hello **Teamwork Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="caaf0-157">Обратите внимание на то, что это не Вещественное значение hello.</span><span class="sxs-lookup"><span data-stu-id="caaf0-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="caaf0-158">У вас есть tooupdate это значение с hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="caaf0-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="caaf0-159">Обратитесь к [группа поддержки командной работы](mailto:support@teamwork.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="caaf0-159">Contact [Teamwork support team](mailto:support@teamwork.com) tooget this value.</span></span> 

4. <span data-ttu-id="caaf0-160">На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="caaf0-162">На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="caaf0-163">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-163">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="caaf0-165">На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="caaf0-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="caaf0-167">На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="caaf0-169">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="caaf0-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="caaf0-171">tooget SSO настроен для вашего приложения, обратитесь в службу [группа поддержки командной работы](mailto:support@teamwork.com) и предоставить им загружаются hello **метаданные**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-171">tooget SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with hello downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="caaf0-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="caaf0-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="caaf0-173">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="caaf0-173">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="caaf0-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="caaf0-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="caaf0-176">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="caaf0-176">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="caaf0-178">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="caaf0-178">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="caaf0-180">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="caaf0-180">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="caaf0-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="caaf0-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="caaf0-184">а.</span><span class="sxs-lookup"><span data-stu-id="caaf0-184">a.</span></span> <span data-ttu-id="caaf0-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="caaf0-186">b.</span><span class="sxs-lookup"><span data-stu-id="caaf0-186">b.</span></span> <span data-ttu-id="caaf0-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="caaf0-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="caaf0-188">c.</span><span class="sxs-lookup"><span data-stu-id="caaf0-188">c.</span></span> <span data-ttu-id="caaf0-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="caaf0-190">d.</span><span class="sxs-lookup"><span data-stu-id="caaf0-190">d.</span></span> <span data-ttu-id="caaf0-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="caaf0-192">Создание тестового пользователя Teamwork</span><span class="sxs-lookup"><span data-stu-id="caaf0-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="caaf0-193">В этом разделе описано, как создать пользователя Britta Simon в Teamwork.</span><span class="sxs-lookup"><span data-stu-id="caaf0-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="caaf0-194">Можно работать с [группа поддержки командной работы](mailto:support@teamwork.com) tooadd hello пользователей на платформе hello работу в команде.</span><span class="sxs-lookup"><span data-stu-id="caaf0-194">Please work with [Teamwork support team](mailto:support@teamwork.com) tooadd hello users in hello Teamwork platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="caaf0-195">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="caaf0-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="caaf0-196">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooTeamwork доступа.</span><span class="sxs-lookup"><span data-stu-id="caaf0-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamwork.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="caaf0-198">**tooassign tooTeamwork Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="caaf0-198">**tooassign Britta Simon tooTeamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="caaf0-199">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-199">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="caaf0-201">В списке приложений hello выберите **работу в команде**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-201">In hello applications list, select **Teamwork**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="caaf0-203">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="caaf0-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-205">Click **Add** button.</span></span> <span data-ttu-id="caaf0-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="caaf0-208">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="caaf0-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="caaf0-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="caaf0-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="caaf0-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="caaf0-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="caaf0-211">Testing single sign-on</span></span>

<span data-ttu-id="caaf0-212">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="caaf0-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="caaf0-213">При выборе плитки сотрудничество hello в hello панели доступа, вы должны получить приложение tooyour автоматически подписан на работу в команде.</span><span class="sxs-lookup"><span data-stu-id="caaf0-213">When you click hello Teamwork tile in hello Access Panel, you should get automatically signed-on tooyour Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="caaf0-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="caaf0-214">Additional resources</span></span>

* [<span data-ttu-id="caaf0-215">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="caaf0-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="caaf0-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="caaf0-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png