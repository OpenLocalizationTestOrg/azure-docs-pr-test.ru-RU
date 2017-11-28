---
title: "Руководство по интеграции Azure Active Directory с Reward Gateway | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и шлюзом вознаграждения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 30cdd538471b373468c3d990e4568ddb08081a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="023d7-103">Учебник. Интеграция Azure Active Directory с Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="023d7-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>

<span data-ttu-id="023d7-104">В этом учебнике вы узнаете, как toointegrate вознаграждения шлюза в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="023d7-104">In this tutorial, you learn how toointegrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="023d7-105">Интеграция шлюза вознаграждения с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="023d7-105">Integrating Reward Gateway with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="023d7-106">Можно управлять в Azure AD, имеющего доступ tooReward шлюза</span><span class="sxs-lookup"><span data-stu-id="023d7-106">You can control in Azure AD who has access tooReward Gateway</span></span>
- <span data-ttu-id="023d7-107">Можно включить на пользователей tooautomatically get вошедшего tooReward шлюза (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="023d7-107">You can enable your users tooautomatically get signed-on tooReward Gateway (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="023d7-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="023d7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="023d7-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="023d7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="023d7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="023d7-110">Prerequisites</span></span>

<span data-ttu-id="023d7-111">tooconfigure интеграция Azure AD с вознаграждения шлюза необходимо hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="023d7-111">tooconfigure Azure AD integration with Reward Gateway, you need hello following items:</span></span>

- <span data-ttu-id="023d7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="023d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="023d7-113">подписка Reward Gateway с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="023d7-113">A Reward Gateway single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="023d7-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="023d7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="023d7-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="023d7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="023d7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="023d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="023d7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="023d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="023d7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="023d7-118">Scenario description</span></span>
<span data-ttu-id="023d7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="023d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="023d7-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="023d7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="023d7-121">Добавление шлюза вознаграждения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="023d7-121">Adding Reward Gateway from hello gallery</span></span>
2. <span data-ttu-id="023d7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="023d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reward-gateway-from-hello-gallery"></a><span data-ttu-id="023d7-123">Добавление шлюза вознаграждения из галереи hello</span><span class="sxs-lookup"><span data-stu-id="023d7-123">Adding Reward Gateway from hello gallery</span></span>
<span data-ttu-id="023d7-124">tooconfigure hello интеграции вознаграждения шлюза в Azure AD, вы должны tooadd вознаграждения шлюза из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="023d7-124">tooconfigure hello integration of Reward Gateway into Azure AD, you need tooadd Reward Gateway from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="023d7-125">**tooadd вознаграждения шлюза из галереи hello выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="023d7-125">**tooadd Reward Gateway from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="023d7-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="023d7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="023d7-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="023d7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="023d7-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="023d7-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="023d7-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="023d7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="023d7-133">Введите в поле поиска hello **шлюза вознаграждения**.</span><span class="sxs-lookup"><span data-stu-id="023d7-133">In hello search box, type **Reward Gateway**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_search.png)

5. <span data-ttu-id="023d7-135">В панели результатов hello выберите **шлюза вознаграждения**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="023d7-135">In hello results panel, select **Reward Gateway**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="023d7-137">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="023d7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="023d7-138">В этом разделе описана настройка и проверка единого входа Azure AD в Reward Gateway с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="023d7-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="023d7-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в вознаграждения шлюза является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="023d7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Reward Gateway is tooa user in Azure AD.</span></span> <span data-ttu-id="023d7-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в вознаграждения шлюза должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="023d7-140">In other words, a link relationship between an Azure AD user and hello related user in Reward Gateway needs toobe established.</span></span>

<span data-ttu-id="023d7-141">В шлюзе вознаграждения, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="023d7-141">In Reward Gateway, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="023d7-142">tooconfigure и теста Azure AD единого входа с шлюза вознаграждения, необходимые hello toocomplete следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="023d7-142">tooconfigure and test Azure AD single sign-on with Reward Gateway, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="023d7-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="023d7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="023d7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="023d7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="023d7-145">**[Создание тестового пользователя шлюза вознаграждения](#creating-a-reward-gateway-test-user)**  -toohave аналог Саймон Britta в шлюз вознаграждения, представление связанных toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="023d7-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - toohave a counterpart of Britta Simon in Reward Gateway that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="023d7-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="023d7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="023d7-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="023d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="023d7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="023d7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="023d7-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении вознаграждения шлюза.</span><span class="sxs-lookup"><span data-stu-id="023d7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Reward Gateway application.</span></span>

<span data-ttu-id="023d7-150">**tooconfigure Azure AD единого входа со шлюзом вознаграждения, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="023d7-150">**tooconfigure Azure AD single sign-on with Reward Gateway, perform hello following steps:**</span></span>

1. <span data-ttu-id="023d7-151">В hello в hello портала Azure **шлюза вознаграждения** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="023d7-151">In hello Azure portal, on hello **Reward Gateway** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="023d7-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="023d7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

3. <span data-ttu-id="023d7-155">На hello **URL-адреса и домена шлюза вознаграждения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="023d7-155">On hello **Reward Gateway Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    <span data-ttu-id="023d7-157">а.</span><span class="sxs-lookup"><span data-stu-id="023d7-157">a.</span></span> <span data-ttu-id="023d7-158">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="023d7-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    <span data-ttu-id="023d7-159">b.</span><span class="sxs-lookup"><span data-stu-id="023d7-159">b.</span></span> <span data-ttu-id="023d7-160">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:</span><span class="sxs-lookup"><span data-stu-id="023d7-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > <span data-ttu-id="023d7-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="023d7-161">These values are not real.</span></span> <span data-ttu-id="023d7-162">Обновите эти значения с hello фактический идентификатор и ответ URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="023d7-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="023d7-163">Обратитесь к [группа поддержки шлюза вознаграждения](mailto:clientsupport@rewardgateway.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="023d7-163">Contact [Reward Gateway support team](mailto:clientsupport@rewardgateway.com) tooget these values.</span></span>
 
4. <span data-ttu-id="023d7-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="023d7-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

5. <span data-ttu-id="023d7-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="023d7-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="023d7-168">tooconfigure единого входа на **шлюза вознаграждения** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки шлюза вознаграждения](mailto:clientsupport@rewardgateway.com).</span><span class="sxs-lookup"><span data-stu-id="023d7-168">tooconfigure single sign-on on **Reward Gateway** side, you need toosend hello downloaded **Metadata XML** too[Reward Gateway support team](mailto:clientsupport@rewardgateway.com).</span></span> <span data-ttu-id="023d7-169">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="023d7-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="023d7-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="023d7-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="023d7-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="023d7-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="023d7-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="023d7-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="023d7-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="023d7-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="023d7-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="023d7-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="023d7-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="023d7-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="023d7-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="023d7-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="023d7-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="023d7-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="023d7-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="023d7-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="023d7-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="023d7-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="023d7-185">а.</span><span class="sxs-lookup"><span data-stu-id="023d7-185">a.</span></span> <span data-ttu-id="023d7-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="023d7-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="023d7-187">b.</span><span class="sxs-lookup"><span data-stu-id="023d7-187">b.</span></span> <span data-ttu-id="023d7-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="023d7-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="023d7-189">c.</span><span class="sxs-lookup"><span data-stu-id="023d7-189">c.</span></span> <span data-ttu-id="023d7-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="023d7-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="023d7-191">d.</span><span class="sxs-lookup"><span data-stu-id="023d7-191">d.</span></span> <span data-ttu-id="023d7-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="023d7-192">Click **Create**.</span></span>
 
### <a name="creating-a-reward-gateway-test-user"></a><span data-ttu-id="023d7-193">Создание тестового пользователя Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="023d7-193">Creating a Reward Gateway test user</span></span>

<span data-ttu-id="023d7-194">В этом разделе описано, как создать пользователя Britta Simon в приложении Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="023d7-194">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="023d7-195">Работать со шлюзом вознаграждения [поддержки](mailto:clientsupport@rewardgateway.com) tooadd hello пользователей на платформе шлюза вознаграждения hello.</span><span class="sxs-lookup"><span data-stu-id="023d7-195">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) tooadd hello users in hello Reward Gateway platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="023d7-196">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="023d7-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="023d7-197">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooReward шлюза.</span><span class="sxs-lookup"><span data-stu-id="023d7-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooReward Gateway.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="023d7-199">**tooassign tooReward Britta Simon шлюза, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="023d7-199">**tooassign Britta Simon tooReward Gateway, perform hello following steps:**</span></span>

1. <span data-ttu-id="023d7-200">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="023d7-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="023d7-202">В списке приложений hello выберите **шлюза вознаграждения**.</span><span class="sxs-lookup"><span data-stu-id="023d7-202">In hello applications list, select **Reward Gateway**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

3. <span data-ttu-id="023d7-204">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="023d7-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="023d7-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="023d7-206">Click **Add** button.</span></span> <span data-ttu-id="023d7-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="023d7-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="023d7-209">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="023d7-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="023d7-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="023d7-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="023d7-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="023d7-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="023d7-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="023d7-212">Testing single sign-on</span></span>

<span data-ttu-id="023d7-213">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="023d7-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="023d7-214">При выборе плитки шлюза вознаграждения hello в hello панели доступа, следует получать автоматически вошедшего tooyour вознаграждения шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="023d7-214">When you click hello Reward Gateway tile in hello Access Panel, you should get automatically signed-on tooyour Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="023d7-215">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="023d7-215">Additional resources</span></span>

* [<span data-ttu-id="023d7-216">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="023d7-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="023d7-217">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="023d7-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png

