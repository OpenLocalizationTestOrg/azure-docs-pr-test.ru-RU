---
title: "Учебник. Интеграция Azure Active Directory с Huddle | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="2641d-103">Руководство. Интеграция Azure Active Directory с Huddle</span><span class="sxs-lookup"><span data-stu-id="2641d-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="2641d-104">В этом учебнике вы узнаете, как toointegrate Huddle с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2641d-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2641d-105">Интеграция Huddle с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="2641d-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2641d-106">Можно управлять в Azure AD, имеющего доступ tooHuddle</span><span class="sxs-lookup"><span data-stu-id="2641d-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="2641d-107">Можно включить на пользователей tooautomatically get вошедшего tooHuddle (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="2641d-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2641d-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="2641d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2641d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2641d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2641d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2641d-110">Prerequisites</span></span>

<span data-ttu-id="2641d-111">Интеграция Azure AD tooconfigure с Huddle, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="2641d-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="2641d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="2641d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2641d-113">Подписка с поддержкой единого входа Huddle</span><span class="sxs-lookup"><span data-stu-id="2641d-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2641d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="2641d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2641d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="2641d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2641d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="2641d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2641d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2641d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2641d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="2641d-118">Scenario description</span></span>

<span data-ttu-id="2641d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="2641d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2641d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="2641d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2641d-121">Добавление Huddle из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2641d-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="2641d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2641d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="2641d-123">Добавление Huddle из галереи hello</span><span class="sxs-lookup"><span data-stu-id="2641d-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="2641d-124">интеграции hello tooconfigure Huddle в Azure AD, вы должны tooadd Huddle из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="2641d-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2641d-125">**tooadd Huddle из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2641d-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2641d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="2641d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2641d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="2641d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2641d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2641d-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="2641d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="2641d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="2641d-133">Введите в поле поиска hello **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="2641d-133">In hello search box, type **Huddle**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="2641d-135">В панели результатов hello выберите **Huddle**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2641d-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2641d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2641d-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2641d-138">В этом разделе описана настройка и проверка единого входа Azure AD с Huddle с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2641d-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2641d-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Huddle является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2641d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="2641d-140">Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в Huddle потребности toobe установлено.</span><span class="sxs-lookup"><span data-stu-id="2641d-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="2641d-141">В Huddle, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="2641d-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2641d-142">tooconfigure и теста Azure AD единого входа с Huddle, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2641d-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2641d-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="2641d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="2641d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="2641d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="2641d-145">**[Создание тестового пользователя Huddle](#creating-a-huddle-test-user)**  -toohave аналог Саймон Britta в Huddle, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="2641d-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="2641d-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="2641d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="2641d-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2641d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2641d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="2641d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2641d-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Huddle.</span><span class="sxs-lookup"><span data-stu-id="2641d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="2641d-150">**tooconfigure Azure AD единого входа с Huddle, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2641d-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="2641d-151">В hello в hello портала Azure **Huddle** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="2641d-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="2641d-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="2641d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="2641d-155">На hello **Huddle доменов и URL-адреса** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2641d-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="2641d-157">В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="2641d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2641d-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="2641d-158">This value is not real.</span></span> <span data-ttu-id="2641d-159">Измените значение этого параметра hello фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="2641d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="2641d-160">Обратитесь к [группа поддержки Huddle клиента](https://huddle.zendesk.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="2641d-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="2641d-161">На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="2641d-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="2641d-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="2641d-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2641d-165">На hello **Huddle конфигурации** щелкните **Настройка Huddle** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="2641d-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2641d-166">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="2641d-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="2641d-168">tooconfigure единого входа на стороне Huddle, необходимо загрузить hello toosend **сертификат**, **SAML единого входа URL-адрес службы**, и **идентификатор сущности SAML** слишком[Группа поддержки huddle клиента](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="2641d-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="2641d-169">Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="2641d-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="2641d-170">Единый вход должен toobe включен группой поддержки Huddle hello.</span><span class="sxs-lookup"><span data-stu-id="2641d-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="2641d-171">Можно получать уведомления, когда после завершения настройки hello.</span><span class="sxs-lookup"><span data-stu-id="2641d-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="2641d-172">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="2641d-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2641d-173">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="2641d-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2641d-174">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2641d-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2641d-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="2641d-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="2641d-176">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2641d-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="2641d-178">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2641d-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2641d-179">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="2641d-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2641d-181">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2641d-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2641d-183">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="2641d-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2641d-185">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2641d-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2641d-187">а.</span><span class="sxs-lookup"><span data-stu-id="2641d-187">a.</span></span> <span data-ttu-id="2641d-188">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2641d-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2641d-189">b.</span><span class="sxs-lookup"><span data-stu-id="2641d-189">b.</span></span> <span data-ttu-id="2641d-190">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2641d-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2641d-191">c.</span><span class="sxs-lookup"><span data-stu-id="2641d-191">c.</span></span> <span data-ttu-id="2641d-192">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="2641d-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2641d-193">d.</span><span class="sxs-lookup"><span data-stu-id="2641d-193">d.</span></span> <span data-ttu-id="2641d-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2641d-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="2641d-195">Создание тестового пользователя Huddle</span><span class="sxs-lookup"><span data-stu-id="2641d-195">Creating a Huddle test user</span></span>

<span data-ttu-id="2641d-196">Пользователи toolog tooenable Azure AD в tooHuddle, их необходимо подготовить в Huddle.</span><span class="sxs-lookup"><span data-stu-id="2641d-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="2641d-197">В случае hello объекта Huddle Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="2641d-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="2641d-198">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2641d-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="2641d-199">Войдите в tooyour **Huddle** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="2641d-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="2641d-200">Нажмите **Рабочая область**.</span><span class="sxs-lookup"><span data-stu-id="2641d-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="2641d-201">Щелкните **People \> Invite People** (Пользователи > Пригласить пользователей).</span><span class="sxs-lookup"><span data-stu-id="2641d-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="2641d-202">![Люди](./media/active-directory-saas-huddle-tutorial/IC787838.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="2641d-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="2641d-203">В hello **создать новое приглашение** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="2641d-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="2641d-204">![Создание приглашения](./media/active-directory-saas-huddle-tutorial/IC787839.png "Создание приглашения")</span><span class="sxs-lookup"><span data-stu-id="2641d-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="2641d-205">а.</span><span class="sxs-lookup"><span data-stu-id="2641d-205">a.</span></span> <span data-ttu-id="2641d-206">В hello **Выбор людей toojoin команды tooinvite** выберите **команды**.</span><span class="sxs-lookup"><span data-stu-id="2641d-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="2641d-207">b.</span><span class="sxs-lookup"><span data-stu-id="2641d-207">b.</span></span> <span data-ttu-id="2641d-208">Тип hello **адрес электронной почты** допустимым Azure AD учетной записи требуется tooprovision в слишком**введите адрес электронной почты людям хотелось бы tooinvite** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="2641d-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="2641d-209">c.</span><span class="sxs-lookup"><span data-stu-id="2641d-209">c.</span></span> <span data-ttu-id="2641d-210">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="2641d-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="2641d-211">Здравствуйте, что владелец получит сообщение электронной почты, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2641d-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="2641d-212">Можно использовать любые другие Huddle пользователя средства создания учетных записей или интерфейсы API, предоставляемые Huddle tooprovision учетных записей пользователей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2641d-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2641d-213">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="2641d-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2641d-214">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHuddle доступа.</span><span class="sxs-lookup"><span data-stu-id="2641d-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="2641d-216">**tooassign tooHuddle Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="2641d-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="2641d-217">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="2641d-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="2641d-219">В списке приложений hello выберите **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="2641d-219">In hello applications list, select **Huddle**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="2641d-221">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="2641d-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="2641d-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2641d-223">Click **Add** button.</span></span> <span data-ttu-id="2641d-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="2641d-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="2641d-226">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="2641d-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2641d-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="2641d-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2641d-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="2641d-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2641d-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="2641d-229">Testing single sign-on</span></span>

<span data-ttu-id="2641d-230">В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.</span><span class="sxs-lookup"><span data-stu-id="2641d-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2641d-231">Если щелкнуть плитку Huddle hello в hello панели доступа, следует получать автоматически страницы входа Huddle приложения.</span><span class="sxs-lookup"><span data-stu-id="2641d-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="2641d-232">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2641d-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2641d-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2641d-233">Additional resources</span></span>

* [<span data-ttu-id="2641d-234">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2641d-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2641d-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2641d-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
