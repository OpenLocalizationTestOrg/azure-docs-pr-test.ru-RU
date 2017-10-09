---
title: "Руководство по интеграции Azure Active Directory с O.C. Tanner — AppreciateHub | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и O.C. Tanner — AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="b269b-105">Руководство по интеграции Azure Active Directory с O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="b269b-106">Tanner — AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="b269b-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="b269b-107">В этом учебнике вы узнаете, как toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="b269b-108">Tanner — AppreciateHub с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b269b-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b269b-109">Интеграция O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-109">Integrating O.C.</span></span> <span data-ttu-id="b269b-110">Петров - AppreciateHub с Azure AD предоставляет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b269b-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b269b-111">Можно управлять в Azure AD, имеющего доступ tooO.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="b269b-112">Tanner — AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="b269b-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="b269b-113">Можно включить на пользователей tooautomatically get вошедшего tooO.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="b269b-114">Tanner — AppreciateHub (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b269b-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b269b-115">Можно управлять учетными записями в одном централизованном месте - hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b269b-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b269b-116">Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b269b-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b269b-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b269b-117">Prerequisites</span></span>

<span data-ttu-id="b269b-118">Интеграция Azure AD с O.C. tooconfigure</span><span class="sxs-lookup"><span data-stu-id="b269b-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="b269b-119">Петров - AppreciateHub, требуется hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="b269b-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="b269b-120">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b269b-120">An Azure AD subscription</span></span>
- <span data-ttu-id="b269b-121">подписка с поддержкой единого входа O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-121">A O.C.</span></span> <span data-ttu-id="b269b-122">подписка Tanner — AppreciateHub с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b269b-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b269b-123">в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b269b-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b269b-124">tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="b269b-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b269b-125">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b269b-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b269b-126">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b269b-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b269b-127">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b269b-127">Scenario description</span></span>
<span data-ttu-id="b269b-128">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b269b-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b269b-129">Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:</span><span class="sxs-lookup"><span data-stu-id="b269b-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b269b-130">Добавление O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-130">Adding O.C.</span></span> <span data-ttu-id="b269b-131">Петров - AppreciateHub из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b269b-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="b269b-132">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b269b-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="b269b-133">Добавление O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-133">Adding O.C.</span></span> <span data-ttu-id="b269b-134">Петров - AppreciateHub из галереи hello</span><span class="sxs-lookup"><span data-stu-id="b269b-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="b269b-135">Интеграция hello tooconfigure O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="b269b-136">Петров - AppreciateHub в Azure AD необходимо tooadd O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="b269b-137">Петров - AppreciateHub из списка tooyour коллекции hello управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b269b-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b269b-138">**tooadd O.C. Петров - AppreciateHub из галереи hello выполнения hello следующие шаги:**</span><span class="sxs-lookup"><span data-stu-id="b269b-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b269b-139">В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b269b-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b269b-141">Перейдите в слишком**корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="b269b-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b269b-142">Затем перейдите слишком**все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b269b-142">Then go too**All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b269b-144">tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b269b-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b269b-146">Введите в поле поиска hello **O.C. Tanner — AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="b269b-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="b269b-148">В панели результатов hello выберите **O.C. Петров - AppreciateHub**, а затем нажмите кнопку **добавить** кнопку tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b269b-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b269b-150">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b269b-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b269b-151">В этом разделе описана настройка и проверка единого входа Azure AD в приложение O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="b269b-152">Tanner — AppreciateHub с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b269b-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b269b-153">Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="b269b-154">Петров - AppreciateHub — tooa пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b269b-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="b269b-155">Другими словами связи между пользователя Azure AD и связанных пользователей hello в O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="b269b-156">Петров - AppreciateHub должен установить toobe.</span><span class="sxs-lookup"><span data-stu-id="b269b-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="b269b-157">В O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-157">In O.C.</span></span> <span data-ttu-id="b269b-158">Значение hello Петров - AppreciateHub, назначьте hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.</span><span class="sxs-lookup"><span data-stu-id="b269b-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b269b-159">tooconfigure и теста Azure AD единого входа с O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="b269b-160">Петров - AppreciateHub, требуются следующие стандартные блоки hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b269b-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b269b-161">**[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.</span><span class="sxs-lookup"><span data-stu-id="b269b-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b269b-162">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.</span><span class="sxs-lookup"><span data-stu-id="b269b-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b269b-163">**[Создание тестового пользователя O.C. Петров - тестового пользователя AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave аналог Саймон Britta в O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="b269b-164">Петров - AppreciateHub, связанные toohello представление пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b269b-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b269b-165">**[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.</span><span class="sxs-lookup"><span data-stu-id="b269b-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b269b-166">**[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b269b-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b269b-167">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b269b-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b269b-168">В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="b269b-169">Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="b269b-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="b269b-170">**Azure AD tooconfigure единого входа с O.C. Петров - AppreciateHub, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="b269b-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="b269b-171">В hello в hello портала Azure **O.C. Tanner — AppreciateHub** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b269b-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b269b-173">На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.</span><span class="sxs-lookup"><span data-stu-id="b269b-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="b269b-175">На hello **O.C. Петров - URL-адреса и домена AppreciateHub** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b269b-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="b269b-177">а.</span><span class="sxs-lookup"><span data-stu-id="b269b-177">a.</span></span> <span data-ttu-id="b269b-178">В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="b269b-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b269b-179">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="b269b-179">This value is not real.</span></span> <span data-ttu-id="b269b-180">Измените значение этого параметра hello фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="b269b-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="b269b-181">Обратитесь в [службу поддержки Петров - группа поддержки AppreciateHub](mailto:sso@octanner.com) tooget это значение.</span><span class="sxs-lookup"><span data-stu-id="b269b-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="b269b-182">b.</span><span class="sxs-lookup"><span data-stu-id="b269b-182">b.</span></span> <span data-ttu-id="b269b-183">Привет открыть файл метаданных, с помощью hello по ссылке: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="b269b-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="b269b-184">c.</span><span class="sxs-lookup"><span data-stu-id="b269b-184">c.</span></span> <span data-ttu-id="b269b-185">Найдите hello **md:AssertionConsumerService** узла.</span><span class="sxs-lookup"><span data-stu-id="b269b-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="b269b-186">d.</span><span class="sxs-lookup"><span data-stu-id="b269b-186">d.</span></span> <span data-ttu-id="b269b-187">Скопируйте значение hello hello **расположение** атрибута.</span><span class="sxs-lookup"><span data-stu-id="b269b-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![Настройка параметров приложения][12]
   
    <span data-ttu-id="b269b-189">д.</span><span class="sxs-lookup"><span data-stu-id="b269b-189">e.</span></span> <span data-ttu-id="b269b-190">В hello **на URL-адрес входа** textbox за значением hello, полученный в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="b269b-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="b269b-191">На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="b269b-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="b269b-193">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b269b-193">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b269b-195">tooconfigure единого входа на **O.C. Петров - AppreciateHub** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[O.C. службе поддержки О.С. Tanner — AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="b269b-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="b269b-196">Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!</span><span class="sxs-lookup"><span data-stu-id="b269b-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b269b-197">После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello.</span><span class="sxs-lookup"><span data-stu-id="b269b-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b269b-198">Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b269b-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b269b-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b269b-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="b269b-200">Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b269b-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b269b-202">**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="b269b-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b269b-203">В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.</span><span class="sxs-lookup"><span data-stu-id="b269b-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b269b-205">hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="b269b-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b269b-207">tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".</span><span class="sxs-lookup"><span data-stu-id="b269b-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b269b-209">На hello **пользователя** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b269b-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b269b-211">а.</span><span class="sxs-lookup"><span data-stu-id="b269b-211">a.</span></span> <span data-ttu-id="b269b-212">В hello **имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b269b-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b269b-213">b.</span><span class="sxs-lookup"><span data-stu-id="b269b-213">b.</span></span> <span data-ttu-id="b269b-214">В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b269b-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b269b-215">c.</span><span class="sxs-lookup"><span data-stu-id="b269b-215">c.</span></span> <span data-ttu-id="b269b-216">Выберите **Показать пароль** и запишите значение hello hello **пароль**.</span><span class="sxs-lookup"><span data-stu-id="b269b-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b269b-217">d.</span><span class="sxs-lookup"><span data-stu-id="b269b-217">d.</span></span> <span data-ttu-id="b269b-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b269b-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="b269b-219">Создание тестового пользователя O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-219">Creating a O.C.</span></span> <span data-ttu-id="b269b-220">Tanner — AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="b269b-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="b269b-221">Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="b269b-222">Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="b269b-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="b269b-223">**toocreate пользователь вызвал Саймон Britta в O.C. Петров - AppreciateHub, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="b269b-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="b269b-224">Попросите [службу поддержки Петров - группа поддержки AppreciateHub](mailto:sso@octanner.com) toocreate пользователь, имеющий как hello атрибута nameID совпадает со значением в имя пользователя hello Саймон Britta в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b269b-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b269b-225">Назначение hello Azure AD тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="b269b-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b269b-226">В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooO.C доступа.</span><span class="sxs-lookup"><span data-stu-id="b269b-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="b269b-227">Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="b269b-227">Tanner - AppreciateHub.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b269b-229">**tooassign tooO.C Britta Simon. Петров - AppreciateHub, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="b269b-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="b269b-230">В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b269b-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b269b-232">В списке приложений hello выберите **O.C. Tanner — AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="b269b-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="b269b-234">В меню слева hello hello выберите **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="b269b-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b269b-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b269b-236">Click **Add** button.</span></span> <span data-ttu-id="b269b-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b269b-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b269b-239">На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b269b-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b269b-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b269b-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b269b-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b269b-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b269b-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b269b-242">Testing single sign-on</span></span>

<span data-ttu-id="b269b-243">Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".</span><span class="sxs-lookup"><span data-stu-id="b269b-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="b269b-244">При нажатии кнопки hello O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-244">When you click hello O.C.</span></span> <span data-ttu-id="b269b-245">Петров - AppreciateHub плитки в Здравствуйте панели доступа, вы должны получить автоматически подписан на tooyour O.C.</span><span class="sxs-lookup"><span data-stu-id="b269b-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="b269b-246">Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="b269b-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b269b-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b269b-247">Additional resources</span></span>

* [<span data-ttu-id="b269b-248">Список учебников по tooIntegrate приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b269b-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b269b-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b269b-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

