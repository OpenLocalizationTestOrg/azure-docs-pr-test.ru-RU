---
title: "Руководство по интеграции Azure Active Directory с Lecorpio | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Lecorpio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 963eb36678c589f942f63c7ab555161255324717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="ee3a7-103">Руководство. Интеграция Azure Active Directory с Lecorpio</span><span class="sxs-lookup"><span data-stu-id="ee3a7-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="ee3a7-104">В этом учебнике вы узнаете, как toointegrate Lecorpio с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ee3a7-104">In this tutorial, you learn how toointegrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee3a7-105">Интеграция с Azure AD Lecorpio предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ee3a7-105">Integrating Lecorpio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ee3a7-106">Можно управлять в Azure AD, имеющего доступ tooLecorpio</span><span class="sxs-lookup"><span data-stu-id="ee3a7-106">You can control in Azure AD who has access tooLecorpio</span></span>
- <span data-ttu-id="ee3a7-107">Можно включить на пользователей tooautomatically get вошедшего tooLecorpio (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee3a7-107">You can enable your users tooautomatically get signed-on tooLecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee3a7-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ee3a7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ee3a7-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee3a7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee3a7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ee3a7-110">Prerequisites</span></span>

<span data-ttu-id="ee3a7-111">tooconfigure интеграция Azure AD с Lecorpio требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ee3a7-111">tooconfigure Azure AD integration with Lecorpio, you need hello following items:</span></span>

- <span data-ttu-id="ee3a7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ee3a7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee3a7-113">подписка Lecorpio с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee3a7-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee3a7-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ee3a7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee3a7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee3a7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee3a7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee3a7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ee3a7-118">Scenario description</span></span>
<span data-ttu-id="ee3a7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee3a7-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="ee3a7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee3a7-121">Добавление Lecorpio из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ee3a7-121">Adding Lecorpio from hello gallery</span></span>
2. <span data-ttu-id="ee3a7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee3a7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-hello-gallery"></a><span data-ttu-id="ee3a7-123">Добавление Lecorpio из галереи hello</span><span class="sxs-lookup"><span data-stu-id="ee3a7-123">Adding Lecorpio from hello gallery</span></span>
<span data-ttu-id="ee3a7-124">tooconfigure hello интеграции Lecorpio в Azure AD, вы должны tooadd Lecorpio из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-124">tooconfigure hello integration of Lecorpio into Azure AD, you need tooadd Lecorpio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee3a7-125">**tooadd Lecorpio из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ee3a7-125">**tooadd Lecorpio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3a7-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ee3a7-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ee3a7-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ee3a7-131">Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="ee3a7-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ee3a7-133">Введите в поле поиска hello **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-133">In hello search box, type **Lecorpio**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="ee3a7-135">В панели результатов hello выберите **Lecorpio**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-135">In hello results panel, select **Lecorpio**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee3a7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee3a7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee3a7-138">В этом разделе описано, как настроить и проверить единый вход Azure AD в Lecorpio с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ee3a7-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Lecorpio является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lecorpio is tooa user in Azure AD.</span></span> <span data-ttu-id="ee3a7-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Lecorpio должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-140">In other words, a link relationship between an Azure AD user and hello related user in Lecorpio needs toobe established.</span></span>

<span data-ttu-id="ee3a7-141">Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lecorpio.</span></span>

<span data-ttu-id="ee3a7-142">tooconfigure и теста Azure AD единого входа с Lecorpio, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ee3a7-142">tooconfigure and test Azure AD single sign-on with Lecorpio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ee3a7-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ee3a7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee3a7-145">**[Создание тестового пользователя Lecorpio](#creating-a-lecorpio-test-user)**  -toohave аналог Саймон Britta в Lecorpio, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - toohave a counterpart of Britta Simon in Lecorpio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee3a7-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee3a7-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee3a7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee3a7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee3a7-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="ee3a7-150">**tooconfigure Azure AD единого входа с Lecorpio, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ee3a7-150">**tooconfigure Azure AD single sign-on with Lecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3a7-151">В hello в hello портала Azure **Lecorpio** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-151">In hello Azure portal, on hello **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ee3a7-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="ee3a7-155">На hello **URL-адреса и домена Lecorpio** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ee3a7-155">On hello **Lecorpio Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="ee3a7-157">а.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-157">a.</span></span> <span data-ttu-id="ee3a7-158">В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="ee3a7-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="ee3a7-159">b.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-159">b.</span></span> <span data-ttu-id="ee3a7-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="ee3a7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee3a7-161">Эти значения не являются реальными hello.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-161">These values are not hello real.</span></span> <span data-ttu-id="ee3a7-162">Обновите эти значения с hello фактический URL-адрес входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="ee3a7-163">Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="ee3a7-164">Обратитесь к [группа поддержки клиента Lecorpio](mailto:info@lecorpio.com) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="ee3a7-165">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="ee3a7-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ee3a7-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ee3a7-169">tooconfigure единого входа на **Lecorpio** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Lecorpio поддержки](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="ee3a7-169">tooconfigure single sign-on on **Lecorpio** side, you need toosend hello downloaded **Metadata XML** too[Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="ee3a7-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="ee3a7-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ee3a7-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ee3a7-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee3a7-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee3a7-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee3a7-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee3a7-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ee3a7-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ee3a7-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3a7-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee3a7-179">Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-179">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee3a7-181">Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-181">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee3a7-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ee3a7-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee3a7-185">а.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-185">a.</span></span> <span data-ttu-id="ee3a7-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee3a7-187">b.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-187">b.</span></span> <span data-ttu-id="ee3a7-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee3a7-189">c.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-189">c.</span></span> <span data-ttu-id="ee3a7-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ee3a7-191">d.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-191">d.</span></span> <span data-ttu-id="ee3a7-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="ee3a7-193">Создание тестового пользователя Lecorpio</span><span class="sxs-lookup"><span data-stu-id="ee3a7-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="ee3a7-194">В этом разделе описано, как создать пользователя Britta Simon в приложении Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="ee3a7-195">Обратитесь к [группа поддержки клиента Lecorpio](mailto:info@lecorpio.com) tooadd пользователей hello в hello Lecorpio приложения.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooadd hello users in hello Lecorpio application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ee3a7-196">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="ee3a7-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ee3a7-197">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLecorpio доступа.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLecorpio.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ee3a7-199">**tooassign tooLecorpio Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="ee3a7-199">**tooassign Britta Simon tooLecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee3a7-200">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ee3a7-202">В списке приложений hello выберите **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-202">In hello applications list, select **Lecorpio**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="ee3a7-204">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ee3a7-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-206">Click **Add** button.</span></span> <span data-ttu-id="ee3a7-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ee3a7-209">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ee3a7-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee3a7-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee3a7-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ee3a7-212">Testing single sign-on</span></span>

<span data-ttu-id="ee3a7-213">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ee3a7-214">При нажатии кнопки hello Lecorpio плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Lecorpio приложения.</span><span class="sxs-lookup"><span data-stu-id="ee3a7-214">When you click hello Lecorpio tile in hello Access Panel, you should get automatically signed-on tooyour Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ee3a7-215">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ee3a7-215">Additional resources</span></span>

* [<span data-ttu-id="ee3a7-216">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee3a7-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee3a7-217">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ee3a7-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

