---
title: "Руководство по интеграции Azure Active Directory с Inkling | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 544101f1972ec16222406b761d2b6f4987458df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="024fe-103">Руководство по интеграции Azure Active Directory с Inkling</span><span class="sxs-lookup"><span data-stu-id="024fe-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="024fe-104">В этом учебнике вы узнаете, как toointegrate Inkling с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="024fe-104">In this tutorial, you learn how toointegrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="024fe-105">Интеграция с Azure AD Inkling предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="024fe-105">Integrating Inkling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="024fe-106">Можно управлять в Azure AD, имеющего доступ tooInkling</span><span class="sxs-lookup"><span data-stu-id="024fe-106">You can control in Azure AD who has access tooInkling</span></span>
- <span data-ttu-id="024fe-107">Можно включить на пользователей tooautomatically get вошедшего tooInkling (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="024fe-107">You can enable your users tooautomatically get signed-on tooInkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="024fe-108">Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure</span><span class="sxs-lookup"><span data-stu-id="024fe-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="024fe-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="024fe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="024fe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="024fe-110">Prerequisites</span></span>

<span data-ttu-id="024fe-111">tooconfigure интеграция Azure AD с Inkling требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="024fe-111">tooconfigure Azure AD integration with Inkling, you need hello following items:</span></span>

- <span data-ttu-id="024fe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="024fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="024fe-113">подписка Inkling с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="024fe-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="024fe-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="024fe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="024fe-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="024fe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="024fe-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="024fe-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="024fe-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="024fe-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="024fe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="024fe-118">Scenario description</span></span>
<span data-ttu-id="024fe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="024fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="024fe-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="024fe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="024fe-121">Добавление Inkling из галереи hello</span><span class="sxs-lookup"><span data-stu-id="024fe-121">Adding Inkling from hello gallery</span></span>
2. <span data-ttu-id="024fe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="024fe-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-hello-gallery"></a><span data-ttu-id="024fe-123">Добавление Inkling из галереи hello</span><span class="sxs-lookup"><span data-stu-id="024fe-123">Adding Inkling from hello gallery</span></span>
<span data-ttu-id="024fe-124">tooconfigure hello интеграции Inkling в Azure AD, вы должны tooadd Inkling из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="024fe-124">tooconfigure hello integration of Inkling into Azure AD, you need tooadd Inkling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="024fe-125">**tooadd Inkling из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="024fe-125">**tooadd Inkling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="024fe-126">В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="024fe-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="024fe-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="024fe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="024fe-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="024fe-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="024fe-131">Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="024fe-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="024fe-133">Введите в поле поиска hello **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="024fe-133">In hello search box, type **Inkling**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="024fe-135">В панели результатов hello выберите **Inkling**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="024fe-135">In hello results panel, select **Inkling**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="024fe-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="024fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="024fe-138">В этом разделе описана настройка и проверка единого входа Azure AD в Inkling с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="024fe-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="024fe-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Inkling является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="024fe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Inkling is tooa user in Azure AD.</span></span> <span data-ttu-id="024fe-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Inkling должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="024fe-140">In other words, a link relationship between an Azure AD user and hello related user in Inkling needs toobe established.</span></span>

<span data-ttu-id="024fe-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Inkling.</span><span class="sxs-lookup"><span data-stu-id="024fe-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Inkling.</span></span>

<span data-ttu-id="024fe-142">tooconfigure и теста Azure AD единого входа с Inkling, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="024fe-142">tooconfigure and test Azure AD single sign-on with Inkling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="024fe-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="024fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="024fe-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="024fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="024fe-145">**[Создание тестового пользователя, прошедшего Inkling](#creating-an-inkling-test-user)**  -toohave аналог Саймон Britta в Inkling, представление связанных toohello Azure AD ей.</span><span class="sxs-lookup"><span data-stu-id="024fe-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - toohave a counterpart of Britta Simon in Inkling that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="024fe-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="024fe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="024fe-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="024fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="024fe-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="024fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="024fe-149">В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Inkling.</span><span class="sxs-lookup"><span data-stu-id="024fe-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="024fe-150">**tooconfigure Azure AD единого входа с Inkling, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="024fe-150">**tooconfigure Azure AD single sign-on with Inkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="024fe-151">На портале управления Azure hello на hello **Inkling** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="024fe-151">In hello Azure Management portal, on hello **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="024fe-153">На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="024fe-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="024fe-155">На hello **URL-адреса и домена Inkling** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="024fe-155">On hello **Inkling Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="024fe-157">а.</span><span class="sxs-lookup"><span data-stu-id="024fe-157">a.</span></span> <span data-ttu-id="024fe-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="024fe-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="024fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="024fe-159">b.</span></span> <span data-ttu-id="024fe-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="024fe-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="024fe-161">Обратите внимание на то, что они не hello реальные значения.</span><span class="sxs-lookup"><span data-stu-id="024fe-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="024fe-162">У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="024fe-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="024fe-163">Обратитесь к [Inkling поддержки](mailto:press@inkling.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="024fe-163">Contact [Inkling support team](mailto:press@inkling.com) tooget these values.</span></span>

4. <span data-ttu-id="024fe-164">На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.</span><span class="sxs-lookup"><span data-stu-id="024fe-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="024fe-166">На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**.</span><span class="sxs-lookup"><span data-stu-id="024fe-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="024fe-167">Затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="024fe-167">Then click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="024fe-169">На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="024fe-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="024fe-171">На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="024fe-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="024fe-173">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="024fe-173">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="024fe-175">tooget SSO настроен для вашего приложения, обратитесь в службу [Inkling поддержки](mailto:press@inkling.com) и предоставьте их с загружены **метаданные**.</span><span class="sxs-lookup"><span data-stu-id="024fe-175">tooget SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="024fe-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="024fe-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="024fe-177">Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="024fe-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="024fe-179">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="024fe-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="024fe-180">В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="024fe-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="024fe-182">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="024fe-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="024fe-184">Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="024fe-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="024fe-186">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="024fe-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="024fe-188">а.</span><span class="sxs-lookup"><span data-stu-id="024fe-188">a.</span></span> <span data-ttu-id="024fe-189">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="024fe-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="024fe-190">b.</span><span class="sxs-lookup"><span data-stu-id="024fe-190">b.</span></span> <span data-ttu-id="024fe-191">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="024fe-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="024fe-192">c.</span><span class="sxs-lookup"><span data-stu-id="024fe-192">c.</span></span> <span data-ttu-id="024fe-193">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="024fe-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="024fe-194">d.</span><span class="sxs-lookup"><span data-stu-id="024fe-194">d.</span></span> <span data-ttu-id="024fe-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="024fe-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="024fe-196">Создание тестового пользователя Inkling</span><span class="sxs-lookup"><span data-stu-id="024fe-196">Creating an Inkling test user</span></span>

<span data-ttu-id="024fe-197">В этом разделе описано, как создать пользователя Britta Simon в приложении Inkling.</span><span class="sxs-lookup"><span data-stu-id="024fe-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="024fe-198">Можно работать с [Inkling поддержки](mailto:press@inkling.com) tooadd hello пользователей на платформе Inkling hello.</span><span class="sxs-lookup"><span data-stu-id="024fe-198">Please work with [Inkling support team](mailto:press@inkling.com) tooadd hello users in hello Inkling platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="024fe-199">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="024fe-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="024fe-200">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooInkling доступа.</span><span class="sxs-lookup"><span data-stu-id="024fe-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooInkling.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="024fe-202">**tooassign tooInkling Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="024fe-202">**tooassign Britta Simon tooInkling, perform hello following steps:**</span></span>

1. <span data-ttu-id="024fe-203">На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="024fe-203">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="024fe-205">В списке приложений hello выберите **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="024fe-205">In hello applications list, select **Inkling**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="024fe-207">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="024fe-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="024fe-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="024fe-209">Click **Add** button.</span></span> <span data-ttu-id="024fe-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="024fe-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="024fe-212">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="024fe-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="024fe-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="024fe-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="024fe-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="024fe-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="024fe-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="024fe-215">Testing single sign-on</span></span>

<span data-ttu-id="024fe-216">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="024fe-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="024fe-217">При нажатии кнопки hello Inkling плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Inkling приложения.</span><span class="sxs-lookup"><span data-stu-id="024fe-217">When you click hello Inkling tile in hello Access Panel, you should get automatically signed-on tooyour Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="024fe-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="024fe-218">Additional resources</span></span>

* [<span data-ttu-id="024fe-219">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="024fe-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="024fe-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="024fe-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png