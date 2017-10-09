---
title: "Учебник. Интеграция Azure Active Directory с Mindflash | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a1bc327ea3867287103acbb64d30f0a8d7d4c5e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="edd72-103">Руководство. Интеграция Azure Active Directory с Mindflash</span><span class="sxs-lookup"><span data-stu-id="edd72-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="edd72-104">В этом учебнике вы узнаете, как toointegrate Mindflash с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="edd72-104">In this tutorial, you learn how toointegrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edd72-105">Интеграция Mindflash с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="edd72-105">Integrating Mindflash with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="edd72-106">Можно управлять в Azure AD, имеющего доступ tooMindflash</span><span class="sxs-lookup"><span data-stu-id="edd72-106">You can control in Azure AD who has access tooMindflash</span></span>
- <span data-ttu-id="edd72-107">Можно включить на пользователей tooautomatically get вошедшего tooMindflash (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="edd72-107">You can enable your users tooautomatically get signed-on tooMindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="edd72-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="edd72-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="edd72-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="edd72-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edd72-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="edd72-110">Prerequisites</span></span>

<span data-ttu-id="edd72-111">tooconfigure интеграция Azure AD с Mindflash, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="edd72-111">tooconfigure Azure AD integration with Mindflash, you need hello following items:</span></span>

- <span data-ttu-id="edd72-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="edd72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edd72-113">Подписка на Mindflash с поддержкой единого входа</span><span class="sxs-lookup"><span data-stu-id="edd72-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edd72-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="edd72-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edd72-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="edd72-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edd72-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="edd72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edd72-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edd72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edd72-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="edd72-118">Scenario description</span></span>
<span data-ttu-id="edd72-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="edd72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edd72-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="edd72-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edd72-121">Добавление Mindflash из галереи hello</span><span class="sxs-lookup"><span data-stu-id="edd72-121">Adding Mindflash from hello gallery</span></span>
2. <span data-ttu-id="edd72-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="edd72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-hello-gallery"></a><span data-ttu-id="edd72-123">Добавление Mindflash из галереи hello</span><span class="sxs-lookup"><span data-stu-id="edd72-123">Adding Mindflash from hello gallery</span></span>
<span data-ttu-id="edd72-124">tooconfigure hello интеграции Mindflash в Azure AD, вы должны tooadd Mindflash из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="edd72-124">tooconfigure hello integration of Mindflash into Azure AD, you need tooadd Mindflash from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="edd72-125">**tooadd Mindflash из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="edd72-125">**tooadd Mindflash from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="edd72-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="edd72-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="edd72-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="edd72-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="edd72-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="edd72-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="edd72-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="edd72-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="edd72-133">Введите в поле поиска hello **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="edd72-133">In hello search box, type **Mindflash**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="edd72-135">В панели результатов hello выберите **Mindflash**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="edd72-135">In hello results panel, select **Mindflash**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="edd72-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="edd72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="edd72-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Mindflash с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edd72-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="edd72-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Mindflash является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="edd72-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mindflash is tooa user in Azure AD.</span></span> <span data-ttu-id="edd72-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Mindflash должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="edd72-140">In other words, a link relationship between an Azure AD user and hello related user in Mindflash needs toobe established.</span></span>

<span data-ttu-id="edd72-141">В Mindflash, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="edd72-141">In Mindflash, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="edd72-142">tooconfigure и теста Azure AD единого входа с Mindflash, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="edd72-142">tooconfigure and test Azure AD single sign-on with Mindflash, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="edd72-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="edd72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="edd72-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="edd72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edd72-145">**[Создание тестового пользователя Mindflash](#creating-a-mindflash-test-user)**  -toohave аналог Саймон Britta в Mindflash, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="edd72-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - toohave a counterpart of Britta Simon in Mindflash that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="edd72-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="edd72-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edd72-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="edd72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="edd72-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="edd72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="edd72-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Mindflash.</span><span class="sxs-lookup"><span data-stu-id="edd72-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="edd72-150">**Azure AD tooconfigure единого входа с Mindflash, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="edd72-150">**tooconfigure Azure AD single sign-on with Mindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="edd72-151">В hello в hello портала Azure **Mindflash** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="edd72-151">In hello Azure portal, on hello **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="edd72-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="edd72-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="edd72-155">На hello **URL-адреса и домена Mindflash** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="edd72-155">On hello **Mindflash Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="edd72-157">а.</span><span class="sxs-lookup"><span data-stu-id="edd72-157">a.</span></span> <span data-ttu-id="edd72-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="edd72-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="edd72-159">b.</span><span class="sxs-lookup"><span data-stu-id="edd72-159">b.</span></span> <span data-ttu-id="edd72-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="edd72-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="edd72-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="edd72-161">These values are not real.</span></span> <span data-ttu-id="edd72-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="edd72-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="edd72-163">Обратитесь к [группа поддержки Mindflash клиента](https://www.mindflash.com/contact/) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="edd72-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="edd72-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="edd72-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="edd72-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="edd72-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="edd72-168">tooconfigure единого входа на **Mindflash** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[поддержки mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="edd72-168">tooconfigure single sign-on on **Mindflash** side, you need toosend hello downloaded **Metadata XML** too[Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="edd72-169">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="edd72-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="edd72-170">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="edd72-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="edd72-171">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="edd72-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="edd72-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="edd72-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="edd72-173">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="edd72-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="edd72-175">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="edd72-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="edd72-176">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="edd72-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="edd72-178">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="edd72-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="edd72-180">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="edd72-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="edd72-182">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="edd72-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="edd72-184">а.</span><span class="sxs-lookup"><span data-stu-id="edd72-184">a.</span></span> <span data-ttu-id="edd72-185">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edd72-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edd72-186">b.</span><span class="sxs-lookup"><span data-stu-id="edd72-186">b.</span></span> <span data-ttu-id="edd72-187">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="edd72-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="edd72-188">c.</span><span class="sxs-lookup"><span data-stu-id="edd72-188">c.</span></span> <span data-ttu-id="edd72-189">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="edd72-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="edd72-190">d.</span><span class="sxs-lookup"><span data-stu-id="edd72-190">d.</span></span> <span data-ttu-id="edd72-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="edd72-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="edd72-192">Создание тестового пользователя Mindflash</span><span class="sxs-lookup"><span data-stu-id="edd72-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="edd72-193">В порядке tooenable toolog пользователей Azure AD в Mindflash их необходимо подготовить в Mindflash.</span><span class="sxs-lookup"><span data-stu-id="edd72-193">In order tooenable Azure AD users toolog into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="edd72-194">В случае hello объекта Mindflash Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="edd72-194">In hello case of Mindflash, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="edd72-195">tooprovision учетных записей пользователей, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="edd72-195">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="edd72-196">Войдите в tooyour **Mindflash** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="edd72-196">Log in tooyour **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="edd72-197">Go слишком**Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="edd72-197">Go too**Manage Users**.</span></span>
   
    <span data-ttu-id="edd72-198">![Управление пользователями](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="edd72-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="edd72-199">Щелкните hello **Добавление пользователей**, а затем нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="edd72-199">Click hello **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="edd72-200">В hello **добавлять новых пользователей** выполните hello инструкциям допустимым Azure AD счета, tooprovision:</span><span class="sxs-lookup"><span data-stu-id="edd72-200">In hello **Add New Users** section, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="edd72-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users") (Добавление новых пользователей)</span><span class="sxs-lookup"><span data-stu-id="edd72-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="edd72-202">а.</span><span class="sxs-lookup"><span data-stu-id="edd72-202">a.</span></span> <span data-ttu-id="edd72-203">В hello **имя** введите **имя** hello пользователя как **Britta**.</span><span class="sxs-lookup"><span data-stu-id="edd72-203">In hello **First name** textbox, type **First name** of hello user as **Britta**.</span></span>

    <span data-ttu-id="edd72-204">b.</span><span class="sxs-lookup"><span data-stu-id="edd72-204">b.</span></span> <span data-ttu-id="edd72-205">В hello **Фамилия** введите **Фамилия** hello пользователя как **Simon**.</span><span class="sxs-lookup"><span data-stu-id="edd72-205">In hello **Last name** textbox, type **Last name** of hello user as **Simon**.</span></span>
    
    <span data-ttu-id="edd72-206">c.</span><span class="sxs-lookup"><span data-stu-id="edd72-206">c.</span></span> <span data-ttu-id="edd72-207">В hello **электронной почты** введите **адрес электронной почты** hello пользователя как  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="edd72-207">In hello **Email** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="edd72-208">b.</span><span class="sxs-lookup"><span data-stu-id="edd72-208">b.</span></span> <span data-ttu-id="edd72-209">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="edd72-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="edd72-210">Можно использовать любые другие Mindflash пользователя средства создания учетных записей или интерфейсы API, предоставляемые Mindflash tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="edd72-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="edd72-211">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="edd72-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="edd72-212">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooMindflash доступа.</span><span class="sxs-lookup"><span data-stu-id="edd72-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMindflash.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="edd72-214">**tooassign tooMindflash Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="edd72-214">**tooassign Britta Simon tooMindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="edd72-215">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="edd72-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="edd72-217">В списке приложений hello выберите **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="edd72-217">In hello applications list, select **Mindflash**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="edd72-219">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="edd72-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="edd72-221">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="edd72-221">Click **Add** button.</span></span> <span data-ttu-id="edd72-222">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="edd72-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="edd72-224">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="edd72-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="edd72-225">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="edd72-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="edd72-226">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="edd72-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="edd72-227">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="edd72-227">Testing single sign-on</span></span>

<span data-ttu-id="edd72-228">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="edd72-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="edd72-229">При нажатии кнопки hello Mindflash плитки в панели доступа hello, должно появиться страница входа приложения Mindflash.</span><span class="sxs-lookup"><span data-stu-id="edd72-229">When you click hello Mindflash tile in hello Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="edd72-230">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="edd72-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="edd72-231">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="edd72-231">Additional resources</span></span>

* [<span data-ttu-id="edd72-232">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="edd72-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edd72-233">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="edd72-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

