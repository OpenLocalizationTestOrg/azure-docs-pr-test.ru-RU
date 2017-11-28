---
title: "Учебник. Интеграция Azure Active Directory с Jostle | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jostle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 617375d8f9e1cebcdb28450fc8d0ad8af99d7b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a><span data-ttu-id="59e29-103">Руководство. Интеграция Azure Active Directory с Jostle</span><span class="sxs-lookup"><span data-stu-id="59e29-103">Tutorial: Azure Active Directory integration with Jostle</span></span>

<span data-ttu-id="59e29-104">В этом учебнике вы узнаете, как toointegrate Jostle с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59e29-104">In this tutorial, you learn how toointegrate Jostle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59e29-105">Интеграция с Azure AD Jostle предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="59e29-105">Integrating Jostle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="59e29-106">Можно управлять в Azure AD, имеющего доступ tooJostle</span><span class="sxs-lookup"><span data-stu-id="59e29-106">You can control in Azure AD who has access tooJostle</span></span>
- <span data-ttu-id="59e29-107">Можно включить на пользователей tooautomatically get вошедшего tooJostle (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e29-107">You can enable your users tooautomatically get signed-on tooJostle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59e29-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="59e29-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="59e29-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59e29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59e29-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="59e29-110">Prerequisites</span></span>

<span data-ttu-id="59e29-111">Интеграция Azure AD tooconfigure с Jostle, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="59e29-111">tooconfigure Azure AD integration with Jostle, you need hello following items:</span></span>

- <span data-ttu-id="59e29-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="59e29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59e29-113">подписка Jostle с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="59e29-113">A Jostle single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59e29-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="59e29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59e29-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="59e29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59e29-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="59e29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59e29-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59e29-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59e29-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="59e29-118">Scenario description</span></span>
<span data-ttu-id="59e29-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="59e29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59e29-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="59e29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59e29-121">Добавление Jostle из галереи hello</span><span class="sxs-lookup"><span data-stu-id="59e29-121">Adding Jostle from hello gallery</span></span>
2. <span data-ttu-id="59e29-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jostle-from-hello-gallery"></a><span data-ttu-id="59e29-123">Добавление Jostle из галереи hello</span><span class="sxs-lookup"><span data-stu-id="59e29-123">Adding Jostle from hello gallery</span></span>
<span data-ttu-id="59e29-124">tooconfigure hello интеграции Jostle в Azure AD, вы должны tooadd Jostle из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="59e29-124">tooconfigure hello integration of Jostle into Azure AD, you need tooadd Jostle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="59e29-125">**tooadd Jostle из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="59e29-125">**tooadd Jostle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e29-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="59e29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="59e29-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="59e29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="59e29-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="59e29-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="59e29-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="59e29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="59e29-133">Введите в поле поиска hello **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="59e29-133">In hello search box, type **Jostle**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_search.png)

5. <span data-ttu-id="59e29-135">В панели результатов hello выберите **Jostle**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="59e29-135">In hello results panel, select **Jostle**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59e29-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59e29-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Jostle с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59e29-138">In this section, you configure and test Azure AD single sign-on with Jostle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="59e29-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Jostle является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e29-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jostle is tooa user in Azure AD.</span></span> <span data-ttu-id="59e29-140">Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в toobe потребности Jostle установлено.</span><span class="sxs-lookup"><span data-stu-id="59e29-140">In other words, a link relationship between an Azure AD user and hello related user in Jostle needs toobe established.</span></span>

<span data-ttu-id="59e29-141">В Jostle, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="59e29-141">In Jostle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="59e29-142">tooconfigure и теста Azure AD единого входа с Jostle, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="59e29-142">tooconfigure and test Azure AD single sign-on with Jostle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="59e29-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="59e29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="59e29-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="59e29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59e29-145">**[Создание тестового пользователя Jostle](#creating-a-jostle-test-user)**  -toohave аналог Саймон Britta в Jostle, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="59e29-145">**[Creating a Jostle test user](#creating-a-jostle-test-user)** - toohave a counterpart of Britta Simon in Jostle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="59e29-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="59e29-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59e29-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="59e29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59e29-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59e29-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Jostle.</span><span class="sxs-lookup"><span data-stu-id="59e29-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jostle application.</span></span>

<span data-ttu-id="59e29-150">**tooconfigure Azure AD единого входа с Jostle, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="59e29-150">**tooconfigure Azure AD single sign-on with Jostle, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e29-151">В hello в hello портала Azure **Jostle** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="59e29-151">In hello Azure portal, on hello **Jostle** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="59e29-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="59e29-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_samlbase.png)

3. <span data-ttu-id="59e29-155">На hello **Jostle доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e29-155">On hello **Jostle Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_url.png)

    <span data-ttu-id="59e29-157">а.</span><span class="sxs-lookup"><span data-stu-id="59e29-157">a.</span></span> <span data-ttu-id="59e29-158">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tanent name>.jostle.us/jostle-prod/`</span><span class="sxs-lookup"><span data-stu-id="59e29-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tanent name>.jostle.us/jostle-prod/`</span></span>

    <span data-ttu-id="59e29-159">b.</span><span class="sxs-lookup"><span data-stu-id="59e29-159">b.</span></span> <span data-ttu-id="59e29-160">В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tanent name>.jostle.us`</span><span class="sxs-lookup"><span data-stu-id="59e29-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tanent name>.jostle.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59e29-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="59e29-161">These values are not real.</span></span> <span data-ttu-id="59e29-162">Обновить значения hello фактический URL-адрес входа и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="59e29-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="59e29-163">Обратитесь к [Jostle поддержки](mailto:support@jostle.me) tooget эти значения.</span><span class="sxs-lookup"><span data-stu-id="59e29-163">Contact [Jostle support team](mailto:support@jostle.me) tooget these values.</span></span> 
 


4. <span data-ttu-id="59e29-164">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="59e29-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_certificate.png) 

5. <span data-ttu-id="59e29-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="59e29-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jostle-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="59e29-168">tooconfigure единого входа на стороне Jostle, требуется toosend hello загружены метаданные XML слишком[Jostle поддержки](mailto:support@jostle.me).</span><span class="sxs-lookup"><span data-stu-id="59e29-168">tooconfigure single sign-on on Jostle side, you need toosend hello downloaded metadata XML too[Jostle support team](mailto:support@jostle.me).</span></span> <span data-ttu-id="59e29-169">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="59e29-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> 

> [!TIP]
> <span data-ttu-id="59e29-170">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="59e29-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="59e29-171">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="59e29-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="59e29-172">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59e29-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59e29-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e29-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="59e29-174">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="59e29-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="59e29-176">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="59e29-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e29-177">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="59e29-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59e29-179">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="59e29-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59e29-181">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="59e29-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59e29-183">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e29-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jostle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59e29-185">а.</span><span class="sxs-lookup"><span data-stu-id="59e29-185">a.</span></span> <span data-ttu-id="59e29-186">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59e29-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59e29-187">b.</span><span class="sxs-lookup"><span data-stu-id="59e29-187">b.</span></span> <span data-ttu-id="59e29-188">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="59e29-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59e29-189">c.</span><span class="sxs-lookup"><span data-stu-id="59e29-189">c.</span></span> <span data-ttu-id="59e29-190">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="59e29-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="59e29-191">d.</span><span class="sxs-lookup"><span data-stu-id="59e29-191">d.</span></span> <span data-ttu-id="59e29-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="59e29-192">Click **Create**.</span></span>
 
### <a name="creating-a-jostle-test-user"></a><span data-ttu-id="59e29-193">Создание тестового пользователя Jostle</span><span class="sxs-lookup"><span data-stu-id="59e29-193">Creating a Jostle test user</span></span>

<span data-ttu-id="59e29-194">В этом разделе описано, как создать пользователя Britta Simon в приложении Jostle.</span><span class="sxs-lookup"><span data-stu-id="59e29-194">In this section, you create a user called Britta Simon in Jostle.</span></span> <span data-ttu-id="59e29-195">Если вы не знаете, как tooadd Britta Simon в Jostle, обратитесь в службу с [Jostle поддержки](mailto:support@jostle.me) tooadd hello тестового пользователя и Включение единого входа.</span><span class="sxs-lookup"><span data-stu-id="59e29-195">If you don't know how tooadd Britta Simon in Jostle, please contact with [Jostle support team](mailto:support@jostle.me) tooadd hello test user and enable SSO.</span></span>

> [!NOTE]
> <span data-ttu-id="59e29-196">Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="59e29-196">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="59e29-197">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="59e29-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="59e29-198">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooJostle доступа.</span><span class="sxs-lookup"><span data-stu-id="59e29-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJostle.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="59e29-200">**tooassign tooJostle Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="59e29-200">**tooassign Britta Simon tooJostle, perform hello following steps:**</span></span>

1. <span data-ttu-id="59e29-201">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="59e29-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="59e29-203">В списке приложений hello выберите **Jostle**.</span><span class="sxs-lookup"><span data-stu-id="59e29-203">In hello applications list, select **Jostle**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jostle-tutorial/tutorial_jostle_app.png) 

3. <span data-ttu-id="59e29-205">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="59e29-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="59e29-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="59e29-207">Click **Add** button.</span></span> <span data-ttu-id="59e29-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="59e29-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="59e29-210">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="59e29-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="59e29-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="59e29-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59e29-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="59e29-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59e29-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="59e29-213">Testing single sign-on</span></span>

<span data-ttu-id="59e29-214">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="59e29-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="59e29-215">Если щелкнуть плитку Jostle hello в hello панели доступа, следует получать автоматически страницы входа Jostle приложения.</span><span class="sxs-lookup"><span data-stu-id="59e29-215">When you click hello Jostle tile in hello Access Panel, you should get automatically login page of Jostle application.</span></span>
<span data-ttu-id="59e29-216">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59e29-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59e29-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="59e29-217">Additional resources</span></span>

* [<span data-ttu-id="59e29-218">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59e29-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59e29-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59e29-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jostle-tutorial/tutorial_general_203.png

