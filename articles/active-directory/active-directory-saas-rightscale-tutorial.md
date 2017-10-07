---
title: "Руководство по интеграции Azure Active Directory с Rightscale | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="0fe9d-103">Руководство по интеграции Azure Active Directory с Rightscale</span><span class="sxs-lookup"><span data-stu-id="0fe9d-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="0fe9d-104">В этом учебнике вы узнаете, как toointegrate Rightscale с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0fe9d-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0fe9d-105">Интеграция с Azure AD Rightscale предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0fe9d-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0fe9d-106">Можно управлять в Azure AD, имеющего доступ tooRightscale</span><span class="sxs-lookup"><span data-stu-id="0fe9d-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="0fe9d-107">Можно включить на пользователей tooautomatically get вошедшего tooRightscale (Single Sign-On) с помощью своих учетных записей Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe9d-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0fe9d-108">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0fe9d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0fe9d-109">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0fe9d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fe9d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0fe9d-110">Prerequisites</span></span>

<span data-ttu-id="0fe9d-111">tooconfigure интеграция Azure AD с Rightscale требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0fe9d-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="0fe9d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0fe9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0fe9d-113">подписка Rightscale с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0fe9d-114">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0fe9d-115">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="0fe9d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0fe9d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0fe9d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0fe9d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0fe9d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0fe9d-118">Scenario description</span></span>
<span data-ttu-id="0fe9d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0fe9d-120">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="0fe9d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0fe9d-121">Добавление Rightscale из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0fe9d-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="0fe9d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe9d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="0fe9d-123">Добавление Rightscale из галереи hello</span><span class="sxs-lookup"><span data-stu-id="0fe9d-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="0fe9d-124">tooconfigure hello интеграции Rightscale в Azure AD, вы должны tooadd Rightscale из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0fe9d-125">**tooadd Rightscale из галереи hello, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0fe9d-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fe9d-126">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0fe9d-128">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0fe9d-129">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-129">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0fe9d-131">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0fe9d-133">Введите в поле поиска hello **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-133">In hello search box, type **Rightscale**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="0fe9d-135">В панели результатов hello выберите **Rightscale**и нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0fe9d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe9d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0fe9d-138">В этом разделе описана настройка и проверка единого входа Azure AD в Rightscale с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0fe9d-139">Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Rightscale является tooa в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="0fe9d-140">Другими словами связи между пользователя Azure AD и связанных пользователей hello в Rightscale должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="0fe9d-141">В Rightscale, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0fe9d-142">tooconfigure и теста Azure AD единого входа с Rightscale, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0fe9d-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0fe9d-143">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0fe9d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0fe9d-145">**[Создание тестового пользователя Rightscale](#creating-a-rightscale-test-user)**  -toohave аналог Саймон Britta в Rightscale, который представляет связанный toohello Azure AD пользователя.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0fe9d-146">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0fe9d-147">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0fe9d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe9d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0fe9d-149">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Rightscale.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="0fe9d-150">**tooconfigure Azure AD единого входа с Rightscale, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0fe9d-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fe9d-151">В hello в hello портала Azure **Rightscale** странице интеграции приложения щелкните **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0fe9d-153">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="0fe9d-155">На hello **URL-адреса и домена Rightscale** статьи, при желании tooconfigure приложения hello в **режиме, инициированный IDP** у вас tooperform все меры как приложение hello уже заранее интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="0fe9d-157">На hello **URL-адреса и домена Rightscale** статьи, при желании tooconfigure приложения hello в **режиме, инициируемая SP**, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0fe9d-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="0fe9d-159">а.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-159">a.</span></span> <span data-ttu-id="0fe9d-160">Щелкните hello **Показывать дополнительные параметры URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="0fe9d-161">b.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-161">b.</span></span> <span data-ttu-id="0fe9d-162">В hello **на URL-адрес входа** текстовом поле введите URL-адрес hello:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="0fe9d-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="0fe9d-163">На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="0fe9d-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0fe9d-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0fe9d-167">На hello **конфигурации Rightscale** щелкните **Настройка Rightscale** tooopen **Настройка входа** окна.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0fe9d-168">Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="0fe9d-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="0fe9d-169">![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="0fe9d-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="0fe9d-170">tooget единого входа, настроенному для вашего приложения, необходимо клиента RightScale tooyour toosign вход в систему с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="0fe9d-171">а.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-171">a.</span></span> <span data-ttu-id="0fe9d-172">В меню в верхней части hello hello щелкните hello **параметры** и выберите **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="0fe9d-174">b.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-174">b.</span></span> <span data-ttu-id="0fe9d-175">Нажмите кнопку hello»**новый**» tooadd кнопку **Your Поставщики удостоверений SAML**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="0fe9d-177">c.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-177">c.</span></span> <span data-ttu-id="0fe9d-178">В текстовом поле hello объекта **отображаемое имя**, введите название вашей компании.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="0fe9d-180">d.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-180">d.</span></span> <span data-ttu-id="0fe9d-181">Выберите **инициированные RightScale разрешить единый вход с использованием подсказки обнаружения** и ввода вашего **имя домена** в hello ниже текстового поля.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="0fe9d-183">д.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-183">e.</span></span> <span data-ttu-id="0fe9d-184">Вставьте значение hello **SAML единого входа URL-адрес службы** скопирован из портала Azure в **конечная точка SAML SSO** в RightScale.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="0fe9d-186">f.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-186">f.</span></span> <span data-ttu-id="0fe9d-187">Вставьте значение hello **идентификатор сущности SAML** скопирован из портала Azure в **SAML EntityID** в RightScale.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="0fe9d-189">ж.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-189">g.</span></span> <span data-ttu-id="0fe9d-190">Нажмите кнопку **браузера** кнопку tooupload hello сертификат, который был загружен с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="0fe9d-192">h.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-192">h.</span></span> <span data-ttu-id="0fe9d-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="0fe9d-194">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="0fe9d-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0fe9d-195">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0fe9d-196">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0fe9d-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0fe9d-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fe9d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="0fe9d-198">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0fe9d-200">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0fe9d-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fe9d-201">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0fe9d-203">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0fe9d-205">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="0fe9d-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0fe9d-207">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0fe9d-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0fe9d-209">а.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-209">a.</span></span> <span data-ttu-id="0fe9d-210">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0fe9d-211">b.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-211">b.</span></span> <span data-ttu-id="0fe9d-212">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0fe9d-213">c.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-213">c.</span></span> <span data-ttu-id="0fe9d-214">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0fe9d-215">d.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-215">d.</span></span> <span data-ttu-id="0fe9d-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="0fe9d-217">Создание тестового пользователя Rightscale</span><span class="sxs-lookup"><span data-stu-id="0fe9d-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="0fe9d-218">В этом разделе описано, как создать пользователя Britta Simon в приложении RightScale.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="0fe9d-219">Работать с [группа поддержки клиента Rightscale](mailto:support@rightscale.com) tooadd hello пользователей на платформе RightScale hello.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0fe9d-220">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="0fe9d-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0fe9d-221">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooRightscale доступа.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0fe9d-223">**tooassign tooRightscale Britta Simon выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="0fe9d-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="0fe9d-224">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0fe9d-226">В списке приложений hello выберите **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-226">In hello applications list, select **Rightscale**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="0fe9d-228">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0fe9d-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-230">Click **Add** button.</span></span> <span data-ttu-id="0fe9d-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0fe9d-233">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0fe9d-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0fe9d-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0fe9d-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0fe9d-236">Testing single sign-on</span></span>

<span data-ttu-id="0fe9d-237">Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="0fe9d-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="0fe9d-238">При нажатии кнопки hello RightScale плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour RightScale приложения.</span><span class="sxs-lookup"><span data-stu-id="0fe9d-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0fe9d-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0fe9d-239">Additional resources</span></span>

* [<span data-ttu-id="0fe9d-240">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fe9d-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0fe9d-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0fe9d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

